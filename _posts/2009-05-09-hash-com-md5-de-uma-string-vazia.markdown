---
layout: post
title: Hash com MD5 de uma string vazia
date: '2009-05-09 01:04:53'
tags:
- cripto
---


MD5 é um algoritmo que calcula o hash de determinado string, muito usado para encriptar senhas. Assim, ao guardar uma senha do tipo “The quick brown fox jumps over the lazy dog” no banco de dados, o que realmente é gravado é:

<div class="code">MD5("The quick brown fox jumps over the lazy dog") = 9e107d9d372bb6826bd81d3542a419d6

</div>E na próxima vez que você digitar a senha, é calculado o hash MD5 de sua senha e comparado com o valor armazenado no banco.

Agora a parte útil. O hash MD5 de uma string vazia é:

<div class="code">MD5("") = d41d8cd98f00b204e9800998ecf8427e

</div>Uma mão na roda cso seja preciso resetar uma senha esquecida e você tenha acesso ao banco de dados.

Mas, se o sistema validar o campo referente à senha, vai ser preciso digitar algo. Uma boa é calcular o MD5 de alguma string não vazia qualquer via terminal, ou então utilizar alguma [ferramenta online](http://www.miraclesalad.com/webtools/md5.php).

**Atenção**: Isto não vai funcionar se o hash estiver [com sal](http://seiti.eti.br/blog/2009/hash-com-tempero)!


