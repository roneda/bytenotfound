
---
title: "jQuery e ASP.NET"
date: 2008-09-29T13:34:00+08:00
lastmod: 2010-06-10T22:23:06+08:00
draft: false
categories: []
tags: ["asp.net", "javascript", ]
---


Não sei quanto a vocês, mas para mim, uma das coisas mais chatas que existem é escrever código *javascript* para rodar em páginas web. Pode ser que esse trauma tenha surgido quanto tive meus primeiros contatos com o desenvolvimento de aplicações web, nos [primórdios da Internet](/blog/post/2007/10/06/10-anos-de-Internet.aspx "primórdios da internet"). Eram vários os problemas: faltava um ambiente de desenvolvimento decente (Notepad na cabeça), havia dificuldades em debugar o código, muitos dos códigos não funcionavam da maneira esperada em todos os browsers, isso sem falar na complexidade em se fazer coisas que deveriam ser simples, o que acarretava em falta de produtividade.

Muita coisa mudou de lá para cá: o Visual Studio melhorou muito o suporte a *javascript* (além disso, surgiram outros editores como o [Aptana Studio](http://www.aptana.com/)), o processo de *debug* foi facilitado (inclusive, no [Internet Explorer 8](/blog/post/2008/03/20/OnedaCast-1-Internet-Explorer-8-Beta-1.aspx "Internet Explorer 8") será possível debugar código *javascript*; isso sem falar no [Firebug](https://addons.mozilla.org/en-US/firefox/addon/1843 "Firebug"), uma extensão para Firefox que já existe há muito tempo e é uma mão na roda para os desenvolvedores web) e até a interoperabilidade entre os browsers melhorou (um pouco, mas melhorou). Mesmo com essa evolução, até hoje, eu sinto calafrios quando ouço falar em fazer algo muito complexo em *javascript*.

Nos últimos tempos, com a onda da Web 2.0 e do AJAX, surgiram muitas bibliotecas para facilitar e aumentar a produtividade no desenvolvimento de código *javascript*. Entre as mais famosas, posso citar o [Dojo](http://dojotoolkit.org/), [Prototype](http://www.prototypejs.org/), [Ext JS](http://extjs.com/), [Script.aculo.us](http://script.aculo.us/), [Yahoo! UI Library](http://developer.yahoo.com/yui/) e [jQuery](http://jquery.com/). A grande vantagem do uso dessas bibliotecas é que elas abstraem muitos aspectos de baixo nível (como por exemplo, fazer um tratamento específico para determinada versão de browser), permitindo que nosso foco esteja na resolução do problema e não em detalhes que não deveriam consumir nosso tempo.

Assim, é com bons olhos que vejo o [anúncio da Microsoft em adotar o jQuery](http://weblogs.asp.net/scottgu/archive/2008/09/28/jquery-and-microsoft.aspx), que é *open-source*, no ASP.NET. Para quê reinventar a roda quando já há uma biblioteca elogiada e consagrada? Meu palpite é que o principal beneficiado dessa integração seja o [ASP.NET MVC Framework](http://www.linhadecodigo.com.br/Artigo.aspx?id=1634), pois nesse modelo, o desenvolvedor tem muito mais contato com HTML/HTTP e o uso de *javascript* é mais explícito e intensivo, o que normalmente não ocorre com o modelo *WebForms*. Isso não quer dizer que quem desenvolve utilizando *WebForms* não poderá se beneficiar, afinal de contas, apesar de nesse modelo de desenvolvimento o ASP.NET fazer o trabalho sujo pelo desenvolvedor, [o resultado final gerado ainda é HTML e muitas coisas só são possíveis com *javascript*](/blog/post/2005/03/28/ASPNET-x-JavaScript.aspx "ASP.NET x JavaScript").

