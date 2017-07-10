---
layout: post
title: Conseguindo a URL completa de uma página
date: '2009-05-19 09:21:12'
tags:
- aspnet
---


O problema é como obter a URL completa, ou absoluta (*absolute URL*), em Asp.NET.

public string ObtemUrl(Control c, string relativePath) { //relativePath deve conter algo como "~/meu/arquivo/no/servidor" return new Uri(c.Page.Request.Url, c.ResolveUrl(relativePath)).ToString(); }

A chamada fica assim:

string umaUrl = objeto.ObtemUrl(this, "~/meu/arquivo/no/servidor");

A variável **umaUrl **conterá** algo como “http://www.example.com/meu/arquivo/no/servidor”.  
**

Não achei nenhum modo mais [simples](http://penyaskitodice.wordpress.com/2008/12/18/aspnet-getting-the-absolute-url-of-a-web-page/).


