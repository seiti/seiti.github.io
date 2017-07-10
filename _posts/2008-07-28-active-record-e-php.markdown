---
layout: post
title: Active Record e PHP
date: '2008-07-28 22:15:22'
tags:
- design-patterns
- php
---


[Active Record](http://en.wikipedia.org/wiki/Active_record_pattern) é um padrão de projeto bem freqüente nas aplicações que guardam seus dados em bancos de dados (BD). Tão usual e freqüente que na maior parte das vezes este padrão é utilizado sem que seu nome seja conhecido.

Este padrão consiste na ligação existente entre a modelagem da **aplicação** e a do BD. Uma classe corresponde à uma tabela, um objeto corresponde à uma linha da tabela. Um relacionamento entre tabelas é traduzido como uma associação entre objetos.

Ao programar uma loja virtual em PHP, tentei implementar este padrão. A maior dificuldade que tive foi no momento em que os objetos estavam inter-relacionados e um update deveria se propagar em cascata. De duas uma: ou você resolve isto via *Stored Procedures* – ou algo equivalente do lado do BD, ou por meio de *transações* dentro da aplicação – usualmente com a ajuda do [PEAR::MDB2](http://pear.php.net/package/MDB2 "MDB2").

Bom, depois desta experiência, passei a utilizar o padrão **DAO** e *arquitetura em camadas* no PHP (e Ajax+Web Services, mas isto é outra história).  Mas agora tô morrendo de vontade de conhecer o ***Ruby on Rails***…


