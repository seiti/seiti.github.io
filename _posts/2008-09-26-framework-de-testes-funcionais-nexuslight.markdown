---
layout: post
title: Framework de testes funcionais NexusLight
date: '2008-09-26 18:01:42'
tags:
- aspnet
---


O [NexusLight](http://www.codeplex.com/aspnet/Wiki/View.aspx?title=ASP.NET%20QA "NexusLight") é um framework de *testes funcionais*. Um teste **funcional **simula a operação de um *usuário* do sistema, diferente de um teste **unitário**, que testa se os métodos de uma dada classe funcionam corretamente.

Ele é bem simples de se utilizar.  Basta baixar o [último pacote](http://www.codeplex.com/aspnet/Release/ProjectReleases.aspx?ReleaseId=17608) e referenciar a DLL Microsoft.Web.Testing.Lightweight em seu projeto, além de criar uma pasta, <tt>Test</tt>, por exemplo, para conter os arquivos Default.aspx e DriverPage.aspx.

Uma classe de teste de exemplo baseado no sample, um pouco mais simplificado:

 using System; using System.Data; using System.Configuration; using Microsoft.Web.Testing.Light; [WebTestClass] public class ProcessosTest { [WebTestMethod] public void GridViewListingTest() { HtmlPage page = new HtmlPage(); LoginAndGoToPage(page, 2824); page.Elements.Find("btnLocalizar").Click(WaitFor.Postback); HtmlTableElement grid = (HtmlTableElement)page.Elements.Find("gridProcessos"); Assert.IsTrue(grid.Rows.Count > 0); } private void LoginAndGoToPage(HtmlPage page, int pageId) { // Navigate to Home page page.Navigate("Default.aspx"); page.Elements.Find("Login_UserName").SetText("adm"); page.Elements.Find("Login_Password").SetText("clone"); page.Elements.Find("Login_LoginImageButton").Click(WaitFor.Postback); page.Navigate("Default.aspx?idPagina="+2824); } }

O que esta classe de teste faz? Ela entra na página <tt>Default.aspx</tt>, preenche o controle <tt>Login</tt>, campos *UserName* e *Password*, “aperta” o botão de envio e, após supostamente ter se logado, navega para uma outra página através de uma querystring.

Após navegar para esta outra página, “aperta” o botão de **id***Localizar* e checa se o grid da página retornou algum resultado.

E, para que todo o comportamento acima ocorra, basta entrar no endereço http://localhost:suaporta/seuprojeto/Test/, selecionar o teste e clicar no botão *Run*!.


