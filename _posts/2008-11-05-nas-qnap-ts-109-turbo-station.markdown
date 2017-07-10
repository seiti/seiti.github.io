---
layout: post
title: NAS Qnap TS-109 Turbo Station
date: '2008-11-05 01:45:42'
tags:
- cacarecos
- linux
- nas
---


[![](http://farm4.static.flickr.com/3153/3004069264_799c701919_m.jpg "Caixa")](http://www.flickr.com/photos/seiti/3004069264/)

Há muito tempo eu pensava e ter uma solução para armazenar meus arquivos: músicas, fotos e documentos, uma solução que fosse prática e que tivesse mais funções que apenas um HD externo para *backup*. Eu já havia pesquisado sobre Network Attached Storage – NAS, mas no Brasil isto é bem difícil de se encontrar, ao menos para o usuário doméstico.

### Achei!! Oh não!

Mas então li um artigo na coluna do Flávio Xandó, no [Fórum PCs](http://www.forumpcs.com.br/coluna.php?b=242567), sobre o  [Qnap TS-109 Turbo Station](http://www.qnap.com/pro_detail_feature.asp?p_id=78 "Street Fighter II' Turbo Hyper Fighting") e fiquei bastante ansioso em adquirir o produto. Entrei em contato com o pessoal da [Almac](http://www.almac.com.br/), que são os revendedores da marca no Brasil, e, levado pela atenção e cuidados que eles tinham comigo, possível cliente, comprei o produto.

[![](http://farm4.static.flickr.com/3202/3003729345_c5e70d4ab9_m.jpg "Qnap TS-109")](http://www.flickr.com/photos/seiti/3003729345/)

Após o pagamento, já tendo sido alertado que demoraria cerca de 7 dias úteis para a chegada da encomenda, iniciou-se minha espera. Bom, passados os 7 dias, entrei novamente em contato, e a atenção que eles haviam tido comigo antes da compra havia caído pela metade… Sempre simpáticos, seja via telefone ou email, mas agora demoravam mais a responder. Para alguém que já havia pago e estava esperando já há uns 15 dias isso não era nada animador. Um geek esperando um *gadget* é uma criatura muito ansiosa…

Mas após mais de mês de espera, algumas ligações, emails enviados, finalmente chega o bendito!! \o\|o|/o/  
 E valeu cada dia de espera! Obrigado ao Roberto e à Priscila da Almac, que sempre me atenderam bem.

### Funções mil

O TS-109 me surpreendeu. Apesar da velocidade não ser *excelente*, as funcionalidades que ele entrega são **muitas**. Vamos ver:

- FTP;
- SSH;
- Servidor HTTP;
- MySQL;
- PHP (pena não ser o 5);
- UPnP DNLA (eu nem sabia o que era isso);
- sistema de gerenciamento de downloads via http, ftp e bittorrent!;
- CIFS/SMB (faltou, ou não achei, suporte a NFS);
- e muitas ferramentas que uma distro Linux dispõem: contas de usuários, quotas, etc.

[![](http://farm4.static.flickr.com/3136/3004569712_ff8ecb7cfc_m.jpg "Qnap TS-109")](http://www.flickr.com/photos/seiti/3004569712/)

A instalação é bem simples: abrir, colocar o HD, fechar, plugar os cabos de força e rede e apertar o botão de ligar.

Ok, precisa de um micro com Windows ou Mac OS para rodar o software de instalação. Este software  busca o aparelho na rede e realiza algumas tarefas, que acredito serem particionar o HD, formatar (em Ext3) e instalar o SO a partir do firmware.

Depois disto todas as funcionalidades ficam disponíveis na interface administrativa via navegador. A interface é bem simples, embora eu ache que os ícones utilizados [não sejam muito felizes](http://www.cnet.com.au/desktops/storage/0,239029473,339288795,00.htm).

[![](http://farm4.static.flickr.com/3186/3004572268_1fbfeeaac4_m.jpg "Qnap TS-109")](http://www.flickr.com/photos/seiti/3004572268/)

### DNLA e UPnP

Bom, minha primeira tarefa foi verificar as funções relacionadas com multimídia. Após algumas **horas** carregando minhas dezenas de gigabytes de fotos e músicas, liguei o famigerado servidor *[DLNA](http://en.wikipedia.org/wiki/DLNA)*. Descobri então que o TS-109 utiliza o [Twonky Media](http://www.twonkyvision.com/) como servidor de conteúdo multimídia.

O Twonky Media (que nomezinho, não?) analisa os arquivos em um diretório pré-definido (<tt>/Qmultimedia</tt>) em busca de **metadados** (coisas como tags ID3), criando um índice. Como testar este servidor multimídia agora?

Bom, saquei meu N95 e perguntei ao [Oráculo](http://www.fwrnando.com/blog/2008/dlna-on-the-n95/). Hmm… Basta ir, no smartphone, em *Ferramentas* → *Conectividade* → *Mídia Local*.  
 Surgirá um *Wizard* com perguntas básicas, e, magicamente, você terá acesso aos arquivos no TS-109, a partir do celular!

Animado com isto, pensei em testar em mais alguma coisa. Pensei então no Amarok. Infelizmente não deu ([por enquanto](http://mail.kde.org/pipermail/amarok/2008-March/005526.html)). Bom, então que tal o Rhythmbox? Este foi fácil Foi só ligar que ele já estava lá:

[![](http://farm4.static.flickr.com/3197/3004763430_91653d5c4a_m.jpg "Qnap TS-109 DLNA UPnP Testing on Rhythmbox")](http://www.flickr.com/photos/seiti/3004763430/)

Veja no cantinho um ícone de um servidor chamada NUMENOR. Foi só clicar nele que surgiram as listas de álbuns/músicas que aparecem na imagem. =)

Meu próximo passo será testar alguma aplicação web usando a pilha [LAMP](http://pt.wikipedia.org/wiki/LAMP). No manual consta a instalação automática do Joomla. Mas isto fica pra outro post.

[![](http://farm4.static.flickr.com/3003/3004619284_3d9dea7947_m.jpg "Qnap TS-109")](http://www.flickr.com/photos/seiti/3004619284/)

### Fechando

O Qnap TS-109 é um NAS pequeno, cabe em qualquer canto, não aquece muito e tem um desenho bem limpo. Ele fica bem em cima da sua mesa, sem incomodar, pois não tem ventoinhas para fazerem barulho.

Possui muitas funções prontas para uso. Requer um pouco de conhecimentos de rede e sistemas Linux para poder usufruir de tudo que ele oferece, mas a interface web ajuda bastante na tarefa.

É uma ótima aquisição para os que buscam algo a mais, muito mais na verdade, que apenas um HD externo do tipo **[WD My Book](http://www.wdc.com/en/products/index.asp?cat=8)**, e recomendo a todos os fuçadores de plantão.

Um computador dedicado teria todas estas funções, mas não seria tão prático, pequeno, silencioso e econômico no consumo de energia.


