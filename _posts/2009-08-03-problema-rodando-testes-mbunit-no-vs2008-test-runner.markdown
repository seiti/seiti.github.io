---
layout: post
title: Problema rodando testes MbUnit no VS2008 Test Runner
date: '2009-08-03 14:30:17'
tags:
- aspnet
- test
---


Importei um projeto para trabalhar em meu Visual Studio 2008. Ao tentar rodar os testes, que utilizam o framework MbUnit, fui contemplado com a seguinte mensagem:

> No tests were run because no tests are loaded or the selected tests are disabled

O problema é que o projeto de testes é tratado como uma simples biblioteca de classes, embora seus métodos sejam decorados com atributos [Test] e similares.

E como fazer o VS2008 entender que o projeto em questão é de **testes**? É necessário abrir o arquivo <tt>.csproj</tt> correspondente ao projeto e incluir o seguinte:

<projecttypeguids> {3AC096D0-A1C2-E12C-1390-A8335801FDAB};{FAE04EC0-301F-11D3-BF4B-00C04F79EFBC} </projecttypeguids>

Logo antes do primeiro <tt></tt> do arquivo. O VS2008 verifica o tipo do projeto em questão através destes identificadores. E como encontrei estes números? Criei um projeto de testes MSTest pelo VS2008 e abri o .csproj.

E [encontrei o significado ](http://alexduggleby.com/2008/02/19/turning-a-class-library-project-into-a-mstest-project-or-using-mbunit-mstest-and-other-frameworks-in-one-project/#comment-1252) destes guids:

- <tt>{3AC096D0-A1C2-E12C-1390-A8335801FDAB}</tt> identifica um *Test Project*
- <tt>{FAE04EC0-301F-11D3-BF4B-00C04F79EFBC}</tt> identifica um *Windows Forms C# Project*


