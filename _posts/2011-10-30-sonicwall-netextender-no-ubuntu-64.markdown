---
layout: post
title: SonicWall NetExtender no Ubuntu 64
date: '2011-10-30 02:24:21'
---


Bom, voltei ao Ubuntu, mas desta vez o 11.10 64bits. Fiquei feliz que o sistema está bem mais estável – até o momento – que o 11.04. Mas tem sempre algo que não funciona, que é o caso do cliente de VPN *NetExtender da SonicWall*.

Eu tinha feito [funcionar no Debian 64](http://seiti.eti.br/blog/2011/sonicwall-netextender-no-debian-64 "SonicWall NetExtender no Debian 64"), mas a mesma solução não coube aqui. O Ubuntu **não tem** uma variável de ambiente <tt>LD_LIBRARY_PATH</tt>. Como resolver então? Passando por cima do arquivo <tt>/etc/ ld.so.conf</tt> e definindo o [caminho para as bibliotecas na mão](http://tldp.org/HOWTO/Program-Library-HOWTO/shared-libraries.html):

sudo /lib/ld-linux.so.2 --library-path /lib32 ./netExtender -u username -d example.com vpn.example.com:4433

E é isso!


