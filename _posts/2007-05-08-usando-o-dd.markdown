---
layout: post
title: Usando o DD
date: '2007-05-08 19:29:02'
---


Resolvi trocar o HD do meu notebook por um de maior capacidade. Para isto comprei o dito HD e um *case* USB/e-SATA para aproveitar o HD que vai sair do computador.

Como eu não queria passar novamente pelo processo de instala/configura/verifica, tanto do Windows como do Linux, decidi procurar alguma alternativa parecida ao Norton Ghost, mas no mundo Linux.  
 Encontrei o comando <tt>dd</tt>.

O <tt>dd</tt> copia um fluxo de dados de uma entrada para uma saída. Pode parecer pouco, mas isto o torna capaz de copiar, bit a bit, partições ou HDs inteiros, mesmo que contenham outros SOs.

Coloquei o HD novo no case USB, e liguei o notebook com o Live CD do Ubuntu 6.06 Dapper Drake. Verifiquei se os HDs realmente **não** estavam montados e executei a seguinte linha de comando:

<div>sudo dd if=/dev/sda of=/dev/sdb

</div>Após pouco mais de 3 horas de espera, o resultado no terminal foi este:

<div>155910825+0 records in 155910825+0 records out 79826342400 bytes (80 GB) copied, 16510.4 seconds, 4.8 MB/s

</div>Troquei os HDs de lugar e liguei o notebook. Tudo certo! Só precisei usar o Gnome Partition Editor (gparted) para extender a partição com o <tt>/home</tt> para ocupar o restante do HD.

Outra execução:

<div>dd: writing to `/dev/sdb': No space left on device 145226113+0 records in 145226113+0 records out 74355769344 bytes (74GB) copied, 3674.27 s, 20.2 MB/s

</div>
