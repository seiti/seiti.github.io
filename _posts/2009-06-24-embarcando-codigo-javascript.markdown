---
layout: post
title: Embarcando código JavaScript
date: '2009-06-24 18:23:24'
tags:
- aspnet
---


Ao se criar um Server Control em Asp.NET, e queremos que ele contenha lógica a ser executada no cliente recorremos ao Javascript.

Uma das maneiras de se incluir código Javascript no controle é este:

protected override void OnPreRender(EventArgs e) { base.OnPreRender(e); if (!Page.ClientScript.IsClientScriptBlockRegistered("algumid")) { string script = @" function MinhaFuncaoJS() { ... ... ... } ... ... ... function OutraFuncaoJS() { ... ... ... } "; Page.ClientScript.RegisterClientScriptBlock( this.GetType(), "algumid", script, true); } }

O que não é muito bom por alguns motivos, entre outros:

- se torna difícil reutilizar código Javascript;
- deve-se tomar cuidado ao incluir mais de um controle na página, pois acaba-se incluindo o mesmo código Javascript mais de uma vez na página;
- é mais fácil cometer equívocos no código Javascript.

A maneira de se contornar isto é **embarcando** o código Javascript na aplicação – ou *embedding the script resource*.

Para tanto você apenas cria o arquivo contendo o script, por exemplo <tt>MeuProjeto/minhasfuncoes.js</tt>, o inclui no projeto e, através de suas propriedades, configura o item **Build Action** como *Embedded Resource*.

<figure class="wp-caption aligncenter" style="width: 254px;">[![Propriedade para embarcar o arquivo](http://farm5.static.flickr.com/4042/4619331459_3803129779.jpg "Embarcando arquivo")](http://www.flickr.com/photos/seiti/4619331459/ "Propriedade para embarcar o arquivo by Seiti Yamashiro, on Flickr")<figcaption class="wp-caption-text">Modifique esta propriedade para Embedded</figcaption></figure>Isto inclui o script na DLL gerada na compilação. Para acessá-lo é preciso registrá-lo no <tt>AssemblyInfo.cs</tt>:

[assembly: WebResource("MeuProjeto.minhasfuncoes.js", "text/javascript")]

E depois em cada controle que irá utilizar o script:

protected override void OnPreRender(EventArgs e) { Page.ClientScript.RegisterClientScriptResource( typeof(GeoImage), "MeuProjeto.minhasfuncoes.js"); base.OnPreRender(e); }

E pronto! O sistema irá incluir o script em sua página através de um handler **WebResource.axd**.

Ah! Se for necessário misturar recursos, tais como incluir o url de uma imagem embarcada em um javascript embarcado, coloque a opção *PerformSubstitution*:

[assembly: WebResource("MeuProjeto.minhasfuncoes.js", "text/javascript", PerformSubstitution =true)] [assembly: WebResource("MeuProjeto.imagens.delete.png", "image/png")]

E para inserir a url da imagem em seu javascript basta incluir:

 


