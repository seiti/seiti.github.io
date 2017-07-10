---
layout: post
title: ASP.NET Development Server (integrated web server)
date: '2006-09-19 19:33:18'
tags:
- aspnet
---


O Visual Studio 2005 vem com um web server integrado, cujo nome é *Cassini* (eu acho). Para utilizarmos os benefícios do *Edit & Continue* é necessário utilizar este servidor. Para isto basta editar as propriedades do seu projeto.

Infelizmente existem arquivos inseridos na aplicação **aspnet_client**, registrada no Internet Information Services (IIS), que não ficam disponíveis para a aplicação rodando no Cassini. Isto ocorre pelo fato do Cassini só rodar uma aplicação web por vez. Ao abrir outra aplicação, O Cassini abre outro processo rodando o servidor em uma nova porta http, impossibilitando as referências inter-aplicações.

**Solução 1**: copiar a pasta *aspnet_client* inteira (ela se encontra, por padrão, em <tt>C:\Inetpub\wwwroot\</tt>) para o seu projeto e editar o arquivo <tt>web.config</tt> inserindo o seguinte trecho na seção <tt>system.web</tt>:

<div class="code" style="font-family: monospace;"><span class="sc3"><span class="re1"><webcontrols><span class="re0">clientScriptsLocation</span>=<span class="st0">“aspnet_client”</span><span class="re2">/></span></webcontrols></span></span></div>Ao copiar a pasta não se esqueça de adicioná-la ao projeto no Visual Studio.

Fonte: [http://delphi.about.com/od/adptips2005/qt/cassinivalidate.htm](http://delphi.about.com/od/adptips2005/qt/cassinivalidate.htm)

**Solução 2**: copiar o **conteúdo** da pasta *aspnet_client*, que deve estar em <tt>c:\Inetpub\wwwroot\aspnet_client</tt>, para dentro de sua aplicação, e renomear o nome da aplicação que aparece na url para *aspnet_client*. Isto fará com que qualquer referência para os arquivos em *http://localhost:porta/aspnet_client* sejam encontrados, afinal, este é o nome de sua aplicação agora.  
 Feio, mas funciona! E dá um jeito nos problemas encontrados em controles *third party*, que não obedecem a tag xml definida na solução 1.


