---
layout: post
title: Impressora Epson TX600FW
date: '2010-03-15 00:59:11'
tags:
- impressora
- linux
- scanner
- ubuntu
- windows
---


A  Epson TX600FW é uma multifuncional de rede, direcionada ao mercado SOHO – escritórios pequenos ou em casa –  oferecendo interfaces tanto ethernet quanto Wi-Fi. Isto significa independência de um computador conectado e ligado.  Para quem tem em sua casa mais de um computador, significa comodidade e facilidade de uso. Mas infelizmente facilidade de uso não é igual a facilidade na instalação.

[![Epson TX600FW](http://farm5.static.flickr.com/4057/4433737775_086c64e63e.jpg)](http://www.flickr.com/photos/seiti/4433737775/ "Epson TX600FW by Seiti Yamashiro, on Flickr")

### Windows Vista

Com o CD de instalação que acompanha o produto só consegui identificar e configurar a impressora na rede. A instalação final da impressora no próprio Windows Vista não deu muito certo, sempre falhando ao final, acusando falta de drivers. O jeito foi baixar o pacote com os drivers mais recentes:

[Drivers para Windows e Mac OS](http://www.epson.com.sg/epson/drivers/driver_download.htm?mode=3&catid=4&productModel=4&catid=&pid=1401&ad=1&downloadType=Windows)

Mas ao instalar não havia a opção TCP/IP ou Rede nas portas disponíveis. O que fiz foi escolher o USB e proceder com a instalação. Após instalado, acessei as **propriedades** da impressora, na guia **portas**, e adicionei uma porta do tipo TCP/IP, apontando para o endereço 192.168.1.4. Este IP é o da impressora, que eu mesmo verifiquei através do roteador.

Após este procedimento a impressora finalmente ficou disponível para uso no Windows Vista.

Quanto ao scanner, instalei os drivers obtidos no link acima. Mas o software de digitalização da EPSON simplesmente não funcionou. Achei que era por falta de configuração e entrei no *Definições EPSON Scan*. Aha! Precisava mesmo configurar o IP da multifuncional. Mas  mesmo após identificá-lo, o EPSON Scan dava pau. Bom, ainda bem que existe o GIMP, que consegue digitalizar facilmente usando a TX600FW. Quer dizer que os drivers estão ok, mas o software de digitalizaçao da EPSON não.

### Windows 7

No mesmo link indicado acima existem os drivers para Windows 7. Ou então acesse este: [http://www.suporte-epson.com.br](http://www.suporte-epson.com.br).  
 Usando o Firefox eu não consegui baixar o arquivo de primeira. Analisando o código fonte do popup dá pra ver que o culpado é um javascript sem vergonha. Assim montei na mão mesmo a [URL para o arquivo](http://189.125.111.120/suporte_down/arquivo1.asp?path=arquivos_temp/CI_TX600FW_WINXPX64_VISTA64_7X64.EX). Ou use o IE.

O link para o arquivo é bem lento e propenso a interrupções. Mas com paciência consegue-se o driver.

### Ubuntu

Num primeiro momento eu ia baixar e instalar os drivers do site da Avasys: [drivers para Linux](http://www.avasys.jp/lx-bin2/linux_e/spc/DL1.do) (Ubuntu e cia.). Mas infelizmente não existem os drivers para a arquitetura 64bits lá no site.

Mas então me ocorreu tentar instalar a impressora sem o uso de drivers externos. Bom, o Ubuntu deu conta do recado. Identificou, configurou e adicionou a impressora em dois cliques. E dizem que Windows é que é simples de usar! Bah.

O scanner ainda não configurei, mas posso adiantar que só instalar o pacote do site Avasys não é suficiente. As instruções que consegui nos [fóruns](http://ubuntuforums.org/showthread.php?t=1393162) do Ubuntu são:

– instalar os driver da Avasys;

– instalar o plugin do sane [iscan-network-nt](http://linux.avasys.jp/drivers/scanner-plugins/iscan-network-nt/1.1.0/iscan-network-nt_1.1.0-2_i386.deb);

– editar o arquivo /etc/sane.d/dll.conf, certificando-se de comentar as linhas *epson* e *epson2* e incluir o *epkowa*;

– editar o arquivo /etc/sane.d/epkowa.conf incluindo a linha net 192.168.1.4 (troque pelo IP da tua máquina).

(ok, ok, o Windows é que é fácil de usar…)

Se alguém conseguir, é só dizer aí embaixo!

### Sem computador

A Epson TX600FW ainda digitaliza imagens e guarda automaticamente em um cartão de memória inserido nela, dispensando o uso de um computador. Uma pasta chamada EPSCAN é criada e uma outra pasta numerada dentro dela, contendo a imagem digitalizada.

<figure class="wp-caption aligncenter" style="width: 224px;">[![Guia EPSON](http://farm3.static.flickr.com/2742/4433714173_447541518e.jpg "Imagem digitalizada direto para o cartão de memória")](http://www.flickr.com/photos/seiti/4433714173/ "Guia EPSON by Seiti Yamashiro, on Flickr")<figcaption class="wp-caption-text">Imagem digitalizada direto para o cartão de memória</figcaption></figure>Só faltou criar um PDF, mas para isto ela precisa de um computador.

Outras funções que não necessitam de um computador são de cópia de documentos – ou “xerox”, impressão de fotos a partir do cartão de memória e os serviços de fax  (que nem se funcionam, pois uso VoIP. Aliás usar FAX sobre uma linha de telefone criada em cima de uma conexão de internet usando pacotes TCP/IP em cima de uma infraestrutura de cabos coaxiais me lembra uma massa folhada…). Um dia ainda testo isso.


