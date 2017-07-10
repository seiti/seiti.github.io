---
layout: post
title: Sincronizando a agenda do Google e a do Google Apps
date: '2009-12-29 00:46:36'
tags:
- google
- milestone
---


Após alguns problemas associando minhas [duas contas do Google no Milestone](http://seiti.eti.br/blog/2009/nao-consegue-adicionar-outra-conta-google-no-motorola-milestone), restou apenas o problema da agenda.  Recapitulando, tenho duas contas: uma do Google, comum, e outra do Google Apps for Your Domain (GAFYD ou apenas [Google Apps](http://seiti.eti.br/blog/2008/migrando-para-o-google-apps-gmail)).

Cada uma delas conta com sua própria agenda, mas eu só utilizo a do Google Apps.  Mas o Milestone  sincroniza a agenda com apenas **uma conta**, a **primeira** que você cadastrar. E para solucionar o problema do [post anterior](http://seiti.eti.br/blog/2009/nao-consegue-adicionar-outra-conta-google-no-motorola-milestone) tive de cadastrar primeiro minha conta Google comum.

Algo estranho, deveria ser possível ao menos escolher com qual conta sincronizar. Bom, o jeito é remediar. Como? Primeiro entre na seção de configuração do calendário, na interface administrativa do Google Apps. O endereço é algo assim:

> https://www.google.com/a/cpanel/example.com/CalendarSettings

Claro que você deve substituir *example.com* por seu próprio domínio.  Note o item “*Sharing options*“. Assegure-se de escolher o item “*<label for="public_fullshare_write">Share all information, and outsiders can change calendars</label>*“.

Atenção!  Para que esta configuração tenha efeito pode demorar alguns minutos. Caso os passos seguintes não dêem resultado, tnte novamente depois.

Bom, agora você pode compartilhar sua agenda do Google Apps e inserí-la na agenda do Google, através do  *My Calendars* → *Settings *→ *Sharing*.  Coloque seu email **@gmail.com** e escolha na caixa a opção *Make changes AND manage sharing*. Pronto!

[![Compartilhando o Google Calendar](http://farm5.static.flickr.com/4032/4224438288_0fe3f2b355.jpg)](http://www.flickr.com/photos/seiti/4224438288/ "Compartilhando o Google Calendar por Seiti Yamashiro, no Flickr")

Agora você conseguirá visulizar ambas as agendas em seu Motorola Milestone. só espero que em um próximo update do Android isto deixe de ser necessário.


