---
layout: post
title: Linked Servers
date: '2008-11-27 19:49:42'
tags:
- sql-server
---


Para realizar consultas em outros bancos através do próprio MS SQL Server é preciso registrá-los via algumas SPs:

sp_addlinkedsrvlogin  
 sp_addlinkedserver  
 sp_linkedservers  
 sp_dropserver

A tabela que contém os bancos de dados externos registrados ficam na tabela **sys.servers**.

[http://msdn.microsoft.com/en-us/library/ms190479.aspx](http://msdn.microsoft.com/en-us/library/ms190479.aspx)


