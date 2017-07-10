---
layout: post
title: Criando um método de log em Asp.NET
date: '2008-08-28 20:18:56'
tags:
- aspnet
---


Muitas vezes é útil saber como fazer algo simples, como gerar um log em texto puro, ao invés de gerar um evento dentro do Windows.

Ao mesmo tempo quero testar um [plugin colorizador de código](http://wordpress.org/extend/plugins/syntaxhighlighter-plus/) que acabo de instalar 😉

Para mais opções veja um [comparativo entre vários](http://www.cagintranet.com/archive/the-definitive-guide-on-wordpress-syntax-highligher-plugins/) destes plugins para o WordPress.

 protected void Log(string s) { StreamWriter sw = File.AppendText(System.AppDomain.CurrentDomain.BaseDirectory +"logs\error.log"); sw.Write(DateTime.Now.ToString() + " [Erro] " + s); sw.Close(); }


