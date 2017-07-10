---
layout: post
title: Impressora Lexmark Z645 no Ubuntu Linux
date: '2008-12-02 21:49:22'
tags:
- hardware
- impressora
- ubuntu
---


![LexmarkZ645](../../gallery2/main.php?g2_view=core.DownloadItem&g2_itemId=3085&g2_serialNumber=3)

Comprei uma impressora baratinha da Lexmark, mas descobri que ela não tem suporte nativo do [Ubuntu Edgy Eft ao Hardy Heron](../../wiki/UbuntuLaptop). Só para constar, uma multifuncional HP que eu havia testado antes foi detectada e funcionou sem nenhum problema. Parece que as HPs possuem um suporte melhor ou mais maduro, seja por parte da comunidade ou da empresa.

> <div class="floatl">Muita gente, aqui nos comentários, parece não notar que uso **Linux**. Se você precisa de um driver para algum sistema **Windows** tente o site de [downloads da Lexmark](http://downloads.lexmark.com/cgi-perl/downloads.cgi?ccs=229:1:0:548:0:0).</div>

Bom, a solução foi instalar pacotes que possuíssem os drivers. No site da própria Lexmark não existem drivers deste modelo para o Linux. Mas pode-se utilizar o do Z600. O arquivo está empacotado em um tarball, mas o binário correspondente está no corpo do script de instalação. E o próprio binário embutido no script está no formato RPM, fazendo com que usuários de distros baseados no Debian tenham de processar o pacote RPM através do <tt>alien</tt>, a fim de criar um pacote [Debian](../../wiki/DebianLaptop).

<span class="strikethrough">Felizmente o pessoal da [Indexdata](http://www.indexdata.com.br/) fez todo este trabalho e disponibilizou para o pessoal baixar gratuitamente: [http://www.indexdata.com.br/Linux/Impressoras/LexMark/](http://www.indexdata.com.br/Linux/Impressoras/LexMark/)</span>

É só pegar os pacotes .deb e instalá-los.

Parece que não existem mais os pacotes Debian. Não há problema, siga as instruções do [Fórum do Ubuntu](http://ubuntuforums.org/showthread.php?t=49714), e depois entre com o comando:

 sudo apt-get install libstdc++5

Depois entre na pasta <tt>/usr/share/cups/model/</tt> e dê o comando:

 sudo ldconfig sudo gunzip Lexmark-Z600-lxz600cj-cups.ppd.gz

Reinicie o CUPS:

sudo /etc/rc2.d/S20cupsys restart

<span class="strikethrough">Eu ainda tive de dar o arquivo PPD aberto acima na hora de adicionar a impressora, na caixa de diálogo do Gnome. Para uma interface mais completa ao CUPS, acesse [http://localhost:631](http://localhost:631/)</span>

Bom, saindo um pouco do escopo do texto, comprei recentemente um cartucho de tinta preta Extralife 4916 (número de série G680021191), pois ela vem sem cartucho preto (só colorido) e na papelaria só havia desta marca.  
 Infelizmente a qualidade do cartucho deixou **muito** a desejar, falhando após a impressão de cerca de 12 folhas em duas semanas (resolvido, veja a *nota 2*).

E estas tais falhas da impressão significam deixar o texto ilegível. Conclusão: compre produtos originais. O barato sai muito mais caro. Na verdade acho que é melhor comprar impressoras HP mesmo.

**Notas:**

1. Parece que minha alegria durou pouco. Hoje, após já ter impresso várias folhas em outras ocasiões, a impressora simplesmente parou de responder aos pedidos. E quando tentei reinstalar, nem ao menos aparece na lista de impressora detectadas… <span class="strikethrough">Bom, o fato é que a impressora pifou. Tentei instalá-la no Windows XP e ele nem ao menos detecta a desgraçada. O negócio é trocá-la por uma HP.</span> A impressora voltou à vida! Deu um pau nela que precisou de um “reboot”. Foi retirá-la da tomada e recolocá-la que ela ressucitou.
2. A Extralife trocou meu cartucho ao custo do envio do cartucho para o escritório em Osasco. Na análise deles o cartucho apresentou defeito no chip. Nem tudo está perdido…


