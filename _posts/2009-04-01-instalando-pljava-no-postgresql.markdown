---
layout: post
title: Instalando PLJava no PostgreSQL
date: '2009-04-01 00:09:04'
tags:
- banco-de-dados
---


O PostgreSQL, como muitos outros bancos de dados, possibilita ao programador criar procedimentos em linguagens específicas. Entre elas o *Java*, ou *PL/Java*.

Vou documentar aqui como instalei o PL/Java no **Ubuntu**, mas creio que as instruções aqui sejam agnósticas o suficiente para servirem a outras distros. Vamos lá:

- Baixar o pacote do [PL/Java](http://pgfoundry.org/projects/pljava/).
- Obter o pacote postgresql.jar.
- Abrir o pacote do PL/Java.
- Copiar o arquivo postgresql.jar no diretório criado.
- Copiar o pljava.so para o diretório */usr/lib/postgresql/8.3/lib*
- Editar o arquivo <tt>/etc/postgresql/8.3/main/postgresql.conf</tt>:`custom_variable_classes = 'pljava'`
- Criar e editar o arquivo */etc/ld.so.confi.d/jvm.conf* com o seguinte conteúdo:```
<code class="prettyprint"><br></br>
/usr/lib/jvm/java-6-sun/jre/lib/i386/<br></br>
/usr/lib/jvm/java-6-sun/jre/lib/i386/client/<br></br>```
- Rodar o *ldconfig*:```
<code class="prettyprint"><br></br>
sudo ldconfig<br></br>```
- Finalmente instalar o pljava em seu banco de dados:```
<code class="prettyprint"><br></br>
sudo java -classpath ./deploy.jar:./postgresql.jar  org.postgresql.pljava.deploy.Deployer -install -database meubanco -user postgres<br></br>```

PL/Java instalado no banco de dados!

Em caso de problemas, existe um ótmo tutorial aqui: http://eltonplima.blogspot.com/2008/11/instalando-o-pljava-no-ubuntu.html

Se surgir algum problema do tipo *undefined symbol*, verifique se você instalou a versão correta do pacote do PL/Java, ou uma [outra versão compilada do PL/Java](http://pgfoundry.org/pipermail/pljava-dev/2008/001280.html), se aparecer um erro contendo *assert_enabled*.


