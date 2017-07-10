---
layout: post
title: Consertando o GRUB
date: '2007-10-10 19:29:55'
tags:
- linux
---


Como sempre ocorre, acabei ficando sem espaço em meu disco rígido. Resolvi então diminuir o espaço dado ao Windows no sistema (qualquer dia eu apago de vez, mas ainda quero jogar GP Legends…) usando o Ubuntu 6.10 LTS Live CD e o **Gparted**.

O melhor a fazer com o Gparted é realizar uma ação por vez. Diminui a partição em 10GB do Windows e criei uma nova no sistema de arquivos <tt>ext3</tt> com o espaço criado. **Reboot!** Ops…

O sistema deixou de subir, mostrando uma mensagem de erro do **GRUB** bem elucidativa: <tt>ERROR</tt>

O fato é que com a movimentação nas partições, os números que as identificam também mudaram. Eu precisava então fazer algumas coisas:

1. descobrir a nova numeração;
2. atualizar o GRUB na MBR;
3. atualizar o arquivo <tt>/boot/grub/menu.lst</tt>.

Solução: usar novamente o Ubuntu Live CD.

Após carregar o sistema do CD, abri um terminal e montei o sistema de arquivos da partição onde se encontrava o Linux, com o seguinte comando:

<div style="font-family: monospace;">sudo mount -o dev /dev/sda5 /media</div>Isto monta a partição raiz do Linux do disco rígido no diretório <tt>/media</tt>. Eu soube que era <tt>/dev/sda5</tt> através do Gparted.

Entrei no diretório <tt>/media</tt> e executei o GRUB, o que abriu seu próprio prompt, :

<div style="font-family: monospace;">$>sudo grubgrub>

</div>Neste prompt procurei então pela nova denominação da partição

<div style="font-family: monospace;">grub>find /boot/grub/stage1</div>O que devolveu:

<div style="font-family: monospace;">(hd0,4)</div>Ah ha! Agora é so consertar o GRUB, configurando corretamente em que partição se encontram seus binários e arquivos de configuração:

<div style="font-family: monospace;">grub>root (hd0,4)  
 grub>setup (hd0)  
 grub>quit</div>Agora o sistema irá ligar e deixar de emitir o erro do GRUB, MAS…. Ainda falta atualizar o arquivo de listagem do boot. Executei então o comando:

<div style="font-family: monospace;">$>sudo gedit /media/boot/grub/menu.lst</div>E troquei todas as instâncias em que estavam escritas **(hd0,6)** por **(hd0,4)**, que é a nova numeração da partição.

E agora que consegui entrar no Ubuntu vou atualizá-lo para o *Feisty Fawn*! =)

Nota: o comando para saber o UUID de uma determinada partição é <tt>vol_id <device></device></tt>.


