
---
title: "Correção de vulnerabilidade do ASP.NET que permitia ataques de negação de serviço"
date: 2012-01-02T17:27:00+08:00
lastmod: 2012-01-02T20:41:40+08:00
draft: false
categories: []
tags: ["segurança", "asp.net", ".net framework", ]
---


Nos últimos dias de 2011, a Microsoft lançou um comunicado e, posteriormente, a correção de uma vulnerabilidade presente em todas versões do ASP.NET que poderia permitir ataques do tipo *Denial of Service* (DoS), ou negação de serviço. Essa vulnerabilidade permitia que uma requisição HTTP especialmente montada consumisse 100% da CPU durante um período de tempo, fazendo com que repetidas requisições degradassem a performance da aplicação, causando a indisponibilidade do serviço.

A causa da vulnerabilidade está na forma como o ASP.NET mapeia os valores de campos de formulários recebidos em um POST HTTP para estruturas do tipo *hash tables*, que poderia causar problemas de colisões de chaves *hash*. A correção disponibilizada pela Microsoft limita a 1.000 o número de campos de formulários que uma aplicação ASP.NET pode receber. Se a requisição possuir mais de 1.000 campos de formulários, ocorrerá um erro. Esse número máximo pode ser alterado através da propriedade **MaxHttpCollectionKeys**, a ser configurada no web.config. A recomendação é que a atualização seja aplicada o mais rápido possível. É interessante notar que esse problema não é exclusividade do ASP.NET. Outros *frameworks web* e linguagens como PHP, Java, Phyton e Ruby também estão sucetíveis a esse tipo de ataque. Mais informações nos links abaixo:

*   [More information about the December 2011 ASP.Net vulnerability](http://blogs.technet.com/b/srd/archive/2011/12/27/more-information-about-the-december-2011-asp-net-vulnerability.aspx "More information about the December 2011 ASP.Net vulnerability")
*   [ASP.NET Security Update Shipping Thursday, Dec 29th](http://weblogs.asp.net/scottgu/archive/2011/12/28/asp-net-security-update-shipping-thursday-dec-29th.aspx "ASP.NET Security Update Shipping Thursday, Dec 29th")
*   [Microsoft Security Bulletin MS11-100 - Critical](http://technet.microsoft.com/en-us/security/bulletin/ms11-100.mspx "Microsoft Security Bulletin MS11-100 - Critical")
*   [Has the hash DoS patch been installed on your site? Check it right now with ASafaWeb! ](http://www.troyhunt.com/2011/12/has-hash-dos-patch-been-installed-on.html "Has the hash DoS patch been installed on your site? Check it right now with ASafaWeb!")
*   [ASP.NET, MS11-100, and POST](http://stackoverflow.com/questions/8684049/asp-net-ms11-100-and-post "ASP.NET, MS11-100, and POST")
*   [An ASP.NET request that has lots of form keys, files, or JSON payload fails with an exception and returns a 500 HTTP status code](http://support.microsoft.com/kb/2661403 "An ASP.NET request that has lots of form keys, files, or JSON payload fails with an exception and returns a 500 HTTP status code")
*   [Hashes Used by PHP, ASP.NET, Java, Python and Ruby Vulnerable to DoS Attacks](http://news.softpedia.com/news/Hashes-Used-by-PHP-ASP-NET-Java-Python-and-Ruby-Vulnerable-to-DoS-Attacks-243594.shtml "Hashes Used by PHP, ASP.NET, Java, Python and Ruby Vulnerable to DoS Attacks")
*   [Effective DoS attacks against Web Application Plattforms – #hashDoS](https://cryptanalysis.eu/blog/2011/12/28/effective-dos-attacks-against-web-application-plattforms-hashdos/ "Effective DoS attacks against Web Application Plattforms – #hashDoS")


