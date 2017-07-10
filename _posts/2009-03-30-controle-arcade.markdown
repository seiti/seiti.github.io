---
layout: post
title: Controle Arcade
date: '2009-03-30 17:28:06'
---


<div style="font-style: italic; float: right; font-size: 90%; color: #555; text-align: right;">” The three most dangerous things in the world are:  
 a programmer with a soldering iron,  
 a hardware type with a program patch and  
 a user with an idea. ”  
 — The Wizardry Compiled – Rick Cook</div>[![Mongagua__jan_2004__045](http://farm3.static.flickr.com/2442/4018187322_21bf6e95e2.jpg)](http://www.flickr.com/photos/seiti/4018187322/ "Mongagua__jan_2004__045 by Seiti Yamashiro, on Flickr")

Nesta seção estão projetos relacionados ao meu famigerado controle arcade. Para quem não sabe, arcade é o termo usado para os “fliperamas”, como é usado amplamente aqui no Brasil (pelo menos em São Paulo =P).

> ***Update**: estou com um [novo controle](../controle-arcade-1p)! Visite a página!  
> *

[![Controle Arcade](http://farm4.static.flickr.com/3334/3565743324_90b2ba0418.jpg)](http://www.flickr.com/photos/seiti/3565743324/ "Controle Arcade by Seiti Yamashiro, on Flickr")

As motivações de se construir um controle arcade são:

- economizar dinheiro em fichas;
- poder jogar a vontade em sua própria residência;
- pretexto para juntar os amigos;
- e finalmente, as casas de fliper estão se extinguindo, sobrando as máquinas dos shoppings, que geralmente cobram o olho da cara para jogar em máquinas de jogos já desatualizados e com controles quebrados.

As informações contidas aqui, assim como as de todo o site, são de uso pessoal e divulgadas apenas para o aprendizado e exercício de linguagens relacionadas à web.

Portanto, eu garanto que não sou nenhum perito em eletrônica, marcenaria ou coisa que o valha. Longe disso, tive que aprender do jeito mais divertido: fazendo. Mas tive a ajuda inestimável de dois companheiros: o computador e o Google.


## Construção

Primeiramente é necessário criar um layout à sua conveniência. Como quase sempre jogo jogos de luta, decidi por 6 botões de ação para cada jogador, além de dois botões auxiliares para funções tais como inserir ficha e start.

[![Controle Arcade](http://farm4.static.flickr.com/3393/3564930055_be1f9b6c7e.jpg)](http://www.flickr.com/photos/seiti/3564930055/ "Controle Arcade by Seiti Yamashiro, on Flickr")

Como pode-se ver, escolhi um desenho bem simples para meu controle. Serve para a maioria dos jogos de luta. Os botões 1P e 2P são os player 1 e player 2. A e B servem para colocar fichas, o resto serve para se divertir.

Depois é hora de desenhar seu projeto. Pode-se usar o [AutoCAD](/wiki/AutoCAD/edit "Create this page"). Mas como eu queria algo simples e não tenho tanta intimidade assim com este software (e nem tenho a baratíssima licença), desenhei com alguns antigos companheiros: lápis, borracha e régua (hoje em dia temos o excelente [Google Sketchup](http://sketchup.google.com "Google Sketchup")).

Logo após, fui comprar as peças, já impaciente em pôr a mão na massa.

Material:

- 2 alavancas
- 20 botões
- 1 placa de acrílico 8mm(o tamanho depende do desenho do teu projeto)
- madeira 15mm(já comprei as tábuas de compensado cortados na medida)
- cola pra madeira
- lixa para madeira
- pregos
- duas dobradiças para armário (para facilitar o acesso ao interior )
- um rolo de contact preto (sobrou bastante, sugiro comprar por metro à granel)
- 8 parafusos franceses (aqueles com cabeça arredondada, presas por meio de porcas)
- uma porrada de fios e cabos
- fitas adesivas e afins

Ferramentas:

- ferro de solda
- furadeira e brocas para madeira
- serras copo (de 1 1/8 para os botões)
- chave de fenda, martelo, etc…

Encontrei os botões e a alavanca na região da Santa Ifigênia/SP, mais precisamente na loja Fratello Games (Rua Sta Efigenia 295, 2º andar). Caso não encontre a loja, ou o site esteja fora do ar (provável…) tente uma busca por “arcade” no Mercado Livre, alguma coisa você deve achar. O resto encontrei no Castorama, Leroy-Merlin, C&C…

Após a aquisição do material peguei uma caixa de papelão que eu tinha em casa e montei todo o controle nele, para testar a ergonomia de meu projeto, tais como separação entre botões, distância deste para a alavanca. Aprovado o desenho, cortemos a madeira.

Desmontei o teclado completamente, sobrando em minhas mãos a placa com circuito e três folhas presas entre si com os contatos para os botões. Agora vêm a parte chata. Obter a matriz que mostra como os contatos se relacionam com os botões. Para esta tarefa recomendo a leitura COMPLETA deste site: [EmuAdvice](../../wiki/EmuAdvice/edit "Create this page").

> Atualização (08/jan/2003)
> 
> Após muitos emails pedindo explicações sobre a leitura da matrix do teclado, reitero que existem muitos exemplos no site da BYOAC. Outra página, para aqueles que gostam de figuras nos textos, é este (encontrado no BYOAC). Um programa útil você pode encontrar aqui. Se mesmo assim está difícil tente este tópico no fórum da revista PCs. Qualquer dúvida me mande um email!
> 
> Atualização (26/ago/2004)
> 
> Pouco contente com o resultado do keyboard hack, devido aos problemas de key ghost/blocking [era muito difícil pressionar uma diagonal e mais três teclas simultaneamente, e mais ainda com dois jogadores, se bem que ninguém joga com o Zangief mesmo, hehe], além de umas soldas frias no PCB do mesmo [ainda aprendo a soldar…], decidi atualizar o miolo do meu controle.
> 
> Assim, retirei a parte sobre o “keyboard-hacking”, agora que meu projeto utiliza o [I-PAC](http://www.ultimarc.com/ipac1.html), substituindo por informações para modularizar o controle, tornando mais simples a adaptação para diversos tipos de consoles de vodeogames. Caso queira informações sobre como usar um teclado velho, visite o ótimo site da [BYOAC](http://arcadecontrols.com/) (Build Your Own Arcade Control). Agora, vamos à construção do monstro.

Após comprada e cortada a madeira necessária, montei a caixa para meu controle passando cola em toda a extensão das bordas das tábuas e depois pregando (com pregos!) as peças. Feito a caixa, fui para o tampo, no qual seria montado o controle.

[![Controle Arcade](http://farm4.static.flickr.com/3652/3565744580_e6dc200f96.jpg)](http://www.flickr.com/photos/seiti/3565744580/ "Controle Arcade by Seiti Yamashiro, on Flickr")

[![Controle Arcade](http://farm3.static.flickr.com/2426/3564926763_9bd8746b40.jpg)](http://www.flickr.com/photos/seiti/3564926763/ "Controle Arcade by Seiti Yamashiro, on Flickr")

Meu tampo consiste em uma placa de acrílico e uma placa de compensado. Decidi utilizar uma placa de madeira bem fina (4mm) para não ter problemas em colocar a alavanca. Desenhei o layout na placa de madeira, chequei o desenho, chequei de novo, chequei mais uma vez (nunca é demais… ) e então a prendi por meio de fita crepe (muuuuuita fita) à placa de acrílico. Passei a furadeira com a serra copo em todos os pontos marcados. Encapei a caixa e a parte de madeira do tampo com o contact e então prendi o tampo à caixa por meio das dobradiças. Coloquei todos os botões e as duas alavancas.

Para a parte elétrica, eu planejei modularizar o controle. De que maneira? Simplesmentes conectando todas micro-chave em um cabo-manga com fios suficientes, e depois utilizar um conector DB-25 (macho, no caso), como aquelas usadas em impressoras.

O antigo controle pronto para receber o novo recheio. Será adicionado um cabo manga com vinte e seis vias, uma para cada botão e dois pro terra. Cabo este que será ligado à um conector DB25, para que possa ser ligado ao adaptador citado acima.

O cabo usado neste projeto foi um cabo-manga com vinte e seis fios. O problema é que muitas cores são repetidas, assim para saber com qual fio estou lidando, de ponta a ponta, só com o auxílio do multímetro.

O esquema elétrico é bem mais simples que com o uso do PCB do teclado (além de não ter de ficar analisando os famigerados “key-ghosting/key blocking”). Todas as micro-chaves tem conexão com o terra. Assim basta passar o mesmo fio, de liagação com o terra, de micro-chave em micro-chave.

O aspecto não é dos piores… Melhor que a bagunça de antes.

[![Controle Arcade](http://farm3.static.flickr.com/2460/3565744720_53822b6d2e.jpg)](http://www.flickr.com/photos/seiti/3565744720/ "Controle Arcade by Seiti Yamashiro, on Flickr")

[![Controle Arcade](http://farm4.static.flickr.com/3371/3564925465_dd2d96051a.jpg)](http://www.flickr.com/photos/seiti/3564925465/ "Controle Arcade by Seiti Yamashiro, on Flickr")

E o que seriam estes módulos? Uma caixa contendo os cicuitos de gamepads (controles de videogames), ligados de alguma maneira em um conector DB-25 (fêmea, para ligar ao controle). Assim, basta eu comprar dois gamepads de um videogame X, abrí-los, dar uma estudada no que fazer, e criar o módulo. E pronto! Controle arcade para o videogame X.

[![Controle Arcade](http://farm4.static.flickr.com/3392/3564926063_ef8c3921af.jpg)](http://www.flickr.com/photos/seiti/3564926063/ "Controle Arcade by Seiti Yamashiro, on Flickr")


## Módulo DreamCast

Após muito tempo imaginando como seria finalmente jogar Street Fighter III em um controle realmente decente e aprender como jogar DE VERDADE, usando o parrying (que é o que realmente inova neste SF), decidi que já era hora de adaptar dois controles de <span class="missingpage">DreamCast</span> (único console a contar com uma versão deste excelente jogo, pelo menos até a presente data) no meu controle arcade.

Para tanto utilizei dois controles de “segunda linha” comprados no Stand Center, conhecida galeria de material contrabadeando da Avenida Paulista. A marca dos controles é Players.  
 gamepads de DreamCast

[![Controle Arcade](http://farm3.static.flickr.com/2453/3565745184_5bb6e31a77.jpg)](http://www.flickr.com/photos/seiti/3565745184/ "Controle Arcade by Seiti Yamashiro, on Flickr")  
<span class="caption" style="width: 150px;">O da direita não serviu.</span>

Para esta adaptação fora utilizados dois controles como este da esquerda. O da direita mostrou-se inútil para este tipo de serviço, pois seu PCB não possuia um terra único. Isto acabava com meus planos, visto o modo como montei meu controle arcade (todos os botões compartilham um mesmo terra). Por isso, um aviso: fiquem longe dos controles com Turbo e funcionalidades desnecessárias.  
 placa do controle  
[![Controle Arcade](http://farm4.static.flickr.com/3313/3565745260_3ffe493321.jpg)](http://www.flickr.com/photos/seiti/3565745260/ "Controle Arcade by Seiti Yamashiro, on Flickr")  
<span class="caption" style="width: 150px;">O PCB do danado</span>

Observando o PCB do controle, nota-se que os contatos têm uma boa área metálica. Isto facilita bastante o trabalho de soldagem, principalmente para pessoas desastradas como eu =P.  
 botão analógico  
[![Controle Arcade](http://farm4.static.flickr.com/3386/3564927541_1683af045f.jpg)](http://www.flickr.com/photos/seiti/3564927541/ "Controle Arcade by Seiti Yamashiro, on Flickr")  
[![Controle Arcade](http://farm3.static.flickr.com/2426/3564927473_7f80364ff2.jpg)](http://www.flickr.com/photos/seiti/3564927473/ "Controle Arcade by Seiti Yamashiro, on Flickr")  
<span class="caption" style="width: 150px;">O botão analógico</span>

Tive de estudar como trabalhar os botões L e R, pois eles são originalmente analógicos.Por sorte o circuito que produz o efeito analógico é muito simples, consistindo em uma trilha de metal resistivo, funcionando como um potenciômetro bem ordinário. Os botões L e R deslizam seus contatos pela placa, aumentando ou diminuindo a resistência, definindo a “força” do pressionamento.  
 conector do VMU  
[![Controle Arcade](http://farm4.static.flickr.com/3410/3565745554_5b4d6edde3.jpg)](http://www.flickr.com/photos/seiti/3565745554/ "Controle Arcade by Seiti Yamashiro, on Flickr")  
<span class="caption" style="width: 150px;">Vamos nos livrar da parte inútil</span>

Como eu coloco meus módulos em práticas e baratas caixas plásticas para fitas de VHS, tive de me livrar da parte inútil do PCB do controle, de modo a deixá-lo um pouco mais magro e poder entrar na caixa. Esta parte “inútil” se trata dos botões L e R e seus respectivos PCBs.  
 conector do VMU serrado  
[![Controle Arcade](http://farm3.static.flickr.com/2427/3565745802_99c7931187.jpg)](http://www.flickr.com/photos/seiti/3565745802/ "Controle Arcade by Seiti Yamashiro, on Flickr")  
<span class="caption" style="width: 150px;">Diversão com a serra</span>

Mas o miolo do controle continuou muito grande. Parte do tamanho é devido ao conector para os VMUs. Mas precisamos de apenas um VMU por controle (ou nem isso) e existem dois em cada. Então, para deixá-los menores, retirei uma das portas para utilização do VMU de cada um deles, após um pouco de trabalho com a micro-retífica.

Dá para se observar pelas fotos o quanto o controle ficou menor, pronto para ser enfiado em uma caixinha de fita VHS.  
 PCB na caixinha de VHS  
[![Controle Arcade](http://farm4.static.flickr.com/3578/3564928165_52c57988b0.jpg)](http://www.flickr.com/photos/seiti/3564928165/ "Controle Arcade by Seiti Yamashiro, on Flickr")  
<span class="caption" style="width: 150px;">Encaixou-se quase perfeitamente</span>

Após soldado tudo, é só encaixar o PCB do controle de modo que a caixinha plástica consiga ser fechada. Para isso fiz um pequeno furo em cada caixa para que o pino metálico do direcional analógico pudesse ter espaço suficiente.  
 caixinhas de VHS com o PCB  
[![Controle Arcade](http://farm3.static.flickr.com/2472/3564928205_d8f47f23e7.jpg)](http://www.flickr.com/photos/seiti/3564928205/ "Controle Arcade by Seiti Yamashiro, on Flickr")  
<span class="caption" style="width: 150px;">Um controle em cada caixinha</span>

Após todo o trabalho, tive que colar duas caixas de VHS entre si para gerar espaço suficiente para os PCBs dos controles, um PCB em cada caixnha. Além de gordo, o PCB era muito largo, assim, apenas uma caixinha de VHS não dava.  
 marcando qual o controle 1 e o 2.  
[![Controle Arcade](http://farm3.static.flickr.com/2434/3564928283_50f1145192.jpg)](http://www.flickr.com/photos/seiti/3564928283/ "Controle Arcade by Seiti Yamashiro, on Flickr")  
<span class="caption" style="width: 150px;">Marcando qual controle é qual</span>

Como o cabo é muito comprido, foi necessário, para facilitar a conexão, marcar qual conector pertence a qual parte do controle arcade: jogador 1 ou jogador 2. Assim não é necessário ficar retirando o colocando de volta o controle no console, atrasando o hora sagrada da jogatina.  
[![Controle Arcade](http://farm3.static.flickr.com/2459/3565746032_ab85c1384a.jpg)](http://www.flickr.com/photos/seiti/3565746032/ "Controle Arcade by Seiti Yamashiro, on Flickr")  
<span class="caption" style="width: 150px;">Ligando os safados no DC</span>

E finalmente o módulo DC para o controle arcade conectado no DreamCast. E o melhor de tudo, funciona! É o mínimo após todo o trabalho. Agora posso continuar a jogar SFIII do jeito que ele deve ser jogado.  
 ligando o modulo no controle  
[![Controle Arcade](http://farm3.static.flickr.com/2479/3565746202_9fa1364432.jpg)](http://www.flickr.com/photos/seiti/3565746202/ "Controle Arcade by Seiti Yamashiro, on Flickr")  
<span class="caption" style="width: 150px;">Como o módulo é ligado no controle</span>

O módulo DC no controle arcade, através de um conector DB25 (igual os utilizados em impressoras paralelas).


## Módulo Playstation

objetivo: Adaptar o controle para que tenha interface USB.

solução: Abrir dois controles para Playstation e usar seus circuitos. Para usar no PC basta um adaptador [ou dois] do tipo PSXUSB.

problema: O adaptador PlayStationUSB/PC não presta para jogos de luta (e talvez a maioria dos jogos de ação). Ele possui um atraso considerável entre o pressionar do botão e a ação no jogo.  
 modulo PS/PS2  
[![Controle Arcade](http://farm4.static.flickr.com/3386/3565744874_ac05cca4d6.jpg)](http://www.flickr.com/photos/seiti/3565744874/ "Controle Arcade by Seiti Yamashiro, on Flickr")<span class="caption" style="width: 150px;">O módulo PS/PS2</span>

Pouco contente com o resultado do keyboard hack, devido aos problemas de key ghost/blocking [era muito difícil pressionar uma diagonal e mais três teclas simultaneamente, e mais ainda com dois jogadores, se bem que ninguém joga com o Zangief mesmo, hehe], além de umas soldas frias no PCB do mesmo [ainda aprendo a soldar…], decidi atualizar o miolo do meu controle.  
 modulo PS/PS2  
[![Controle Arcade](http://farm4.static.flickr.com/3316/3564926125_d68d266e38.jpg)](http://www.flickr.com/photos/seiti/3564926125/ "Controle Arcade by Seiti Yamashiro, on Flickr")  
<span class="caption" style="width: 150px;">O módulo pronto</span>

Escolhi como novo cérebro joysticks de Playstation da Players [à venda em qualquer camelô especializado em videogame e acessórios] que custaram 10 reais cada [devem ser mais baratos no lugar certo, mas enfim…].

Um pouco de trabalho de solda com o miolo dos controles de Playstation. Cada botão do controle é acionado ao se realizar um curto, fechando o circuito entre o terra e o contato correspondente. Assim eu soldei um fio em cada contato (direcionais e botões de ação) e um no terra, a partir do cabo manga, ligando tudo num conector DB-25.

Eis o módulo criado por mim. Ele é destacável, assim posso criar, a partir de controles de outros videogames, outros adaptadores compatíveis. O controle Arcade pode funcionar em qualquer console, bastando trocar o módulo, que se conecta no controle Arcade por um simples conector DB-25.

[![Controle Arcade](http://farm4.static.flickr.com/3392/3564926063_ef8c3921af.jpg)](http://www.flickr.com/photos/seiti/3564926063/ "Controle Arcade by Seiti Yamashiro, on Flickr")

### Comentários antigos

Os comentários abaixo vieram da página do wiki, que migrei para cá.

<div style="margin: 4pt 0; padding: 8pt 4pt; background-color: #eee;">hahah, beleza, legal!!

Somos nós, os loucos por videogames!!

<div class="commentinfo">— dial-up-200-184-37-52.intelignet.com.br (2006-10-12 12:22:15)</div></div><div style="margin: 4pt 0; padding: 8pt 4pt; background-color: #fff;">Aeee… muito bom o tutorial, cara me diz uma  
 coisa, tem como você disponibilizar o projeto ou coisa parecida?! faz o sistema  
 pra venda? sem as madeiras? para não pesar no sedex?!Valeu Cara!! Abraço!

<div class="commentinfo">— 201008241136.user.veloxzone.com.br (2006-12-01 10:27:50)</div></div><div style="margin: 4pt 0; padding: 8pt 4pt; background-color: #eee;">ah sim, davigmatos@gmail.com o e-mail se você  
 resolver alguma coisa! =D<div class="commentinfo">— 201008241136.user.veloxzone.com.br (2006-12-01 10:41:53)</div></div><div style="margin: 4pt 0; padding: 8pt 4pt; background-color: #fff;">Parabens pela idéia, eu confesso que copiei usar  
 as caixas de fita para as placas de controle e o uso de conectores, mas para dar  
 uma flexibilidade ainda maior ao meu arcade eu usei além do db25 um db9, pois  
 não usei o comum, eu jupeei os botões par por par individualmente, deu mais  
 trabalho, mas assim eu garanto maior flexibilidade.<div class="commentinfo">— 201.53.83.81 (2007-03-26 21:25:50)</div></div><div style="margin: 4pt 0; padding: 8pt 4pt; background-color: #eee;">m tempo, meu e-mail é lhcca@ig.com.br (eu que  
 copiei suas idéias).<div class="commentinfo">— 201.53.83.81 (2007-03-26 21:26:45)</div></div><div style="margin: 4pt 0; padding: 8pt 4pt; background-color: #eef;">Comprei direto no site. Veio certinho e sem  
 problemas, EXCETO a super taxa de importação que teve de ser paga na entrega,  
 que chegou a um pouco mais de 100% do valor bruto do produto… (imposto + taxa  
 de desembaraçamento)<div class="commentinfo">— [SeitiYamashiro](http://seiti.eti.br/wiki/SeitiYamashiro)  
 (2007-04-02 00:57:10)</div></div><div style="margin: 4pt 0; padding: 8pt 4pt; background-color: #eee;">Blz Seiti! Vc poderia me dizer mais sobre as  
 taxas de importação? Tenho um amigo q tem uns contatos nos EUA e pensei em pedir  
 pra comprarem lá e me enviarem. Será que terei q pagar essas taxas tb? Qto  
 acabou saindo o seu IPAC?<div class="commentinfo">— 201-14-252-161.paemt705.dsl.brasiltelecom.net.br (2007-04-02 11:25:26)</div></div><div style="margin: 4pt 0; padding: 8pt 4pt; background-color: #eef;">Deve ter custado uns 180 dólares… =P

<div class="commentinfo">— [SeitiYamashiro](http://seiti.eti.br/wiki/SeitiYamashiro)  
 (2007-04-09 22:24:59)</div></div><div style="margin: 4pt 0; padding: 8pt 4pt; background-color: #eee;">entao cara eu fiz com o controle de playstation e  
 funcionou normal eu ate adaptei o analogico ficou show de bola<div class="commentinfo">— 200-100-70-66.dial-up.telesp.net.br (2007-06-16 19:54:52)</div></div><div style="margin: 4pt 0; padding: 8pt 4pt; background-color: #fff;">Olá, Como resolveste os VMUs do dreamcast?  
 Ficaram dentro da caixa do arcade? Muito bom essa sua ideia to pensando em  
 copia-lá para montar um….Ate mais,

Mauro

<div class="commentinfo">— 189.27.128.148.host.gvt.net.br (2007-07-18 18:15:38)</div></div><div style="margin: 4pt 0; padding: 8pt 4pt; background-color: #eef;">Ficam dentro da caixa plástica para VHS. =)

Ao menos ficam protegidas.

<div class="commentinfo">— [SeitiYamashiro](http://seiti.eti.br/wiki/SeitiYamashiro)  
 (2007-07-20 23:55:34)</div></div><div style="margin: 4pt 0; padding: 8pt 4pt; background-color: #fff;">Beleza Seiti?

Eu comprei no site da Ultimarc um I-pac para 4 controles, mas ao chegar em  
 Viracopos deu problema porque a DHL não tinha como cobrar os impostos no meu  
 endereço, poderias entrar em contato no meu mail:  
 bruno.piazera.zacchi@terra.com.br para eu saber como aconteceu contigo? Abraços!

<div class="commentinfo">— 200-215-99-124.fnsce701.dsl.brasiltelecom.net.br (2007-07-30 12:14:25)</div></div><div style="margin: 4pt 0; padding: 8pt 4pt; background-color: #eef;">Bruno, a entrega foi realizada sem problemas, mas  
 tive de pagar o imposto na contra-entrega para o funcionário da transportadora.<div class="commentinfo">— [SeitiYamashiro](http://seiti.eti.br/wiki/SeitiYamashiro)  
 (2007-08-14 21:06:49)</div></div><div style="margin: 4pt 0; padding: 8pt 4pt; background-color: #fff;">Seiti,

Notei agora o que aconteceu com o vmu’s, o qual quero montar pretentdo  
 aproveitar um vmu no proprio arcade, com saves de jogos de luta mesmo. Irei  
 fazer os controles independentes, mas fiquei em duvida sobre o DB-25, como fazer  
 as conexões para o controle e para o PC? Tem algum link que eu possa dar uma  
 pesquisada?…desculpa a demora, é a falta do tempo eheheh Valeu pela resposta  
 anterior…

Até mais,

Mauro

<div class="commentinfo">— 201.86.202.140.adsl.gvt.net.br (2007-09-10 12:56:58)</div></div><div style="margin: 4pt 0; padding: 8pt 4pt; background-color: #eef;">Bom, nào tem mistério. Arranje um controle bem  
 baratinho (um da Players, por exemplo), desmonte-o e teste as ligações elétricas  
 com um cabo. Geralmente existe um terra compartilhado por todos os botões.Um site legal é o arcadecontrols.com !

<div class="commentinfo">— [SeitiYamashiro](http://seiti.eti.br/wiki/SeitiYamashiro)  
 (2007-09-11 01:08:45)</div></div><div style="margin: 4pt 0; padding: 8pt 4pt; background-color: #fff;">Caro,

Parabens pelo tutorial. Eu tenho um controle de play adaptado para arcade mas  
 ele quebra com rapidez. Já que os comandos são feitos com fechamento de  
 circuito, não seria mais interessante fechar diretamente o circuito sem passar  
 pela placa do play? favor se puder responda pra o meu email: gilson401@yahoo.com

<div class="commentinfo">— trap-t.br-petrobras.com.br (2007-10-19 14:47:07)</div></div><div style="margin: 4pt 0; padding: 8pt 4pt; background-color: #eee;">eu queria um esquema do controle de ps2 para  
 arcade por favor mande para esse email; sandrinho-costa@hotmail.com<div class="commentinfo">— 18912227162.user.veloxzone.com.br (2007-11-19 14:28:46)</div></div><div style="margin: 4pt 0; padding: 8pt 4pt; background-color: #eef;">Não existe “esquema” nenhum…

<div class="commentinfo">— [SeitiYamashiro](http://seiti.eti.br/wiki/SeitiYamashiro)  
 (2007-11-22 21:16:47)</div></div><div style="margin: 4pt 0; padding: 8pt 4pt; background-color: #eee;">Nossa cara, deixa eu esclarecer uma dúvida… o  
 fato de vc colocar o DB-25 como ponte para depois ligar o controle (hack) em si  
 não causa um atraso nao? (delay)Valeu.

Rodrigo.

<div class="commentinfo">— proxy.semad.mg.gov.br (2007-12-07 11:14:55)</div></div><div style="margin: 4pt 0; padding: 8pt 4pt; background-color: #eef;">Não creio ser o caso, pois não envolve nenhum  
 circuito lógico, apenas um curto envolvendo o DB25.<div class="commentinfo">— [SeitiYamashiro](http://seiti.eti.br/wiki/SeitiYamashiro)  
 (2007-12-07 19:49:48)</div></div><div style="margin: 4pt 0; padding: 8pt 4pt; background-color: #eee;">Seiti,

Afinal como fez com os botões L e R?

Tenho um xbox e gostaria de fazer um controle (módulo xbox). O controle do X é  
 semalhante o do Dreamcast…

Obrigado.

Rodrigo – BH

<div class="commentinfo">— 20158187239.user.veloxzone.com.br (2007-12-09 16:15:22)</div></div><div style="margin: 4pt 0; padding: 8pt 4pt; background-color: #eef;">Com o circuito do controle original não havia  
 jeito. Por isso comprei um controle genérico, que possuia um circuito muito mais  
 simples para trabalhar.<div class="commentinfo">— [SeitiYamashiro](http://seiti.eti.br/wiki/SeitiYamashiro)  
 (2007-12-09 18:11:32)</div></div><div style="margin: 4pt 0; padding: 8pt 4pt; background-color: #eee;">Seiti, ficou maneiro o que voce fez com o  
 controle de DC mas eu queria pedir que se pudesse botar uma foto com melhor  
 resolucao de como ficou a placa conectada pois esta muito fraca a resolucao.Eu ja montei quase tudo mas ta faltando os analgicos, o meu controle eh original  
 pois nao acho nenhum da players pra vender “(

<div class="commentinfo">— 20151014031.user.veloxzone.com.br (2008-01-25 00:19:40)</div></div><div style="margin: 4pt 0; padding: 8pt 4pt; background-color: #eef;">No controle original os gatilhos analógicos, pelo  
 que pude observar, funcionam de um modo mais complexo. Preso aos botões L e R  
 está um imã, que, ao aproximar-se de um circuito embutido na placa principal do  
 controle, deve aumentar ou diminuir a resistência elétrica neste circuito.Não encontrei uma maneira óbvia para aproveitar o controle original, por isso  
 comprei um controle genérico, que utiliza um circuito mais simples (e barato).

<div class="commentinfo">— [SeitiYamashiro](http://seiti.eti.br/wiki/SeitiYamashiro)  
 (2008-01-26 12:55:44)</div></div><div style="margin: 4pt 0; padding: 8pt 4pt; background-color: #eee;">queria saber a respeito das direcionais ??? :/

<div class="commentinfo">— 20151100182.user.veloxzone.com.br (2008-01-28 21:30:13)</div></div><div style="margin: 4pt 0; padding: 8pt 4pt; background-color: #eef;">Os direcionais funcionam! =)

<div class="commentinfo">— [SeitiYamashiro](http://seiti.eti.br/wiki/SeitiYamashiro)  
 (2008-02-26 18:02:05)</div></div><div style="margin: 4pt 0; padding: 8pt 4pt; background-color: #eee;">queria saber se você vende o controle de arcade  
 com baia dupla para playstation 1 e 2 e o preço valeuuuuuuuuu.  
 email:www.cleiberrodrigues@bol.com.br<div class="commentinfo">— 201.67.226.141 (2008-03-02 11:56:16)</div></div><div style="margin: 4pt 0; padding: 8pt 4pt; background-color: #fff;">Olá seiti,

Ainda to na luta pra montar o arcade, hehehe mas pesquisando é que a gente  
 aprende, eu vi a montagem usando o lpt-switch. Além de barato, bem simples..Será  
 que é possivel fazer a montagem do modulo dreamcast, com essa configuração? e o  
 DB25 é realmente necessário? ou posso fazer a ligação diretamente nos fios dos  
 botões? peguei a ideia deste  
 site..http://www.arcadebr.com.br/modules/xt_conteudo/index.php?id=21

<div class="commentinfo">— 201.86.194.10.adsl.gvt.net.br (2008-03-05 12:01:50)</div></div><div style="margin: 4pt 0; padding: 8pt 4pt; background-color: #eef;">Para o Dreamcast o mais viável é você comprar,  
 como eu, alguns controles baratinhos. E pode-se ligar direto no circuito dos  
 gamepads, mas daí você não poderá trocar o circuito tão facilmente, que era meu  
 objetivo!<div class="commentinfo">— [SeitiYamashiro](http://seiti.eti.br/wiki/SeitiYamashiro)  
 (2008-03-05 20:43:34)</div></div><div style="margin: 4pt 0; padding: 8pt 4pt; background-color: #fff;">Entendo, no meu caso não quero fazer trocas de  
 pads, e além do mais encontrar controle de Dreamcast aqui em porto alegre é  
 coisa pra arqueólogo, como tenho 2 sobrando usarei para a montagem dos arcades,  
 o único intuito é fazer para o PC e Dream….<div class="commentinfo">— 201.86.211.137.adsl.gvt.net.br (2008-03-10 09:41:10)</div></div><div style="margin: 4pt 0; padding: 8pt 4pt; background-color: #eee;">e ae caras,bom estou com um problema,comprei um  
 controle arcade de locadora até ai tudo bem mas tem um porem,este controle veio  
 com um contadorde minutos eu nao consigo tirar este contador de minutos,uma pergunta para o  
 controle de arcade pegar é só fazer a fiaçao ou tem que coloca lo na energia  
 avaleu caras se poderem me responder

meu e-mail:pudy_dead@hotmail.com valeu

<div class="commentinfo">— 189-46-71-244.dsl.telesp.net.br (2008-03-12 14:17:22)</div></div><div style="margin: 4pt 0; padding: 8pt 4pt; background-color: #eef;">Sobre o Dreamcast: cara, se você conseguir fazer  
 os botões L/R funcionarem no arcade, me passa! Sem ser por um sistema mecânico,  
 ou criação de um circuito, eu não tenho idéia.Quanto ao arcade com timer, acho que só abrindo e fuçando para saber!

<div class="commentinfo">— [SeitiYamashiro](http://seiti.eti.br/wiki/SeitiYamashiro)  
 (2008-04-15 10:48:11)</div></div><div style="margin: 4pt 0; padding: 8pt 4pt; background-color: #eee;">Po, bem bacana. Vocês saberiam me informar onde  
 testar e adquirir um controle para PC-USB compatível com windows vista starter  
 que funcione com o NeorageX 5.0? Desculpem, mas a minha turma entrou no túnel do  
 tempo e tem sido divertido quando jogamos em playstation, mas é bem melhor no  
 PC. Aguardo uma resposta e desde já, agradeço pela atenção. Leandro Ribeiro<div class="commentinfo">— 189-46-95-66.dsl.telesp.net.br (2008-04-21 22:38:49)</div></div><div style="margin: 4pt 0; padding: 8pt 4pt; background-color: #fff;">Caso possam me dar mais dicas, segue meu email:  
 Leandro Ribeiro – leandroribeiro8@hotmail.com<div class="commentinfo">— 189-46-95-66.dsl.telesp.net.br (2008-04-21 22:41:23)</div></div><div style="margin: 4pt 0; padding: 8pt 4pt; background-color: #eef;">Bom, eu não uso o Windows Vista, mas acredito que  
 qualquer controle USB deva servir. Se não servir aconselho a trocar de sistema  
 operacional. Bah, mesmo se servir, aconselho a troca. =)<div class="commentinfo">— [SeitiYamashiro](http://seiti.eti.br/wiki/SeitiYamashiro)  
 (2008-04-28 10:01:40)</div></div><div style="margin: 4pt 0; padding: 8pt 4pt; background-color: #fff;">Estava lendo seu tutorial e ficou lindo seu  
 controleme inspirei e quero fazer um Igual

Meu nome é Gustavo sou de Salvador,faço Biologia, tenho 30 anos e dês dos 09  
 anos eu jogo em arcade, para mim é o melhor!!

Eu gostaria de fazer meu controle igualzinho ao seu, e tenho umas perguntas:

Qual a medidas que você usou do controle, tipo da madeira o tamanho, o espaço  
 entre os componentes, de um player para o outro

A outra é sobre os módulos (ótima idéia!) tem algum esquema?

Meu email é carlosgustavoss@gmail.com

Desde de já agradeço e Obrigado por colocar na internet essa maravilha de  
 tutorial

<div class="commentinfo">— 189104012149.user.veloxzone.com.br (2008-07-06 11:41:21)</div></div><div style="margin: 4pt 0; padding: 8pt 4pt; background-color: #eef;">As medidas foram tiradas no olhômetro. Direi o  
 que fiz. Comprei as alavancas e botoões arcade. Depois construí um protótipo  
 utilizando uma caixa de papelão.Quando fiquei satisfeito com a posição dos botões eu tirei as medidas e  
 finalmente cortei a madeira, uma chapa de prensado 2mm.

<div class="commentinfo">— [SeitiYamashiro](http://seiti.eti.br/wiki/SeitiYamashiro)  
 (2008-07-10 08:12:14)</div></div><div style="margin: 4pt 0; padding: 8pt 4pt; background-color: #fff;">Bom, segui seus conselhos e já fiz a caixa, ta  
 uma maravilha, falta eu compra os botões e alavanca ( o dim dim acabou) tenho  
 uma duvida (desculpa encher o saquinho :D) eu queria saber o que voce usou para  
 fixar o arcadinho para ele não “rebolar”Des de já agradeço e desculpa o incomodo

<div class="commentinfo">— 189104012149.user.veloxzone.com.br (2008-07-14 21:12:51)</div></div><div style="margin: 4pt 0; padding: 8pt 4pt; background-color: #eee;">Olá ! Eu estou interessado em montar meu controle  
 de arcade também, eu pretendo montá-lo com a placa de um controle de playstation  
 e queria saber como funciona e o que eu vou precisar, esse ferro de solda é  
 caro? Enfim, eu não entendo muito disso, mas fiquei interessado no que você fez  
 e queria fazer um também? pode me dar umas dicas? meu e-mail é  
 nery-666@hotmail.com, desde já obrigado !<div class="commentinfo">— 189.27.201.251.adsl.gvt.net.br (2008-07-17 13:17:03)</div></div><div style="margin: 4pt 0; padding: 8pt 4pt; background-color: #fff;">Olá! sou eu de novo, o Nery, eu estava analisando  
 meu controle de playstation e entendi o que você fez no exemplo, mas ainda tenho  
 uma duvida : o que é esse cabo terra? se eu soldar cada contato o controle vai  
 funcionar normalmente ou é preciso mexer no terra? obrigado !<div class="commentinfo">— 189.27.200.86.adsl.gvt.net.br (2008-07-18 08:08:54)</div></div><div style="margin: 4pt 0; padding: 8pt 4pt; background-color: #eee;">hehehe…. ótimo esse tuto…

estou montando meu controle de arcade. comecei ontem. estou fazendo com  
 controles de dreamcast originais!!!

fiz o teste hoje e até o momento esta tudo dando muito certo. só tenho duvidas  
 se o “L” e o “R” vão funcionar bem em jogos que têm que ficar apertados por um  
 longo tempo.tou baixando o lemans 24 h e chegando em casa farei o teste da  
 aceleração. depois eu mostro como foi que eu fiz para ligar o “L” e o “R” com  
 detalhes.

abraços

<div class="commentinfo">— 189-46-95-51.dsl.telesp.net.br (2008-07-23 16:19:35)</div></div><div style="margin: 4pt 0; padding: 8pt 4pt; background-color: #fff;">tenho duvidas sobre a espessura dos fios de  
 ligção do arcade???????????<div class="commentinfo">— 189-78-169-149.dsl.telesp.net.br (2008-07-29 20:01:12)</div></div><div style="margin: 4pt 0; padding: 8pt 4pt; background-color: #eee;">marcelo cesar

ae.. como disse que faria… vai aqui o link para as fotos da montagem do meu  
 controle de arcade com controle original de dreamcast

http://picasaweb.google.com.br/marcelo.cesards/ControleDeArcade

espero que seja muito útil para alguem.

abraços

<div class="commentinfo">— 189-18-227-7.dsl.telesp.net.br (2008-07-29 20:02:29)</div></div><div style="margin: 4pt 0; padding: 8pt 4pt; background-color: #fff;">marcelo cesar

eu usei um cabo velho de impressora que eu tinha.. hehehe…

mas de uma olhada nas fotos do meu controle que montei no link

http://picasaweb.google.com.br/marcelo.cesards/ControleDeArcade

talvez possa lhe ajudar

<div class="commentinfo">— 189-18-227-7.dsl.telesp.net.br (2008-07-29 20:05:13)</div></div><div style="margin: 4pt 0; padding: 8pt 4pt; background-color: #eef;">Hey Marcelo, ficou bem bacana teu controle! =)

Legal a idéia de prender os gamepads embaixo do tampo.

<div class="commentinfo">— [SeitiYamashiro](http://seiti.eti.br/wiki/SeitiYamashiro)  
 (2008-07-30 22:22:01)</div></div><div style="margin: 4pt 0; padding: 8pt 4pt; background-color: #fff;">marcelo cesar

e ae beleza

tenho que te agradecer seiti yamashiro, teu tuto foi muito importante na  
 construção do meu controle e, volto a repetir que o teu tuto ficou ótimo. um  
 abraço

<div class="commentinfo">— 201-92-155-64.dsl.telesp.net.br (2008-08-02 13:02:09)</div></div><div style="margin: 4pt 0; padding: 8pt 4pt; background-color: #eee;">Ae seiti,

Eu ainda nao tive como iniciar o controle mas ano que vem vai eheheh,tive  
 problemas estudantis no curso, então tive de me dedicar mais (pra nao repetir de  
 ano) e então eu voltei a sua página mais para procurar se tinha alguma coisa  
 sobre o controle arcade com botoes turbo, to pensando em fazer pelo menos um dos  
 botoes com essa caracteristica, sobre os botoes L/R eu nao tinha pensando ainda  
 sobre este problema mas quero ver se resolvo sem ter de mexer muito na placa de  
 repente diretamente na saida dos fios, sei lá….bom se tu tiver alguma idéia  
 sobre como fazer um botão turbo usando componentes e não via software, eu  
 agradeço…se nao for incomodo poderia me enviar pelo email:

mandraqueazul@gmail.com

Valeu por toda a ajuda, e ano que vem esse filho nasce eheheh até mais

<div class="commentinfo">— 189-30-224-240.paemt701.dsl.brasiltelecom.net.br (2008-12-31 16:37:36)</div></div><div style="margin: 4pt 0; padding: 8pt 4pt; background-color: #eef;">Resolução de ano novo? =)

Cara, recomendo você comprar controles com turbo para poder utilizar o circuito.  
 Não tem mistério. Cada botão funciona como uma chave, fechando/abrindo um  
 contato.

Ligando dois fios por contato você terá o resultado desjado! Meu projeto ficou  
 mais complicado que isso por conta do uso do fio terra comum, e para que  
 funcionasse em vários aparelhos.

Boa sorte no projeto! E não deixe de postar teu link aqui!

<div class="commentinfo">— [SeitiYamashiro](http://seiti.eti.br/wiki/SeitiYamashiro)  
 (2009-01-06 16:54:06)</div></div><div style="margin: 4pt 0; padding: 8pt 4pt; background-color: #eee;">olá seiti,

Estou usando umm controle comum mesmo, é o que temos no momento, estou tentando  
 fazer uma gambiarra com um multivibrador astável…vamos ver se dá certo…valeu  
 pela dica…. até mais…

<div class="commentinfo">— 201-66-181-86.paemt701.dsl.brasiltelecom.net.br (2009-01-14 19:36:23)</div></div><div style="margin: 4pt 0; padding: 8pt 4pt; background-color: #fff;">Olá a respeito do surporte para o controle na  
 foto acima oque vcs usaram para ficar em uma altura ideal????!Grato!!!<div class="commentinfo">— smtp.engevix.com.br (2009-01-19 15:39:44)</div></div><div style="margin: 4pt 0; padding: 8pt 4pt; background-color: #eee;">Eu usei um suporte de teclado. Teclado musical, e  
 não teclado de digitar! O problema é que mesmo assim, devido ao peso do  
 controle, não ficou uma maravilha. Balança um pouco, mas dá pro gasto. =)<div class="commentinfo">— c9342454.virtua.com.br (2009-01-29 01:33:11)</div></div><div style="margin: 4pt 0; padding: 8pt 4pt; background-color: #fff;">POxa… eu queria a sequencia de cabos para o  
 dreamcast… não dá para ver direto. talmid12@hotmail.com<div class="commentinfo">— 20150094047.user.veloxzone.com.br (2009-02-14 22:00:36)</div></div><div style="margin: 4pt 0; padding: 8pt 4pt; background-color: #eee;">Olá Seiti,

Finalmente consegui terminar o projeto dos meus arcades caseiros para o  
 Dreamcast, como não tinha um outro uso para eles, então não sei se terei uma  
 adaptação para o PC…mas isso é algo para futuro. Não coloquei as fotos em  
 algum servidor de imagens, as coloquei direto no meu orkut então deixo o link  
 para vocês darem uma olhada e se quiserem comentar também….

http://www.orkut.com.br/Main#Album.aspx?uid=4990526142223843215&aid=1235563002  
 Gostaria de te agradecer Seiti, pelo tutorial e pela ajuda que me deste no  
 começo deste projeto. Ele se tornou muito satisfatório e compensador no final  
 das contas, é um projeto tecnicamente fácil e aos iniciantes, tenham  
 paciência…Por fim, muito obrigado pela sua colaboração.

Até mais,  
 Mauro Ledesma

<div class="commentinfo">— 201-66-160-136.paemt701.dsl.brasiltelecom.net.br (2009-02-25 16:19:26)</div></div><div style="margin: 4pt 0; padding: 8pt 4pt; background-color: #eef;">Ficou bem bacana Mauro! Usou MDF? Dá mais  
 trabalho, mas o resultado fica bem mais profissional, como pode-se ver no seu  
 controle.E é isso ae, só precisa de vontade e não ter medo de errar! =)

<div class="commentinfo">— [SeitiYamashiro](http://seiti.eti.br/wiki/SeitiYamashiro)  
 (2009-03-16 13:46:37)</div></div>
