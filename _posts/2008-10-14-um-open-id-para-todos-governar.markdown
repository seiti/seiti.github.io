---
layout: post
title: Um Open ID para todos governar
date: '2008-10-14 15:41:30'
tags:
- openid
- php
- web
---


[![](http://openid.net/logo-graphics/openid-icon-100x100.png "OpenID")](http://openid.net/)

Recentemente tenho utilizado mais o **[OpenID](http://openid.net/)** para me autenticar em alguns sites, tal como no [stackoverflow.com](http://stackoverflow.com). O objetivo do Open ID é oferecer um perfil centralizado para o usuário poder entrar nos mais variados sites, sem ter de passar pelo processo de registrar-se em cada um deles, cadastrando os mesmos dados, inventar (ou não) mais uma senha etc e tal.

Embora o objetivo seja este, e o efeito desejado seja de diminuir o número de *logins* existentes que sejam vinculados a mesma pessoa, o que de fato ocorre é que eu já possuo alguns logins, ou IDs, em alguns serviços: Google, Yahoo/Flickr, WordPress etc. Somando os OpenIDs vinculados a estas contas, o que eram alguns agora são **muitos**!

E a história de centralizar tudo? Escolher um único destes provedores de autenticação OpenID pode ser uma boa idéia, mas seria **muito melhor** se eu pudesse ter meu OpenID em meu *próprio domínio*!

Bom, já tenho meu domínio, meu próprio site e sei PHP. Entra então o [phpMyID](http://siege.org/projects/phpMyID/).

O phpMyID consiste em apenas dois arquivos php. Não é necessário banco de dados nem nada. Por outro lado ele autentica apenas uma única pessoa, não servindo para atuar como um servidor de logins OpenID. O que é ótimo, pois só existe um de mim (outra coisa ótima!), como o próprio [Christopher](http://siege.org/resume) diria.


