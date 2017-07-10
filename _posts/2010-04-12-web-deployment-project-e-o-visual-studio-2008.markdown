---
layout: post
title: Web Deployment Project e o Visual Studio 2008
date: '2010-04-12 15:01:44'
tags:
- visual-studio
---


O [Web Deployment Project](http://www.microsoft.com/downloads/details.aspx?familyId=0AA30AE8-C73B-4BDD-BB1B-FE697256C459&displaylang=en) é uma extensão do Visual Studio 2008 que permite a prévia compilação de páginas e controles de uma aplicação web. Assim podemos detectar se determinada página apresentará erro antes de algum usuário visitar a página em questão.

A parte chata é que isto impossbilita a edição das páginas e controles à quente, direto no servidor. Opa, na verdade esta é parte boa.

Após instalar basta clicar com o botão direito sobre o seu projeto no Visual Studio que surgirá uma opção *Add Web Deployment Project…*. Clicando nesta opção o projeto deveria ser criado. Deveria. Ao menos aqui no Windows 7 não funciona.

Um erro surge dizendo, entre outras coisas: **Unable to create the project file**.

Como solucionar? Você deve rodar o Visual Studio como **Administrador**. Simples assim.


