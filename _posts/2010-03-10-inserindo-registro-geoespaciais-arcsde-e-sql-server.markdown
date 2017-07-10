---
layout: post
title: 'Inserindo registros geoespaciais: ArcSDE e SQL Server'
date: '2010-03-10 18:13:34'
tags:
- arcgis
- geo
---


Inserir registros diretamente através de comandos SQL é bem simples. Note que estou usando como tipo de dado geoespacial o [GEOMETRY](http://seiti.eti.br/blog/2009/arcsde-e-ms-sql-server-2008), nativo do SQL Server 2008.

Primeiro  é necessário criar uma tabela no SQL Server e registrá-la junto ao ArcSDE. Isto é bem simples de se realizar utilizando o ArcCatalog (note que também dá para se criar a tabela via SQL e registrá-la no ArcSDE via linha de comando).  Basta entrar no ArcCatalog, conectar-se com sua instância do ArcSDE e clicar com o botão direito no ícone do banco de dados. Depois é só escolher o *Feature Class*:

<figure class="wp-caption aligncenter" style="width: 333px;">[![Feature Class](http://farm5.static.flickr.com/4068/4423382146_547ffd9792.jpg "Criando um Feature Class")](http://www.flickr.com/photos/seiti/4423382146/ "Feature Class by Seiti Yamashiro, on Flickr")<figcaption class="wp-caption-text">Criando um Feature Class</figcaption></figure>É apresentada então uma caixa de diálogo para criar sua tabela que conterá sua feição. Criei uma tabela chamada *MeuFeatureClass*. As colunas **OBJECTID** e **SHAPE** são criadas por padrão. Adicionei um **campo1** e um **campo2** também. E escolhi o tipo da geometria como *POINT*.

Criada a tabela é bem simples de se inserir um registro através de comando SQL:

 INSERT INTO MeuBD.sde.MeuFeatureClass (OBJECTID, campo1, campo2, shape) VALUES (1, valor1, valor2, geometry::STGeomFromText('POINT (-46.616667 -23.533333)', 4674))

O comando acima insere um registro na tabela contendo um ponto localizado no município de São Paulo – SP, usando o SRID 4674 ([SIRGAS 2000](http://seiti.eti.br/blog/2010/sirgas-2000)).

Note que não usamos uma função típica do T-SQL  para transformar o texto dado em uma coordenada válida pro sistema.  Isto me deixou confuso no início, pois eu não encontrava funções geoespaciais no banco de dados. Liste as funções existentes no banco de dados do ArcSDE que oê não encontrará nada relacionado ao sistema geo.

Estas funções ficam disponíveis como métodos da classe e objetos  ***geometry***.  No caso acima, o <tt>STGeomFromText</tt> é um método estático da classe <tt>geometry</tt>. Os mundos da Orientação a Objetos e do SQL se mesclam cada vez mais…


