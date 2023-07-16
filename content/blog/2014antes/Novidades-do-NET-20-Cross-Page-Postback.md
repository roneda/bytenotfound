
---
title: "Novidades do .NET 2.0: Cross-Page Postback"
date: 2005-11-08T00:30:00+08:00
lastmod: 2009-05-29T02:42:44+08:00
draft: false
categories: []
tags: [".net framework", "asp.net", ]
---


Na minha opinião, uma das grandes limitações do ASP.NET 1.X era a incapacidade de se fazer um post para outra página de forma simples. Existiam formas de se contornar tal limitação, como o uso de Response.Redirect() ou do Server.Transfer(), mas exigia um certo trabalho. No ASP.NET 2.0 essa limitação foi extinta graças a introdução da propriedade *PostBackUrl*. Basta configurar esta propriedade em algum controle que gera um post (como um botão) fornecendo o nome da página de destino e pronto. Caso ela não seja configurada, o post é feito para a própria página.

O conteúdo da página anterior pode ser acessado através da propriedade *PreviousPage* da classe *Page*, que também possui a nova propriedade *IsCrossPagePostBack*, que tem função semelhante à propriedade *IsPostBack*, velha conhecida do ASP.NET 1.X.

Referências:

[Cross-Page Posting in ASP.NET Web Pages](http://msdn.microsoft.com/en-us/library/ms178139(vs.80).aspx)  
[Design Considerations for Cross Page Post Backs in ASP.NET 2.0](http://odetocode.com/Articles/421.aspx)

Ricardo Oneda

