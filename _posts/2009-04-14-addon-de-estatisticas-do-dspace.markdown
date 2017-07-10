---
layout: post
title: AddOn de estatísticas do DSpace
date: '2009-04-14 02:42:33'
tags:
- dspace
- instalacao
---


[![](http://www.dspace.org/templates/dspace_home//images/logo.jpg)](http://www.dspace.org) O [**Dspace**](http://www.dspace.org/) é um sistema de Biblioteca Digital implementado em Java, que gerencia e armazena documentos digitais e seus dados descritivos.

Um dos pontos fracos dele é o sistema de estatísticas, que é bem simplório, ainda mais quando nos acostumamos com coisas como o *Google Analytics*.

Mas a Universidade do Minho desenvolveu um addon que [oferece um sistema](http://wiki.dspace.org/index.php/StatisticsAddOn) bem mais completo de estatísticas.

Para instalá-lo, basta seguir a documentação oficial, que segue basicamente este checklist:

- [Instalar o PL/Java](http://seiti.eti.br/blog/2009/instalando-pljava-no-postgresql)
- Criar a linguagem PL/Java no esquema dspace:`createlang -U postgres plpgsql dspace`
- Rodar os scripts SQL no banco do DSpace;
- Instalar o código java;
- Editar algum código Java;
- Criar tags jsp;
- Criar entradas na configuração do log4j, para que ele inclua dados em uma tabela no bd;
- Atualizar e inserir alguns dados no BD;
- Compilar o código atualizado do DSpace;
- Implantar os arquivos war gerados;
- Registrar no BD os arquivos jar gerados;
- Pronto! Visite http://www.example.com/stats

Nota: cuidado com [um bug](http://seiti.eti.br/blog/2009/bug-no-plugin-de-estatisticas-do-uminho-para-o-dspace) que encontrei!!

Para que este sistema de estatísticas funcione corretamente, identificando a região de origem do visitante do site, não se esqueça de usar o **mod_jk**, se você estiver utilizando o Apache como frontend do Tomcat. Não utilize acesso Proxy, senão qualquer acesso será registrado como proveniente da própria máquina.


