---
layout: post
title: 'DataSource Parameters: falta um PropertyParameter!'
date: '2008-09-22 18:44:33'
tags:
- aspnet
- programacao
---


Sempre que utilizo um controle ObjectDataSource sinto falta de um parâmetro. Um parâmetro que associe uma propriedade, existente na classe vinculada à página pelo *codebehind*,  ao controle. Isto é, se existe uma propriedade <tt>usuário</tt> na classe, seria legal um parâmetro do tipo *PropertyParameter* com um atributo <tt>Propertyname</tt>, ou algo assim.

Existem parâmetros para associar controles, query strings, objetos da sessão, mas nenhum para uma propriedade.

Uma solução, talvez a melhor,  é popular dinamicamente o valor do parâmetro:

[http://www.pluralsight.com/community/blogs/fritz/archive/2006/01/16/18054.aspx](http://www.pluralsight.com/community/blogs/fritz/archive/2006/01/16/18054.aspx)


