
---
title: "DataSet ou Classe Customizada?"
date: 2006-01-11T01:57:00+08:00
lastmod: 2009-05-29T21:21:02+08:00
draft: false
categories: []
tags: [".net framework", "arquitetura", ]
---


Uma das dúvidas quando se está planejamento a arquitetura de um sistema multicamadas feito em .NET é sobre como fazer a comunicação entre as camadas da aplicação: utilizar DataSet ou desenvolver classes customizadas? A resposta para esta pergunta - e para todas as outras polêmicas como esta - é...depende.

Ambas abordagens tem suas vantagens e desvantagens: enquanto o DataSet pode ser bom pois já traz uma série de características prontas que podem nos poupar tempo, ele também é mais "pesado" já que possui muita coisa que talvez não iremos utilizar. Já a utilização de classes de negócios customizadas traz um maior controle sobre nossa arquitetura, já que podemos otimizá-las de acordo com nossas necessidades, mas o que num primeiro momento pode ser uma vantagem pode se tornar uma desvantagem, já que teremos que desenvolver muita coisa do zero, o que pode consumir um tempo grande do projeto. Outra alternativa que também pode ser considerada é a utilização de DataSet Tipados, que entre suas vantagens está o fato de ser fortemente tipado (ao contrário do DataSet "puro"), mas que também está longe de ser a solução de todos os nossos problemas.

Com o objetivo de ajudar a fazer uma escolha tão complexa quanto essa, sugiro a leitura do artigo [DataSets vs. Collections](http://msdn.microsoft.com/msdnmag/issues/05/08/CuttingEdge/) do mestre [Dino Esposito](http://weblogs.asp.net/despos), no qual ele analisa cada caso e explica em qual situação utilizar cada uma das opções. Do artigo, chamo a atenção para uma [tabela](http://msdn.microsoft.com/msdnmag/issues/05/08/CuttingEdge/default.aspx?fig=true#fig3) comparativa entre as várias possibilidades.

E a seguir alguns outros artigos que podem ajudar a decidir qual o melhor para o seu caso (percebam o quanto o assunto é polêmico):

[On the Way to Mastering ASP.NET: Introducing Custom Entity Classes](http://msdn.microsoft.com/asp.net/default.aspx?pull=/library/en-us/dnaspp/html/CustEntCls.asp)  
[Poor MSDN article on Custom Business Entities and DataSets](http://web.archive.org/web/20070125163217/http://blogs.wdevs.com/angelos/archive/2005/03/10/2685.aspx)  
[Typed DataSets and Business Entities: A Compromise (Part 1)](http://web.archive.org/web/20070103133302/http://blogs.wdevs.com/angelos/archive/2005/03/03/2580.aspx)  
[Typed DataSets and Business Entities: A Compromise (Part 2)](http://web.archive.org/web/20061116025344/http://blogs.wdevs.com/angelos/archive/2005/03/12/2714.aspx)  
[Typed DataSets and Business Entities: A Compromise (Part 3)](http://web.archive.org/web/20061116025121/http://blogs.wdevs.com/angelos/archive/2005/03/23/2851.aspx)

Ricardo Oneda.

