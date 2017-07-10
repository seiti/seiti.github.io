---
layout: post
title: Apache Tomcat
date: '2008-04-15 21:39:19'
---


O Apache [Tomcat](http://tomcat.apache.org/) é um servidor de aplicações Java. Vamos instalá-lo no [Ubuntu Feisty Fawn](http://seiti.eti.br/blog/2007/edgy-eft-para-feisty-fawn).

Primeiro instale os seguintes pacotes:

sudo apt-get install sun-java6-jre sun-java6-jdk tomcat5.5 tomcat5.5-webapps tomcat5.5-admin

Talvez seja preciso definir qual o [Java padrão](../../wiki/Eclipse) do sistema.

Depois edite o arquivo <tt>/etc/default/tomcat5.5</tt>, colocando a seguinte linha:

JAVA_HOME=/usr/lib/jvm/java-6-sun

E crie o arquivo de log, removendo o pipe quebrado (dica do [fórum do Ubuntu](http://ubuntuforums.org/showthread.php?t=436295)):

cd /var/log/tomcat5.5/ sudo rm catalina.out sudo touch catalina.out sudo chown tomcat55:nogroup catalina.out sudo chmod uo-wrx catalina.out

Como instalamos o pacote <tt>tomcat5.5-admin</tt>, basta apontar para o endereço [http://localhost:8180/admin](http://localhost:8180/admin) que será apresentada uma tela de login. Mas que usuário e senha utilizamos? Nenhum, ainda falta configurá-lo. Devemos editar o arquivo <tt>/var/lib/tomcat5.5/conf/tomcat-users.xml</tt>, editando a seguinte linha:

<div class="code"><user password="tomcat" roles="tomcat" username="tomcat"></user>

</div>Para algo como isto:

<user password="senhadotomcat" roles="tomcat,admin" username="tomcat"></user>

Reinicie, ou inicie, o bichano:

sudo /etc/init.d/tomcat5.5 restart


