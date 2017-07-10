---
layout: post
title: Migrando emails do Gmail para o Google Apps
date: '2008-06-29 00:26:35'
tags:
- cloud
- gmail
- google
- servicos
---


Após configurada sua conta no [Google Apps](http://seiti.eti.br/blog/2008/migrando-para-o-google-apps-gmail), é hora de migrar seus emails da conta **Gmail** pré-existente. Eu tenho cerca de 60 mil emails em 2GB de espaço.

Primeiro habilite em sua conta original no Gmail o acesso via **IMAP**. Por quê IMAP? Por que assim suas mensagens estarão separadas em *pastas*, uma para cada **label** que foi criada. E daí? Veremos mais para frente.

Depois vem a sacada: compre o **Google Apps Premier Edition**. O custo é de *50 dólares por ano, por conta* de email. **Mas** pode-se *cancelar* esta assinatura em até 30 dias sem custo algum.

Após comprado o Premier Edition surgirão novas opções. Uma delas é migrar emails de sua conta antiga via IMAP. Esta opção fica sob a seção *Advanced Tools*. Configure a conta a ser acessada como segue:  
**URL**: <span style="font-family: Courier New,Courier,mono;">imap.gmail.com</span>  
**Use SSL**: Yes  
**Port**: 993

Pronto, inicie a migração. No meu caso demorou quase o dia todo para completar. Surgirão de volta todos os *labels* pré-existentes, além de um novo, chamado **Migrated**, que marca os emails oriundos da migração.

Bom, depois da migração completada fica a seu critério continuar ou não com os benefícios e o custo da conta Premier. Caso queira cancelar a *Premier Edition* siga as [instruções](http://www.google.com/support/a/bin/answer.py?answer=60755&hl=en "Cancelling Premier Edition").

### Firefox: Gmail Notifier

Se você utiliza a extensão do Firefox **Gmail Notifier**, vai precisar efetuar os seguintes passos para que passe a indicar sua nova caixa de email em *seu domínio*:

- desabilite o Gmail Notifier;
- feche o Firefox;
- entre no diretório que contém o *profile* e edite o arquivo **prefs.js**;
- removas todas as entradas que contiver **gm-notifier**
- ligue o Firefox

Agora basta inserir seu novo email, eu@meu.dominio, e sua senha. Dica do site [Tanglebones](http://tanglebones.com/articles/2007/08/10/just-a-small-gmail-notifier-firefox-extension-tip-for-users-of-google-apps-for-your-domain/).


