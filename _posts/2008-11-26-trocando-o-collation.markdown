---
layout: post
title: Trocando o Collation
date: '2008-11-26 19:51:04'
tags:
- sql-server
---


Simples e rápido.  
 ALTER DATABASE bdname SET SINGLE_USER WITH ROLLBACK IMMEDIATE  
 ALTER DATABASE bdname _RH COLLATE Latin1_General_CI_AS –ou outro qualquer  
 ALTER DATABASE bdname _RH SET MULTI_USER


