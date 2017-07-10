---
layout: post
title: Hash com tempero
date: '2009-05-08 01:09:44'
tags:
- cripto
---


![salt](http://pubs.usgs.gov/of/1998/of98-805/lessons/chpt6/shaker.gif "WikiImage")Para armazenarmos senhas em algum lugar, seja em uma lista em um arquivo texto, seja em uma tabela no banco de dados, é prática comum apenas guardarmos o *hash* da senha.

Mas o que é um *hash*? Para a necessidade descrita acima basta saber que o hash é uma forma de transformar um texto qualquer em uma seqüência de caracteres de comprimento fixo, de tal forma que é *quase* impossível gerarmos duas seqüências iguais para dois textos de entrada diferentes. Para isto utilizamos a chamada **função de hash**.

Existem diversos algoritmos que tentam resolver este problema, sendo os mais conhecidos, pelo menos por mim, o MD5 e o SHA1.

Vejamos um exemplo. Utilizando o algoritmo MD5, o hash gerado pela seqüência “teste do hash” é <tt>92c2cafeb0c5fb58998be977b7deffbb</tt>.

Para calcular o hash visite a página [http://www.fileformat.info/tool/hash.htm](http://www.fileformat.info/tool/hash.htm).

Voltando às senhas, após guardar este hash no banco de dados, como fazemos para conferir a senha posteriormente? É simples, Basta tomarmos o texto de entrada, calcular seu hash e comparar os dois: o gerado no momento com o valor armazenado.

Por exemplo: tenho em meu BD o texto <tt>92c2cafeb0c5fb58998be977b7deffbb</tt>.  
 Alguém insere “blablabla” na caixa de texto de minha página.  
 Eu calculo o hash MD5 de “blablabla” e comparo com o valor que tenho guardado:

guardado no BD:  <tt>92c2cafeb0c5fb58998be977b7deffbb</tt>  
 “blablabla”:  <tt>1a36591bceec49c832079e270d7e8b73</tt>

Os valores calculados são diferentes. Então **blablabla** não é a senha. Note que não preciso saber qual a senha.  Só seu hash.

### O sal, por favor!

Existe um problema na abordagem acima. Caso alguém obtenha acesso indevido às consultas no banco de dados, pode utilizar o ataque de dicionário para obter as senhas. Isto é, tomando palavras comuns, pode-se gerar seus hashes e verificar se no banco existem hashes iguais a este gerado.

O problema piora se existirem senhas iguais para usuários diferentes. Eles terão valores de hash iguais guardados no banco de dados. Para evitar este problema e dificultar um pouco (pois é, só um pouco) a vida do atacante existe o **sal**. Devemos **salgar o hash** (*temperá-lo com sal*, ou *hash salting*).

Esta técnica consiste em criarmos uma *seqüência aleatória* de caracteres, que chamamos de *sal*, e anexarmos este valor ao texto da senha, para só depois calcularmos seu hash. Isto diminui bastante a chance de termos valores iguais de hash armazenados.

Como o sal é gerado aleatoriamente, precisamos guardá-lo para que seja possível compararmos senhas no futuro. É prática comum apenas concatenarmos o sal com o hash antes de armazenarmos seu valor.

> ### Receitas
> 
> Hash salgado:
> 
> - tomar o texto de entrada, ou a senha;
> - pegar o sal;
> - salgar a senha;
> - calcular o hash da senha salgada;
> - salgar o hash;
> - guardar o hash salgado.
> 
> Dizem que um hash salgado dura mais que um sem sal!  
>  E para conferir um valor contra o hash armazenado:
> 
> - pegar o hash armazenado e extrair o sal;
> - tomar o texto de entrada e salgá-lo com o sal extraído anteriormente;
> - calcular o hash do texto salgado;
> - salgar o hash calculado;
> - comparar o hash calculado com o armazenado.


