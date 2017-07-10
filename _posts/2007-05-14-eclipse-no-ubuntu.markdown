---
layout: post
title: Eclipse no Ubuntu
date: '2007-05-14 21:27:38'
tags:
- eclipse
- java
- ubuntu
---


No **Ubuntu** é muito simples instalar o Eclipse, basta instalá-lo a partir dos repositórios oficiais. (mas sempre [dá para instalar](ttp://seiti.eti.br/blog/2007/eclipse-no-ubuntu-antes) o pacote baixado da SUN)

Quanto ao Java, caso não queira utilizar o [GCJ](http://en.wikipedia.org/wiki/GCJ), não é necessário baixar diretamente da SUN os pacotes da versão mais recente (já estamos no Java 6). É só instalar a partir do *Synaptic*. Faça uma busca por <tt>sun-java</tt> e instale os pacotes necessários.

Depois, para mudar qual dos javas será o padrão para o sistema em geral entre com o seguinte comando para listar as versões instaladas:

 update-java-alternatives -l

Para configurar o Java 6 como padrão entre com:

 update-java-alternatives -s java-6-sun

Caso o Eclipse teime em usar o GCJ, você tem duas alternativas: editar o arquivo <tt>/etc/eclipse/java_home</tt> (mudança global) ou editar o arquivo <tt>~/.eclipse/eclipserc</tt> (mudança em nível de usuário).

Caso resolva-se editar o <tt>eclipserc</tt>, basta adicionar a seguinte linha:

 JAVA_HOME="/usr/lib/jvm/java-1.6.0-sun"

E para saber que problemas estão ocorrendo no Eclipse, nada como o log de erros: **Window->Show View->PDE runtime->Error log**

Referência: [http://weblogs.java.net/blog/robogeek/archive/2007/05/ubuntu_and_easi.html](http://weblogs.java.net/blog/robogeek/archive/2007/05/ubuntu_and_easi.html)


