---
layout: post
title: Gerando boletos bancários em Asp.NET - Parte I
date: '2009-05-13 21:54:15'
tags:
- aspnet
- boleto
- crystal-reports
- linq
- linq-to-sql
- programacao
---


Estou em um projeto que necessita a criação de um boleto bancário para o pagamento de um serviço. Como gerá-lo, usando o Visual Studio 2008, Crystal Reports e o [Linq To Sql](http://seiti.eti.br/blog/2009/boas-praticas-em-linq-to-sql) ?

### Boleto?

Vamos primeiro entender do que é composto basicamente um boleto:

- **Banco**:  quem gerencia a transação;
- **Cedente**:  quem vai receber a grana;
- **Sacado**:  quem paga;
- **Valor do documento**: quanto será pago
- **Data de vencimento**: até quando pode ser pago;
- **Modalidade**:  com ou sem registro. O comum para vendas online é *sem registro*.  Se o sacado não pagar, a responsabilidade de correr atrás é do cedente.

A entidade que padroniza os boletos no Brasil é  a Federação Brasileira de Bancos – [FEBRABAN](http://www.febraban.com.br).

É claro que o desenvolvedor deve conhecer mais que o básico, caso queira gerar um boleto.  Segue então o modelo do boleto do Itaú.  Mas note que ainda assim a descrição está resumida:[![Modelo de boleto Itaú](http://farm4.static.flickr.com/3398/3525955045_d49dbcd0f5_o.png)](http://www.flickr.com/photos/seiti/3525955045/ "Modelo de boleto Itaú")

**1** – *Nome do banco*, que pode conter também seu logotipo;

**2** –* Código do banco*, com seu respectivo DV;

**3** – *Local de pagamento*;

**4** – *Data do documento,* que é  quando ele foi gerado;

**5** – *Número do documento*, obrigatório para carteiras sem registro

**6** – *Carteira*, não utilizado pelo Itaú

**7** – *Espécie*, use R$ para usar nossa moeda

**8** – *Agência/Código Cedente*,  no formato 1234/56789-7 e  *Nosso Número*, no formato 123/45678901-5

**9** – Uso exclusivo do funcionário caixa

**10** – *Instruções*, condições para recebimento,  dados sobre multas por atraso, bancos autorizados etc.

A duas listagens acima já ajudam o programador a saber quais dados ele **precisa** ter à mão para gerar um boleto bancário. Alguns itens do boleto deverão ser **criados automaticamente** pelo sistema a partir destes dados, tais como a *linha digitável* e o *código de barras*.

Uma excelente fonte de documentação se encontra em [http://www.phpboleto.com.br/](http://www.phpboleto.com.br/). Lá existem outros modelos disponíveis para download.  E,  se seu projeto é em PHP, recomendo utilizá-lo!

Outro lugar legal para se informar é o site [macoratti.com](http://www.macoratti.net/boleto.htm).

### Criando um template

Por meio do *Crystal Reports*, que já vem no Visual Studio 2008, criei o seguinte template:

[![Template do boleto do Itaú no Crystal Reports](http://farm4.static.flickr.com/3541/3528627827_0cc3fcfaee_o.png)](http://www.flickr.com/photos/seiti/3528627827/ "Template do boleto do Itaú no Crystal Reports")

Note que ele contém só o esqueleto. Nenhum campo dinâmico foi adicionado (bom, talvez a **espécie**, que considerei ser sempre R$) ainda.

Template pronto,  precisamos dos dados para populá-lo. Criei uma classe cujas propriedades são os dados a serem inseridos no boleto:

namespace namespace Portal.Controles.Boleto { public class Dados { public DateTime DataDocumento { get; set; } public DateTime DataVencimento { get; set; } public DateTime DataProcessamento { get; set; } public string Cedente { get; set; } public string SacadoResumido { get; set; } public string SacadoCompleto { get; set; } public string Agencia { get; set; } public string CodigoCedente { get; set; } public int NumeroDocumento { get; set; } public string EspecieDocumento { get; set; } public string Aceite { get; set; } public string NossoNumero { get; set; } public string Carteira { get; set; } public string Instrucoes { get; set; } public int Quantidade { get; set; } public decimal Valor { get; set; } public decimal ValorDocumento { get; set; } public string CodigoBaixa { get; set; } public bytes[] CodigoBarra { get; set; } public string LinhaDigitavel { get; set; } } }

Agora é preciso terminar o template do boleto. Ao compilar o projeto podemos inserir as propriedades da classe acima em nosso template.

Para adicionar  a classe recém criada como fonte de dados (*Data Source*) é só ir para *DataBase Fields → DataBase Expert*:

[![DataBase Fields -> Expert](http://farm3.static.flickr.com/2384/3529470418_1d040bb663_o.png)](http://www.flickr.com/photos/seiti/3529470418/ "DataBase Fields -> Expert")

Na caixa de diálogo que se abre, é só escolher a classe recém criada.  Ficam à  disposição  todas as propriedades necessárias para popular o boleto:

[![DataBase Fields](http://farm4.static.flickr.com/3374/3529475678_9c499b492e_o.png)](http://www.flickr.com/photos/seiti/3529475678/ "DataBase Fields")

Por meio do famigerado *arrastar e soltar*, é só terminar de criar o template, colocando os campos nos lugares corretos. Um trabalho simples, mas meio chato,  eu sei.

### Testando a geração do boleto

Template pronto. Posso então criar uma classe encarregada de pegar os **dados**, pegar o **template**,****juntá-los e serví-los. A classe não tem nada de mais, e está preparada para funcionar em ambiente Asp.NET:

namespace Portal.Controles.Boleto { public enum Banco { ITAU } public class Boleto { CrystalDecisions.CrystalReports.Engine.ReportDocument rel; public Boleto(Banco banco, HttpServerUtility server) { rel = new CrystalDecisions.CrystalReports.Engine.ReportDocument(); rel.Load(GetTemplateFilePath(banco, server)); } public void Baixa(HttpResponse response, IEnumerable dataSource) { rel.SetDataSource(dataSource); rel.ExportToHttpResponse( CrystalDecisions.Shared.ExportFormatType.PortableDocFormat, response, true, string.Format("Boleto_{0}.pdf", DateTime.Now.Date.ToShortDateString())); } protected string GetTemplateFilePath(Banco banco, HttpServerUtility server) { switch (banco) { case Banco.ITAU: return server.MapPath("~/Controles/Boleto/TemplateItau.rpt"); default: throw new Exception("Este tipo de boleto não foi implementado ainda"); } } } }

É claro que muita coisa na classe pode ser melhorada, como o caminho até o arquivo do template, que está *hardcoded*. Mas já funciona e está preparado para funcionar com mais de um tipo de template.

Como testar então o danado?

Criei uma página ASPX contendo um botão. Vinculei um método ao evento **OnClick**. O corpo do método segue abaixo:

protected void botao_OnClick(object sender, EventArgs e) { Portal.Controles.Boleto.Boleto boleto = new Portal.Controles.Boleto.Boleto(Portal.Controles.Boleto.Banco.ITAU, Server); List dados = new List (); dados.Add( new Portal.Controles.Boleto.Dados() { Aceite = "N", Agencia = "1234", Carteira = "123", Cedente = "Indústria ACME", CodigoBaixa = "123/12345678-9", CodigoBarra = File.ReadAllBytes(Server.MapPath("~/Caminhp/para/uma/imagem.jpg")), CodigoCedente = "12345-6", DataDocumento = DateTime.Now, DataProcessamento = DateTime.Now, DataVencimento = DateTime.Now.AddDays(5), EspecieDocumento = "AB", Instrucoes = @"Sujeito a protesto se ñao for pago no vencimento no vencimento pagavel em qualquer agenia bancaria apos vencimento cobrar R$ 0,42 por dia de atraso apos vencimento cobrar multa de R$ 6,66", LinhaDigitavel = "12345.12345 12345.123456 12345.123456 1 1230000066600", NossoNumero = "123/12345678-9", NumeroDocumento = 123456890, Quantidade = 0, SacadoCompleto = @"Dino da Silva Sauro CNPJ - 12.345.678/123-11 Rua das Casas, S/N 01111-111 Vl Das Ruas Sao Paulo SP", SacadoResumido = "Dino da Silva Sauro", Valor = 0, ValorDocumento = 666 }); boleto.Baixa(Response, dados); }

Ou seja, crie uma lista, lhe adicione um objeto passe tudo e mais um pouco para a classe Boleto e chame o método *Baixa*. Um boleto em pdf será gerado e entregue ao usuário pelo navegador.

### E agora?

Agora que já temos a geração de um boleto *dummy* funcionando, precisamos acertar os dados que o compõem.

Existem regras para a linha digitável, precisamos calcular alguns dígitos verificadores e ainda gerar a imagem correspondente ao código de barras.

Isto fica para a **Parte II**! Aguardem!  
 [**Atualização**: [Template do boleto](http://dl.dropbox.com/u/2295190/blog/TemplateItau.zip) no Crystal Reports]  
 [**Atualização**: Segunda parte no ar!  
[http://seiti.eti.br/blog/2009/gerando-boletos-bancarios-em-aspnet-parte-ii](http://seiti.eti.br/blog/2009/gerando-boletos-bancarios-em-aspnet-parte-ii)]


