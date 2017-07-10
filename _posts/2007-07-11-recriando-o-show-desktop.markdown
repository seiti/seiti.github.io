---
layout: post
title: Recriando o Show Desktop
date: '2007-07-11 19:44:01'
tags:
- windows
---


Desde o Windows 95 existe um botão muito útil, o *Show Desktop*, que minimiza todas as janelas abertas, permitindo uma visualização rápida do desktop. Se você o apagou sem querer ou utiliza o Windows 2003 Server, vai ser necessário recriá=lo. Como?

Basta criar o arquivo abaixo em seu desktop:

<div class="code_header">Show Desktop.scf</div><div class="code" style="font-family: monospace;">[Shell]  
 Command=2  
 IconFile=explorer.exe,3  
 [Taskbar]  
 Command=ToggleDesktop</div>Depois mova-o com o botão direito para o *quick launch area*!


