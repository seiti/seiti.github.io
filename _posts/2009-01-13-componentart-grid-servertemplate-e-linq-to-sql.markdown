---
layout: post
title: ComponentArt Grid, ServerTemplate e Linq to SQL
date: '2009-01-13 13:58:07'
tags:
- aspnet
- programacao
---


Micro post para reclamar e aliviar a cabeça.

Estou tentando melhorar uma listagem de dados, de forma a ficar mais simples, mais elegante e  mais versátil. É claro que o código fonte também deve ficar mais simples, mais elegante e mais versátil.  Por isso aproveitei para estudar o uso do Linq To Sql.

Fui dar uma olhada também no ComponentArt Grid. Ai de mim.

O ServerTemplate do** ComponentArt Grid** ([CA Grid](http://www.componentart.com/webui/demos/demos_control-specific/grid/features/ajax_grid/webform1.aspx "CA Grid")) não funciona com o LinqDataSource. Ao menos não diretamente, apenas configurando no template *aspx*. É preciso programar no *code-behind*.

Mas surge outro problema, montar expressões Linq sob demanda é complicado. É preciso *Reflection* e bastante persistência (do programador, não dos dados), OU utilizar o [*Dynamic Linq*](http://weblogs.asp.net/scottgu/archive/2008/01/07/dynamic-linq-part-1-using-the-linq-dynamic-query-library.aspx "Dynamic linq"), uma mão na roda para criar expressões programaticamente.

É claro que outro (velho)  problema apareceu: controles no ServerTemplate não conseguem disparar eventos consistemente. Falham, por xemplo,  se o usuário realiza um agrupamento no Grid e logo depois tentar disparar um evento apertando algum botão do Grid.  O problema é criar o botão a ser apertado usando o ImageButton. Deve-se utilizar o LinkButton. Para qualquer caso. Na verdade esqueça que existe o ImageButton. Eu já esqueci.


