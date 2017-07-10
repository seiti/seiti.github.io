---
layout: post
title: Seu domínio no localhost
date: '2009-04-28 21:21:59'
tags:
- programacao
- web
---


Da série *como não pensei nisto antes*?

Dica útil para quem desenvolve sistemas web e quer testar o tal sistema em condições mais próximas possíveis do ambiente de produção.

Da série *como não pensei nisto antes*?

Quem desenvolve sites e sistemas web precisa testar seu produto em sua própria máquina (é claro que você não desenvolve direto no servidor de produção, estou certo?). Para isto é bem útil e prático configurar um **servidor Apache** para rodar em seu computador, principalmente se você estiver programando em alguma [linguagem server sided](../../wiki/EclipsePDT).

O mais legal é que é possível criar uma **URL***fictícia* para testar seu site. Esta dica me foi dada pelo [Alex](http://zaip.net/).

Se você ainda não fez, instale o pacote <tt>apache2</tt> a partir dos repositórios do [Ubuntu](../../wiki/UbuntuLaptop).

Vamos então editar o arquivo <tt>hosts</tt>:

<div class="code">sudo gedit /etc/hosts

</div>Com o seguinte conteúdo:

<div class="code">127.0.0.1 localhost 127.0.0.1 www.meudominio.xyz

</div>Note que apenas adicionei a linha **127.0.0.1 www.meudominio.xyz**  
 Vamos então criar o arquivo de configuração *copiando* o **default**:

<div class="code">cd /etc/apache2/sites-available/ sudo cp default www.meudominio.xyz

</div>Depois edite o arquivo <tt>/etc/apache2/sites-available/www.dominio.xyz</tt> com o segunte conteúdo:

<div class="code">NameVirtualHost www.meudominio.xyz <virtualhost www.meudominio.xyz=""> ServerAdmin webmaster@localhost DocumentRoot /home/username/sites <directory></directory> Options FollowSymLinks AllowOverride None <directory></directory> ... ...</virtualhost>

</div>Trocando */home/username/sites* pela pasta em que reside seu site. Note que o arquivo não está completo, coloquei apenas uma parte dele.

Depois **habilite** o site e *recarregue* o Apache:

<div class="code">sudo a2ensite www.meudominio.xyz sudo /etc/init.d/apache2 reload

</div>**Pronto**! Teste entrando no site recém configurado: [www.meudominio.xyz](http://www.meudominio.xyz/)


