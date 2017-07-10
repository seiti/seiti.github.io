---
layout: post
title: MPlayer e Compiz Fusion no Ubuntu
date: '2007-12-20 21:23:19'
tags:
- mplayer
- ubuntu
---


Caso você use, como eu, o **Ubuntu** em seu computador e tenha habilitado o *Compiz Fusion* (no menu: Aparência->Efeitos Visuais) poderá notar que o mplayer não roda como deveria.

Ocorre um efeito de cintilamento, ou *flickering*, principalmente quando a janela do mplayer fica logo acima de alguma outra janela. Outro problema ocorre ao arrastarmos a janela do mplayer: a janela vai, mas o vídeo **fica**.

Para solucionar isto, basta clicar com o botão direito do mouse na janela do mplayer e entrar n configuração de preferências. Na aba de vídeo mude o driver para o **x11**.

O problema é que agora, ao ampliarmos a janela, o vídeo permanece do mesmo tamanho, não acompanhando o tamanho da janela. É preciso habilitar o *zoom*. Para isto abra um terminal de linha de comando (ou então apenas pressione <kbd class="keys">Alt</kbd> + <kbd class="keys">F2</kbd>) e entre com o comando:

echo "zoom=yes" >> ~/.mplayer/config

Pronto! Isto é apenas outra maneira de incluir a linha *zoom=yes* no arquivo <tt>~/.mplayer/config</tt>. Se quiser utilize um editor de textos.


