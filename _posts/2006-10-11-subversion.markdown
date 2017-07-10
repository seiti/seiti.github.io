---
layout: post
title: Subversion
date: '2006-10-11 19:35:50'
---


Uma equipe que tenha de trabalhar em cima de um mesmo projeto necessita de um sistema de controle de código-fonte com versionamento. Decidi testar o Subversion como alternativa ao [SourceSafe](../../wiki/SourceSafe/edit "Create this page") da Microsoft, um sistema muito criticado pela web afora.

O [Subversion (SVN)](http://subversion.tigris.org/) trata-se de um sistema de controle de código e versionamento.

O [TortoiseSVN](http://tortoisesvn.tigris.org/) é um cliente SVN que integra-se ao Windows Explorer, permitindo efetuar o controle de versão de qualquer pasta de sua máquina de trabalho.

Já o [AnkhSVN](http://ankhsvn.tigris.org/) é um addin para o Visual Studio que permite o controle das versões dos arquivos de seu projeto a partir do próprio Visual Studio.

Instalei o Subversion, o [AnkhSVN](../../wiki/AnkhSVN/edit "Create this page") e o [TortoiseSVN](../../wiki/TortoiseSVN/edit "Create this page") através de seus respectivos instaladores disponíveis nos sites de seus projetos.

Depois criei um reposítório e nele um projeto, seguindo a documentação do próprio SVN.

Dica: se você tiver uma máquina que sirva de servidor SVN, seria legal instalar o SVN como um serviço do Windows, assim ele estará disponível sempre que rebootar a máquina:

<div class="code">sc create svnserve binpath= "c:\svnserve\svnserve.exe --service --root c:\repos" displayname= "Subversion" depend= tcpip start= auto

</div>Mude o <tt>c:\repos</tt> para qualquer diretório **local** do servidor (unidades de rede não funcionam).

Mais info: [Manual do TortoiseSVN](http://tortoisesvn.net/docs/nightly/TortoiseSVN_en/tsvn-serversetup-svnserve.html)


