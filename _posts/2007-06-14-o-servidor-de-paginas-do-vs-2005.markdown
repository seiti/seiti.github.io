---
layout: post
title: O servidor de páginas do VS 2005
date: '2007-06-14 19:38:46'
tags:
- iis
- wtf
---


Hoje reparei em uma coisa, que quase me fez perder os cabelos.

Os links para algumas imagens em uma página aspx não apareciam na minha máquina. Daí reparei que os links estavam assim:

<div class="code">![](/caminho/para/imagens//imagem.gif)

</div>Reparou na dupla barra? Isto fazia com que não aparecesse a imagem aqui, tanto no IE quanto no FF. Depois de quebrar a cabeça um tempão, tentando fazer com que os image links (gerados por um template column em um datagrid) tivessem o src correto, verifiquei que no servidor, com o fonte do aspx idêntico ao meu, funcionava!

Tanto na própria máquina do servidor quanto na minha, acessando pelo navegador de minha máquina local. Percebi que isto era problema do servidor de páginas, e não de qqer outra coisa.  
 O servidor embutido (Cassini) no VS2005 se embanana e não consegue entregar a imagem quando existe // no endereço. =(

O IIS entrega a imagem sem problemas…. =)


