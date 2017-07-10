---
layout: post
title: 'Erro no deploy automático: Hudson versus MSBuild'
date: '2010-05-11 20:48:15'
tags:
- aspnet
- desenvolvimento
- msbuild
---


Usamos o excelente Hudson como servidor de integração contínua, junto do plugin MSBuild.

<figure class="wp-caption aligncenter" style="width: 96px;">[![](http://hudson-ci.org/images/butler.png "Hudson")](http://hudson-ci.org/)<figcaption class="wp-caption-text">O fiel mordomo</figcaption></figure>Mas estes dias criei um projeto no Hudson, referente à uma solução já no framework .NET v4, escrita no Visual Studio 2010 (v10).

O primeiro passo foi entrar nas configurações do Hudson e criar outra entrada para o plugin MSBuild, apontando para a versão 4 do mesmo. Basta ir para *Gerenciar Hudson* → *Configurar Sistema* → *MSBuild* e incluir:

> C:\Windows\Microsoft.NET\Framework\v4.0.30319\MSBuild.exe

Feito isto, configurei o novo projeto para usar esta nova entrada do MSBuild. E o projeto falhou na construção com a seguinte mensagem:

> error MSB4019: The imported project "C:\Program Files (x86)\MSBuild\Microsoft\VisualStudio\v10.0\WebApplications\Microsoft.WebApplication.targets" was not found. Confirm that the path in the <import> declaration is correct, and that the file exists on disk. </import>

O jeito foi atender a demanda: criei as respectivas pastas e copiei o arquivo do meu micro para o servidor. Pronto. Agora só resta resolver alguns pepinos com *assemblies*…

**Update**: parece que preciso instalar ou o Visual Studio 2010 ou o Windows 7 SDK  no servidor em questão. Mas ocorrem dois problemas: (1) o VS2010 é caro e (2) o SDK ainda [não saiu](http://blogs.msdn.com/windowssdk/archive/2010/04/07/coming-soon-win-sdk-for-windows-7-and-net-4.aspx). O jeito é aguardar meados de junho.


