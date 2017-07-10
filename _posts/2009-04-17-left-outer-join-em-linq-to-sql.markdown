---
layout: post
title: Left Outer Join em Linq To Sql
date: '2009-04-17 14:57:13'
tags:
- linq
---


Como criar um left outer join em Linq To Sql:

var q = from c in customers join o in orders on c.id equals o.id into x from o in x.DefaultIfEmpty() select new {Name = c.Name, OrderNumber = o == null ? "NA" : o.OrderNumber};

Atente para o **into x** e logo após o **x.DefaultIfEmpty()**.


