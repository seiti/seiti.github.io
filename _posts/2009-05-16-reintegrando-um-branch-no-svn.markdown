---
layout: post
title: Reintegrando um branch no SVN
date: '2009-05-16 09:09:49'
tags:
- subversion
---


No meu trabalho utilizamos o excelente [Subversion](http://seiti.eti.br/blog/2006/subversion) já há algum tempo (nem gosto de lembrar da época de zipar aquivos, colocar em uma pasta compartilhada da rede, nomear os zips com a data, sua cópia do projeto sempre diferente das dos colegas etc e tal).

Mas só há algum tempo começamos a nos organizar um pouco melhor e utilizar o esquema de *trunk, branches e tags*.

E um problema surgiu ao tentarmos reintegrar um *branch* ao *trunk*:

> Retrieval of mergeinfo unsupported

Que diabos é isto? Após pesquisar no [oráculo](http://www.google.com) descobri que se trata de uma atualização do Subversion ocorrida entre as versões 1.4 e 1.5 que adicionaram novas funcionalidades.

Entretanto, para que estas funcionalidades sejam utilizadas é necessário atualizar seu repositório através do comando **[svnadmin upgrade](http://subversion.tigris.org/svn_1.5_releasenotes.html#repos-upgrades)**:

svnadmin upgrade caminho_do_repositorio

Feito isto, tudo ok!


