---
layout: post
title: IIS e arquivos mdb (e mdf também!)
date: '2008-11-17 19:45:17'
tags:
- iis
- windows
---


Rodamos aqui no meu trabalho uma aplicação web no IIS. E por algum motivo o sistema não deixava o usuário do site baixar arquivos mdb/mdf, relacionados com o *Access*. Mesmo adicionando a extensão nos *MIME Types* permitidos para a aplicação.

O caso é que o IIS trata arquivos com estas extensões como possíveis candidatos à execução/interpretação. É prciso então entrar na configuração do site e remover este tipo de arquivo dos tipos passíveis de execução/interpretação (tais como .php, .asp etc.).


