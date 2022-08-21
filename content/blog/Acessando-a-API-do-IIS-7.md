
---
title: "Acessando a API do IIS 7"
date: 2006-04-23T01:19:00+08:00
lastmod: 2009-06-09T01:23:09+08:00
draft: false
categories: []
tags: ["iis", "código", ]
---


O Scott Guthrie, do time de produtos Web da Microsoft, escreveu um post bem interessante sobre as [novidades do IIS 7](http://weblogs.asp.net/scottgu/archive/2006/04/20/443513.aspx), que é a versão do servidor Web da Microsoft que virá no Windows Vista e Windows Longhorn Server. Entre as principais características, destaco a utilização de arquivos no estilo do *web.config* para configurar o IIS, uma ferramenta gráfica de administração integrada do IIS e do ASP.NET e ferramentas de linhas de comando e APIs de configuração melhoradas. Veja em alguns exemplos de utilização da nova API como será fácil criar uma aplicação que consiga interagir com o IIS:

// criando um site na porta 8080
ServerManager iisManager = new ServerManager();
iisManager.Sites.Add("NewSite", "http", "*:8080:", "d:\\MySite");
iisManager.Update(); 

// parando um site
ServerManager iisManager = new ServerManager();
iisManager.Sites["NewSite"].Stop(); 


Os exemplos acima foram retirados do [blog do Carlos](http://blogs.msdn.com/carlosag/archive/2006/04/17/MicrosoftWebAdministration.aspx), do time do IIS. 

Ricardo Oneda

