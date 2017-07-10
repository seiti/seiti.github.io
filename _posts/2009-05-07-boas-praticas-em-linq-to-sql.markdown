---
layout: post
title: Boas práticas em Linq To Sql
date: '2009-05-07 16:26:39'
tags:
- design-patterns
- linq
---


Estou tentando descobrir uma boa maneira de lidar com o Linq To Sql. Determinar um padrão que seja robusto e flexível no uso desta ferramenta. Mas para se usar uma ferramenta da melhor maneira possível é preciso conhecê-la!

### Funcionamento

Não colocarei aqui instruções para uso básico do Linq, mesmo porque já existem [excelentes tutoriais por aí](http://weblogs.asp.net/scottgu/archive/2007/05/19/using-linq-to-sql-part-1.aspx) (aos interessados na tecnologia, recomendo assinar o feed do [Scott Guthrie](http://weblogs.asp.net/scottgu)).

Para o Linq To Sql funcionar devemos criar um arquivo de *classes Linq to Sql* (dbml). Este XML serve de metacódigo, utilizado para criar dinamicamente várias classes de forma automatizada. Dentre estas classes é criada também um  
*Unit of Work* e um *Data gateway* em um único objeto: [o DataContext](http://www.west-wind.com/weblog/posts/246222.aspx).

O DataContext é responsável por guardar/conter/seguir as alterações em todos objetos Linq ([Unit of Work](http://martinfowler.com/eaaCatalog/unitOfWork.html)) e por conversar com o banco de dados ([Data Gateway](http://martinfowler.com/eaaCatalog/tableDataGateway.html)).

É através do DataContext que conversamos com o banco de dados. E o DataContext gosta de conversar sobre objetos.

Imaginemos uma tabela **Abacaxi** em nosso banco de dados, com as colunas *id, responsavel, tarefa e datalimite*.

[![Tabela Abacaxi](http://farm4.static.flickr.com/3387/3511174990_624a64d95c_o.png)](http://www.flickr.com/photos/seiti/3511174990/ "Tabela Abacaxi")

Mapeando através do *dbml*, cria-se a classe Abacaxi no sistema, com as seguintes propriedades: *id, responsavel, tarefa e datalimite*.

[![Abacaxi Linq Object](http://farm4.static.flickr.com/3336/3511174978_749a3a9e4c_o.png)](http://www.flickr.com/photos/seiti/3511174978/ "Abacaxi Linq Object")

Simples não? O Linq To Sql te dá o Abacaxi, pronto para descascar.

### Problemas

Mesmo após a curva inicial de aprendizado, em que devemos nos acostumar com a sintaxe Linq, e a reaprender a escrever  consultas triviais em SQL, existem outros problemas que permanecem.

Cada objeto Linq To Sql se refere à uma entrada em uma tabela de banco de dados. Como ele serve primariamente para transportar dados, não contendo métodos próprios,  podemos chamá-lo de DTO (Data Transfer Object).

Este DTO é de díficil utilização, quando desconectados. Digo, se você consulta a tabela Abacaxi através do Linq To Sql, você consegue uma monte de objetos Abacaxi’s.

Tome um destes objetos Abacaxis. Vamos batizá-lo de **abac**. Eu pego o **abac** e jogo o DataContext que o criou fora. Atualizo o **abac**. Instancio um novo DataContext, do mesmo tipo que o anterior.

Este **abac** deve ser conectado a um DataContext de [uma maneira muito complicada](http://www.west-wind.com/WebLog/posts/134095.aspx). Muito mais complicada do que deveria.

Há quem diga que, por esta e outras,  o Linq To Sql não está pronto para uma [aplicação em  camadas](http://www.dotnetlog.com/archive/2008/03/24/is-v1-of-linq-to-sql-only-suitable-for-rad.aspx) (*N-tier*),  situação  atendida plenamente por ferramentas como o **Hibernate**.

Se mesmo assim você quser utilizar o Linq, [já existe uma excelente discussão](http://www.west-wind.com/weblog/posts/246222.aspx) sobre as possibilidades de se arquitetar seu projeto com o uso do Linq To Sql em mente.

### Meu uso

No projeto em que estou trabalhando, utilizamos o Linq To Sql sem muitas dores de cabeça. No momento é esta a arquitetura empregada:

- Para cada subsistema, um DBML;
- Para cada tabela, uma classe de negócios;
- Para cada view no BD, uma classe correspondente (para cada coluna uma propriedade);
- Cada objeto de negócios, **uma **instância do DataContext.

A classe de negócios acaba ficando bem parecida com uma DAL, com a importante diferença dela se utilizar do Linq To Sql para intermediar o acesso ao BD.

Segue o esqueleto da classe de negócios:

 public class AbacaxiBLL: ITestableCrud<abacaxi>, IDisposable { protected ExemploDataContext dc; public AbacaxiBLL() { dc = new ExemploDataContext(); } public Abacaxi Le(int id) { throw new NotImplementedException(); } public Abacaxi Adiciona(Abacaxi obj) { throw new NotImplementedException(); } public Abacaxi Atualiza(Abacaxi obj) { throw new NotImplementedException(); } public void Exclui(int id) { throw new NotImplementedException(); } public void Dispose() { throw new NotImplementedException(); } }</abacaxi>

O corpo do método *Adiciona *fica assim então:

public Abacaxi Adiciona(Abacaxi obj) { dc.Abacaxis.InsertOnSubmit(obj); dc.SubmitChanges(); return obj; }

Isto te dá a liberdade de operar com o objeto **Abacaxi obj** antes de inserí-lo no BD.

E eu sempre tomo o cuidado de implementar a interface **IDisposable**, o que te obriga a criar o seguinte método:

public void Dispose() { dc.Dispose(); }

No final, o uso deste objeto de negócio é bem simples:

 using (AbacaxiBLL bll = new AbacaxiBLL()) { Abacaxi a = new Abacaxi(); a.responsavel = "Seiti Yamashiro"; a.tarefa = "Criar um post sobre o Linq To Sql no blog seiti.eti.br"; a.datalimite = new DateTime(2009, 5, 7); a = bll.Adiciona(a); }

Aos DBAs de plantão, meus métodos nas classes de negócios seriam o equivalente às SPROCs no banco de dados, que cuidadriam de toda a manipulação de dados. O ganho é a organização de maior possibilidade de reutilizar e compartilhar código. E fica muito mais fácil de se versionar (*Subversion*, anyone?) isto!

### Conclusão

Não tão robusto quanto um Hibernate, muito melhor que DataSets tipados. Fácil de aprender e usar, difícil de estabelecer uma arquitetura que satisfaça plenamente. Este é o **Linq To Sql**.


