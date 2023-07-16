
---
title: "Novidades do .NET 2.0: Classes Partial"
date: 2005-11-02T01:00:00+08:00
lastmod: 2009-05-28T23:41:17+08:00
draft: false
categories: []
tags: ["linguagens de programação", ".net framework", ]
---


No .NET 2.0, foi introduzido o conceito de classes parciais (*partial*). Isso significa que a definição de uma classe pode ser dividida em vários arquivos distintos. Esta característica pode ser útil em projetos grandes, onde vários desenvolvedores trabalham sobre a mesma classe, ou então na alteração de código gerado automaticamente - por exemplo, nos *proxys* gerados para acesso a Web Services - pois assim o código pode ser gerado novamente e não se tem que fazer as alterações outra vez, já que as customizações estarão em outro arquivo. Isso sem falar que todo novo modelo de código do ASP.NET 2.0 utiliza classes *partial*.

Referências:

[Create Elegant Code with Anonymous Methods, Iterators, and Partial Classes](http://msdn.microsoft.com/en-us/magazine/cc163682.aspx)  
[Partial Class Definitions](http://msdn2.microsoft.com/en-us/library/wa80x488.aspx)  

Ricardo Oneda

