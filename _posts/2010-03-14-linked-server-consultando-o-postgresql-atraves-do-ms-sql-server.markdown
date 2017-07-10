---
layout: post
title: 'Linked Server: consultando o PostGreSQL através do MS SQL Server'
date: '2010-03-14 16:51:57'
tags:
- postgresql
- sql-server
---


Antes de tudo é necessário instalar os [drivers ODBC](http://www.postgresql.org/ftp/odbc/versions/msi/) do PostGreSQL no servidor em que se encontra o MS SQL Server.

Depois registre um *System DSN*, ou Fonte de Dados do Sistema. Para isto basta se encaminhar para:

> Painel de Controle → Ferramentas Administrativas → Fontes de Dados ODBC.

Basta preencher as caixinhas e depois testar. Com a conexão funcionando,  agora é hora de se criar um *Linked Server* entre o MS SQL Server e o PostGreSQL.

 EXEC master.dbo.sp_droplinkedsrvlogin @rmtsrvname=N'LINKEDSERVERNAME' , @locallogin=NULL EXEC master.dbo.sp_dropserver @server = 'LINKEDSERVERNAME' EXEC master.dbo.sp_addlinkedserver @server = 'LINKEDSERVERNAME' , @provider = 'Postgresql OLE DB' , @datasrc = 'Postgresql ANSI' EXEC master.dbo.sp_addlinkedsrvlogin @rmtsrvname=N'LINKEDSERVERNAME' , @useself=N'False' , @locallogin=NULL , @rmtuser='usuariopostgres' , @rmtpassword='senhapostgres'

Agora você pode fazer consultas assim:

 SELECT * FROM openquery(LINKEDSERVERNAME, 'SELECT * FROM TABELADOPOSTGRES')


