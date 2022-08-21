
---
title: "Sua aplicação web está preparada para o Internet Explorer ActiveX Update?"
date: 2006-03-28T00:59:00+08:00
lastmod: 2009-05-29T22:29:16+08:00
draft: false
categories: []
tags: ["browsers", "microsoft", ]
---


A Microsoft lançou uma [atualização](http://support.microsoft.com/kb/912945/en-us) que altera a maneira que o Internet Explorer lida com controles ActiveX, como Flash, Adobe Reader, Windows Media Player, applets Java, etc, que são carregados pelas *tags* APPLET, EMBED e OBJECT. Após a instalação do update, a interação do usuário com esses controles ficará desativada até que que eles sejam habilitados manualmente. Ou seja, o usuário terá que habilitar cada controle ActiveX da página, um a um, cada vez que acessar o site. Não preciso nem dizer que isso pode causar um certo transtorno, né?

Para evitar essa intervenção manual do usuário (que pode se tornar uma chatice), existem algumas recomendações na maneira como os controles ActiveX são carregados, que os desenvolvedores Web devem seguir. Mais detalhes podem ser encontrados no artigo [Activating ActiveX Controls](http://msdn.microsoft.com/en-us/library/ms537508.aspx).

Essa atualização é resultado de um [processo judicial](http://www.windowsitpro.com/Articles/Index.cfm?ArticleID=40468&DisplayTab=Article) do caso de quebra de patentes envolvendo a Microsoft e a empresa [Eolas](http://www.eolas.com/home.html) e está disponível como download opcional do Windows Update desde o dia 28/02/06. Entretanto, no próximo dia 11 de Abril, ela se tornará um download obrigatório. Assim, os efeitos serão sentidos com maior intensidade a partir desta data.

Ricardo Oneda.

