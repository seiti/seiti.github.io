---
layout: post
title: Constantes no PHP e o padrão Typesafe enum
date: '2008-06-05 11:26:54'
tags:
- design-patterns
- php
- programacao
---


Lidando com o PHP e suas idiossincrasias, notei que os campos de classe declarados com o modificador ***const*** só podem receber valores *escalares*. Por escalares entendam *string* e *números*, pois até referências para objetos (que nada mais são que números, pois guardam endereços de memória) são proibidos.

Procurando pela web pela razão disto encontrei este ótimo post:  
[ Constantes e as limitações do PHP](http://joseberardo.blogspot.com/2007/02/constantes-e-as-limitaes-do-php.html "Constantes e as limitações do PHP")

[](http://http://joseberardo.blogspot.com/2007/02/constantes-e-as-limitaes-do-php.html "Constantes e as limitações do PHP")  
 Outro assunto discutido no post acima é o padrão [Typesafe enum](http://www.javacamp.org/designPattern/enum.html "Typesafe Enum"), padrão incorporado em .Net. Muito útil, por sinal.


