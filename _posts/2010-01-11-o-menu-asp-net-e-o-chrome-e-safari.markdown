---
layout: post
title: O Menu Asp.NET e o Chrome (e Safari)
date: '2010-01-11 15:52:08'
tags:
- aspnet
---


Existe um problema no controle Menu no Asp.NET WebForms que faz com que ele não seja renderizado corretamente no Safari e no Google Chrome. O que acontece é que o servidor detecta o *user-agent* do navegador do cliente e monta a página de acordo.  Mas o  Asp.NET não reconhece o Safari e o Chrome como** navegadores capazes**, e por isso não conseguem renderizar um Menu em toda sua glória infestada de table’s, tr’s e td’s. Então lhes é servido um menu mais pobre, feio e maltratado .

O jeito é então alertar o Asp.NET  da existência destes navegadores.  E para isto basta criar uma pasta e um arquivo.

Se já não existir, crie em seu projeto uma pasta *App_Browsers*. E dentro dela crie um arquivo chamado *safari.browser*, que deve conter o seguinte:

<browsers><browser refid="Safari1Plus"><controladapters><adapter adaptertype="" controltype="System.Web.UI.WebControls.Menu"></adapter></controladapters></browser></browsers>

E pronto! Tanto Safari quanto Chrome agora poderão mostrar seus lindos menus *tablefull.*


