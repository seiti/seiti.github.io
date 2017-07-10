---
layout: post
title: Cache e camadas no ArcGIS Server
date: '2010-02-08 16:59:30'
tags:
- arcgis
- gis
---


Estou trabalhando com o ArcGIS Server 9.3.1 e tenho de inserir alguns serviços nele. Cada serviço corresponde à uma camada, ou * layer*, em meu mapa.

Para melhorar o  desempenho – sofrível se comparado com o [MapServer](http://mapserver.org/) – existe uma opção para a utilização de *cache* no ArcGIS Server que funciona bem. Ao invés do servidor ter de reconstruir a imagem, toda vez que ela é requisitada, ele gera esta imagem apenas uma vez, grava em algum lugar e depois apenas a repassa para o servidor de aplicação.

Isto gerou um problema. Quando as imagens era geradas dinamicamente, havia a possibilidade do ArcGIS Server reprojetar e/ou reposicionar o mapa para  combiná-la com todos os layers.  Se um serviço usa EPSG:[4618](http://spatialreference.org/ref/epsg/4618/) e outro usa [SR-ORG:95](http://spatialreference.org/ref/sr-org/95/),  por exemplo. Mas com o uso do cache, a imagem criada possui apenas o sistema de referenciamento definida no serviço, não podendo mudar.

Assim, ao combinar dois layers cujos sistemas de referenciamento espacial são diferentes, temos as seguintes situações:

- Os dois layers são dinâmicos:  um sistema é escolhido e os dois layers utilizam este;
- Um dos layers é dinâmico e o outro possui cache: o dinâmico é projetado/adaptado ao sistema do que tem cache;
- Os dois layers usam cache: apenas um deles é exibido. Não há reprojeção.

O ideal então é manter um único sistema de referenciamento espacial nos serviços. E aproveitar para deixar todos no [SIRGAS2000](http://seiti.eti.br/blog/2010/sirgas-2000).


