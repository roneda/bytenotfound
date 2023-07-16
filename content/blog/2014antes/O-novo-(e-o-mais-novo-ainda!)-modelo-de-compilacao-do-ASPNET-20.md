
---
title: "O novo (e o mais novo ainda!) modelo de compilação do ASP.NET 2.0"
date: 2005-12-15T18:49:00+08:00
lastmod: 2009-05-29T03:43:18+08:00
draft: false
categories: []
tags: ["asp.net", "visual studio", ]
---


Sem dúvida, uma das mudanças do ASP.NET 2.0 que mais causou impacto foi no [modelo de compilação](/blog/post/2005/11/03/Novidades-do-NET-20-mudancas-na-infra-estrutura-do-ASPNET-20.aspx). Para aqueles acostumados com o modelo do ASP.NET 1.X e que estão confusos sobre o novo modelo, sugiro a leitura do artigo [Codebehind and Compilation in ASP.NET 2.0](http://msdn.microsoft.com/msdnmag/issues/06/01/ExtremeASPNET/), publicado na [MSDN Magazine americana](http://msdn.microsoft.com/msdnmag/default.aspx).

Aliás, esta alteração deve ter sido tão polêmica, que já estão planejando um [novo modelo de projeto Web para o Visual Studio 2005](http://weblogs.asp.net/scottgu/archive/2005/12/07/432630.aspx) (e olha que ele acabou de ser lançado!). Neste novo modelo, o funcionamento será semelhante ao que tínhamos no ASP.NET 1.X/Visual Studio 2003, ou seja, ao compilarmos a aplicação, será gerada uma única DLL, entre outras "novidades". Este novo tipo de projeto será disponibilizado gratuitamente para download e será "incorporado" pelo Visual Studio 2005.

Se você está com dúvidas em relação a migração de aplicações ASP.NET 1.X para ASP.NET 2.0, sugiro a leitura dos seguintes artigos:

[Step-By-Step Guide to Converting Web Projects from Visual Studio .NET 2002/2003 to Visual Studio 2005](http://msdn.microsoft.com/asp.net/default.aspx?pull=/library/en-us/dnaspp/html/webprojectsvs05.asp)  
[Common Web Project Conversion Issues and Solutions](http://msdn.microsoft.com/asp.net/default.aspx?pull=/library/en-us/dnaspp/html/conversionissuesasp_net.asp)  
[The Great Migration](http://odetocode.com/Blogs/scott/archive/2005/12/04/2573.aspx)

<span style="color: #ff0000;">**Atualizado em 19/12**</span>  
Já está disponível para [download](http://webproject.scottgu.com/) um *preview *do novo modelo de projeto Web para o Visual Studio 2005. Após instalá-lo, no momento de criar um novo projeto, você poderá escolher entre o *template* "ASP.NET Web Site" (o padrão do Visual Studio 2005) ou "ASP.NET Web Application" (o novo modelo que é parecido com o antigo do Visual Studio 2003). Este preview não é suportado pelo Visual Web Developer Express.

Ricardo Oneda

