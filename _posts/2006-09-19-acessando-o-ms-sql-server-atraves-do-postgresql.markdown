---
layout: post
title: Acessando o MS SQL Server através do PostGreSQL
date: '2006-09-19 19:52:19'
tags:
- postgresql
- sql-server
---


Para acessar o MS SQL Server através de aplicativos que não possuam os meios oficiais de acesso (protocolo TDS) devemos utilziar ou o [FreeTDS](http://freetds.org/) ou uma conexão ODBC (Open Database Communication).  
 Segue como utilizar uma conexão ODBC através do módulo DBI do Perl:

Configurando o [PostGreSQl](../../wiki/PostGreSQl/edit "Create this page") para acessar fontes externas de dados:

- instale o Perl (padrão para usuários Unix/Linux, [ActivePerl](http://aspn.activestate.com/ASPN/Downloads/ActivePerl/) no caso de usuários Windows);
- instale os módulos DBI e DBD-ODBC do Perl via <tt>ppm</tt> (ou “Perl Package Manager”);
- adicione a linguagem <tt>plperlu</tt> à lista de linguagens de seu banco de dados (utilize o [PgAdmin](http://www.pgadmin.org/) ou vá por linha de comando: <tt>psql</tt>)
- instale o módulo [dbi-link](http://pgfoundry.org/projects/dbi-link/) no [PostGreSQL](../../wiki/PostGreSQL/edit "Create this page"), basta rodar os scripts (note que o script do arquivo <tt>remote_query.sql</tt> está com problemas, tente este no lugar: [remote_query2.sql](../../wiki/SQLServer/files.xml?action=download&file=remote_query2.sql));
- teste!!

<div class="code" style="font-family: monospace;"><span class="kw1">SELECT</span> * <span class="kw1">FROM</span> remote_select<span class="br0">(</span>  
<span class="st0">‘dbi:ODBC:DRIVER=SQL Server;UID=nom_usuario;PWD=senha_usuario;WSID=nom_maquina;DATABASE=nome_BD;APP=Microsoft Data Access Components;SERVER=(local);Description=Sql Server ODBC’</span>  
 , <span class="st0">‘nom_usuario’</span>  
 , <span class="st0">‘senha_usuario’</span>  
 , <span class="st0">‘{AutoCommit => 1, RaiseError => 1}’</span>  
 , <span class="st0">‘SELECT * FROM tabela’</span><span class="br0">)</span>  
<span class="kw1">AS</span><span class="br0">(</span>id int4, coluna varchar, outracoluna varchar<span class="br0">)</span></div>A consulta acima resulta numa tabela com três colunas: <tt>id, coluna e outracoluna</tt>.  
 Talvez seja preciso mudar o primeiro parâmetro da chamada da função, que é onde se encontra o DSN (“Data Source Name”) do ODBC. Tente criar pelo próprio Windows (estou numa estação com Windows 2003), indo na seção de configuração de <span class="notes">Fontes de Dados ODBC</span>, na aba <span class="notes">Fonte de dados de arquivos</span> (que eu acho que deveria ter sido traduzido como “arquivo de fonte de dados”, mas enfim…). Siga o “wizard” apresentado e depois abra o arquivo .dsn num editor de texto para obter a string de conexão.

Note que é preciso que os nomes das tabelas no SQL Server estejam todos em minúsculo. Se este não for o caso, tente utilizar aspas duplas nos nomes das colunas:

<div class="code" style="font-family: monospace;"><span class="kw1">SELECT</span> * <span class="kw1">FROM</span> remote_select<span class="br0">(</span>  
<span class="st0">‘dbi:ODBC:DRIVER=SQL Server;UID=nom_usuario;PWD=senha_usuario;WSID=nom_maquina;DATABASE=nome_BD;APP=Microsoft Data Access Components;SERVER=(local);Description=Sql Server ODBC’</span>  
 , <span class="st0">‘nom_usuario’</span>  
 , <span class="st0">‘senha_usuario’</span>  
 , <span class="st0">‘{AutoCommit => 1, RaiseError => 1}’</span>  
 , <span class="st0">‘SELECT * FROM tabela’</span><span class="br0">)</span>  
<span class="kw1">AS</span><span class="br0">(</span><span class="st0">“Id”</span> int4, <span class="st0">“coluna”</span> varchar, <span class="st0">“outraColuna”</span> varchar<span class="br0">)</span></div>E é isso.


