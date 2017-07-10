---
layout: post
title: Edgy Eft para Feisty Fawn
date: '2007-05-09 21:42:12'
tags:
- ubuntu
---



## Update Manager

Como recente lançamento final do **Ubuntu Feisty Fawn**, resolvi atualizar meu sistema utilizando seu próprio *Update Manager*. Após seguir as instruções do [site oficial](http://www.ubuntu.com/getubuntu/upgrading) o sistema não subia. Até passava pelo GRUB, mostrava o splashscreen do Ubuntu (um pouco modificado com relação ao do Edgy) mas aparecia um erro e parava num terminal com o prompt dizendo apenas: <tt>(initramfs)</tt>.

E agora?

Bom, tive uma experiência semelhante após reparticionar o disco com o Gparted e eu já sabia que eu deveria:

1. montar o sistema de arquivos na mão com o <tt>mount</tt>;
2. editar o arquivo de configuração do GRUB <tt>/boot/grub/menu.lst</tt>

Pesquisei também no Google e encontrei isto: [http://ubuntuforums.org/showthread.php?t=392854](http://ubuntuforums.org/showthread.php?t=392854)  
 Que diz para trocar onde diz

<div class="code">kernel /vmlinuz-2.6.20-13-generic root=UUID=702e3aab-4a86-4374-8763-af456ddb9620 ro splash

</div>para

<div class="code">kernel /vmlinuz-2.6.20-13-generic root=/dev/sda5 ro splash

</div>(sda5 é a partição em que se encontra o **meu** Linux, em outros sistemas pode ser outra)

Para não ter de rebootar com sistema usando o Live CD, resolvi aprender a usar o <tt>sed</tt>, única ferramenta disponível para edição de texto no terminal que me foi dado (aquele do <tt>iniotramfs</tt> do começo do texto, lembra?).

Assim eu montei o sistema de arquivos:

 mkdir /image mount -o dev /dev/sda5/ /image

E depois editei o arquivo <tt>menu.lst</tt>

 cd /image/boot/grub/ sed -i 's_root=UUID=702e3aab-4a86-4374-8763-af456ddb9620_root=/dev/sda5_' menu.lst

REBOOT!

A estranha seqüencia de caracteres **UUID=702e3aab-4a86-4374-8763-af456ddb9620** (veja abaixo) tive de pegar listando o arquivo <tt>menu.lst</tt> com o comando **cat** e digitando um por um…

O estranho é que depois de inicializado o sistema, verifiquei outra sequëncia estranha de caracteres no mesmo arquivo, no trecho:

 #kopt=root=430e3aab-4a86-4374-8763-af456ddb9620 #kopt_2_6=root=/dev/sda7 ro

que tratei de mudar para:

 #kopt=root=/dev/sda5 #kopt_2_6=root=/dev/sda5 ro

Assim na próxima atualização do kernel não terei problemas (espero!).


## UUID

Nada como o Wikipedia para tirar nossas dúvidas. O [UUID](http://en.wikipedia.org/wiki/UUID), ou *Universally Unique Identifier* trata-se de um identificador de propósito geral criado pela *Open Software Foundation*, que por sua vez foi criada para padronizar a implementação de sistema UNIX.

No nosso caso, no sistema de arquivos **ext3**, que é o que eu uso, o UUID é utilizado para identificar cada partição da máquina, além dos vários dispositivos de armazenamento que possam ser plugados no mesmo, tais como pen-drives, hds portáteis, mp3 players…

Assim cada dispositivo terá seu próprio número e poderá possuir uma configuração individual.

O Ubuntu, a partir da versão 6.10 (*Edgy Eft*) passou a utilizar este sistema.

Para descobrir qual o UUID de uma determinada partição podemos utilizar o comando <tt>vol_id</tt>:

 sudo vol_id -u /dev/sda1

O comando acima mostrará o UUID da primeira partição do dispositivo **sda**, que no caso é meu HD SATA.

Bom, fica a critério usuário manter-se nos <tt>/dev/</tt> da vida ou utilizar os UUID. Ao menos no que se refere ao <tt>menu.lst</tt> =)


