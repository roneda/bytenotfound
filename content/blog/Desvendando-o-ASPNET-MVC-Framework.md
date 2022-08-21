
---
title: "Desvendando o ASP.NET MVC Framework"
date: 2008-01-13T19:30:00+08:00
lastmod: 2009-07-10T21:35:45+08:00
draft: false
categories: []
tags: ["artigos", "asp.net", "mvc", ]
---


O [Linha de Código](http://www.linhadecodigo.com.br/) publicou um artigo que escrevi chamado "[ASP.NET 3.5 Extensions: Desvendando o ASP.NET MVC Framework](http://www.linhadecodigo.com.br/Artigo.aspx?id=1634 "ASP.NET 3.5 Extensions: Desvendando o ASP.NET MVC Framework")". Ao contrário do [artigo anterior](/blog/post/2007/12/05/Consideracoes-iniciais-sobre-o-ASPNET-MVC-Framework.aspx), no qual foram apresentados aspectos mais conceituais, pois na época o ASP.NET MVC Framework ainda não estava disponível publicamente, neste novo artigo a abordagem é prática.

É apresentado como funciona o mecanismo de mapeamento de URLs do MVC Framework (que não referencia mais páginas, mas sim, classes - os *controllers*), como implementar esses *controllers* e passar dados para as *views*, além de algumas alternativas para renderizá-las (inclusive, utilizando alguns *extension methods* do MVC Toolkit). Durante o artigo, é desenvolvido um exemplo simples de leitor de *feeds* RSS utilizando o ASP.NET MVC Framework. Esse leitor armazena os dados dos *feeds* em um arquivo XML (que é manipulado através de classes do *model* utilizando *LINQ to XML*) e consulta as últimas atualizações de maneira on-line. Você pode fazer o [download](/files/2009%2f7%2fExemploMvcApplication.zip) do código-fonte do exemplo e analisar seu funcionamento.

Como o artigo foi escrito utilizando-se a versão CTP do ASP.NET MVC Framework, as informações apresentadas estão sujeitas a alterações até o lançamento da versão definitiva. Sugestões e críticas são sempre bem-vindas. Espero que gostem!

[](/files/2009%2f7%2fExemploMvcApplication.zip)

[ExemploMvcApplication.zip (86,60 kb)](/files/2009%2f7%2fExemploMvcApplication.zip)

