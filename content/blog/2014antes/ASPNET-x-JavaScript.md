
---
title: "ASP.NET x JavaScript"
date: 2005-03-28T04:19:00+08:00
lastmod: 2009-05-25T22:39:50+08:00
draft: false
categories: []
tags: ["asp.net", "javascript", "linguagens de programação", ]
---


Com o ASP.NET ficou mais fácil e produtivo desenvolver aplicações Web, pois ele já fornece vários controles que antes tínhamos que desenvolver e com os quais gastávamos muito tempo. Além disso, o ASP.NET deixou o processo de se desenvolver uma aplicação web bem mais parecido com o processo de se desenvolver uma aplicação desktop. Isso quer dizer que podemos ignorar o JavaScript e o HTML (ou DHTML), pois só o ASP.NET e o código escrito em linguagem *server-side* é suficiente, certo? Quem pensa assim, não poderia estar mais enganado.  

Apesar das inegáveis facilidades trazidas pelo ASP.NET, não podemos nos esquecer que o resultado do processamento do servidor web que é enviado ao browser ainda é HTML e JavaScript. Isso é o que garante (ou pelo menos deveria garantir) que a aplicação irá funcionar em qualquer browser de qualquer plataforma (Windows, Unix, Mac, etc). O que o ASP.NET faz é esconder o trabalho sujo do desenvolvedor, ou seja, o HTML e JavaScript são gerados automicamente e faz com que muitas vezes nos esqueçamos que eles ainda estão lá.  

Muitas pessoas têm dificuldade (ou até mesmo não querem) em aceitar isso, principalmente aqueles que vieram do desenvolvimento de aplicações desktop e só agora, com o ASP.NET, estão tendo o primeiro contato com desenvolvimento Web.   

Já muitos daqueles que desenvolviam aplicações web antes do ASP.NET reclamam que a integração com o JavaScript ficou mais complicada. Não sei se "complicada" é uma boa definição, mas com certeza é bem diferente da maneira tradicional a qual estávamos acostumados. Mas isso é questão de costume e, depois que nos adaptamos, fica bem mais fácil.  

Vejo muitas pessoas reclamarem que a Microsoft deveria ter mudado isso e ter extinto o JavaScript, além de ter implementado várias outras coisas que só são possíveis com scripts *client-side*, como se dependesse dela ditar estes padrões! Em vez de ficarem esperando tudo e mais um pouco da Microsoft, porque não desenvolver seu próprio controle? Afinal, você pode desenvolver (ou adquirir de terceiros) um controle que atenda as suas necessidades e depois reaproveitá-lo em vários projetos. A plataforma .NET é bem flexível com relação a isso. Ela não te obriga a ficar amarrado ao que é nativo da plataforma.   

Apesar de ser possível desenvolver uma aplicação web em ASP.NET sem ter nenhum conhecimento de HTML e JavaScript, você ficará muito limitado e sua aplicação deixará de ter muitas funcionalidades que só são possíveis através de scripts que rodam no cliente (neste caso, o browser). O exemplo clássico é a manipulação de janelas pop-ups e de frames.  

Abaixo, seguem alguns links que mostram como trabalhar com JavaScript e ASP.NET:  

[Client-Side Script Integration in ASP.NET](http://www.informit.com/articles/article.asp?p=173412&seqNum=1 "Client-Side Script Integration in ASP.NET")  
[Injecting Client-Side Script from an ASP.NET Server Control](http://msdn.microsoft.com/library/default.asp?url=/library/en-us/dnaspp/html/aspnet-injectclientsidesc.asp "Injecting Client-Side Script from an ASP.NET Server Control")  
[Using JavaScript Along with ASP.NET](http://msdn.microsoft.com/library/default.asp?url=/library/en-us/dnaspp/html/aspnet-usingjavascript.asp "Using JavaScript Along with ASP.NET")  

E agora, alguns links que tratam de JavaScript, HTML e DHTML:  

[Dynamic Drive HTML](http://www.dynamicdrive.com/ "Dynamic Drive HTML")  
[HTML Code Tutorial](http://www.htmlcodetutorial.com/ "HTML Code Tutorial")  
[JavaScript Source](http://javascript.internet.com/ "JavaScript Source")  
[Doc JavaScript](http://www.webreference.com/js/ "Doc JavaScript")  

Ricardo Oneda.  

