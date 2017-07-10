---
layout: post
title: Quirks mode - que diabo é isto?
date: '2009-05-10 01:14:01'
tags:
- browser
- html
---


*Quirks mode* ([Wikipedia:Quirks_mode](http://en.wikipedia.org/wiki/Quirks_mode)) é um modo de compatibilidade existente nos browsers, para que renderizem corretamente página antigas, escritas em uma época em que o CSS e o modelo de separação entre conteúdo e apresentação não estava disseminado.

Ou seja, páginas que foram escritas tendo em vista seu funcionamento em navegadores da época (Internet Explorer 4.x, Netscape Navigator 4.x), mas não seguiam os padrões ditados pela W3C, precisam rodar no quirks mode nos browsers modernos, a fim de manterem as mesmas características de antes.

Como abrir uma página em quirks mode?  
 Simples. Basta **deixar** de colocar a tag indicando o <tt>DOCTYPE</tt> logo no início do código da página. Como esta, retirada desta mesma página:

<div class="code" style="font-family: monospace;"><span class="sc0">#8220;-//W3C//DTD XHTML 1.0 Transitional//EN” “http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd”></span>  
<span class="sc2">[<span class="kw2"></span>](http://december.com/html/4/element/html.html)</span>  
 …</div>  
 E para que a página funcione em *standard mode* é só **incluir** o <tt>doctype</tt> acima.  
 Inclua sempre e use o standard mode. Evita **MUITAS** dores de cabeça.


