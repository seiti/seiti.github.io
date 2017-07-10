---
layout: post
title: Login failed for user 'NT AUTHORITY\NETWORK SERVICE'
date: '2010-03-31 16:46:25'
tags:
- aspnet
- sql-server
---


Acabou de instalar o SQL Server? Surgiu um dos seguintes erros?

> Login failed for user ‘NT AUTHORITY\NETWORK SERVICE’

ou

> Falha no login ‘AUTORIDADE NT\SERVIÇO DE REDE’

Não se preocupe. Execute o seguinte no banco de dados **master** no SQL Server:

 sp_grantlogin 'NT AUTHORITY\NETWORK SERVICE'

ou

 sp_grantlogin 'AUTORIDADE NT\SERVIÇO DE REDE'

Pronto, sua aplicação conversará com seu banco de dados.


