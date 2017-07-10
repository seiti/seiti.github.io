---
layout: post
title: Não consegue listar os Databases no SQL Management Studio?
date: '2009-06-16 18:05:29'
tags:
- banco-de-dados
- sql-management-studio
- windows
---


O MS SQL Management Studio (SMS) é uma ferramenta excelente para gerenciar seus bancos de dados. Isto não quer dizer que ele não tenha seus problemas.

O pior deles é que, ao se tentar listar os bancos de dados do sistema, e você não tiver permissão para visualizar **um** deles, o SMS graciosamente te apresentará esta mensagem de erro:

[![](http://farm4.static.flickr.com/3620/3632901689_d9fbe33a0d.jpg?v=0 "Failed to retreive data for this request")](http://www.flickr.com/photos/seiti/3632901689/)

> Failed to retrieve data for this request. (Microsoft.SqlServer.Management.Sdk.Sfc)
> 
> Additional information:  
>  An exception occured while executing a Transact-SQL statement or batch.  
>  (Microsoft.SqlServer.ConnectionInfo)  
>  The server principal “Seiti” is not able to access the database “AlgumBanco” under the current security context. (Microsoft SQL Server, Error: 916)

Como então listar os bancos de dados? Não sou o único nem serei o último a enfrentar este problema, então é claro que alguém já [blogou sobre isto e o resolveu](http://blogs.sftsrc.com/stuart/archive/2009/05/13/SQL-2008-Management-Studio---Unable-to-Enumerate-Databases.aspx), inclusive [mais de uma pessoa](http://sqlblog.com/blogs/aaron_bertrand/archive/2008/07/07/a-little-management-studio-oops.aspx).

O problema consiste-se nas informações que são apresentadas no *Object Explorer Details* – para visualizá-lo tecle F7. Note as colunas que existem na visualização padrão: *Name, Policy Health State, Recovery Model, Compatibilty Level , Collation *e* Owner*.

Observe a coluna **Collation**. O SMS lista os bancos e verifica as informações que devem constar no *Object Explorer Details*.  Você não tem permissão sobre **um** dos bancos listados. Mas para saber o *collation* do banco deve-se ter permissões sobre o mesmo. O SMS entra em pânico, interrompe tudo, deixa de fazer o que deveria e mostra a mensagem de erro acima. Simples.

Como resolver? Clique com o direito sobre os nones das colunas e remova o *Collation*. O SMS ficará feliz da vida e fará o que devia fazer.


