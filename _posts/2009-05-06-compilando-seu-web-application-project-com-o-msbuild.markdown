---
layout: post
title: Compilando seu Web Application Project com o MSBuild
date: '2009-05-06 18:44:03'
tags:
- aspnet
- compilacao
- programacao
- projeto
---


Programar em um IDE como o Visual Studio te dá muitas facilidades. O processo de compilação fica quase imperceptível para o desenvolvedor.

O problema surge no momento em que você quer algo diferente, como compilar versões distintas do código a partir do mesmo fonte, automatizar o *build* no servidor etc .

Para os que já usam **Makefile** ou o **Ant**, isto é trivial. Mas isto também é simples para os que usam o Visual Studio!

Vamos ver como construir um simples arquivo para o **MSBuild **compilar nosso projeto.

Primeiro é necessário que você possua o MSBuild instalado. Não se preocupe,  o Visual Studio 2008 já o instala .

E onde está o diabo do **msbuild.exe**? Aqui:

%windir%\Microsoft.NET\Framework\

Ou melhor,  execute (com as aspas!) o seguinte comando em um terminal:

"%VS90COMNTOOLS%\..\..\VC\vcvarsall.bat"

Teste digitando **msbuild.exe /help**

Precisamos agora construir um <span style="text-decoration: line-through;">makefile</span> arquivo de instruções para o MSBuild, que chamarei de Makefile.proj:

<?xml version="1.0" encoding="utf-8"??>
<project defaulttargets="Build" toolsversion="3.5" xmlns="http://schemas.microsoft.com/developer/msbuild/2003"><import project="MeuProjeto.csproj"></import><propertygroup><versionnumber>1.0.0</versionnumber><buildroot>Deploy\Releases\$(VersionNumber)\</buildroot><newinstalldir>$(BuildRoot)Install\</newinstalldir><upgradedir>$(BuildRoot)Upgrade\</upgradedir><copyroot>..\EruditoHAOC_PROD_test\</copyroot></propertygroup><itemgroup><sourcefiles include="**\*.*"></sourcefiles></itemgroup><target name="Build"><msbuild projects="MeuProjeto.sln" properties="OutputPath=$(NewInstallDir)bin\"></msbuild><copy destinationfiles="@(Content->'$(NewInstallDir)%(RelativeDir)%(FileName)%(Extension)')" sourcefiles="@(Content->'%(RelativeDir)%(FileName)%(Extension)')"></copy><copy destinationfiles="@(None->'$(NewInstallDir)%(RelativeDir)%(FileName)%(Extension)')" sourcefiles="@(None->'%(RelativeDir)%(FileName)%(Extension)')"></copy><makedir directories="@(Folder->'$(NewInstallDir)%(RelativeDir)')"></makedir><createitem exclude="**\App_Themes\**;**\Web.config" include="$(NewInstallDir)**"><output itemname="UpgradeFiles" taskparameter="Include"></output></createitem><copy destinationfiles="@(UpgradeFiles->'$(UpgradeDir)%(RecursiveDir)%(FileName)%(Extension)')" sourcefiles="@(UpgradeFiles)"></copy><makedir directories="@(Folder->'$(UpgradeDir)%(RelativeDir)')"></makedir></target><target name="Deploy"><copy destinationfiles="@(SourceFiles->'$(DeployRoot)%(RecursiveDir)%(FileName)%(Extension)')" sourcefiles="@(SourceFiles)"></copy></target></project>

Para compilar seu projeto agora basta rodar o comando <span style="text-decoration: line-through;">make</span> msbuild.exe, da seguinte forma:

MSBuild.exe Makefile.proj /target:Build

Isto irá compilar e copiar o resultado da menira definida no xml Makefile.proj.

Referências:

- [http://www.writebetterbits.com/2008/02/deploying-aspnet-web-application.html](http://www.writebetterbits.com/2008/02/deploying-aspnet-web-application.html)
- [http://msdn.microsoft.com/en-us/library/ms164311.aspx](http://msdn.microsoft.com/en-us/library/ms164311.aspx)


