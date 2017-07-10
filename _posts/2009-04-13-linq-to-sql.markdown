---
layout: post
title: Linq to Sql
date: '2009-04-13 18:25:24'
tags:
- aspnet
- bug
- linq
- orm
---


Ando utilizando o Linq To SQL, um mapeador objeto relacional da própria Microsoft, que facilita a vida de quem tenta transformar objetos em tabelas e vice-versa.

Embora a ferramenta seja muito boa, o modo como você configura este mapeamento é um tanto… estilo Microsoft de se fazer as coisas. Você deve criar um arquivo do tipo *Linq To Sql Classes*, que não passa de um xml com a extensão **dbml**. Este arquivo xml orienta o compilador a criar as classes dinamicamente .

O problema fica na atualização deste arquivo. Você deve necessariamente abrir o arquivo, no Visual Studio, remover as tabelas atualizadas, e inserí-las novamente. Existe outra solução, mas preciso investigar o executável de linha de comando *SqlMetal.exe*. Enquanto isto fico editando o dbml.

Outro problema é definir a connection string, que fica embutida no dbml. Caso você necessite definir a *connection string* para que seja lida a partir do *web.config*, basta implementar um construtor no *code-behind* do dbml:

 namespace Portal.Ferramentas.Evento { using System.Configuration; partial class EventoL2SDataContext { public EventoL2SDataContext() : base(ConfigurationManager.ConnectionStrings["constr"].ConnectionString) { OnCreated(); } } }

E limpe as proriedades relacionadas com conexão ao banco de dados do dbml.

Nota: Lembre-se de colocar as diretivas de importação de bibliotecas (os *using*s) **dentro** do *namespace*. Senão surgirá um erro muito interessante: *[Error unespecified](http://dscheidt.spaces.live.com/blog/cns!75582706FFDC005!1345.entry)*, ao se clicar em **View Code** no menu interativo do dbml.


