---
layout: post
title: Graft, rollback, commit nunca mais!!
date: '2014-03-15 00:04:57'
tags:
- hg
- mercurial
---


Alguns devs fazem grafts de uma branch para outra e, para ajustar arquivos e mesmo melhorar os comentários, executam um rollback do resultado do graft e depois fazem o commit:

$ hg graft 123412341234 $ hg rollback $ hg ci -m "msg melhor"

<figure class="wp-caption aligncenter" id="attachment_1317" style="width: 188px;">[![rollbaaaack!!](http://seiti.eti.br/blog/wp-content/uploads/2014/03/Rollback-188x300.png "rollbaaaack!!")](http://seiti.eti.br/blog/wp-content/uploads/2014/03/Rollback.png)<figcaption class="wp-caption-text">rollbaaaack!!</figcaption></figure>Tenho dúvidas se esta é a melhor abordagem para resolver o problema. Bom,  
 isto não é necessário.

Pode-se usar o argumento –amend no commit:

$ hg graft 12341234123 $ hg ci -m "msg melhor" --amend

e pronto. Pode-se inclusive editar/incluir/remover arquivos e ir ajustando o último commit:

$ echo 'conteudo' > arquivo_que_preciso_incluir.sql $ hg addremove $ hg ci -m "msg melhor" --amend

Observação

É necessário uma versão do mercurial >= 2.2. A que vem por padrão nos repositórios do Ubuntu 12.04 é a versão 2.0.x. Para instalar uma versão mais atual recomendo o seguinte PPA:

[https://launchpad.net/~tortoisehg-ppa/+archive/releases](https://launchpad.net/~tortoisehg-ppa/+archive/releases "https://launchpad.net/~tortoisehg-ppa/+archive/releases")

Instale assim:

$ sudo add-apt-repository ppa:tortoisehg-ppa/release $ sudo apt-get install tortoisehg

E você ainda ganha o tortoisehg, muito útil para se fazer consultas no hg.


