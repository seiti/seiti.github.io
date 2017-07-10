---
layout: post
title: Esquema do BD do Travian
date: '2008-01-03 01:20:14'
tags:
- mmo
- travian
---


![Romanos](http://travian.pt/img/un/h/roemer.jpg "WikiImage")O [Travian](http://www.travian.pt/) é um MMO de estratégia em tempo *real* (ou surreal?), onde suas construções podem ficar prontas em minutos ou em algumas dezenas de horas.

O parte interessante, deixando o jogo de lado, é que os servidores deste jogo disponibilizam parte de seu banco de dados para os usuários, possibilitando a criação de inúmeras ferramentas de suporte ao jogo.

Para acessar estes dados basta entrar no endereço <tt>*url_do_travian*</tt>/maq.sql, onde *<tt>url_do_travian</tt>* é o endereço de algum servidor travian (ex: [http://s6.travian.pt/map.sql)](http://s6.travian.pt/map.sql%29).

Para baixar de um jeito mais fácil que pelo navegador, é só digitar a seguinte linha de comando:

<div class="code" style="font-family: monospace;">wget http://s6.travian.pt/map.sql</div>Para carregar este dados em seu próprio banco de dados basta criar um banco qualquer e a seguinte tabela (considerando que você esteja usando o [MySQL](../../wiki/MySQL/edit "Create this page")):

<div class="code" style="font-family: monospace;"><span class="kw1">CREATE</span><span class="kw1">TABLE</span> x_world <span class="br0">(</span>  
 lochash MEDIUMINT <span class="kw1">UNSIGNED</span><span class="kw1">PRIMARY</span><span class="kw1">KEY</span><span class="kw1">NOT</span><span class="kw1">NULL</span>,  
 x SMALLINT <span class="kw1">NOT</span><span class="kw1">NULL</span>,  
 y SMALLINT <span class="kw1">NOT</span><span class="kw1">NULL</span>,  
 race TINYINT <span class="kw1">NOT</span><span class="kw1">NULL</span>,  
 town_id MEDIUMINT <span class="kw1">UNSIGNED</span><span class="kw1">NOT</span><span class="kw1">NULL</span>,  
 town_name CHAR<span class="br0">(</span><span class="nu0">20</span><span class="br0">)</span><span class="kw1">NOT</span><span class="kw1">NULL</span>,  
 owner_id MEDIUMINT <span class="kw1">UNSIGNED</span><span class="kw1">NOT</span><span class="kw1">NULL</span>,  
 owner_name CHAR<span class="br0">(</span><span class="nu0">16</span><span class="br0">)</span><span class="kw1">NOT</span><span class="kw1">NULL</span>,  
 guild_id MEDIUMINT <span class="kw1">UNSIGNED</span><span class="kw1">NOT</span><span class="kw1">NULL</span>,  
 guild_name CHAR<span class="br0">(</span><span class="nu0">8</span><span class="br0">)</span><span class="kw1">NOT</span><span class="kw1">NULL</span>,  
 population MEDIUMINT <span class="kw1">NOT</span><span class="kw1">NULL</span>,  
<span class="kw1">INDEX</span><span class="br0">(</span>town_name<span class="br0">)</span>, <span class="kw1">INDEX</span><span class="br0">(</span>owner_name<span class="br0">)</span>, <span class="kw1">INDEX</span><span class="br0">(</span>guild_name<span class="br0">)</span>,  
<span class="kw1">INDEX</span><span class="br0">(</span>owner_id<span class="br0">)</span>, <span class="kw1">INDEX</span><span class="br0">(</span>guild_id<span class="br0">)</span>, <span class="kw1">INDEX</span><span class="br0">(</span>x<span class="br0">)</span>, <span class="kw1">INDEX</span><span class="br0">(</span>y<span class="br0">)</span>,  
<span class="kw1">INDEX</span><span class="br0">(</span>race<span class="br0">)</span>, <span class="kw1">INDEX</span><span class="br0">(</span>population<span class="br0">)</span>  
<span class="br0">)</span>;</div>E para carregar os dados no seu banco:

<div class="code" style="font-family: monospace;">mysql -u nome_usuario -p nome_bd Trocando, é claro, *nome_usuario* pelo nome do usuário no BD (**root**?) e *nome_bd* pelo nome do banco onde se encontra a tabela **x_world** criada anteriormente.

Mais info no help do [Travian](http://help.travian.com/index.php?type=faq&mod=230#dmp).

</div>
