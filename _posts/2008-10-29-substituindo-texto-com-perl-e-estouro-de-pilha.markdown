---
layout: post
title: Substituindo texto com Perl e Estouro de Pilha
date: '2008-10-29 23:45:33'
tags:
- perl
- script
- visual-studio
---


Vez por outra chega a hora de reformular a estrutura do seu projeto, organizando melhor onde devem se localizar alguns arquivos. Isto ocorre principalmente quando seu projeto começa pequeno e vai crescendo aos poucos, mas inexoravelmente .

Isto ocorreu em um projeto em que estou trabalhando, e após trocar os arquivos de lugar é preciso atualizar todas as referências que apontavam para o antigo local do arquivo. É aqui que entram as *expressões regulares*, ou **regex**.

Qualquer IDE atual nos dá a possibilidade de utilizarmos expressões regulares nas ferramentas *find & replace*. No Visual Studio, por exemplo, para substituir um texto do tipo:

Src = "../AlgumArquivo.ascx"

Para

Src = "~/APasta/AlgumArquivo.ascx"

Basta pressionar CTRL+SHIT+H e preencher os campos de substituição com:

Src:b*=:b*"(\.\./)+/{:a+}.ascx"

e

Src="~/APasta/\1.ascx"

### Hora do café

![](http://i.msdn.microsoft.com/bb969057.VS08CorpBlue220(en-us).png "VS2008")![](http://upload.wikimedia.org/wikipedia/commons/thumb/f/f5/Cup-o-cofee-simple.svg/200px-Cup-o-cofee-simple.svg.png "Café")

O problema é que uso o **Visual Studio 2008**, e com isto preciso de um de dois pré-requisitos para a substituição ser viável:

1. ter um projeto bem pequenininho;
2. ter bastante tempo (e paciência).

Bom, como o problema que quero solucionar vem do fato do projeto ter crescido, então (1) não ocorre. E ultimamente ando sem paciência… Quando eu tentava substituir os textos no arquivos do projeto pelo Visual Studio, eu podia ir tomar uma água, depois um café, visitar o banheiro e retornar antes do término da substituição.

Bom, a solução é **Perl**. Mas daí surge outro problema, devem fazer alguns séculos que não programo em Perl, mas o pouco que sei é que deve existir uma maneira de resolver isto.

Acabei encontrando algumas soluções, até instalei o *Cygwin+ActivePerl *aqui no Windows Vista, mas ainda assim não consegui um script decente.

### Estourando a pilha

![](http://stackoverflow.com/Content/Img/stackoverflow-logo-250.png "Stackoverflow")

Tenho visitado bastante o [stackoverflow.com](http://stackoverflow.com). É um ótimo site para programadores darem dicas, fazerem perguntas, obterem respostas, interagirem. Mas eu apenas visitava para ler os textos e aprender alguma coisa.  Resolvi então buscar [ajuda para o meu pequeno script](http://stackoverflow.com/questions/248668/bulk-file-text-substitution-in-place-any-simple-way-to-do-that).

Postei minha dúvida e um script simples que comecei a escrever. Em alguns **minutos** já havia uma resposta.

Em cerca de **três** horas (!!!) obtive mais respostas, muito boas, e dentre elas uma que me resolveu o problema. Impressionante! Isto mostra a força dos sistemas colaborativos.


