---
layout: post
title: Problemas com o Hibernate
date: '2007-12-16 22:00:00'
tags:
- hibernate
- ubuntu
---


Ao testar a opção de **hibernar**, o sistema apenas tentou gravar as informaçõe da **RAM** na partição *swap*. Tentou e não conseguiu, pois eu estava sem swap. Fui verificar e realmente o swap acusava zero de espaço livre.

Fui ver o <tt>/etc/fstab</tt> e parecia que estava ok. Usando o *Gnome Partition Editor* dava pra ligar o swap (<tt>swapon</tt>), mas não usando o terminal, através do comando <tt>swapon -s</tt>.

O caso é que a entrada da partição swap no fstab estava errada. O **UUID** estava com um valor diferente do indicado pelo comando <tt>vol_id</tt>.

Através de uma busca no google encontrei isto: [https://bugs.launchpad.net/ubuntu/+bug/105490](https://bugs.launchpad.net/ubuntu/+bug/105490)

Bom, basicamente é o seguinte. Encontre qual o dispositivo associado à sua partição swap:

sudo fdisk -l

No meu caso é o <tt>/dev/sda7</tt>. Então veja qual o UUID dele executando o seguinte comando em um terminal:

sudo vol_id /dev/sda7

Algo parecido com isto será mostrado:

ID_FS_USAGE=other ID_FS_TYPE=swap ID_FS_VERSION=2 ID_FS_UUID=9c465eac-fb28-4ead-a3dd-8b364da88a4e ID_FS_LABEL= ID_FS_LABEL_SAFE=

Pegue o UUID correto mostrado e coloque nos arquivos <tt>/etc/fstab</tt> e <tt>/etc/initramfs-tools/conf.d/resume</tt>.

<tt>/etc/initramfs-tools/conf.d/resume</tt>:

RESUME=UUID=9c465eac-fb28-4ead-a3dd-8b364da88a4e

<tt>/etc/fstab</tt>:

UUID=9c465eac-fb28-4ead-a3dd-8b364da88a4e none            swap    sw              0       0

Agora execute o comando:

sudo update-initramfs -u

Após um tempinho, o initram é atualizado e tudo funcionará.


