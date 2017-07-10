---
layout: post
title: Desligando o automount no Ubuntu
date: '2010-01-05 13:10:04'
tags:
- ubuntu
---


Meu cartão micro SD de 16GB resolveu deixar de funcionar. Embora ele possa ser aberto e eu até consiga listar o primeiro nível de diretórios, não há jeito de abrir arquivos, ou mesmo copiar muitos deles. Sorte que, salvo algumas fotos recentes, quase todos os arquivos eu tenho guardado no HD ou no Google ou no Flickr.

A parte chata é tentar desmontar, no Ubuntu,  o cartão. Como o cartão estava com defeito o gnome travava e era preciso matar uns processos. A fato é que não conseguia desmontar o cartão, que era montado automaticamente. E eu precisava dele desmontado, mas inserido no sistema, para tentar rodar um *dosfsck* ou  uma formatação.

A solução foi desligar o automount do Ubuntu 9.10 – Karmic Koala. Como? Assim:

 gconftool-2 --type bool --set /apps/nautilus/preferences/media_automount false

E pronto! Pena que o cartão não teve jeito. RIP, cartão de 16GB…


