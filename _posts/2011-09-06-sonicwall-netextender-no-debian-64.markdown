---
layout: post
title: SonicWall NetExtender no Debian 64
date: '2011-09-06 11:02:12'
---


Ao migrar do Ubuntu 11.04 – que estava dando muita dor de cabeça – para o Debian 64 tive alguns problemas para configurar o NetExtender (trocando dor de cabeça por diversão).

<figure class="wp-caption aligncenter" id="attachment_1256" style="width: 400px;">[![](http://seiti.eti.br/blog/wp-content/uploads/2011/09/esticador_rede.jpg "esticador_rede")](http://seiti.eti.br/blog/wp-content/uploads/2011/09/esticador_rede.jpg)<figcaption class="wp-caption-text">NetExtender</figcaption></figure>Baixei o programa e instalei o tarball. Ao executar o cliente gráfico, <tt>netExtenderGui</tt>, foi apresentado o erro:  
```
<br></br>
There was a problem loading the NetExtender JNI library.<br></br>
Please reinstall NetExtender, and make sure you have a<br></br>
compatible version of Java installed. SonicWALL recommends<br></br>
Sun Java 1.4 or higher.<br></br>```

Bom, estou com o Sun Java 1.6 e ele está configurado corretamente. Olhando no terminal, o erro é um pouco mais específico, mas não ajudou muito:  
```
<br></br>
Could not load libNetExtender.so<br></br>```

Jogando a mensagem no Google encontrei [um post](https://bbs.archlinux.org/viewtopic.php?id=73641) com pessoas com o mesmo problema, que é a arquitetura usada: 64bits.

Sabendo qual o problema fica mais fácil resolver. No diretório <tt>/usr/lib32</tt> crie dois arquivos simbólicos:

sudo ln -s libcrypto.so.0.9.8 libcrypto.so.6 sudo ln -s libssl.so.0.9.8 libssl.so.6

Se não existirem o libssl.so.0.9.8 e o libcrypto.so.0.9.8, instale o pacote **<tt>ia32-libs</tt>**.  
 Agora crie um script para configurar o LD_CONFIG_PATH:

#!/bin/sh export LD_LIBRARY_PATH=/usr/lib32:$LD_LIBRARY_PATH export COMMAND=/home/seiti/devel/netExtenderClient/netExtender $COMMAND "$@"

Basta agora dar permissão de execução e correr pro abraço:  
```
<br></br>
./netExtender.sh -u usuario -p 'senha' -d example.com vpn.example.com:1234<br></br>```


