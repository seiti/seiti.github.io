---
layout: post
title: Agrupando arquivos na árvore do VS 2005
date: '2006-12-21 19:37:29'
tags:
- visual-studio
- windows
---


Uma dica legal. Sabe quando você cria um controle **aspx**? Além do arquivo <tt>.aspx</tt> são criados também arquivos <tt>.aspx.cs</tt> e <tt>aspx.cs.designer</tt>, ficando agrupados abaixo do arquivo aspx.  
 Bom, podemos incluir neste agrupamente outros tipos de arquivos, basta editar a seguinte chave do registro do Windows:

<div class="code">HKLM:\SOFTWARE\Microsoft\VisualStudio\8.0\Projects\{E24C65DC-7377-472B-9ABA-BC803B73C61A}\RelatedFiles\.aspx

</div>Incluindo nela uma chave que represente a extensão desejada, como, por exemplo, <tt>.js</tt> ou <tt>.xsd</tt>. Assim, se criarmos um controle <tt>bla.aspx</tt> e um arquivo <tt>bla.aspx.js</tt>, este ficará na mesma árvore daquele.

Fonte: [http://extraview.co.uk/blog/default,month,2006-07.aspx](http://extraview.co.uk/blog/default,month,2006-07.aspx)


