---
layout: post
title: Asp.Net, Web Forms e Ninjas - Parte 1
date: '2011-09-05 00:48:48'
tags:
- aspnet
- di
- programacao
- web
---


Um padrão que facilita muito a montagem de um sistema orientado à objetos é o de Inversão de Controle e Injeção de Dependência – *Inversion of Control / Dependency Injection*, ou simplesmente **IoC/DI**. O padrão tira das mãos do programador o trabalho de instanciar objetos – que pode ficar bem complicado, restando apenas configurar a aplicação.


## IoC/DI

<figure class="wp-caption aligncenter" style="width: 64px;">![Ninja!!!!](http://www.linux.ime.usp.br/~cef/mac499-05/monografias/roberto/figuras/nukenin_animado_2.gif "Ninja!!!!")<figcaption class="wp-caption-text">Ninja!!!!</figcaption></figure>Programando para a web, geralmente temos de aprender o ciclo de vida da aplicação web, quais os pontos de chamadas de páginas, controles, beans e etc. Quem tem o controle da aplicação é o servidor de aplicação – IIS/.NET, JBoss, WebSphere – e não o programador. Isto é um tipo de Inversão de Controle. 

No caso da Injeção de Dependência, a Inversão de Controle se refere a quem cria os objetos. Quem deve criar os objetos é a própria aplicação. Por que isto? A criação de objetos pode ser complexa e cheia de dependências. Um exemplo: a criação de um objeto **Samurai**. Mas um Samurai obrigatoriamente precisa de uma **Espada**. Então você deve primeiro criar uma Espada, para depois criar o Samurai. Mas para criar uma Espada você precisa de uma **Forja** e um **Ferreiro** e assim por diante.

A solução é usar um contêiner – ou *container* – que faça este trabalho e crie estes objetos para nós. Ao programador resta elaborar e estabeler as regras para esta criação.

Um contêiner DI muito utilizado em Java é o Spring Framework. Em .Net temos vários, mas nenhum em amplo uso e aval da MS. Aqui vou falar de um que considero bem prático de usar e cuja configuração não é baseada em XML. O [Ninject](http://ninject.org/ "Ninject!").


## Ninjas!

Ok, criar objetos pode ser complicado e sujo, então contratemos ninjas para fazê-lo. O Ninject possui uma [documentação](https://github.com/ninject/ninject/wiki "Wiki do Ninject") bem simples de se acompanhar, mas vejamos aqui mesmo o básico.

Segue um código com comentários para exemplificar como o Ninject funciona:

 class Samurai { readonly IWeapon _weapon; //O atributo 'Inject' faz com que o Ninject, ao instanciar um Samurai, instancie primeiro um IWeapon. //Este IWeapon é então passado para o Samurai como um parâmetro do construtor. [Inject] public Samurai(IWeapon weapon) { _weapon = weapon; } public void Attack(string target) { _weapon.Hit(target); } } class Espada implements IWeapon { public Metal Metal { get; private set; } public double Weight { get; private set; } public double Length { get; private set; } public string Name{ get; private set; } public Blacksmith Blacksmith { get; private set; } //Este 'Inject' é semelhante ao de cima, com a diferença do Ninject instanciar e atribuir um //DamageCalculator após a construção desta Espada. //Seria semelhante à um new Espada(...) { DamageCalculator = new DamageCalculator(...) } [Inject] public DamageCalculator Calculator { get; set; } [Inject] public Espada(Blacksmith blacksmith) { Metal = Metal.Iron; Weight = 1; Length = 2; Name = name; Blacksmith = blacksmith; } public Espada(Metal metal, double weight, double length, string name, Blacksmith blacksmith) { Metal = metal; Weight = weight; Length = length; Name = name; Blacksmith = blacksmith; } public void Hit(string target) { //código com o ataque, levando em conta as características da espada etc. } } //etc...

Acima vemos onde marcar nosso código de forma a instruir o Ninject onde agir. Mas como o Ninject sabe qual arma criar para o Samurai, se o Samurai recebe qualquer coisa que implemente IWeapon? Utilizando NinjectModule:

 public class SamuraiModule : NinjectModule { public override void Load() { //Sempre que o código pedir um Samurai, um Samurai será criado Bind<samurai>().ToSelf(); //Sempre que o código pedir um IWeapon, uma Espada será criada Bind<iweapon>().To<espada>(); Bind<blacksmith>().ToSelf(); } } </blacksmith></espada></iweapon></samurai>

Basta agora configurar sua aplicação para ter um Ninject funcional sempre que necessário. Como escolhi, por vários motivos, criar meu projeto como um Asp.NET Web Forms (ao contrário do Asp.NET MVC), tive de alterar o Ninject para dar suporte. Sorte que [alguém já havia feito isto](http://stackoverflow.com/questions/1274026 "Ninject, ASP.NET and Custom Controls").  
 Basta baixar o código fonte do Ninject, aplicar o patch e compilar.

Agora devemos alterar o <tt>Global.asax.cs</tt> para que ele estenda **NinjectHttpApplication** e instanciar um novo Ninject.IKernel sempre que a aplicação subir.  
 É o IKernel o responsável pelo tedioso e oneroso trabalho de instanciar seus objetos, suprindo-os dos elementos necessários para seu funcionamento.

 public class Global : NinjectHttpApplication { protected override void OnApplicationStarted() { base.OnApplicationStarted(); } protected override Ninject.IKernel CreateKernel() { IKernel kernel = new StandardKernel( new List() { new SamuraiModule() }.ToArray() ); return kernel; } }

Nos próximos posts mostrarei como usar o Ninject e o NHibernate em uma aplicação Asp.NET Web Forms.


