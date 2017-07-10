---
layout: post
title: 'HttpPostedFile: IE versus Firefox'
date: '2009-05-17 09:17:09'
tags:
- aspnet
- bug
---


Estou aqui programando, feliz da vida, e me enviam um bug para matar.

Ao subir um arquivo em nosso sistema Asp.NET surge o erro:

"The given path's format is not supported."

ou

"Não há suporte para o formato do caminho dado." (maldita MS por traduzir mensagens de erro)

Mas eu não conseguia reproduzir o problema de nenhuma maneira. Até testar no Internet Explorer. O método que utilizo para gravar o arquivo é este:

public string Grava(HttpPostedFile postedFile, string id) { string newfilename = id + postedFile.FileName; string fullName = DirPath + newfilename; postedFile.SaveAs(fullName); return fullName; }

A chamada é realizada assim, onde fupAnexo é um controle **FileUpload**:

string path = anexo.Grava(fupAnexo.PostedFile, guid.ToString());

O problema está nesta propriedade: **postedFile.FileName**. O conteúdo dela depende de qual navegador é utilizado pelo usuário.

No IE o conteúdo é o caminho completo do arquivo no computador do usuário: *C:\\Pasta\\Pasta\\Macarrao\\arquivo.xis*.

No Firefox apenas o nome do arquivo: *arquivo.xis*.

O framework deveria uniformizar o acesso aos recursos do sistema, mas aprendo cada vez mais que não dá para confiar em dados vindos do usuário **nem do sistema**. Não confie em nada.

Acertei o método para o que segue:

public string Grava(HttpPostedFile postedFile, string id) { string[] filename = postedFile.FileName.Split('\\'); string newfilename = id + filename[filename.Count() - 1]; string fullName = DirPath + newfilename; postedFile.SaveAs(fullName); return fullName; }

Falta testar o caso em que o usuário acessa o sistema a partir do Linux (ou Mac OSX) usando o Internet Explorer. Mas acho que não existam tantos loucos por aí.


