---
layout: post
title: ".Net Assembly versioning"
date: '2009-06-17 17:05:18'
tags:
- aspnet
---


Estou enviando vários deploys de um sistema para produção.  Quem realmente deve colocar no ar é o pessoal encarregado do servidor. Como me assegurar que a aplicação mais atual já está no ar?

Podemos utilizar a versão do assembly do projeto para isto. Existe um atributo em .Net que marca a versão de sua aplicação. Este atributo é o [*AssemblyVersion*](http://msdn.microsoft.com/en-us/library/system.reflection.assemblyversionattribute(VS.71).aspx).

Por *default* ele é marcado da seguinte maneira, no arquivo <tt>AssemblyInfo.cs</tt>:

> <tt>[assembly:AssemblyVersion("1.0.*")]</tt>

A versão sempre segue o seguinte padrão:

> <major version="">.<minor version="">.<build number="">.<revision></revision></build></minor></major>

O que o asterisco faz é incrementar automaticamente o *build number* e *revision*. E, embora não esteja explícito na página da MSDN, no [CodeProject](http://www.codeproject.com/KB/dotnet/ManagingAssemblyVersions.aspx) tem a informação de que o *build number* gerado é o número de dias desde **1° de <span style="text-decoration: line-through;">fevereiro</span> janeiro de 2000**, e o *revision *o **número de segundos desde a meia noite divido por dois**.

Daí é só utilizar o seguinte método:

 public static string GetSystemVersion(HttpServerUtility server) { string projectName = "NameOfYourProjectThatNamesYourDLL"; Assembly assembly = Assembly.Load(projectName); return assembly.GetName().Version.ToString(); }

Coloque o valor gerado pelo método em algum lugar do sistema que você tenha acesso. Para calcular a data exata de build do assembly use este site: [http://www.timeanddate.com/date/timeadd.html](http://www.timeanddate.com/date/timeadd.html)

PS: Este é o post *666*. Creepy…..


