---
layout: post
title: Fluent NHibernate
date: '2010-07-19 21:12:29'
tags:
- ddd
- net
- orm
---


O [NHibernate](http://nhforge.org) é um port para .NET do [Hibernate](http://hibernate.org/), um **mapeador objeto relacional** (ou ORM) com esteróides. Vamos ver como usá-lo para mapear e persistir nossos objetos no banco de dados.

O NHibernate é um grande auxílio para quem deseja implementar um sistema usando DDD (não, não é quando você liga para o programador que mora longe. É *Domain Driven Design*).

<figure class="wp-caption aligncenter" id="attachment_1185" style="width: 64px;">[![Me deixa dormir!](http://seiti.eti.br/blog/wp-content/uploads/2010/07/NhLogo.png "NhLogo")](http://nhforge.org)<figcaption class="wp-caption-text">Me deixa dormir!</figcaption></figure>Quem já usou o Hibernate sabe que configurá-lo pode ser a porta de entrada para o primeiro dos [nove círculos do inferno](http://en.wikipedia.org/wiki/Inferno_%28Dante%29). Bom, não passei por isto, pois nunca havia usado diretamente o Hibernate. Se existe algo bom em chegar na festa por **último** no mundo do desenvolvimento, é de ter mais coisas prontas e mastigadinhas. Entra então o ***Fluent NHibernate***.


## Historinha para bovinos hibernarem

Primeiro o contexto. Enfrento um código legado (código legado == código sem testes, segundo [Feathers](http://www.amazon.com/Working-Effectively-Legacy-Michael-Feathers/dp/0131177052)) que usa o framework *Castle ActiveRecord* (Castle AR). Embora este framework facilite bastante a vida, poupando o pobre programador da tarefa de escrever muito código CRUD, ganhando uma tendinite, ele não se dá muito bem com o DDD, tornando mais trabalhoso que o necessário a separação das *Entidades* do sistema de *persistência.*

Outro problema é que, apesar do Castle AR fornecer uma camada de abstração sobre o Hibernate, é necessário que você saiba como o Hibernate funciona. Decidi então me livrar do Castle AR e usar apenas o Hibernate. E como não quero editar os arquivos XML do Hibernate eu mesmo (o Castle AR fazia este trabalho) decidi usar o Fluent NHibernate.


## Programação, sistemas e zumbis

O Fluent NHibernate segue uma sintaxe *fluente* para realizar toda a configuração do Hibernate usando a própria linguagem de programação. No meu caso, C#.

Primeiro um esquema altamente complexo do sistema que servirá de exemplo:

<figure class="wp-caption aligncenter" style="width: 500px;">[![Diagrama do sistema](http://farm5.static.flickr.com/4114/4809510719_ef4e9bea45.jpg)](http://www.flickr.com/photos/seiti/4809510719/ "Diagrama do sistema by Seiti Yamashiro, on Flickr")<figcaption class="wp-caption-text">Chamem o Chris Redfield!</figcaption></figure>Um <span style="text-decoration: line-through;">RaccoonCity</span>*City* possui inúmeros *Zombies*. O *City* tem uma data, *Month*, com mês e ano, de quando se iniciou a infecção de sua população. *Zombie* possui uma data, *Month*, de quando ele mesmo foi infectado. Por enquanto não podemos estimar estas datas com precisão de dias, por isso queremos apenas mês e ano.

O diagrama acima gerou as seguintes classes:  
[![](http://seiti.eti.br/blog/wp-content/uploads/2010/07/screen1.png "screen")](http://seiti.eti.br/blog/wp-content/uploads/2010/07/screen1.png)

- <tt>City</tt> é uma *Entidade*. E é uma Raíz de Agregado, ou *Aggregate Root*;
- <tt>Zombie</tt> é um *Objeto Valor*, ou* Value Object*. Quer dizer que todos os zumbis são iguais, desde que tenham as mesmas propriedades: *FormerName* e *Infected*. Deixei um Id mesmo assim;
- <tt>Month</tt> também é um Objeto Valor. Ele determina um mês e ano. Não estou interessado no dia.

Uma preocupação na modelagem foi quanto à lista *Zombies*. Para se adicionar um Zombie em um City é preciso usar o método AddZombie(). Assim tenho um lugar onde posso checar e validar o Zombie antes da adição.

Mas se eu exponho Zombies como um *List<zombie></zombie>* nada impede o programador de fazer isso:

 City raccoon = new City("Raccoon City", new Month(2010, 4)); raccoon.Zombies.Add(new Zombie("Zé Ninguém", new Month(2010, 7)));

ao invés de:

 City raccoon = new City("Raccoon City", new Month(2010, 4)); raccoon.AddZombie(new Zombie("Zé Ninguém", new Month(2010, 7)));

Para resolver este problema eu guardo a lista como um *List<zombie></zombie>* e exponho apenas um *IEnumerable<zombie>:</zombie>*

 public class City { public virtual int Id { get; private set; } public virtual string Name { get; private set; } public virtual Month InfectionStart { get; private set; } private readonly IList<zombie> _zombies = new List<zombie>(); public virtual IEnumerable<zombie> Zombies { get { return _zombies; } } protected City() {} public City(string name, Month startMonth) { Name = name; InfectionStart = startMonth; } public virtual void AddZombie(Zombie z) { _zombies.Add(z); } } </zombie></zombie></zombie>

O IEnumerable apenas expõe método de consulta. Exatamente o que eu queria.

Vamos agora implementar a classe *Zombie*. Esta acaba sendo mais complicada, pois se trata de um VO (*Value Object*). É necessário realizar um override nos métodos *Equals()* e *GetHashCode()* para que o sistema possa comprar dois zumbis com as mesmas propriedades, mesmo que de instâncias diferentes, e devolver um resultado útil. E já podemos aproveitar para fazer override nos operadores == e !=, para que devolvam o mesmo resultado que o Equals():

 public class Zombie { public virtual int Id { get; private set;} public virtual string FormerName { get; set; } public virtual Month Infected { get; set; } public static bool operator ==(Zombie b1, Zombie b2) { return b1.FormerName == b2.FormerName && b1.Infected == b2.Infected; } public static bool operator !=(Zombie b1, Zombie b2) { return b1.FormerName != b2.FormerName || b1.Infected != b2.Infected; } public static bool operator >(Zombie b1, Zombie b2) { return b1.Infected > b2.Infected; } public static bool operator =(Zombie b1, Zombie b2) { return b1.Infected >= b2.Infected; } public static bool operator Até aproveitei para implementar os operadores , que dependem da data de infecção do safado.

E só resta a classe *Month*:

 public class Month: IComparable { private int Dia { get { return 1; } } public int Mes { get; private set; } public int Ano { get; private set; } protected Month() {} public Month(int ano, int mes) { if (!AnoValido(ano)) throw new ArgumentOutOfRangeException(String.Format("Ano não cabível. Ano apresentado: {0}", ano)); if (!MesValido(mes)) throw new ArgumentOutOfRangeException(String.Format("Mês não cabível. Mês apresentado: {0}", mes)); Ano = ano; Mes = mes; } private bool AnoValido(int ano) { // Valores válidos para o SQL Server. // Observe que dado o escopo do problema não faz sentido nada fora deste intevalo mesmo. if (1753 d2.Ano) return false; if (d1.Mes =(Month d1, Month d2) { if (d1 == d2) return true; if (d1.Ano > d2.Ano) return true; if (d1.Ano d2.Mes) return true; return false; } public static bool operator d2.Ano) return false; if (d1.Mes (Month d1, Month d2) { if (d1 == d2) return false; if (d1.Ano > d2.Ano) return true; if (d1.Ano d2.Mes) return true; return false; } public override bool Equals(object obj) { if (!(obj is Month)) return false; return this == (Month) obj; } public override int GetHashCode() { return Ano.GetHashCode() ^ Mes.GetHashCode(); } public int CompareTo(object obj) { Month d = (Month)obj; if (this d) return 1; return 0; } }

Mesma história dos Zumbis: implementei Equals(), e GetHashCode() e os operadores. Asism posso escrever código do tipo:

 Data d1 = new Data(2000, 1); Data d2 = new Data(2000, 1); if (d1 == d2) doSomething(); else if (d1 > d2) doSomethingElse(); else if (d1 Com as classes do modelo implementadas, posso adicionar validações, testes e tudo mais, sem me preocupar com a camada de persistência, tornando a criação de testes unitários um trabalho bem simples. Mas este post não é sobre DDD.


## Persistência != Teimosia

Vamos mapear nossas estimadas classes, usando o *Fluent NHibernate*, para que possam ir para o banco de dados. Comecemos com a classe *Zombie*, mapeada pela classe **ZombieMap**:

 public class ZombieMap: ClassMap<zombie> { public ZombieMap() { Id(x => x.Id); Map(x => x.FormerName); Map(x => x.Infected); } } </zombie>

Bem simples, não? Isto nos informa que a classe *Zombie* será mapeada para uma tabela <tt>Zombie</tt>, com campos **FormerName** (com tipo nvarchar(255)) e **Infected** (com tipo … hmmm, calma aí, veremos adiante).

Vamos ver a classe City:

 public class CityMap: ClassMap<city> { public CityMap() { Id(x => x.Id); Map(x => x.Name); Map(x => x.InfectionStart); HasMany<zombie>(x => x.Zombies) .Access.CamelCaseField(Prefix.Underscore) .Cascade.AllDeleteOrphan() .AsBag(); } } </zombie></city>

Também bem simples. A diferença aqui fica por conta do **HasMany<zombie></zombie>**, cujo significado é bem simples, um City possui muitos Zombies.

Algo não tão óbvio é o *Access.CamelCaseField(Prefix.Underscore)*. Isto diz que a propriedade Zombies possui um campo que serve de suporte, com nome escrito no estilo camelCase (diferente de PascalCase) e iniciado por um underscore. Se trata do campo **_zombies**, que é Zombies escrito em camelCase e iniciado por underscore.

*Cascade.AllDeleteOrphans()* informa ao NHibernate para apagar os Zombies órfãos, quer dizer, que não possuem um City.

*AsBag()* é mais complicado. Primeiro é preciso entender que o NHibernate lida com [vários tipos de coleções](http://blogs.hibernatingrhinos.com/nhibernate/archive/2008/06/12/mapping-collections-in-nhibernate-part-1.aspx): **Set**, **Bag**, **Map** e **List**. Cada uma com características próprias. No caso optei por **bag**, mas poderia ter usado **list** (que é um bag indexado).

Bom, resta agora a classe ***Month***. Decidi não guardar o month em uma tabela própria. Ela nada mais é que uma data, onde apenas mês e ano importam. Então é apropriado guardá-lo em um campo DATETIME no banco de dados.

Para isso acontecer configuramos o NHibernate para tratar o Month como um DATETIME na hora de persistir tanto o *City* quanto o *Zombie* (campos *Infected*), criando uma classe que implementa a interface ***IUserType***:

 public class MonthUserType: IUserType { public new bool Equals(object x, object y) { if (ReferenceEquals(x, y)) return true; if (x == null || y == null) return false; return x.Equals(y); } public int GetHashCode(object x) { return x == null ? typeof(Month).GetHashCode() : x.GetHashCode(); } //voltando do BD: passar de datetime para Month public object NullSafeGet(IDataReader rs, string[] names, object owner) { var date = NHibernateUtil.DateTime.NullSafeGet(rs, names[0]) as DateTime?; if (date == null) return null; return new Month(date.Value.Year, date.Value.Month); } //indo pro BD: passar de Month para datetime public void NullSafeSet(IDbCommand cmd, object value, int index) { DateTime? date = null; if (value != null) date = ((Month) value).AsDateTime(); NHibernateUtil.DateTime.NullSafeSet(cmd, date, index); } public object DeepCopy(object value) { return value; } public object Replace(object original, object target, object owner) { return original; } public object Assemble(object cached, object owner) { return cached; } public object Disassemble(object value) { return value; } public SqlType[] SqlTypes { get { return new[] { NHibernateUtil.DateTime.SqlType }; } } public Type ReturnedType { get { return typeof (Month); } } public bool IsMutable { get { return false; } } }

Esta classe vai tratar do trabalho de converter de Month para DATETIME e vice-versa. Para usar nosso MonthUserType é necessário configurar os mapeamentos das classes City e Zombie:

 Map(x => x.Infected).CustomType(typeof(MonthUserType));

Mas eu não usei esta abordagem. Imagine que tenhamos mais que essas duas classes para alterar ou que eu deseje deixar a configuração mais limpa. Podemos deixar os mapeamentos já configurados do mesmo jeito, e informar o NHibernate a usar o MonthUserType usando [Convenções](http://wiki.fluentnhibernate.org/Conventions) (*Conventions*).

Basta implementar uma classe com a informação de que nossa convenção é usar MonthUserType para persistir objetos Month:

 public class MonthUserTypeConvention: UserTypeConvention<monthusertype> { } </monthusertype>

É assim mesmo, vazio. No caso nem foi necessário realizar nenhum override dos métodos *Apply()* ou *Accept()*.

E pronto! Suas classes estão prontas para serem persistidas no banco de dados.


## Infraestrutura

Bom, mas para se gravar os dados no banco é preciso ao menos saber como se conectar ao banco. Vamos facilitar nossa vida criando um método fábrica de objetos fábricas (ou algo assim):

 public static class FluentSessionFactory { public static ISessionFactory CreateFactory(string connectionString) { return Fluently.Configure() .Database(MsSqlConfiguration.MsSql2005.ConnectionString(connectionString)) .Mappings( m => m.FluentMappings .AddFromAssemblyOf<city>() .Conventions.AddFromAssemblyOf<monthusertypeconvention>() ) .ExposeConfiguration(BuildSchema) .BuildSessionFactory(); } private static void BuildSchema(Configuration config) { SchemaExport schema = new SchemaExport(config); schema.Drop(false, true); schema.Create(false, true); } } </monthusertypeconvention></city>

Note que meu banco é um Sql Server 2005. Acerte o código para teu banco de dados. E para usar:

 ISessionFactory factory = FluentSessionFactory.CreateFactory(@"Database=test_db;Server=localhost\sqlexpress;user=theuser;pwd=thepassword;"); ISession session = factory.OpenSession(); /** cria objetos e manda para o bd usando Session.Save(objeto) **/ session.Close();

Mas tome **cuidado**. Note um *schema.Drop()* e um *schema.Create()* lá em cima. Eles jogam as tabelas do banco fora e depois recriam-nas. Bom para o ambiente de desenvolvimento. Ruim para ambiente de produção. Muito ruim.


## 1, 2, 3 Testando

Nada melhor que usar testes automatizados para verificar se está tudo funcionando. Quer dizer, comer camarão na praia tomando cerveja é melhor que isso, mas vamos lá.

O Fluent NHibernate conta com um método muito útil para verificar se os mapeamentos estão redondinhos. Se trata do *PersistenceSpecification.VerifyTheMappings().*

Veja como é simples:*  
*

 [TestClass] public class CityMapTest { private static readonly string ConnString = @"Database=db_test;Server=localhost\sqlexpress;user=theuser;pwd=thepassword;"; private static ISession Session; private TestContext testContextInstance; public TestContext TestContext { get { return testContextInstance; } set { testContextInstance = value; } } [ClassInitialize()] public static void MyClassInitialize(TestContext testContext) { ISessionFactory factory = FluentSessionFactory.CreateFactory(ConnString); Session = factory.OpenSession(); } [ClassCleanup()] public static void MyClassCleanup() { Session.Close(); } [TestMethod] public void CrudTest() { new PersistenceSpecification<city>(Session) .CheckProperty(x => x.Id, 1) .CheckProperty(x => x.Name, "Raccoon City") .CheckProperty(x => x.InfectionStart, new Month(1998, 8)) .CheckList( x => x.Zombies, new [] { new Zombie { FormerName = "John Doe", Infected = new Month(1998, 7) }, new Zombie { FormerName = "José da Silva", Infected = new Month(1998, 6) } }, (r, z) => r.AddZombie(z)) .VerifyTheMappings(); } } </city>

Ao executar o teste acima serão criadas as tabelas City e Zombie no banco de dados, que serão preenchidas com os dados fornecidos. Depois esses dados serão lidos e convetidos em objetos do sistema. Daí estes objetos serão comparados com os objetos originais. Se estiver tudo ok, o teste sinalizará **verde**. Se não, hora de corrigir **bugs**.

E é isso. Ah, para quem quiser o [código do projeto…](http://dl.dropbox.com/u/2295190/blog/FluentNH.zip)


