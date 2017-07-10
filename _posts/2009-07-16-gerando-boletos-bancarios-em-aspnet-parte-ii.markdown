---
layout: post
title: Gerando boletos bancários em Asp.NET - Parte II
date: '2009-07-16 15:58:21'
tags:
- aspnet
---


Na [Parte I](http://seiti.eti.br/blog/2009/gerando-boletos-bancarios-em-aspnet-parte-i) vimos como emitir um boleto para impressão.  O que falta é populá-lo com dados que façam sentido. Vamos então populá-lo com dados relevantes.

Em primeiro lugar é necessário que você tenha os dados armazenados em algum lugar, um banco de dados talvez. Mas vou presumir que seu código já trate dos dados e me ater à construção de duas partes fundamentais do boleto: a *linha digitável* e o *código de barras*.

Note que, embora alguns dígitos da **linha digitável** sigam um padrão, cada banco pode possuir regras próprias para gerá-la. Entre em contato com seu banco para ter essas informações.

### Linha digitável

A linha digitável, lembrando novamente que estou seguindo as instruções do Itaú, possui 47 dígitos.

Abaixo segue a construção da linha, lembrando que DAC significa *dígito de auto-conferência*, ou simplesmente **dígito verificador**.

<table border="0" cellpadding="2" cellspacing="0"><tbody><tr><td>AAABC.CCDDX</td><td>DDDDD.DEFFFY</td><td>FGGGG.GGHHHZ</td><td>K</td><td>UUUUVVVVVVVVVV</td></tr><tr><td>campo 1  
 10 dígitos</td><td>campo 2  
 11 dígitos</td><td>campo 3  
 11 dígitos</td><td>4</td><td>campo 5  
 14 dígitos</td></tr></tbody></table>Campo 1 (AAABC.CCDDX):

- AAA = código do banco – Itaú = 341;
- B = código da moeda – Real = 9;
- CCC = código da carteira de cobrança;
- DD = dois primeiros dígitos do *Nosso Número*;
- X = DAC  módulo 10 do campo 1;

Campo 2 (DDDDD.DEFFFY):

- DDDDDD = restante do *Nosso Número;*
- E = DAC do grupo *agência/conta/carteira/nosso número*;
- FFF = três primeiros números da agência;
- Y = DAC módulo 10 do campo 2;

Campo 3 (FGGGG.GGHHHZ):

- F = último número da agência;
- GGGGGG = conta corrente + DAC;
- HHH = zeros;
- Z = DAC módulo 10 do campo 3;

Campo 4 (K):

- K = DAC módulo 11 do código de barras (único DAC que vai para o código de barras);

Campo 5 (UUUUVVVVVVVVVV):

- UUUU = fator de vencimento;
- VVVVVVVVVV = valor do boleto, sem ponto e vírgula, ou zeros, no caso do valor ser preenchido pelo próprio sacado.

O* fator de vencimento* contém 4 dígitos e é o número de dias desde 7 de outubro de 1997,  servindo para indicar a data de vencimento do boleto (teremos o bug do <span style="text-decoration: line-through;">milênio</span> 21 de fevereiro de 2025?).

Seu cálculo é bem simples, como podemos ver pelo método abaixo:

private int FatorVencimento(DateTime date) { DateTime zeroDay = new DateTime(1997, 10, 7); return (date - zeroDay).Days; }

### DAC

Analisando as regras anteriores, temos que a maior parte do trabalho consiste-se em concatenar strings e calcular DACs.

Para criar nossa Linha Digitável iremos dispor de dois algoritmos para calcular os DAC:s o módulo 10 e o módulo 11.

O cálculo do DAC módulo 10 é realizado da seguinte forma. Tome o campo a ter calculado o DAC. Multiplique cada algarismo do campo pela sequência de multiplicadores 2, 1, 2, 1, 2, 1…, posicionados  
 da direita para a esquerda. Some os resultados, que chamarei de *N*.  
 Calcule o módulo 10 de N – **mod10(N)** ou **N%10**.  
 O DAC será **10 – mod10(N)**. Caso o DAC seja 10, considere-o como 0.

Segue abaixo um método para calcular o DAC módulo 10:

private int CalculaDacMod10(string campo) { int soma = 0; int m; // caso exista um número par de algarismos, inicia a mult. por 1 if ((campo.Length % 2) == 0) m = 1; else m = 2; foreach (char c in campo) { soma += Convert.ToInt32(c) * m; m = 3 - m; //regra aplicada: (x+y) - x = y; (x+y) - y = x } int dac = 10 - (soma % 10); if (dac == 10) return 0; return dac; }

O cálculo do DAC módulo 11 é bem semelhante.Ele depois será utilizado para compor o **DAC do código de barras**.

Tendo o trecho a ter o DAC calculado, tome seus algarismos e multiplique-os, iniciando-se da direita para a esquerda, pela sequência numérica de 2 a 9 ( 2, 3, 4, 5, 6,  
 7, 8, 9, 2, 3, 4… e assim por diante). Some o resultado obtendo nosso *N.*

Calcule agora o módulo 11 de *N* – **mod11(N)** ou **N%11**. O DAC será **11 – mod11(N)**. Caso o cálculo do DAC tenha dado 0, 10 ou 11, considere-o como 1.

O método abaixo faz o cálculo do DAC módulo 11:

private int CalculaDacMod11(string campo) { int soma = 0; int m = 2; //Invertendo a string, para facilitar o trabalho com os multiplicadores char [] arr = campo.ToCharArray(); Array.Reverse(arr); string reversed = new String(arr); foreach(char c in reversed) { soma += Convert.ToInt32(c) * m; m = (m + 1 > 9 ? 2 : m + 1); } int dac = 11 - (soma % 11); if (dac == 0 || dac == 10 || dac == 11) return 1; return dac; }

### Código de Barras

O padrão de código de barras para os boletos no Brasil é o denominado [**2 de 5 intercalado**]((http://www.barcodeman.com/info/c2of5.php), que pode ser resumido nas seguintes características:

- codifica apenas caracteres numéricos (*0-9*);
- cada caractere é representado por 5 barras, dentre os quais 2 são mais longas;
- codificação binária – largo é **1**, estreito é ***0***;
- os espaços também possuem signifcado, por isso o *intercalado*

Este código de barras serve apenas para representar nossa linha digitável, tranformado o que é uma seqüência de números em uma imagem. Existem muitos controles por aí que fazem isto, mas não encontrei nenhum gratuito para Asp.NET.

Neste exemplo vou utilizar o [barcodenet.net](http://barcodenet.net/). Ele pode ser testado e é completamente funcional, a diferença é que, enquanto você não resgistrá-lo,  ele  criará uma linha escrito *barcodenet.net* (ou algo assim) logo acima do código de barras.

Embora a linha digitável possua 47 dígitos, o número que será codificado em barras possui apenas 44. Por quê? Porque devemos nos livrar de três dos quatro DACs que constam nela. Assim o código de barra terá apenas um DAC.

Outra diferença importante é de que a ordem em que os campos se apresentam na linha digitável **não é a mesma** da apresentada pelo código de barras.

Segue como gerar então os dígitos que compõem o código de barras:

- 3 dígitos do código do Banco (341);
- 1 dígito com o código da moeda (3);
- 1 dígito do DAC do Código de Barras;
- 4 dígitos do fator de vencimento;
- 10 dígitos do valor do tíitulo, desconsiderando qualquer sinal de pontuaçaõ;
- 3 dígitos da carteira;
- 9 dígitos do Nosso Número mais seu próprio DAC;
- 4 dígitos da agência;
- 6 dígitos da conta corrente, com seu próprio DAC;
- 3 dígitos não utilizados e composto por zeros (000).

Depois de gerar os dígitos que compõem o código de barras, é questão de torná-lo em imagem utilizando o controle comentado anteriormente:

public byte[] CodigoBarras() { BarcodeNETWeb barcode = new BarcodeNETWeb(); barcode.BarcodeText = DigitosCodigoBarrasComDac(); barcode.BarcodeType = BARCODE_TYPE.INT2OF5; return barcode.GetBarcodeBitmap(FILE_FORMAT.PNG); }

### Código

Segue então a listagem do código fonte utilizado neste trabalho. Claro que há muito o que melhorar nele, mas isto fica como exercício. =)

Note que modifiquei a classe Dados do post anterior.

public class LinhaDigitavel { public int Banco { get; private set; } public int Moeda { get {return 9; }} public string CarteiraCobranca { get; private set; } public string NossoNumero { get; private set; } public string Agencia { get; private set; } public string ContaCorrente { get; private set; } public DateTime Vencimento { get; private set; } public decimal Valor { get; private set; } public LinhaDigitavel( int banco, string carteira, string nossonumero, string agencia, string contacorrente, DateTime vencimento, decimal valor) { this.Banco = banco; this.CarteiraCobranca = carteira; this.NossoNumero = nossonumero; this.Agencia = agencia; this.ContaCorrente = contacorrente; this.Vencimento = vencimento; this.Valor = valor; } public LinhaDigitavel(Dados dados) { this.Banco = dados.Banco; this.CarteiraCobranca = dados.Carteira; this.NossoNumero = dados.NossoNumero; this.Agencia = dados.Agencia; this.ContaCorrente = dados.ContaCorrente; this.Vencimento = dados.DataVencimento; this.Valor = dados.ValorDocumento; } public string FormatoParaImpressao() { return Campo1().Substring(0, 5) + "." + Campo1().Substring(5) + " " + Campo2().Substring(0, 5) + "." + Campo2().Substring(5) + " " + Campo3().Substring(0, 5) + "." + Campo3().Substring(5) + " " + Campo4() + " " + Campo5(); } public byte[] CodigoBarras() { BarcodeNETWeb barcode = new BarcodeNETWeb(); barcode.BarcodeText = DigitosCodigoBarrasComDac(); barcode.BarcodeType = BARCODE_TYPE.INT2OF5; return barcode.GetBarcodeBitmap(FILE_FORMAT.PNG); } private string Campo1() { string campo = this.Banco.ToString("000") + this.Moeda.ToString("0") + this.CarteiraCobranca.Trim() + this.NossoNumero.Split('-')[0].Substring(0, 2); if (campo.Length != 9) throw new Exception("Entrada inválida"); return campo + CalculaDacMod10(campo).ToString("0"); } private string Campo2() { string campo = this.NossoNumero.Split('-')[0].Substring(2, 6) + this.DacAgenciaContaCarteiraNossNumero().ToString("0") + this.Agencia.Substring(0, 3); if (campo.Length != 10) throw new Exception("Entrada inválida"); return campo + CalculaDacMod10(campo).ToString("0"); } private string Campo3() { string campo = this.Agencia.Substring(3, 1) + this.ContaCorrente.Split('-')[0] + this.ContaCorrente.Split('-')[1] //sinto falta de explode/implode + "000"; if (campo.Length != 10) throw new Exception("Entrada inválida"); return campo + CalculaDacMod10(campo).ToString("0"); } private string Campo4() { return DacCodigoBarras().ToString("0"); } private string Campo5() { return this.FatorVencimento().ToString("0000") + FormataValor(this.Valor); } private string FormataValor(decimal valor) { string[] value = this.Valor.ToString("00000000.00", System.Globalization.CultureInfo.InvariantCulture).Split('.'); return value[0] + value[1]; } private int DacAgenciaContaCarteiraNossNumero() { string termo = this.Agencia + this.ContaCorrente.Split('-')[0] + this.CarteiraCobranca + this.NossoNumero.Split('-')[0]; if (termo.Length != 20) throw new Exception("Entrada inválida"); return CalculaDacMod10(termo); } private int DacCodigoBarras() { return CalculaDacMod11(DigitosCodigoBarrasSemDac()); } private string DigitosCodigoBarrasSemDac() { string termo = this.Banco.ToString("000") + this.Moeda.ToString("0") + this.FatorVencimento().ToString("0000") + this.Valor.ToString("0000000000") + this.CarteiraCobranca + this.NossoNumero.Split('-')[0] + this.NossoNumero.Split('-')[1] + this.Agencia + this.ContaCorrente.Split('-')[0] + this.ContaCorrente.Split('-')[1] //sinto falta de explode/implode + "000"; return termo; } private string DigitosCodigoBarrasComDac() { string termo = DigitosCodigoBarrasSemDac(); return termo.Substring(0, 4) + DacCodigoBarras().ToString("0") + termo.Substring(4); } private int FatorVencimento() { DateTime zeroDay = new DateTime(1997, 10, 7); return (this.Vencimento - zeroDay).Days; } /// /// DAC móulo 10 /// Exemplo: /// Considerando-se a seguinte representação numérica do código de barras: /// 34191.1012? 34567.88005? 71234.57000? 6 16670000012345 /// Temos: /// a) Multiplicando a sequência dos campos pelo módulo 10: /// Campo 1 341911012 Campo 2 3456788005 Campo 3 7123457000 /// X 212121212 X 1212121212 X 1212121212 /// Observação: Os campos 4 e 5 não tem DAC /// b) Some, individualmente, os algarismos dos resultados do produtos: /// Campo 1 : 6 + 4 + 2 + 9 + 2 + 1 + 0 + 1 + 4 = 29 /// Campo 2 : 3 + 8 + 5 + 1 + 2 + 7 + 1 + 6 + 8 + 0 + 0 + 1 + 0 = 42 /// Campo 3 : 7 + 2 + 2 + 6 + 4 + 1 + 0 + 7 + 0 + 0 + 0 = 29 /// c) Divida o total encontrado por 10, a fim de determinar o resto da divisão: /// Campo 1 : 29 / 10 = 2, resto 9 /// Campo 2 : 42 / 10 = 4, resto 2 /// Campo 3 : 29 / 10 = 2, resto 9 /// d) Calculando o DAC: /// Campo 1 : DAC = 10 - 9 : DAC = 1 /// Campo 2 : DAC = 10 - 2 : DAC = 8 /// Campo 3 : DAC = 10 - 9 : DAC = 1 /// Portanto, a sequência correta da linha digitável será: /// 34191.10121 34567.880058 71234.570001 6 16670000012345 /// /// <span> </span> /// private int CalculaDacMod10(string campo) { int soma = 0; int m; // caso exista um número par de algarismos, inicia a mult. por 1 if ((campo.Length % 2) == 0) m = 1; else m = 2; foreach (char c in campo) { soma += Convert.ToInt32(c) * m; m = 3 - m; //regra aplicada: (x+y) - x = y; (x+y) - y = x } int dac = 10 - (soma % 10); if (dac == 10) return 0; return dac; } /// /// Considerando o seguinte conteúdo do Código de Barras: /// 3419?1667000001234511012345678800571423457000 /// onde: /// 341 = Código do Banco /// 9 = Código da Moeda /// ? = DAC do Código de Barras /// 1667 Fator de Vencimento (01/05/2002) /// 0000012345 = Valor do Título (123,45) /// 110123456788 = Carteira/Nosso Número/DAC (110/12345678-8) /// 0057123457 = Agência/Conta Corrente/DAC (0057/12345-7) /// 000 = Posições Livres (zeros) /// Temos: /// a) Multiplica-se a sequência do código de barras pelo módulo 11: /// 3419166700000123451101234567880057123457000 /// X 4329876543298765432987654329876543298765432 /// b) Soma-se o resultado dos produtos obtidos no item “a” acima: /// 12 + 12 + 2 + 81 + 8 + 42 + 36 + 35 + 0 + 0 + 0 + 0 + 0 + 7 + 12 + 15 + 16 + 15 + 2 + /// 9 + 0 + 7 + 12 + 15 + 16 + 15 + 12 + 63 + 64 + 56 + 0 + 0 + 20 + 21 + 2 + 18 + 24 + /// 28 + 30 + 35 + 0 + 0 + 0 = 742 /// c) Determina-se o resto da Divisão: /// 742 / 11 = 67, resto 5 /// d) Calcula-se o DAC: /// DAC = 11 – 5 então DAC = 6 /// Portanto, a sequência correta do código de barras será: /// 34196166700000123451101234567880057123457000 /// ^---DAC /// /// /// private int CalculaDacMod11(string campo) { int soma = 0; int m = 2; //Invertendo a string, para facilitar o trabalho com os multiplicadores char [] arr = campo.ToCharArray(); Array.Reverse(arr); string reversed = new String(arr); foreach(char c in reversed) { soma += Convert.ToInt32(c) * m; m = (m + 1 > 9 ? 2 : m + 1); } int dac = 11 - (soma % 11); if (dac == 0 || dac == 10 || dac == 11) return 1; return dac; } }

public class Dados { public DateTime DataDocumento { get; set; } public DateTime DataVencimento { get; set; } public DateTime DataProcessamento { get; set; } public string Cedente { get; set; } public string SacadoResumido { get; set; } public string SacadoCompleto { get; set; } public int Banco { get; set; } public string Agencia { get; set; } public string ContaCorrente { get; set; } public string CodigoCedente { get; set; } public int NumeroDocumento { get; set; } public string EspecieDocumento { get; set; } public string Aceite { get; set; } public string NossoNumero { get; set; } public string Carteira { get; set; } public string Instrucoes { get; set; } public int Quantidade { get; set; } public decimal Valor { get; set; } public decimal ValorDocumento { get; set; } public string CodigoBaixa { get; set; } public byte[] CodigoBarra { get { LinhaDigitavel linha = new LinhaDigitavel(this); return linha.CodigoBarras(); } } public string LinhaDigitavel { get { LinhaDigitavel linha = new LinhaDigitavel(this); return linha.FormatoParaImpressao(); } } }

Um exemplo de uso do gerador de boletos:

protected void btnGeraBoleto_OnClick(object sender, EventArgs e) { Boleto boleto = new Boleto(Portal.Controles.Boleto.Banco.ITAU, Server); List dados = new List (); dados.Add( new Portal.Controles.Boleto.Dados() { Aceite = "N", Agencia = "1234", Banco = 341, Carteira = "109", Cedente = "Indústria ACME", CodigoBaixa = "109/12345678-9", CodigoCedente = "12345-6", ContaCorrente = "12345-6", DataDocumento = DateTime.Now, DataProcessamento = DateTime.Now, DataVencimento = new DateTime(2009, 4, 5), EspecieDocumento = "DM", Instrucoes = @"Não receber após o vencimento", NossoNumero = "12345678-9", NumeroDocumento = 0000000012, Quantidade = 0, SacadoCompleto = @"Padoca do Zé - LTDA CNPJ - 12.345.678/0001-23 Rua das Casas, 123 01234-123 Vl do Bairro Sao Paulo SP", SacadoResumido = "Padoca do Zé - LTDA", Valor = 0, ValorDocumento = 2637.00m }); boleto.Baixa(Response, dados); }

### Fechando

Embora existam outras opções, como cartões de crédito e pagamento direto online, o boleto ainda é utilizado devido à familiaridade e facilidade de pagamento por parte do comprador. Por isso temos de saber gerá-lo em nossos sistemas, mesmo que utilizemos soluções prontas.

Vimos que gerar um boleto na plataforma .Net é algo simples, composto por uma guia impressa, alguma lógica para a geração da linha digitável e uma ferramenta de terceiros para a criação do código de barras. A parte mais difícil fica no sistema subjacente, não abordada, onde entra o retorno do pagamento do boleto e finalmente na remessa da mercadoria. Mas isto fica para uma próxima.


