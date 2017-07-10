---
layout: post
title: Upgrade no PostGIS
date: '2009-08-11 19:48:35'
tags:
- gis
---


Algumas vezes é necessário um upgrade no banco de dados. E chegou a vez do PostgreSQL, para ir da versão 8.2 para a 8.3.  Aproveitando, fiz um upgrade do PostGIS 1.1.6 para a versão 1.4.  Surpreendentemente não ocorreram grandes problemas. Quer dizer, não até eu migrar os dados.

O próprio PostGIS possui um [script para migração de dados](http://postgis.refractions.net/docs/ch02.html#hard_upgrade). Se trata de um script *Perl* que recebe um dump do PostgreSQL e mais alguns outros parâmetros, trata-os gerando um novo dump e depois finalmente faz o *restore* do dump no banco de dados.

### Problemas

Parecia tudo ok, até eu tentar fazer um backup do novo banco:

> ERROR:  geometry contains non closed rings

Será que os dados se corromperam durante a migração?

O PostGIS 1.4 é um pouco mais restritivo quanto aos dados que armazena. Um *multipolygon *ou *polygon*, por exemplo, só podem ser inseridos no sistema se estiverem bem formados, o que significa que devem ser polígonos **fechados** (hmm,  e existe “polígono aberto”?).

O problema é que a versão 1.1.6 é mais, digamos, liberal. Você consegue gravar “polígonos  abertos”, consegue fazer *SELECT*s e backups em cima deles. Apenas operações  que envolvam as formas geométricas podem dar problema.

E o processo de migração de dados não realiza nenhuma verificação de validade destas entidades.

Assim, os dados migrados para a nova versão continua com “polígonos abertos”,  impossibilitando, na versão 1.4,  até mesmo um simples *select* sobre os dados da tabela.

A solução foi encontrar os registros com este problema e removê-los da tabela através da seguinte consulta SQL:

DELETE FROM <nome_da_tabela> WHERE isvalid(coords) != 't'</nome_da_tabela>

E se você possui muitas tabelas com o problema, boa sorte!


