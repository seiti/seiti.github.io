---
layout: post
title: Type "casting" no Javascript
date: '2009-05-11 01:26:37'
tags:
- javascript
---


O Javascript possui uma característica que pode incomodar quem está acostumado à linguagens como C, Java, C++: ele é *<span style="text-decoration: line-through;">fracamente</span> dinamicamente tipificado*.  
 Mas a possibilidade de modificar qual o tipo de uma variável é  útil.  Esta modificação de tipo é o *casting*.

Podemos efetuar um *casting* de um <tt>float</tt> para <tt>int</tt> através da função <tt>parseInt</tt>:

 b = 3; c = 2; a_int   = parseInt(b/c); //a_int contém 1 a_float = b/c; //a_float contém 1.5

E o contrário também, através do <tt>parseFloat</tt>.

Note que essas funções, na verdade, efetuam o *parse* do parâmetro de entrada, que pode ser uma string, devolvendo o valor final no tipo identificado por seu nome.

Mais info: [W3Schools:parseInt()](http://www.w3schools.com/jsref/jsref_parseInt.asp), [W3Schools:parseFloat()](http://www.w3schools.com/jsref/jsref_parseFloat.asp)


