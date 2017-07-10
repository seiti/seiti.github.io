---
layout: post
title: Cdr para SVG
date: '2008-06-23 11:13:00'
tags:
- svg
- ubuntu
---


Vez por outra recebo arquivos em formatos estranhos, muitas vezes não possuindo o programa necessário para abrí-los. Daí a importância da utilização de formatos abertos e software livre.

Emfim, o arquivo que recebi possuía a extensão *cdr*, utilizado pelo programa Corel Draw. A fim de acessar o conteúdo deste arquivo, e quem sabe editá-lo no Inkscape, é preciso convertê-lo para o padrão SVG. Segue uma pequena receita.

Ingredientes:

- Ubuntu (ou a distro de sua preferência; mas acerte a receita de acordo)
- pacote RPM do *uniconvertor*
- pacote *alien*
- pacote *python-imaging* (Python Image Library)

Fora o pacote do Uniconvertor, todos os outros estão nos repositórios oficiais, Instale-os.

Baixe o pacote **RPM** Uniconvertor ([http://sk1project.org](http://sk1project.org "sk1project")) e transforme-o em um pacote **DEB**, através do comando *alien*.

Instale o pacote DEB gerado. Utilize o comando ***uniconv*** para converter seus arquivos para SVGs.


