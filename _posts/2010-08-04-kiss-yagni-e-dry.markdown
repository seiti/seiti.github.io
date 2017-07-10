---
layout: post
title: KISS, YAGNI e DRY
date: '2010-08-04 20:43:09'
---


Hoje fui lembrado de algo importante, que…, hmm.., bem…, às vezes é esquecido: o **desenvolvedor** deve *entregar software*.

E acho que não sou só eu que devo ser lembrado disto, pois há até um [site cujo propósito é lembrar isto](http://agilemanifesto.org/) (bom,  existe [site para tudo](http://sadtrombone.com/), mas enfim…).

Como não poderia deixar de ser nesta área, existem alguns acrônimos e lemas que te auxiliam nesta tarefa tão importante, que é entregar um software de valor e respeito no prazo. **KISS**, **YAGNI** e **DRY**.

Comecemos pelo mais simpático:


## *KISS – Keep It Simple, Stupid*

Mantenha simples. A simplicidade facilita o entendimento. O que é simples é fácil de usar, de manipular. É fácil de explicar. Mas isto não quer dizer que a simplicidade como objetivo é algo simples. Complexo?

A simplicidade, a elegância são características que necessitam de experiência, de criatividade para serem alcançadas. Usando um  exemplo já surrado , o iPhone. Simples. Elegante. Lembra-se dos smartphones antes dele? Pois então. E o que fazer? Estudar, compreender, testar e inventar. E depois ver se sua mãe compreendeu seu invento.


## *YAGNI – You Ain’t Gonna Need It*

Não implemente *nada*, a não ser que seja *necessário* para seu produto. Não produza o que não será usado. Senão será mais trabalho no momento de criar e no momento de dar manutenção.

Entra a questão: e o que realmente é necessário? Pergunta difícil. Se perguntar ao cliente o que é necessário, você terá de criar o *Facebook*.  A resposta requer experiência e análise fundamentada do problema em questão. Entra novamente um pouco de senso estético. [Elegância](http://www.brainyquote.com/quotes/quotes/e/edsgerdijk204339.html). Descreva as *features*. Elimine todas quanto possível.  Tire qualquer uma em que restem dúvidas.  Depois de criar este conjunto mínimo, escolha uma *feature* para jogar fora. Aí, talvez, sobre uma lista contendo apenas o que é necessário.

Mas sejamos pragmáticos também. A aplicação de YAGNI deve levar em conta também o custo de implementação. Se é barato fazer agora e barato depois, deixe para depois. Se é barato agora, mas ficará caríssimo depois, faça agora. Este conhecimento, de novo, requer prática e experiência.


## *DRY – Don’t Repeat Yourself*

Uma regra, uma especificidade (repita em voz alta, comendo paçoca Amor), um pedaço do conhecimento deve estar declarada, escrita, de forma clara, em um único ponto do sistema.

Pode ser fácil. Ou bem difícil. Depende do tamanho. Do tamanho do produto e da equipe.  É muito comum equipes grandes de desenvolvimento escreverem diversas soluções para o mesmo problema, sem um ter conhecimento da solução do outro.

Já ouvi que isso ocorre em alguns lugares entre equipes de departamentos distintos, que são muito “ciosos” de seu código…

O fato é que é preciso que o sistema seja claro o suficiente e que os desenvolvedores se comuniquem de maneira eficiente para a aplicação do DRY. Como fazer isso? Seria uma boa perguntar ao Fred Brooks.


## Disk-sistema entregas rápidas

E o que isto tudo significa? Significa a prática da **Programação Zen**. *O melhor código é o não-código*. Executar isso difícil. Requer perseverança e auto-controle. Exerçamos a [melhor qualidade de um programador](http://seiti.eti.br/blog/?p=276). Mantenha o sistema limpo, enxuto, conciso. Não crie, não produza a mais. Menos *features*, menos código, menos trabalho, menos tempo gasto. Talvez até dê para cumprir aquele prazo….


