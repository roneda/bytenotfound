
---
title: "Novidades do .NET 2.0: SQL Cache Dependency"
date: 2005-11-11T00:50:00+08:00
lastmod: 2009-05-29T02:47:04+08:00
draft: false
categories: []
tags: [".net framework", "asp.net", "sql server", ]
---


No ASP.NET 1.X, era possível criar dependências para valores armazenados no objeto Cache do namespace System.Web.Caching. A invalidação do Cache poderia ficar associada a vários eventos, como após um determinado período de tempo, mudança em um ou mais arquivos e/ou diretórios ou mudança em um valor de outra chave de cache. Sempre que um desses eventos ocorresse, o cache seria inutilizado. Era possível até mesmo informar um *delegate* que deveria ser chamado quando o evento de invalidação do cache ocorresse.

Uma grande melhoria do ASP.NET 2.0 nesse campo foi a introdução da possibilidade de se criar uma dependência do Cache com o banco de dados SQL Server. Assim, sempre que algum dado for alterado no banco de dados, o cache é invalidado. Deste modo, é possível ter os benefícios de performance que o uso de cache propricia juntamente com dados sempre atualizados.

Referências  
[Improved Caching in ASP.NET 2.0](http://msdn.microsoft.com/asp.net/reference/infrastructure/default.aspx?pull=/library/en-us/dnvs05/html/cachingnt2.asp)  
[SqlCacheDependency Class (System.Web.Caching)](http://msdn.microsoft.com/en-us/library/system.web.caching.sqlcachedependency.aspx)  
[Walkthrough: Using ASP.NET Output Caching with SQL Server](http://msdn.microsoft.com/en-us/library/e3w8402y.aspx)  

Ricardo Oneda

