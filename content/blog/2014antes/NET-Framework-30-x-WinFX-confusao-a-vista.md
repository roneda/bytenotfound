
---
title: ".NET Framework 3.0 x WinFX: confusão à vista?"
date: 2006-06-12T01:25:00+08:00
lastmod: 2009-06-20T15:12:44+08:00
draft: false
categories: []
tags: [".net framework", "linguagens de programação", ]
---


Li no [blog do Alfred](http://thespoke.net/blogs/alfred_myers/archive/2006/06/10/netfx30.aspx) que a Microsoft decidiu [rebatizar o WinFX](http://blogs.msdn.com/somasegar/archive/2006/06/09/624300.aspx), nova API do Windows, para .NET Framework 3.0. Um dos motivos da mudança seria o fato de muita gente não saber exatamente o que era o WinFX, pensando que seria uma tecnologia à parte ou concorrente do .NET Framework. Lendo o blog de Jason Zander, *General Manger* do .NET Framework, encontrei algumas [perguntas e respostas](http://blogs.msdn.com/jasonz/archive/2006/06/09/624629.aspx) interessantes sobre o assunto:

*1.  What version of the compilers are being used?  
.NET FX 3.0 is built on .NET FX 2.0 including the CLR and BCL.  This means you will be using the 2.0 C# and VB compilers from the redist when using .NET FX 3.0.*

Ou seja, apesar da versão do .NET Framework ser chamada de 3.0, os compiladores das linguagens, a CLR (*Common Language Runtime*) e a BCL (*Base Class Library*), serão os da versão 2.0. Assim, pode-se concluir que o .NET Framework 3.0 vai ser, nada mais, do que o .NET Framework 2.0 com suporte a algumas novas tecnologias como *Windows Presentation Foundation* - WPF  (antigo *Avalon*), *Window Communication Foundation* - WCF (antigo *Indigo*) e *Windows Workflow Foundation*. Em outras palavras, utilizaremos o C# 2.0 e o VB.NET 2.0 no .NET Framework 3.0

*2.  Will .NET FX 3.0 contain LINQ support?  
No.  LINQ support is in the Orcas product which is shipping after .NET FX 3.0 (which ships in Vista).*

Agora a coisa ficou confusa de vez: segundo a resposta acima, não haverá suporte ao [LINQ](http://msdn.microsoft.com/data/ref/linq/) no .NET Framework 3.0. O mesmo só será feito a partir do Visual Studio codenome *Orcas*, que é a próxima versão do Visual Studio, a ser entregue após o lançamento do .NET Framework 3.0, ou seja, o LINQ será suportado somente na versão 4.0 do .NET Framework (se é que ela vai ser chamada assim). Entretanto, se dermos uma olhada no site do [LINQ](http://msdn.microsoft.com/data/ref/linq/) ou no de [futuras versões do C#](http://code.msdn.microsoft.com/csharpfuture), perceberemos que a versão do C# que terá suporte ao LINQ já está sendo chamada de 3.0. Mas como não haverá uma versão 3.0 do C# no .NET Framework 3.0, isso quer dizer que o C# 3.0 fará parte do .NET Framework 4.0 (ou seja lá como ele for chamado no lançamento do *Orcas*)?

Se o que eu escrevi acima realmente acontecer, ou seja, versões de linguagens diferentes da versão do Framework, aí sim teremos confusão. Já que o .NET Framework 3.0 utilizará no seu núcleo o .NET Framework 2.0, poderiam chamá-lo de .NET Framework 2.1. Ou então, seguir o exemplo do [IE 7 para o Windows Vista](/blog/post/2006/05/25/Internet-Explorer-7-para-Windows-Vista.aspx): chamá-lo de .NET Framwork 2.0+ ![Tongue out](http://localhost/blog/editors/tiny_mce3/plugins/emotions/img/smiley-tongue-out.gif "Tongue out")

Ricardo Oneda.

