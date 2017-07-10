---
layout: post
title: eeeXubuntu no Asus Eee PC
date: '2008-03-12 21:54:54'
---


![AsusEeePC e Toshiba 14 polegadas 2](../../gallery2/main.php?g2_view=core.DownloadItem&g2_itemId=3182&g2_serialNumber=3)

Adquiri recentemente um [AsusEeePC](../../wiki/AsusEeePC) e apesar do sistema instalado ser razoavelmente bem acabado, o [XandrOS](http://www.xandros.com/), me senti um pouco amarrado, seja pela falta de softwares nos repositórios oficiais, seja pelo KDE (prefiro o estilo Gnome).

Decidi então testar o Xubuntu, que tem o XFCE como *desktop environment*, além de compartilhar com o Ubuntu a vasta gama de softwares contidos em seus repositórios.

Existe um site dedicado àqueles que tem um Eee PC, o [http://www.eeeuser.com](http://www.eeeuser.com/), além de alguns projetos que objetivam modificar distribuições linux para que sirvam perfeitamente no Eee.


## Criando um Live <span class="strikethrough">CD</span> USB flash drive

![live_flash_drive](../../gallery2/main.php?g2_view=core.DownloadItem&g2_itemId=3207&g2_serialNumber=3)  
 Para criar um *bootable USB flash drive* é preciso:

- um USB flash drive, é claro (também chamado de pendrive)
- os arquivos a serem colocados no pendrive
- o **syslinux**, um *bootloader* que opera a partir de um sistema de arquivos FAT (basta instalar o pacote <tt>syslinux</tt>).

Com o pendrive na mão, o primeiro passo é baixar o [eeeXubuntu](http://wiki.eeeuser.com/ubuntu:eeexubuntu:home). Com a ISO em seu disco, monte-o como *loop device*:

sudo mount eeeXubuntu.iso /cdrom/ -o loop

Isto fará com que o conteúdo da ISO fique disponível no diretório <tt>/cdrom</tt>. A alternativa é queimar um CD usando a ISO.

Depois basta entrar no diretório <tt>/cdrom</tt> e executar o *script*<tt>mkusbinstall.sh</tt>:

sudo /cdrom/mkusbinstall.sh --autodetect


## Sistema funcional

Para aqueles que usam Windows, ainda acostumados a caçar *drivers* pela internet afora, o Xandros funcionou com o [VivoZap](../../wiki/VivoZap). Bastou plugar, configurar uma conexão *dialup*, informando o número a ser discado, nome de usuário e senha, e pronto!

Tenha em mãos um pendrive de pelo menos 1GB e siga as instruções. Será necessário marcar o pendrive como um **dispositivo de boot**. Para isto eu utilizei o Gparted.

Durante a criação do Live USB flash drive, surgiram para mim montes de mensagens do tipo:

cp: failed to preserve ownership for `/media/usbdev.Jp7694/install/sbm.bin': Operation not permitted

Mas elas podem ser ignoradas. Agora basta plugar o flash drive no seu Asus Eee PC, ligá-lo e segurar o <kbd>ESC</kbd> até surgir uma tela de escolha de dispositivo de boot. Faça a escolha apropriada e aguarde o Xubuntu carregar!


