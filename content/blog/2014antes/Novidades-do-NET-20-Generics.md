
---
title: "Novidades do .NET 2.0: Generics"
date: 2005-11-01T01:40:00+08:00
lastmod: 2009-05-28T23:38:34+08:00
draft: false
categories: []
tags: ["linguagens de programação", ".net framework", ]
---


Apesar da Microsoft já ter liberado o download da versão final do Visual Studio 2005/.NET Framework 2.0/SQL Server 2005 para os [assinantes do MSDN](http://msdn.microsoft.com/subscriptions/), o lançamento oficial dos novos produtos só ocorrerá em 07 de novembro, ou seja, semana que vem. Nestes dias que antecedem o lançamento oficial, pretendo escrever sobre algumas novidades que as novas versões dos produtos nos trazem. Por novidades eu quero dizer desde algo "revolucionário" até a introdução de uma simples propriedade que tenha trazido algum benefício. É claro que eu não tenho a pretensão de citar todas as novidades do .NET 2.0 e muito menos fazer uma lista das melhores. Encarem isso apenas como uma pequena lista de novidades, na qual apresentarei uma pequena introdução ao assunto, de forma resumida, e links, nos quais se pode aprofundar sobre o tema. O primeiro assunto é:

Generics

Generics são uma novidade do .NET 2.0 que nos permitem criar classes, métodos ou outra estrutura de dados de forma genérica, ou seja, independentes de um tipo de dados. Os Generics nos proporcionam reusabilidade de código, tipagem forte de dados (type safe) e melhora na performance, já que não é necessário fazer o boxing/unboxing na conversão de dados, permitindo criar coleções genéricas de um determinado tipo de dado. Por exemplo, antes dos Generics, poderíamos usar um ArrayList para guardar objetos, mas não havia garantia de que o ArrayList contivesse somente um determinado tipo de objeto, o que poderia causar erros em tempo de execução na hora de fazer a conversão. Com os Generics, podemos definir que uma coleção irá conter somente objetos de um tipo específico, e caso essa regra seja quebrada, haverá um erro de compilação.

Referências:

[An Introduction to C# Generics](http://msdn.microsoft.com/library/default.asp?url=/library/en-us/dnvs05/html/csharp_generics.asp)  
[Introducing Generics in the CLR](http://msdn.microsoft.com/en-us/magazine/cc164094.aspx)  
[More on Generics in the CLR](http://msdn.microsoft.com/en-us/magazine/cc164081.aspx)  
[Generics (C#)](http://msdn2.microsoft.com/en-us/library/512aeb7t.aspx)  
[Generics FAQ: Fundamentals](http://msdn.microsoft.com/en-us/library/aa479859.aspx)  
[Generics FAQ: .NET Framework](http://msdn.microsoft.com/netframework/default.aspx?pull=/library/en-us/dndotnet/html/NetFramework.asp)  
[Generics FAQ: Tool Support](http://msdn.microsoft.com/netframework/default.aspx?pull=/library/en-us/dndotnet/html/ToolSupport.asp)  
[Generics FAQ: Best Practices](http://msdn.microsoft.com/en-us/library/aa479858.aspx)  

Ricardo Oneda

