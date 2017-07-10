---
layout: post
title: Linked server com Oracle
date: '2008-12-02 19:48:31'
tags:
- sql-server
---


Lembre-se de substituir 127.0.0.1 pelo IP que roda o servidor Oracle XE. O driver OraOLEDB.Oracle acompanha o pacote [Oracle Developer Tools for Visual Studio](http://www.oracle.com/technology/software/tech/windows/odpnet/index.html).

A SP [add_linkedserver](http://msdn.microsoft.com/en-us/library/ms190479.aspx) abaixo funciona para o Oracle XE:

<div class="code" style="font-family: monospace;">EXEC sp_addlinkedserver  
 @server = <span class="st0">‘ORA’</span>,  
 @srvproduct = <span class="st0">‘Oracle’</span>,  
 @provider = <span class="st0">‘OraOLEDB.Oracle’</span>,  
 @datasrc = <span class="st0">‘(DESCRIPTION=(ADDRESS=(PROTOCOL=TCP)(HOST=127.0.0.1)(PORT=1521))(CONNECT_DATA=(SERVICE_NAME=XE)))’</span>  
 GO</div>É necessário também ticar a opção <tt>Allow inprocess</tt> nas propriedadas do *provider*. É possível acessar os provedores em:

<div class="indent">*Server Objects* → *Linked Servers* → *Providers*</div>Depois é só configurar um usuário e senha para o *Linked Server* gravado através da SP [sp_addlinkedsrvlogin](http://msdn.microsoft.com/en-us/library/ms189811.aspx):

<div class="code" style="font-family: monospace;">EXEC sp_addlinkedsrvlogin  
 @rmtsrvname = <span class="st0">‘ORA’</span>,  
 @useself = <span class="st0">‘FALSE’</span>,  
 @rmtuser = <span class="st0">‘orausr’</span>,  
 @rmtpassword = <span class="st0">‘orapass’</span>  
 GO</div>Note que no MSSQL2005 há um problema referente aos campos *number* no Oracle e *int* no MSSQL. O provedor não consegue fazer a conversão, lançando um erro de conversão para *numeric*.

Já no SQL2008 parece funcionar.

As consultas podem ser realizadas através do comando <tt>openquery</tt>:

<div class="code" style="font-family: monospace;"><span class="kw1">SELECT</span> * <span class="kw1">FROM</span> openquery<span class="br0">(</span>ORA, <span class="st0">‘SELECT * FROM TABELA’</span><span class="br0">)</span></div>
