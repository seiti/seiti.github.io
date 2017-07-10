---
layout: post
title: Odbc DataSource 32bits no Windows 7
date: '2009-08-31 19:26:36'
tags:
- driver
- odbc
- windows
---


Ando efetuando uns testes com o Postgresql e o Virtual Box, ambos excelentes sistemas. No Virtual Box eu criei uma máquina virtual, nele instalando um Ubuntu Server 64 bits com o Postgresql – e configurando o *postgresql.conf* e *pg_hba.conf* como sempre.

A partir de outra máquina virtual, rodando o Ubuntu Jaunty Desktop, consigo normalmente acessar o banco de dados no Ubuntu Server, então tudo ok. Ou quase tudo ok.

Para acessar o banco de dados postgresql a partir de meu sistema **hospedeiro** – ou seria **anfitirião**? **estalajadeiro**?, rodando o indefectível ( até o momento) Windows 7 tive de instalar os controladores ODBC (disponíves no [ftp do Postgresql](http://www.postgresql.org/ftp/odbc/versions/msi/)) .

Depois de instalar, navego até o *Painel de Controle*, depois para *Fontes de dados Odbc* e, CADÊ? Sumiu, ninguém viu. Só aparecem listados os controladores das fontes de dados do SQL Server. Muito estranho.

Mas eu já havia feito isto. Uma busca em [minha memória](http://www.google.com) e[ me lembrei](http://razorsql.com/docs/odbc_setup.html) que era um problema de versão do sistema. O controlador, ou *driver* , que instalei é de 32 bits. O sistema é de 64 bits. E o Windows não gosta de misturar alhos com bugalhos.

Para acessar finalmente o gerenciador de fontes de dados ODBC 32 bits é necessário executar este safado:

> C:\Windows\SysWOW64\odbcad32.exe

Agora sim!


