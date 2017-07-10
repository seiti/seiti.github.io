---
layout: post
title: Múltiplas imagens no topo do seu blog
date: '2009-05-02 00:40:33'
tags:
- css
- design
- php
---


Cansado de olhar a mesma imagem na testeira do meu blog (que nem uma foto era, apenas uma imagem artificial), decidi trocá-la. Por **oito outras**.

Oito? Sim, mas elas são trocadas aleatoriamente (randômico não existe!) a cada *reload* da página.

Como? Usando PHP, é claro!

[![](http://farm4.static.flickr.com/3591/3483991793_09e05d8b1d_m.jpg)](http://www.flickr.com/photos/seiti/3483991793/)

Darei algumas instruções logo abaixo,  que **não** são específicas do WordPress.

Primeiro eu criei um arquivo *CSS* denominado *multiple_header_images.css.php* (é verdade, basta olhar no código fonte daqui do blog). Este arquivo é um script php que gera um arquivo css. Para isto basta colocar uma linha especial logo no início do arquivo:

<?php header("Content-Type:text/css"); ??>

E por quê PHP? Para poder trocar o arquivo de imagem carregado pelo css. Basta observar o arquivo completo para entender:

<?php header("Content-Type:text/css"); ??>
 #header { background:url(img/header_ echo rand(1,8);?>.jpg) 0 0 no-repeat !important; }

Note a tag echo rand(1,8);?>. Ela gera um número aleatório entre 1 e 8. A cada vez que o arquivo css é carregado ele vem com um conteúdo ligeiramente diferente. Ora ele carrega uma imagem *header_1.jpg*, ora uma *header_5.jpg* e assim em diante.

Claro que é preciso criar as 8 imagens, nomeá-las header_1.jpg, header_2.jpg etc, e depois colocá-las no local apropriado, no meu caso na pasta **img** (todas as imagens que utilizei foram fotografadas por mim! :-)).

A diretiva **!important** serve para assegurar que o meu css referente ao #header terá precedência sobre o outro #header que já existe em algum outro lugar do passado.

E é só! <del datetime="2009-04-29T04:00:14+00:00">Roubei</del> Me inspirei [neste](http://www.robservatory.com/?p=191) post.


