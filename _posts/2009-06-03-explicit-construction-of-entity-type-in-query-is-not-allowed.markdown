---
layout: post
title: Explicit construction of entity type '###' in query is not allowed
date: '2009-06-03 01:44:38'
tags:
- linq
- linq-to-sql
---


Estava eu programando, feliz da vida, quando percebi subitamente que felicidade e programação não se misturam muito bem. Surge então esta mensagem de erro:

> A construção explícita do tipo de entidade ‘###’ na consulta não é permitida.

ou, em bom inglês *Google friendly*:

> Explicit construction of entity type ‘###’ in query is not allowed

O código que gerou a mensagem pouco agradável foi este:

var res = from m in MyDataContext.INSCRICAOs group m by m.PESSOA into p select new MAILING() { idMailingTexto = idMailingTexto, nomPessoa = p.First().PESSOA.nomPessoa, eMail = p.First().PESSOA.eMail, flaEnviado = false, };

Minha intenção é de, a partir de dados extraídos da tabela *INSCRICAO*, criar entradas na tabela *MAILING*, usando o Linq To SQL (sem sermões sobre formas normais em banco de dados, por favor). Mas o Linq **não deixa** eu criar estes objetos MAILING, não a partir de uma consulta do próprio Linq.

O problema, que descobri ser um *feature *(como se traduz isto para o português?) parece [ser antigo](http://social.msdn.microsoft.com/Forums/en-US/linqprojectgeneral/thread/1ce25da3-44c6-407d-8395-4c146930004b?prof=required), e a resposta é esta:

> This check was added because it was supposed to be there from the beginning and was missing.  Constructing entity instances manually as a projection pollutes the cache with potentially malformed objects, leading to confused programmers and lots of bug reports for us. In addition, it is ambiguous whether projected entities should be in the cache or changed tracked at all. The usage pattern for entities is that they are created outside of queries and inserted into tables via the DataContext and then later retrieved via queries, never created by queries.

Para mim isto é nivelar por baixo, mas enfim. O jeito foi criar um objeto idêntico ao existente, que chamei de MAILINGCLONE:

 public class MAILINGCLONE { public int idMailingTexto { get; set; } public string nomPessoa { get; set; } public string eMail { get; set; } public bool flaEnviado { get; set; } public DateTime datAtualiza { get; set; } }

E trocar a consulta para:

var res = from m in MyDataContext.INSCRICAOs group m by m.PESSOA into p select new MAILINGCLONE() { idMailingTexto = idMailingTexto, nomPessoa = p.First().PESSOA.nomPessoa, eMail = p.First().PESSOA.eMail, flaEnviado = false };

Isto até que não doeu. O que dói no coração é trocar isto:

 dc.MAILINGs.InsertAllOnSubmit(mails); dc.SubmitChanges();

por isto:

 foreach (MAILINGCLONE mc in mails) { MAILING m = new MAILING() { idMailingTexto = mc.idMailingTexto, nomPessoa = mc.nomPessoa, eMail = mc.eMail, flaEnviado = mc.flaEnviado, codPessoa = mc.codPessoa, datAtualiza = DateTime.Now }; dc.MAILINGs.InsertOnSubmit(m); } dc.SubmitChanges();


