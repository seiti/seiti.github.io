---
layout: post
title: Resolvendo o problema da busca no DSpace
date: '2009-05-28 00:46:39'
tags:
- tomcat
---


Ocorre um problema em minha [instalação  do DSpace](http://seiti.eti.br/blog/2009/addon-de-estatisticas-do-dspace). As buscas realizadas contendo caracteres com [diacríticos](http://pt.wikipedia.org/wiki/Diacr%C3%ADtico) (acentuação e etc.) retornam resultados estranhos, pois os termos da busca ficam desfigurados. E [não sou só eu](http://seiti.eti.br/blog/2009/addon-de-estatisticas-do-dspace#comment-275) que enfrento isto.

Fui escarafunchar o código fonte tentando encontrar alguma solução. Não encontrei nenhuma. Vamos apelar ao **[onisciente](http://www.google.com.br/search?q=dspace+diacritics+starts_with)** então.

Um [post](http://www.nabble.com/Acute-Accents----Searching-td23594758.html) me chamou a atenção para a configuração do Tomcat. É necessário editar o arquivo <tt>/etc/tomcat5/server.xml</tt> de formar que o elemento *Connector* em questão  tenha um atributo **URIEncoding=”UTF-8″**.

Embora este atributo seja sempre configurado no Connector padrão , que escuta na porta 8080,  me lembrei que eu havia configurado o [Tomcat](http://seiti.eti.br/blog/2008/apache-tomcat) para funcionar em conjunto com o Apache, através do *mod_jk*, na porta **8009 com o AJP Connector**.

Fui verificar o arquivo server.xml e **bingo**! Foi só mudar de

<connector enablelookups="false" port="8009" protocol="AJP/1.3" redirectport="8080"></connector>

para

<connector enablelookups="false" port="8009" protocol="AJP/1.3" redirectport="8080" uriencoding="UTF-8"></connector>

E a busca voltou a funcionar.


