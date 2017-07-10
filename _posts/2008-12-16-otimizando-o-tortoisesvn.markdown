---
layout: post
title: Otimizando o TortoiseSVN
date: '2008-12-16 10:44:18'
tags:
- otimizacao
- subversion
- windows
---


Ainda me admiro com a capacidade do **Windows** de se tornar mais lento a cada dia que passa.  Mas a culpa não é apenas do SO e sua permissividade com que trata os processos de terceiros. Bom, talvez seja.  Enfim, notei que o meu sistema fica uma carroça todo *reboot*, e um dos culpados é o processo <tt>TSVNCache.exe</tt>.

Felizmente alguém já enfrentou [este problema](http://www.paraesthesia.com/archive/2007/09/26/optimize-tortoise-svn-cache-tsvncache.exe-disk-io.aspx), e ele é resolvido com os seguintes passos:

- Abrir o menu de contexto e entrar na opção *settings* do submenu do TortoiseSVN;
- Entrar no item *icon overlays*;
- Editar as caixas *Exclude Paths* e *Include Paths*.

[![TortoiseSVN Settings](http://seiti.eti.br/gallery2/main.php?g2_view=core.DownloadItem&g2_itemId=5833&g2_GALLERYSID=d336cef1cb76df1575934589a197678c "Configurações do Tortoise SVN")](http://seiti.eti.br/blog/fotos?g2_itemId=5833)

Exclua o máximo que puder e inclua o mínimo possível. Na minha máquina coloquei o seguinte:

Exclude Paths:  
<tt>C:\*</tt>

Include Paths:  
<tt>C:\Documents and Settings\seiti\Meus documentos\Workspace*</tt>

Agora mate o processo <tt>TSVCache.exe</tt> ou reinicie a máquina.


