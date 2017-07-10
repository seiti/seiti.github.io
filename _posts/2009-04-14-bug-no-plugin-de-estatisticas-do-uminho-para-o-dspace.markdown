---
layout: post
title: Bug no Plugin de estatísticas do UMinho para o DSpace
date: '2009-04-14 02:44:49'
tags:
- bug
- dspace
---


O [DSpace](http://www.dspace.org/) é um sistema de armazenamento digital. O [plugin de estatísticas](http://wiki.dspace.org/index.php/StatisticsAddOn) foi desenvolvido pelo pessoal da [Universidade do Minho](https://repositorium.sdum.uminho.pt/).

Notei que o plugin não estava funcionando, após a [epopéia da instalação](http://seiti.eti.br/blog/2009/addon-de-estatisticas-do-dspace).

No arquivo *dspace-1.4-source/src/org/dspace/stats/util/Country.java*, a linha 63 faz referência a um arquivo cujo caminho está **hardcoded**:

String dbfile = "/dspace/config/stats/GeoIP.dat";

Infelizmente o caminho para o arquivo em meu sistema fica em outro lugar. O melhor seria configurar isto em um arquivo separado. Mas por enquanto deixo assim:

String dbfile = "/opt/dspace/config/stats/GeoIP.dat";

Compile o código e faça o deploy dos arquivos *war*. Não se esqueça de logar no banco de dados Postgresql e rodar a seguinte consulta:

SELECT sqlj.replace_jar('file:///opt/dspace/lib/dspace.jar', 'dspace', true);

Note o **replace**_jar. Aponte para o caminho correto do arquivo.


