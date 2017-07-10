---
layout: post
title: Compilation Error CS0433
date: '2007-10-04 01:02:28'
tags:
- bug
- registro
---


<div class="code">Compiler Error Message: CS0433: : The type '<um tipo="">' exists in both '<um local="">' and '<outro local="">'</outro></um></um>

</div>Este erro surgiu em minha aplicação. O que isto quer dizer? Simplesmente que a aplicação tem uma ou mais **classes** definidas com o mesmo nome em *assemblies* distintos.

Mas como isto pode ocorrer? Bom, pode ser resultado de uma migração da aplicação da versão 1.1 para a versão 2.0 do .Net ([http://forums.asp.net/t/980517.aspx](http://forums.asp.net/t/980517.aspx) e [http://webproject.scottgu.com/CSharp/Migration2/Migration2.aspx)](http://webproject.scottgu.com/CSharp/Migration2/Migration2.aspx%29). Refaça a migração que tudo ficará ok (haha).

Pode também ocorrer se você atualizou algum assembly mas o servidor de páginas não atualizou o cache, geralmente localizado em <tt>C:\WINDOWS\Microsoft.NET\Framework\v2.0.50727\Temporary ASP.NET Files</tt>. Vá para a pasta em questão e remova tudo. Pode ser necessário fechar o Visual Studio antes disto.

Se nada disso resolveu (provável), pode ser que os assemblies conflitantes estejam uma na aplicação e uma no GAC de sua máquina. Para remover o assembly do GAC entre em <tt>C:\WINDOWS\assembly</tt>, encontre o safado e escolha a opção <tt>Uninstall</tt>. **Com sorte** você conseguirá realmente apagá-lo ([http://technet.microsoft.com/en-us/library/aa559881.aspx)](http://technet.microsoft.com/en-us/library/aa559881.aspx%29).

Sem sorte? Pois é, o jeito é chafurdar no temível registro do windows, e remover algumas entradas de lá ([http://support.microsoft.com/?scid=kb%3Ben-us%3B873195&x=11&y=17](http://support.microsoft.com/?scid=kb%3Ben-us%3B873195&x=11&y=17) e [http://blogs.msdn.com/alanshi/archive/2003/12/10/42690.aspx)](http://blogs.msdn.com/alanshi/archive/2003/12/10/42690.aspx%29). Após editar o registro, quem sabe seja possível remover o assembly.

Não conseguiu remover a entrada *Default* (ou Padrão) do registro? Cheque suas permissões quanto à entrada em questão. Quem diz que configurar o Linux é complicado nunca mexeu no registro do Windows…


