---
layout: post
title: ArcGIS Javascript, Dojo e o método require
date: '2009-09-16 20:30:21'
tags:
- arcgis
- gis
- javascript
---


Ando investigando a API [Javascript ArcGIS](http://resources.esri.com/arcgisserver/index.cfm?fa=JSAPIs). Esta API é escrita em cima do framework [Dojo](http://dojotoolkit.org/), que provê um monte de funções úteis, além de um biblioteca bacana de *widgets*.

Tentando criar um código [JS mais organizado](http://en.wikipedia.org/wiki/Mission:_Impossible), encontrei o método [*dojo.require*](http://docs.dojocampus.org/dojo/require), que, em conjunto dos métodos *dojo.declare* e *dojo.provide*, devolvem um pouco de sanidade ao programandor.  Ele funciona da seguinte maneira.  Você inventa um namespace/pacote,  e depois associa um caminho à ele:

dojo.registerModulePath( "pacote", "http://localhost/scripts/")

E depois pode incluir ou importar pacotes assim:

dojo.require("pacote.MinhaClasse");

A mágica é que o arquivo ***http://localhost/scripts/MinhaClasse.js*** é carregado automaticamente. Legal! Parecido com Java, C# e um monte de outras linguagens. Agora vou criar arquivos correspondentes às classes que criarei, e organizar a macarronada Javascript.

<span style="text-decoration: line-through;">Mas não. A API Javascript ArcGIS, por alguma razão, procura pelo arquivo ***http://localhost/scripts/MinhaClasse.xd.js*** !!! De onde saiu este **xd**? E mesmo criando o arquivo que ele espera, seu conteúdo não é processado da forma correta.</span>

<span style="text-decoration: line-through;">Elaborando alguns testes eu susbtitui a referência:</span>

> <span style="text-decoration: line-through;"><script src="”http://serverapi.arcgisonline.com/jsapi/arcgis/?v=1.4″" type="”text/javascript”"></script></span>

<span style="text-decoration: line-through;">pela:</span>

> <span style="text-decoration: line-through;"><script src="”http://dojotoolkit.org/sites/all/modules/dojo/dtk_build/dojo/dojo.js”" type="”text/javascript”"></script></span>

<span style="text-decoration: line-through;">E funcionou ok. Parece que a versão do dojo entregue pela ESRI no ArcGIS não permite o uso do *dojo.require*. Para que isto seja possível, é necessário compilar o dojo de forma a permiti-lo carregar arquivos de domínios distintos, ou [*cross domain*](http://www.dojotoolkit.org/node/17). Mas na API da ESRI não dá. Pena.</span>

Encontrei como resolver o problema:

 djConfig = { parseOnLoad: true, baseUrl: "./scripts", modulePaths: { "minhasClasses": "./minhasClasses", "meusDijits": "./BLA" }, isDebug: true }

Isto me ensina a aprender direito antes de escrever! =)


