---
layout: post
title: Colemak no Ubuntu 13.04, sem mudar o Caps Lock
date: '2013-09-19 12:44:04'
---


Finalmente, antes tarde do que nunca, decidi aprender a *touch-typing, *ou seja, teclar sem olhar o teclado e usar todos os dedos.

Mas é bem difícil aprender com os vícios que já tenho sobre o teclado qwerty. Memória mecânica é algo difícil de controlar. Por isto decidi aprender também a usar Dvorak, ou mais especificamente [Br Nativo](http://pt.wikipedia.org/wiki/BR-Nativo "br nativo"), ou Dvorak para os brasileiros.

![Colemak, e não Dvorak](http://upload.wikimedia.org/wikipedia/commons/thumb/f/f1/KB_US-Colemak_with_AltGr.svg/500px-KB_US-Colemak_with_AltGr.svg.png)Colemak, e não Dvorak

O teclado é bem diferente, mas decidido a aprender, encontrei algumas formas bem legais de treinar:

- [typing.io](http://typing.io "typing.io") – você treina digitando código fonte em diversas linguagens;
- [Z-Type](http://phoboslab.org/ztype/) – jogo online;
- [Massacre Street](http://www.playtowerdefensegames.com/games/1161/play.html) – outro jogo online;
- [typingweb.com](http://pt.typingweb.com/) – um tutor online;
- [klavaro.sourceforge.net](http://klavaro.sourceforge.net/pt/) – um EXCELENTE tutor desktop, disponível para windows, ubuntu etc.

Mas após atingir cerca de 20 palavras por minuto, desisti do Br Nativo por alguns motivos. Primeiro ele se adequa apenas ao layout brasileiro de teclado, o ABNT2, impossibilitando, ou dificultando bastante, o acesso a um maior leque de opções em teclados – principalmente os teclados mecânicos. Segundo, ele se presta a digitar rapidamente textos, mas para digitar código fonte me pareceu mais complicado.

Existe um Dvorak para programadores, mas acaba restando ainda o primeiro problema. Bom, como eu também digito bastante em inglês, não é imprescindível ter um teclado otimizado para a freqüência das letras no idioma português. Foi quando descobri o Colemak.

O [Colemak](http://wikipedia.org/wiki/Colemak "Colemak"), criado por Shai Coleman é um teclado que possibilita o digitador a manter as mãos sobre a **home row **– a fileira central de teclas – ao digitar em inglês.

Decidido a aprender Colemak, fui configurar no Ubuntu o tal do layout. Mas eu também estou me acostumando com outra alteração: substituir o Caps Lock pelo Control. Infelizmente no Colemak o Caps Lock é remapeado para atuar como Backspace. E no Ubuntu acabou que o Caps Lock atua como Control **e** Backspace. Bem estranho!

Bom, o jeito foi alterar alguns arquivos, para deixar o caps lock do jeito que era.  
 Primeiro incluir o bloco no arquivo <span style="color: #888888;">/usr/share/X11/xkb/rules/evdev.xml</span>:

    <variant>
        <configItem>
            <name>colemak2</name>    
            <description>English (Colemak caps no remap)</description>
        </configItem>
    </variant>

E depois incluir o bloco no arquivo /usr/share/X11/xkb/symbols/us:

    // Colemak symbols for xkb on X.Org Server 7.x
    // 2006-01-01 Shai Coleman, http://colemak.com/ . Public domain.
    // edited by seiti to not remap caps lock
    partial alphanumeric_keys
    xkb_symbols "colemak2" {
        //include "us"
        name[Group1]= "English (Colemak caps not remapped)";

        // Alphanumeric section
        key <TLDE> { [   grave,   asciitilde, dead_tilde,  asciitilde ] };
        key <AE01> { [  1,  exclam, exclamdown, onesuperior ] };
        key <AE02> { [  2, at,  masculine, twosuperior ] };
        key <AE03> { [  3,   numbersign,ordfeminine,    threesuperior ] };
        key <AE04> { [  4,  dollar,  cent,    sterling ] };
        key <AE05> { [  5, percent,   EuroSign,    yen ] };
        key <AE06> { [  6,  asciicircum,    hstroke,Hstroke ] };
        key <AE07> { [  7,    ampersand,   eth,    ETH ] };
        key <AE08> { [  8,asterisk, thorn,  THORN ] };
        key <AE09> { [  9,    parenleft,  leftsinglequotemark,  leftdoublequotemark ] };
        key <AE10> { [  0,   parenright, rightsinglequotemark,  rightdoublequotemark ] };
        key <AE11> { [   minus,   underscore,endash, emdash ] };
        key <AE12> { [   equal,    plus,   multiply,    division ] };

        key <AD01> { [  q,  Q, adiaeresis,  Adiaeresis ] };
        key <AD02> { [  w,  W, aring,  Aring ] };
        key <AD03> { [  f,  F,atilde, Atilde ] };
        key <AD04> { [  p,  P,oslash,    Ooblique ] };
        key <AD05> { [  g,  G,dead_ogonek,  asciitilde ] };
        key <AD06> { [  j,  J,    dstroke,Dstroke ] };
        key <AD07> { [  l,  L,    lstroke,Lstroke ] };
        key <AD08> { [  u,  U,uacute, Uacute ] };
        key <AD09> { [  y,  Y, udiaeresis,  Udiaeresis ] };
        key <AD10> { [    semicolon,   colon, odiaeresis,  Odiaeresis ] };
        key <AD11> { [  bracketleft,    braceleft,   guillemotleft,   0x1002039 ] };
        key <AD12> { [ bracketright,   braceright,  guillemotright,   0x100203a ] };
        key <BKSL> { [    backslash,bar, asciitilde,  asciitilde ] };

        key <AC01> { [  a,  A,aacute, Aacute ] };
        key <AC02> { [  r,  R, dead_grave,  asciitilde ] };
        key <AC03> { [  s,  S,ssharp,  asciitilde ] };
        key <AC04> { [  t,  T, dead_acute, dead_doubleacute ] };
        key <AC05> { [  d,  D,  dead_diaeresis,  asciitilde ] };
        key <AC06> { [  h,  H, dead_caron,  asciitilde ] };
        key <AC07> { [  n,  N,ntilde, Ntilde ] };
        key <AC08> { [  e,  E,eacute, Eacute ] };
        key <AC09> { [  i,  I,iacute, Iacute ] };
        key <AC10> { [  o,  O,oacute, Oacute ] };
        key <AC11> { [   apostrophe,quotedbl,otilde, Otilde ] };

        key <AB01> { [  z,  Z,    ae,AE ] };
        key <AB02> { [  x,  X, dead_circumflex,  asciitilde ] };
        key <AB03> { [  c,  C,   ccedilla,    Ccedilla ] };
        key <AB04> { [  v,  V,    oe,OE ] };
        key <AB05> { [  b,  B, dead_breve,  asciitilde ] };
        key <AB06> { [  k,  K,  dead_abovering,  asciitilde ] };
        key <AB07> { [  m,  M,dead_macron,  asciitilde ] };
        key <AB08> { [   comma,    less,    dead_cedilla,  asciitilde ] };
        key <AB09> { [  period, greater,   dead_abovedot,  asciitilde ] };
        key <AB10> { [   slash,question,    questiondown,  asciitilde ] };

        key <LSGT> { [   minus,   underscore,endash, emdash ] };
        key <SPCE> { [   space,   space, space,nobreakspace ] };

        include "level3(ralt_switch)"
    };

Uma opção contendo a descrição **English (Colemak caps not remapped)** estará diponível para seleção. Enjoy!


