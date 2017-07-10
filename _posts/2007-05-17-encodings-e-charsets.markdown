---
layout: post
title: Encodings e charsets
date: '2007-05-17 19:31:58'
tags:
- aspnet
---


Geralmente não precisamos nos preocupar com os [Encodings](../../wiki/Encodings) em uma aplicação em .NET. Isto porque ao desenvolvermos um sistema **.NET**, utilizamos ferramentas uniformizadas, afinal, elas provêm de uma mesma fabricante: Microsoft.

(Já quando desenvolvemos soluções **LAMP** ([Wikipedia:LAMP](http://en.wikipedia.org/wiki/LAMP)), ou mesmo WAMP, nosso cuidado precisa aumentar e muito.)

Mas e quando precisamos mudar o encoding de alguma string em Asp.NET? Simples:

 Encoding.UTF8.GetString(Encoding.GetEncoding("iso8859-1").GetBytes("Média"));

A código acima toma uma *string* em ISO-8859-1 e tranforma-a em uma no formato UTF-8.


