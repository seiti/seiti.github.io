---
layout: post
title: Laptop + Debian GNU/Linux
date: '2005-02-26 00:00:00'
tags:
- debian
- linux
- notebook
---


<div style="font-style: italic; float: right; font-size: 90%; color: #555555; text-align: right; width: 220px;">“Os usuários do Linux não apenas gostam de seus sistemas-  
 eles estão preparados para batalharem por eles,  
 consertá-los e torná-los melhores, mais rápidos e seguros  
 do que um computador com Windows jamais sonhou em ser.”  
 — Nemeth, Snyder e Hein – Manual Completo do Linux</div>![debian laptop](../../wiki/images/laptop.jpg "Meio surrado, mas em bom estado")

***Nota**: as informações abaixo se referem ao *Debian Sarge*. Mudei recentemente (out/2006) o SO para o *[Ubuntu Dapper (6.06)](../../wiki/UbuntuLaptop)* e tudo funcionou corretamente após instalado (bom, menos a cedilha…). Placa Wi-FI PCMCIA, Ethernet PCMCIA, som, medidor de bateria… Recomendo para todos que desejam uma primeira experiência com o Linux sem dores de cabeça. Sendo assim este texto está em sua maior parte obsoleto.*

Como eu me mudei para um lugar um tanto longe de minha casa, e precisava de um micro, acabei optando pelo conforto e conveniência de um laptop (ou notebook). Pesquisando alguns preços, acabei decidindo pela compra de um Toshiba Satellite 1000-S157 usado, cuja configuração pode ser conferida logo abaixo.

Vendo que não conseguiria jogar (no máximo um Starcraft) devido ao fraco desempenho em 3D, e decidido em instalar um sistema Linux, acabei por descartar completamente o Windows como opção até para um eventual sistema dual-boot.

Quebrando um pouco a cabeça para configurar e instalar certas coisas, criei esta página para relatar minhas experiências neste processo. Tenha em mente que isto deu certo para mim. Não quer dizer que dará certo para você. Mas quem sabe não seja útil para alguém. =)

Note que para entender os processos descritos nesta página é necessário um pouco de conhecimento sobre os sistemas GNU/Linux. Um ótimo livro para isto é o *Manual Completo do Linux – Guia do Administrador*, de Nemeth, Snyder e Hein. A página oficial do livro é [www.admin.com](http://www.admin.com/) (em inglês). A versão que eu tenho é a traduzida, editada pela Pearson Education/Makron Books.

[![Tuxmobil](http://tuxmobil.org/pics/tuxmobil_sticker.png "Tuxmobil Listed!")](http://tuxmobil.org/)


## descrição

**modelo/n.** Toshiba Satellite 1000-S157  
**processador** Mobile Intel® Celeron® 1.06GHz (núcleo do PIII)  
**memória/max.** 256MB/512MB  
**hdd** 15GB  
**monitor** 14.1 TFT 102468  
**controladora grÃ¡fica** Intel 830MG  
**memÃ³ria de vÃ­deo** 8MB (UMA)  
**som** Crystal CS4299-A Codec Chip  
**pc card (PCMCIA)**[TypeIIx2](../../wiki/TypeIIx2/edit "Create this page") ou [TypeIIIx1](../../wiki/TypeIIIx1/edit "Create this page")  
**usb** 3 portas  
**modem** V.90/56K integrado


## instalaÃ§Ã£o do sistema Debian GNU/Linux

A distribuiÃ§Ã£o de Linux que escolhi foi o Debian Sarge, devido Ã  grande quantidade de pacotes disponÃ­veis e Ã  ampla literatura existente para consulta na internet. E tambÃ©m por simpatizar com o conceito do projeto Debian, de ser um sistema totalmente produzido por voluntÃ¡rios de todo o mundo.

O Ãºnico cuidado na instalaÃ§Ã£o, relativo ao funcionamento do X system, Ã© utilizar o driver de vÃ­deo do Intel i810, pois nÃ£o existe uma especÃ­fica ao 830MG do laptop.

Para modificar qual tipo de distribuiÃ§Ã£o Debian vocÃª quer apÃ³s a instalaÃ§Ã£o, basta modificar o arquivo <tt>/etc/apt/apt.conf</tt> colocando/editando a seguinte linha:

<div class="code">APT::Default-Release "testing";

</div>E para instalar qualquer pacote diretamente dos servidores Debian, basta dar o comando:

<div class="code" style="font-family: monospace;"><span class="re3"># apt-get -t distribution install package  
</span></div>  
 Onde distribution pode ser *stable*, *testing* ou *unstable* e *package* Ã© o nome do pacote a ser instalado. Veja o manual do <tt>apt</tt> para mais informaÃ§Ãµes.

Note que o meu kernel Ã© o 2.6, compilado a fim de poder decidir quais mÃ³dulos incluir.


## compilando um kernel otimizado

Para otimizar o desempenho de minha mÃ¡quina, assim como finalmente aprender a configurar e compilar um kernel Linux, decidi por a mÃ£o na massa. O fato Ã© que o processo foi bem mais fÃ¡cil do que eu esperava, principalmente por causa das ferramentas do pacote kernel-package.

E posso dizer que o trabalho todo compensa! Tomei um susto ao me deparar com diferenÃ§a no desempenho antes e depois de compilar o kernel. Eu nÃ£o sei quantificar esta diferenÃ§a, mas ela foi claramente perceptÃ­vel em qualquer uso que eu fiz do laptop. Melhor e mais barato que um upgrade de hardware. Deu vontade atÃ© de compilar todos meus programas, ao invÃ©s de baixar os pacotes prÃ©-compilados. Mas fiquei quieto num canto atÃ© esta vontade passar. =)

As instruÃ§Ãµes para se compilar um kernel no Debian podem ser vistas na seguinte pÃ¡gina: [newbiedoc.sourceforge.net](http://newbiedoc.sourceforge.net/system/kernel-pkg.html)


## HDparm

Primeiramente, vamos melhorar a velocidade do HD. Mas como isto Ã© possÃ­vel? Bom, o Debian, por padrÃ£o, configura seus dispositivos da maneira mais confiÃ¡vel possÃ­vel, minimizando possibilidade de problemas. Ou seja, o HD Ã© configurado para operar sem o DMA ativado: lerdeza na certa.

Vamos entÃ£o utilizar o HDparm para melhorar o desempenho do HD. Para ativar o DMA basta inserir o seguinte bloco de texto no arquivo <tt>/etc/hdparm.conf</tt>:

<div class="code">command_line { hdparm -c3 -m16 -d1 /dev/hda }

</div>E pronto! Ao reinicializar sua mÃ¡quina, tudo estarÃ¡ mais ligeiro.

Para ver o quanto seu HD ficou mais rÃ¡pido, antes de modificar o arquivo supracitado, dÃª algumas vezes o comando

<div class="code" style="font-family: monospace;"><span class="re3"># hdparm -t /dev/hda  
</span></div>  
 Agora dÃª o comando

<div class="code" style="font-family: monospace;"><span class="re3"># hdparm -c3 -m16 -d1 /dev/hda  
</span></div>  
 , e logo apÃ³s dÃª o comando

<div class="code" style="font-family: monospace;"><span class="re3"># hdparm -t /dev/hda  
</span></div>  
 novamente. Viu como melhorou?


## [WindowMaker](../../wiki/WindowMaker)

Como gerenciador de janelas, ou window manager, eu costumo utilizar o [WindowMaker](../../wiki/WindowMaker). Antes era por causa do desempenho, agora Ã© por questÃ£o de gosto mesmo.

Para instalar o pacote Debian mais recente para sua configuraÃ§Ã£o basta dar o comando:

<div class="code" style="font-family: monospace;"><span class="re3"># apt-get install wmaker  
</span></div>
## Giro (VÃ©sper)

Finalmente consegui configurar o Giro para funcionar no meu laptop. Para quem nÃ£o sabe, Giro Ã© o serviÃ§o de banda larga da VÃ©sper, em SÃ£o Paulo. A diferenÃ§a para outros serviÃ§os de banda larga Ã© que este utiliza um modem com tecnologia CDMA (G3) e interface USB. Ou seja, dor de cabeÃ§a (ou diversÃ£o, dependendo do usuÃ¡rio) para quem usa Linux. A marca e modelo do modem Ã© LG LST-D400.

Antes de mais nada, configure o seu kernel para possuir os seguintes mÃ³dulos:

<div class="code">alias char-major-108 ppp_generic alias /dev/ppp ppp_generic alias tty-ldisc-3 ppp_async alias tty-ldisc-14 ppp_synctty alias ppp-compress-21 bsd_comp alias ppp-compress-24 ppp_deflate alias ppp-compress-26 ppp_deflate

</div>Os itens da lista acima foi tirado do meu <tt>modules.conf</tt>. Aproveite e coloque as linhas acima no <tt>modules.conf</tt>, caso apÃ³s ter incluÃ­do os mÃ³dulos via configuraÃ§Ã£o do kernel eles nÃ£o tenham surgido.

Depois crie/edite os seguintes arquivos: <tt>/etc/ppp/peers/giro</tt> e <tt>/etc/chatscripts/giro</tt>. Eis o arquivo <tt>/etc/ppp/peers/giro</tt>:

<div class="code">/dev/ttyACM0 noauth connect "/usr/sbin/chat -V -v -f /etc/chatscripts/giro" defaultroute lock usepeerdns debug user "kamikaze@giro.com.br" noipdefault nobsdcomp

</div>E eis o <tt>/etc/chatscripts/giro</tt>:

<div class="code">TIMEOUT 10 ABORT "BUSY" ABORT "NO ANSWER" ABORT "NO CARRIER" ABORT "NO DIAL TONE" ABORT "RING\r\n\r\nRING\r" '' AT+CRM=1 TIMEOUT 60 OK ATD\#777 CONN

</div>SÃ³ falta definir sua senha no arquivo <tt>/etc/chap-secrets</tt>. Basta inserir no arquivo a seguinte linha:

<div class="code">"usuario@giro.com.br" * "suasenha"

</div>Ã claro que vocÃª deve utilizar suas prÃ³prias informaÃ§Ãµes.

Agora basta dar o seguinte comando:

<div class="code" style="font-family: monospace;">$ sudo pon giro</div>  
 E pronto! VocÃª estarÃ¡ conectado! Caso isto nÃ£o ocorra, dÃª um tail no arquivo <tt>/var/log/messages</tt> para saber qual o problema.


## placa de rede wireless

![debian laptop](../../wiki/images/wificard.jpg "Agora posso ver emails atÃ© no banheiro!") Comprei uma plaquinha PCMCIA para poder acessar o Speedy Wi-Fi, cuja marca e modelo Ã© TRENDnet tew-226pc.

Embora eu ainda nÃ£o tenha acessado os hotspots Speedy Wi-Fi, consegui estabeler com sucesso uma conexÃ£o caseira usando o roteador D-Link DI-514, um roteador com 4 portas RJ45 e access point padrÃ£o 802.11b (11Mbps) para acesso sem-fio. Assim, basta eu ligar o laptop que jÃ¡ estou ligado Ã  internet.

Seguem os passos executador por mim, recolhidos de fontes na internet. (a maior parte das informaÃ§Ãµes foi obtida em [http://tiefighter.et.tudelft.nl/~arthur/wpc54g/](http://tiefighter.et.tudelft.nl/%7Earthur/wpc54g/))

Primeiro identifiquei qual o driver certo para o funcionamento da placa pcmcia em sistemas Linux. Meus dados sÃ£o:  
 * modelo: TRENDnet tew-226pc  
 * nÃºcleo: Realtek RTL8180L  
 * driver: driver correspondente ao nÃºcleo RTL8180L, para Windows XP(v1.73), atravÃ©s do ndiswrapper

ApÃ³s baixar o driver e descompactÃ¡-lo em local conveniente, editei o arquivo <tt>/etc/apt/sources.list</tt> adicicionado o seguinte endereÃ§o:

<div class="code">deb http://rigtorp.se/debian/ unstable/

</div>ApÃ³s atualizar o <tt>apt</tt> (com o comando <tt>apt-get update</tt>), instalei o restante dos pacotes necessÃ¡rios:

<div class="code" style="font-family: monospace;"><span class="re3"># apt-get install ndiswrapper ndiswrapper-<span class="kw3">source</span>  
</span></div>  
 Abri o pacote com o cÃ³digo fonte do mÃ³dulo, e entrei no mesmo para criar um pacote debian (adapte KSRC para apontar para o cÃ³digo-fonte de seu kernel)(note que rules Ã© um executÃ¡vel que se encontra dentro do diretÃ³rio criado):

<div class="code" style="font-family: monospace;"><span class="re3"># debian/rules binary-modules <span class="re2">KSRC=</span>/lib/modules/`uname -r`/build  
</span></div>Instale o pacote debian criado:

<div class="code" style="font-family: monospace;"><span class="re3"># dpkg -i ../ndiswrapper-modules-*.deb  
</span></div>  
 Agora vÃ¡ para o diretÃ³rio com o driver de sua placa e carregue o mÃ³dulo com o driver:

<div class="code" style="font-family: monospace;"><span class="re3"># ndiswrapper -i NET8180.inf # update-modules # modprobe ndiswrapper  
</span></div>  
 Para que o mÃ³dulo seja sempre carregado em tempo de boot:

<div class="code" style="font-family: monospace;"># <span class="kw3">echo</span> ndiswrapper <span class="st0">“”</span>>><span class="st0">“”</span> /etc/modules</div>  
 Agora instale o pacote dhcpcd:

<div class="code" style="font-family: monospace;"><span class="re3"># apt-get install dhcpcd  
</span></div>  
 Acrescentei estas linhas ao arquivo <tt>/etc/dhcpc/config</tt>:

<div class="code">wlan0) # Uncomment this to allow dhcpcd to set the DNS servers in /etc/resolv.conf # If you are using resolvconf then you can leave this commented out. #SET_DNS='yes' # Add other options here, see man 8 dhcpcd-bin for details. OPTIONS='' ;;

</div>Embora eu ache que nÃ£o faÃ§a diferenÃ§a =).

![debian laptop](../../wiki/images/di514.jpg "roteador poadrÃ£o IEEE 802.11b") Para que tudo se automatize, e as configuraÃ§Ãµes entrem em vigor ao inserir a placa pcmcia, instale os pacotes **waproamd** e **ifplugd**:

<div class="code" style="font-family: monospace;"><span class="re3"># apt-get install waproamd ifplugd  
</span></div>  
 Edite o arquivo <tt>/etc/default/ifplugd</tt>, configurando HOTPLUG_INTERFACES para “all” e edite <tt>/etc/default/waproamd</tt> configurando HOTPLUG_INTERFACES para “all”. Por fim edite o arquivo <tt>/etc/network/interfaces</tt> e inclua:

<div class="code">iface wlan0 inet dhcp

</div>E reinicie os seguintes serviÃ§os:

<div class="code" style="font-family: monospace;"><span class="re3"># /etc/init.d/ifplugd restart # /etc/init.d/waproamd restart  
</span></div>  
 Cheque se tudo estÃ¡ funcionando atravÃ©s dos comandos <tt>iwlist</tt> e <tt>iwconfig</tt>. Cheque as pÃ¡ginas de manual para saber como utilizar estas ferramentas (inclusas no pacote **wireless-tools**).


## cÃ¢mera digital

Comprei uma cÃ¢mera digital, uma Canon [PowerShot](../../wiki/PowerShot/edit "Create this page") A400. Esta cÃ¢mera Ã© muito boa, considerando a qualidade das imagens e funcionalidades. Mas existe um porÃ©m: nÃ£o consegui acessar seu conteÃºdo montando sua memÃ³ria como um dispositivo de armazenamento USB padrÃ£o.

O problema Ã© que as cÃ¢meras da Canon nÃ£o utilizam o protocolo “USB Mass Storage”. Sendo assim, Ã© necessÃ¡rio a instalaÃ§Ã£o dos seguintes pacotes Debian: **libgphoto2-2**, **gphoto2** e **gtkam** (opcional).

ApÃ³s instalados, Ã© sÃ³ digitar a seguinte linha de comando (note que Ã© necessÃ¡rio estar como superusuÃ¡rio, ou usar sudo) :

<div class="code" style="font-family: monospace;"><span class="re3"># gphoto2 –auto-detect  
</span></div>  
 Assim Ã© possÃ­vel observar se a cÃ¢mera foi detectada corretamente. Para ter acesso Ã s imagens em sua memÃ³ria, basta entrar com:

<div class="code" style="font-family: monospace;"><span class="re3"># gphoto2 –list-files  
</span></div>  
 O resto dos comando veja nas pÃ¡ginas de manual do **gphoto2**, ou utilize o **gtkam**, um ui para o gphoto2.


## USB Mass Storage Device

Comprei um HD de 200GB para armazenar alguns tÃ­tulos de MP3 e coloquei-o em um dispositivo USB para acesso externo ao HD, mas tive problemas em montÃ¡-lo utilizando o comando:

<div class="code" style="font-family: monospace;">$ mount /media/usb</div>  
 Descobri que, devido ao modo como particionei o HD, o mesmo nÃ£o constava como <tt>/dev/sda1</tt>, como acontece costumeiramente com pendrives e similares, e sim em <tt>/dev/sda5</tt>. Descobri isto atravÃ©s do comando:

<div class="code" style="font-family: monospace;"><span class="re3"># fdisk -l  
</span></div>  
 Assim, bastou acrescentar a seguinte linha no arquivo <tt>/ets/fstab</tt>:

<div class="code">/dev/sda5 /media/ehdd auto rw,user,noauto 0 0

</div>E, obviamente, criar o diretÃ³rio /media/ehdd:

<div class="code" style="font-family: monospace;"><span class="re3"># mkdir /media/ehdd  
</span></div>  
 Assim, para montar o HD externo, basta executar:

<div class="code" style="font-family: monospace;">$ mount /media/ehdd</div>
## Unison

Como possuo contas em vÃ¡rios micros (casa, estÃ¡gio, faculdade), com arquivos interrelacionados espalhados por todos eles, Ã© muito difÃ­cil saber qual arquivo estÃ¡ onde e em que mÃ¡quina estÃ¡ o arquivo mais recententemente editado. Para solucionar isto procurei por algum sofware que pudesse sincronizar meus arquivos, inclusive entre sistemas Windows e Linux. Encontrei o Unison

Muito prÃ¡tico. Para que funcione tambÃ©m no Windows (que nÃ£o possui SSH, necessÃ¡rio ao Unison), instale o [OpenSSH](../../wiki/OpenSSH/edit "Create this page"). Posso dizer que funciona bem, pois sincronizei quase 1GB de fotos que tirei em minha cÃ¢mera digital entre o o meu desktop (Windows) e meu laptop (Debian Linux). E para visualizar estas fotos utilizo o gtksee.


## Xine e MPlayer

Para instalar o MPlayer siga as instruÃ§Ãµes da pÃ¡gina [http://debian.video.free.fr/](http://debian.video.free.fr/), que hospeda pacotes nÃ£o oficiais (e portanto mais recentes) do MPlayer.

Ou seja, caso sua distribuiÃ§Ã£o Debian seja Sarge (testing), coloque a seguinte linha no arquivo /etc/apt/sources.list:

<div class="code">deb ftp://ftp.nerim.net/debian-marillat/ testing main

</div>Agora instale o pacote mplayer-686 e todos os pacotes recomendados e sugeridos por ele.

O Xine eu nÃ£o me lembro, mas devo ter instalado dos repositÃ³rios oficiais mesmo, com o comando:

<div class="code" style="font-family: monospace;"><span class="re3"># apt-get -t unstable install xine-lib xine-ui  
</span></div>
## [TeX](../../wiki/TeX/edit "Create this page")/[LaTeX](../../wiki/LaTeX/edit "Create this page")

Para produzir textos na faculdade, costumo utilizar o [LaTeX](../../wiki/LaTeX/edit "Create this page"). Caso vocÃª se interesse, existe um Ã³timo tutorial para editar textos usando esta ferramenta, o The Not So Short Introduction to [LaTex](../../wiki/LaTex/edit "Create this page") (arquivo PDF).

Para ter um ambiente [LaTeX](../../wiki/LaTeX/edit "Create this page") em sua mÃ¡quina, basta instalar os seguintes pacotes:

<div class="code" style="font-family: monospace;"><span class="re3"># apt-get install tetex-base tetex-bin tetex-extra tetex-doc lacheck  
</span></div>
## Squeak

Squeak se trata de um arcabouÃ§o (ou framework) para a linguagem [SmallTalk](../../wiki/SmallTalk/edit "Create this page"), considerada por muitos a melhor linguagem jÃ¡ escrita.

Infelizmente o Squeak, apesar de ser um projeto Open Source, nÃ£o possui um pacote oficial do Debian. Assim foi preciso modificar algumas coisinhas antes de instalÃ¡-lo em meu sistema.

Assim foi necessÃ¡rio inserir no arquivo de fontes do APT os repositÃ³rios para os pacotes prÃ©-compilados do Squeak. O arquivo a ser modificado Ã© o <tt>/etc/apt/sources.list</tt>, e deve-se colocar as seguintes linhas:

<div class="code">deb http://box2.squeakfoundation.org/files/debian/ unstable main deb-src http://box2.squeakfoundation.org/files/debian/ unstable main

</div>Depois devemos atualizar o banco de dados do APT e instalar o Squeak com os seguintes comandos:

<div class="code" style="font-family: monospace;">$ sudo apt-get update  
 $ sudo apt-get install squeak squeak-image3<span class="nu0">.6</span></div>  
 E pronto, basta digitar squeak na linha de comando e tudo funcionarÃ¡ bem.

Fonte: [http://minnow.cc.gatech.edu/squeak/3616](http://minnow.cc.gatech.edu/squeak/3616)


