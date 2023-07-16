
---
title: "Utilizando o ASP.NET MVC Framework com o Visual Web Developer 2008 Express"
date: 2008-02-13T01:11:00+08:00
lastmod: 2009-06-28T23:48:04+08:00
draft: false
categories: []
tags: ["asp.net", "mvc", ]
---


O [ASP.NET MVC Framework](http://www.linhadecodigo.com.br/Artigo.aspx?id=1634) foi projetado para o .NET Framework 3.5, mas você não é obrigado a utilizar a versão comercial do Visual Studio 2008. Se você ficou com vontade de experimentar o novo *framework* mas não tem acesso ao Visual Studio 2008, poderá utilizá-lo com o [Visual Web Developer 2008 Express](http://go.microsoft.com/?linkid=7653519), que é uma versão mais enxuta (e gratuita) do Visual Studio 2008.

É importante levar em consideração que o ASP.NET MVC Framework foi feito utilizando o modelo de projeto *Web Application*. Atualmente, o Visual Web Developer 2008 Express (VWD Express) não suporta este tipo de projeto (ele cria somente projetos do tipo *Web Site*). Portanto, se você simplesmente instalar o ASP.NET MVC Framework e tentar criar um projeto no VWD Express, não irá conseguir. Você tem duas alternativas: a primeira, é adaptar manualmente seu projeto do tipo *Web Site* para utilizar o ASP.NET MVC Framework, como é mostrado [neste post](http://www.lazycoder.com/weblog/index.php/archives/2007/12/10/using-the-aspnet-mvc-framework-with-visual-web-developer-express). A outra maneira, mais rápida e prática, é utilizar um *template* para projetos MVC para o VWD Express, feito por um desenvolvedor independente e que pode ser baixado em [seu site](http://jason.whitehorn.ws/2007/12/10/Using+ASPNET+MVC+From+Visual+Web+Developer+Express+2008.aspx).

Vale lembrar que essas são soluções temporárias, já que o ASP.NET MVC Framework ainda se encontra em versão CTP e o suporte nativo ao VWD Express será adicionado, pela Microsoft, em versões futuras.

