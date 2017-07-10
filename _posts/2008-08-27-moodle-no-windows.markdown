---
layout: post
title: Moodle no Windows
date: '2008-08-27 14:16:20'
---


O Moodle é um sistema de gerenciamento de cursos (Course Management System), que até onde sei, é o padrão de facto para ensino à distância, ou EAD, em faculdades.

### WISP?

Se LAMP é o acrônimo para Linux+Apache+MySQL+PHP, WISP é o contraponto, composto pela pilha Windows+IIS+SQLServer+PHP. Devido às vicissitudes da vida irei instalar o Moodle num servidor WISP e relatar o causo por aqui.

Existe um módulo PHP ISAPI pronto para ser usado, mas se seu negócio é desempenho, então use Linux. Se não der, o site oficial da MS para PHP indica o FastCGI como melhor opção.  
 Lembre-se de instalar a versão thread-safe do PHP, ao contrário da recomendação do site. Tentei utilizar a versão non-thread-safe (nts) sem sucesso.

Instalado o fastcgi e o PHP, resta configurar supote ao banco de dados MS SQL Server. Parece que o módulo php_mssql.dll não serve. Mas a alternativa funcionou muito bem.


