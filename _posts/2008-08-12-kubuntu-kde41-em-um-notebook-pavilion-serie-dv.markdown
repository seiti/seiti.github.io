---
layout: post
title: Kubuntu + KDE4.1 em um Notebook Pavilion Série DV
date: '2008-08-12 17:55:13'
tags:
- kde4
- kubuntu
- notebook
- ubuntu
---


Troquei de notebook: meu [[UbuntuLaptop|Toshiba]] por um HP Pavilion DV6775. Baixei o *Kubuntu Remix Live CD* e bootei o dito. Quase tudo funcionou de primeira. O item que mais fez falta foi a rede sem fio. O interessante foi abrir o terminal, rodar um <tt>sudo iwlist wlan0 scanning</tt> e obter resultados! Quer dizer que o sistema identificou o *wifi*, mas não me ofereceu ajuda gráfica para configurá-la. Culpa do KDE, eu acho…

<div style="margin: 4pt 4pt 4pt 0pt; padding: 0pt 8pt 4pt; float: left; width: 40%; background-color: #ddedff;">#### Kubuntu 8.04 Hardy Heron Remix

O **Kubuntu** é o Ubuntu com o *KDE* como *desktop manager*. O **Kubuntu Remix** é o Ubuntu com o *KDE **4*** como *desktop manager*.

</div>Mas sabendo que tudo pode ser diferente depois de instalado, iniciei o processo de instalação. Infelizmente não encontrei o **gparted**, **kparted** nem o raio que o parted. Não confiando muito no assistente de instalação para definir minhas partições sem perder meu *outro SO* (sim, preciso do Windows para jogar e programar em C#/Asp.Net), me lembrei de um pendrive com o [[AsusEeePC | eeeXubuntu]] pronto para usar!

Bootei com o pendrive, particionei o HD com o gparted, tornei a bootar pelo Kubuntu Live CD e finalmente instalei o sistema. Sem muita surpresa, o sistema estava com tudo funcional: gravador de DVD, rede wifi, som, botões multimídia (exceto o Play/Pause…), controle remoto, leitor de cartões. Outros itens, tais como saída HDMI e a de s-vídeo, eu ainda não testei.

### KDE4.1

Infelizmente o KDE 4 deixou muito a desejar, o jeito foi fazer um upgrade para o [KDE 4.1](http://www.kubuntu.org/news/kde-4.1). O mensageiro instantâneo padrão é o Kopete. Minha supresa foi verificar que a webcam funcionava com ele! Sem dores de cabeça. Após [configurar](http://www.guiadohardware.net/dicas/google-talk-kopete.html) minha conta do [Google Apps](http://seiti.eti.br/blog/2008/migrando-para-o-google-apps-gmail) tudo funcionou ok.

Um software que achei bem bacana foi o **Marble**. Pena que o mapa de ruas de São Paulo deixe a desejar. Já o Amarok 2 Alpha apresentou um visual muito bom. O problema é que não tocava música nenhuma.

O **Firefox **mostrou uma cara bem feia, solucionado com este [tema](https://addons.mozilla.org/pt-BR/firefox/addon/7574), que casa muito bem com o visual do *Oxygen*.  
 Para finalizar preciso configurar meu acesso a partição ext3 [a partir do Windows](http://www.fs-driver.org/).

Muita coisa ainda não funciona a contento, como o som, algumas teclas multimídia, algumas teclas **Fn** (como a de aumentar o brilho do backlight do LCD), o Kate. Isto memso aplicando várias soluções encontradas nos fóruns do Ubuntu. O estranho é que tudo isto funciona bem sob o *Ubuntu Hardy Heron*.

Bom, talvez ainda não seja a hora de migrar para o Kubuntu 4.1.


