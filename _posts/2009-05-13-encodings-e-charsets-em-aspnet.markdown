---
layout: post
title: Encodings e charsets em Asp.NET
date: '2009-05-13 09:00:10'
tags:
- aspnet
- net
---


Geralmente não precisamos nos preocupar com os Encodings em uma aplicação em .NET. Isto porque ao desenvolvermos um sistema .NET, utilizamos ferramentas uniformizadas, afinal, elas provêm de uma mesma fabricante: Microsoft.

(Já quando desenvolvemos soluções LAMP, ou mesmo WAMP, nosso cuidado precisa aumentar e muito.)

O fato é que o framework Asp.NET provê uma facilidade incrível para lidar com esta questão que sempre perturba os desenvolvedores. Mesmo no momento de se gravar ou ler arquivos do sistema de arquivos o encoding é tratada de forma automática.

A regra então é: não se preocupe com isto, a menos que algo dê errado e surja algum caractere estranho. E é claro que algo sempre dará errado.

Bom, então quando precisamos mudar o encoding de alguma string em Asp.NET? Simples:

Encoding.UTF8.GetString(Encoding.GetEncoding("iso8859-1").GetBytes("Texto com acentuação e caracteres não-ANSI"));

A código acima toma uma string em** ISO-8859-1** e tranforma-a em uma no formato **UTF-8**.


