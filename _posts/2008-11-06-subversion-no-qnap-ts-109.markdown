---
layout: post
title: Subversion no Qnap TS-109
date: '2008-11-06 23:56:35'
tags:
- arm
- linux
- nas
- subversion
- web
---


Após comprar meu [NAS Qnap TS-109](http://seiti.eti.br/blog/2008/nas-qnap-ts-109-turbo-station) e fuçar suas configurações, dar uma olhada no sistema de arquivos, ligar o MySQL, o FTP e o Apache, percebi que seria uma boa configurar um servidor *Subversion* nele.

[![](http://farm4.static.flickr.com/3003/3004619284_3d9dea7947_m.jpg "NAS Qnap")](http://www.flickr.com/photos/seiti/3004619284/)

Após consultar o [Oráculo](http://www.google.com) encontrei dois sites muito úteis: o [Wiki](http://wiki.qnap.com) e o [Fórum](http://forum.qnap.com) da Qnap.Visitando o fórum percebi que existe uma maneira bem prática de se instalar um aplicativo qualquer no NAS. É só usar o [IPKG](http://www.handhelds.org/moin/moin.cgi/Ipkg).

O ipkg é um gerenciador de pacotes no estilo *apt-get* e *yum*, mas voltado para dispositivos móveis. Como a arquitetura do meu NAS é **ARM**, similar aos *handhelds* que comumente rodam o ipkg, a própria Qnap adicionou suporte à este gerenciador de pacotes, denominando o pacote QPKG.

Para adicionar suporte ao ipkg foi bem simples, foi só [atualizar o firmware](http://www.qnap.com/download_detail.asp?pl1=download.asp%3Fpl%3D1&p_mn=TS-109+Pro&Keypl=1&pl=1&ct_name=Latest) do NAS, e depois seguir as instruções que o próprio site da [Qnap oferece](http://www.qnap.com/pro_features_QPKG.asp).

[![](http://seiti.eti.br/gallery2/main.php?g2_view=core.DownloadItem&g2_itemId=5796&g2_serialNumber=6&g2_GALLERYSID=5a994d495664f7f37b4075065ced2a4f "QKPG")](http://seiti.eti.br/blog/fotos?g2_itemId=5795)

Instalado o QPKG, ficou bem simples instalar o Subversion:

#ipkg update #ipkg install svn

[![](http://seiti.eti.br/gallery2/main.php?g2_view=core.DownloadItem&g2_itemId=5800&g2_serialNumber=6&g2_GALLERYSID=5a994d495664f7f37b4075065ced2a4f "SVN com IPKG")](http://seiti.eti.br/blog/fotos?g2_itemId=5799)

E está instalado!

### Repos

Instalado o Subversion, criei um diretória para conter o repositório que guardará meus dados. Para isto basta criar um *Network Share*,  que chamei de  **Repos**. Para criar basta entrar na página web do seu NAS e ir em *Administration → Network Share Management*. Por que não direto no shell? É por que os diretórios criados pela interface do NAS ficam disponíveis para o FTP, backup, Web File Manager, ACLs, sem dores de cabeça. Os diretórios criados assim ficam disponíveis como links simbólicos em <tt>/share.</tt>

Criado o diretório, foi só transformá-lo em um repositório SVN:

#svnadmin create /share/Repos

### Daemon

Falta apenas ligar um *daemon* para que o SVN fique ativo a cada reboot. Para que isto funcione, criei um [script autorun.sh](http://wiki.qnap.com/wiki/Autorun.sh) no diretório de configuração do NAS. Este diretório reside na memória flash do danado, então é necessário montá-lo, criar o script, tornar o script executável, desmontá-lo. E foi o que fiz:

# mount -t ext2 /dev/mtdblock5 /tmp/config # vi /tmp/config/autorun.sh

Editei o arquivo com o *Vi*, inserindo o seguinte [conteúdo](http://forum.qnap.com/viewtopic.php?f=124&t=7528):

#!/bin/sh #sym-link /opt to /opt rm -rf /opt ln -sf /share/MD0_DATA/.qpkg/Optware /opt #export PATH export PATH='/bin:/sbin:/usr/bin:/usr/sbin:/usr/bin/X11:/usr/local/sbin/opt/bin:/opt/sbin' #run Optware packages start scripts for optscript in `ls /opt/etc/init.d/S* | grep -v '~' | sort` ${optscript} done

# chmod +x /tmp/config/autorun.sh # umount /tmp/config

Isto faz com que quaisquer scripts que residam em <tt>/opt/etc/init.d/</tt>, e cujo nome comece com **S**, sejam rodados em ordem alfanumérica.

Só faltou criar o script que inicia o daemon do SVN:

#mkdir /opt/etc/init.d #vi /opt/etc/init.d/S01svnserve

Com o seguinte conteúdo:

/opt/bin/svnserve -d -r /share/Repos

Testei em meu laptop com um:

svn list svn://IPdoNAS/

E tudo ok!

### Fechando

O Qnap TS-109 me surpreendeu por sua flexibilidade. Muitos dispositivos por aí rodam com Linux embarcado, mas poucos se preocupam em oferecer ao usuário a possibilidade de extrair mais deste excelente SO, não se diferenciando de produtos que rodam com SO proprietário.

Mas o TS-109 é uma exceção. Só o fato de disponibilizar os pacotes [Optware](http://www.nslu2-linux.org/) através do ipkg já se abrem as portas para inúmeros aplicativos, dentre eles o Subversion.


