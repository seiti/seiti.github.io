---
layout: post
title: Campo DateField em um formulário ExtJS
date: '2008-07-24 11:33:26'
tags:
- extjs
- javascript
- programacao
---


Estou usando o [ExtJS](http://extjs.com/products/extjs/ "ExtJS") em alguns projetos, e estou muito satisfeito com ele. No início, como em todo *framework*,  é meio complicado de entender. Mas basta ler e testar os vários exemplos que vem junto do código.

Só fiquei decepcionado ao me deparar com um problema na hora de editar um campo *DateField*. Mesmo após ter corretamente configurado os objetos **Record**, **ColumnModel** (para colocar no meu grid) etc e tal, eu consigo visualizar a data, eu consigo editá-lo, mas ao salvar o ExtJS cria uma data [quase, mas nem tanto, completamente diferente](http://en.wikipedia.org/wiki/Notable_phrases_from_The_Hitchhiker%27s_Guide_to_the_Galaxy) da que eu inseri.

Como todo bom programador, achei que a culpa era minha e fiquei remoendo o código e fazendo testes sem resultado. E como todo bom programador fiz várias consultas ao [oráculo](http://www.google.com "O oráculo"). Até encontrar [isto](http://extjs.com/forum/showthread.php?t=40738 "OMG").

Procurei pelo SVN e encontrei. Infelizmente a versão que está no [Google Code](http://code.google.com/p/extjs-public/ "SVN") não é a mais atual, é a versão de lançamento que data de abril deste ano (2008).

Olhando no site do ExtJS vi que é preciso **pagar** para acessar os repositórios de desenvolvimento. Bom, agora preciso de US$ 299 para ter acesso ao servidor de versionamento do ExtJS…

*C’est la vie*


