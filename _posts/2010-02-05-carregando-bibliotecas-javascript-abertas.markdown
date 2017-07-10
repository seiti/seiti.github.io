---
layout: post
title: Carregando bibliotecas Javascript abertas
date: '2010-02-05 12:49:34'
tags:
- javascript
---


Ext, jQuery, prototype, MooTools, Dojo, scrip.taculo.us, YUI. São algumas das feras que um desenvolvedor web tem de enfrentar, no caminho para [matar o Dragão](http://www.scribd.com/doc/320372/How-to-kill-a-Dragon-with-Programming).

Algo que pode ajudar nesta tarefa é usar a própria API Google para carregar estas outras APIs:

[http://code.google.com/apis/ajaxlibs/](http://code.google.com/apis/ajaxlibs/)

O código, retirado direto do site, é o seguinte:

 // Load Google JS API <script src="http://www.google.com/jsapi"></script><script>
// Load jQuery
google.load("jquery", "1");
</script>

Você simplesmente:

- carrega a API javascript do Google;
- utiliza a API do Google para carregar as outras APIs, podendo escolher a versão, inclusive.

A opção de escolher a versão do script ajuda bastante a manter seus sistemas atualizados de forma bem simples.

O problema é apenas não poder guardar as APIs no servidor. Em uma rede local sem acesso à internet, por exemplo, isto já não serve.


