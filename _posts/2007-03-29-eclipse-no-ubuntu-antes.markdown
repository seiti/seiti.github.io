---
layout: post
title: Eclipse no Ubuntu (antes)
date: '2007-03-29 21:32:05'
tags:
- eclipse
- ubuntu
---


> Para ver como é atualmente: [http://seiti.eti.br/blog/2007/eclipse-no-ubuntu](http://seiti.eti.br/blog/2007/eclipse-no-ubuntu)

Instalando o Eclipse no Ubuntu. Primeiro baixe o Eclipse no site oficial (htp://www.eclipse.org), descompacte-o e depois mova os arquivos descompactados para o diretório <tt>/usr/local/</tt>:

 tar xzf eclipse-SDK-3.2-linux-gtk.tar.gz sudo cp -R eclipse /usr/local

Copie o ícone do Eclipse para o diretório de ícones do sistema:

 sudo cp /usr/local/eclipse/icon.xpm /usr/share/pixmaps/

Crie o atalho que constará no menu de aplicativos, criando e editando o arquivo <tt>usr/share/applications/eclipse.desktop</tt> (use seu editor de texto favorito):

 sudo vi /usr/share/applications/eclipse.desktop

E insira o seguinte texto:

 [Desktop Entry] Comment=Eclipse SDK Name=Eclipse SDK Exec=/usr/local/eclipse/eclipse MultipleArgs=true Terminal=false Type=Application Categories=Application;Development; Icon=eclipse.xpm

Quase pronto! Falta ainda criar o grupo **development**, inserir seu próprio usuário neste grupo, e configurar todos os arquivos e diretórios do Eclipse para pertencer ao grupo development. Só assim para você poder atualizar e instalar plugins sem rodar o Eclipse como root.  
 Crie o grupo e se insira nele atraves do Gerenciador de Usuários do Gnome. Fácil e indolor.

Depois configure os arquivos do Eclipse para pertencerem ao grupo criado:

 sudo chgrp development -R /usr/local/eclipse/ sudo chmod g+w -R /usr/local/eclipse/

Pronto!


