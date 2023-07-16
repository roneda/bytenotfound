
---
title: "Aplicações web ricas e interativas somente com AJAX? Reveja seus conceitos com o WPF/E"
date: 2006-12-06T14:55:00+08:00
lastmod: 2009-06-20T01:16:19+08:00
draft: false
categories: []
tags: ["ajax", "asp.net", "ria", ]
---


Se você acha que uma melhor experiência do usuário e interatividade em aplicações ASP.NET, ou uma aplicação web qualquer, só são plenamente atingidas com o uso de técnicas AJAX, então é porque você não conhece o WPF/E. Isso é até natural, já que o CTP - *Community Technology Preview* - acabou de ser lançado no dia 04/12 :smiley:

O ASP.NET AJAX, que ainda nem teve sua versão final lançada - [está no beta 1](/blog/post/2006/10/22/ASPNET-AJAX-Beta-1.aspx), foi só o começo e já adquire ares de coisa do passado. O WPF/E - sigla para *Windows Presentation Foundation Everywhere* - é o codinome da tecnologia Microsoft para o desenvolvimento de aplicações web ricas e interativas, através do uso de vetores gráficos, animações e outros recursos multimídia. Como seu nome indica, ele é um subconjunto do WPF, tecnologia responsável pela parte de *User Interface* - UI - no .NET 3.0/Windows Vista, e utiliza o XAML (*eXtensible Application Markup Language*) como linguagem de definição de interface (uma espécie de HTML turbinado).

Para utilizar uma aplicação que faz uso do WPF/E, é necessário instalar um *plug-in* (cujo tamanho é de aproximadamente 1 MB) para que o browser consiga interpretar o conteúdo XAML. Mas não pense que a utilização do WPF/E ficará restrita aos usuários do Windows ou do Internet Explorer. Já existe uma versão do plug-in para Macintosh, e também suporte aos browsers Firefox e Safari. Ainda não há uma versão do plug-in para Linux, mas levando-se em conta o anúncio do [acordo entre Novell e Microsoft para promover a integração entre as duas plataformas](http://news.zdnet.com/2100-3513_22-6132119.html "Microsoft makes Linux pact with Novell"), feito há algumas semanas, não será surpresa se ela for anunciada no futuro.

A notícia é boa também para os desenvolvedores, já que, através de HTML e JavaScript, será possível acessar e manipular o conteúdo WPF/E. Além disso, ele também se integrará totalmente com a arquitetura do ASP.NET (inclusive fazendo uso do ASP.NET AJAX, mas sendo possível a utilização de qualquer outro framework AJAX), reaproveitando os conhecimentos anteriormente adquiridos pelos desenvolvedores, além da integração com as ferramentas Visual Studio (e linguagens já conhecidas como C# e VB.NET) e, no caso dos designers, o [Expression Studio](http://www.microsoft.com/expression), para a criação de código XAML.

Muitos já estão chamando o WPF/E de "Flash Killer", uma alusão ao fato de que essa nova tecnologia é um concorrente direto do Flash, da Macromedia/Adobe. A grande vantagem, a meu ver, é a integração com tecnologias já existentes, o que não obriga o desenvolvedor a aprender uma arquitetura ou linguagem totalmente nova, como acontece com o Flash. Seguem alguns links úteis para se aprofundar no assunto:

[Announcing the release of the first "WPF/E" CTP](http://weblogs.asp.net/scottgu/archive/2006/12/04/announcing-the-release-of-the-first-wpf-e-ctp.aspx)

[Getting Started with "WPF/E" (Code Name)](http://go.microsoft.com/fwlink/?linkid=78580&clcid=0x409)

["WPF/E" (Code Name) Architecture Overview](http://go.microsoft.com/fwlink/?linkid=78578&clcid=0x409)

["WPF/E" Downloads](http://msdn2.microsoft.com/bb187452)

["WPF/E" FAQ](http://msdn2.microsoft.com/bb187438)

[Documentação e White Papers](http://msdn2.microsoft.com/bb187448)

