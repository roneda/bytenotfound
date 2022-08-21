
---
title: "Tech-Ed Brasil 2007"
date: 2007-12-09T19:27:00+08:00
lastmod: 2009-06-24T01:29:02+08:00
draft: false
categories: []
tags: ["eventos", "microsoft", ]
---


Neste ano, infelizmente, não pude ir a todos os dias do Tech-Ed Brasil (mas já foi melhor que o ano passado, quando não estive presente em nenhum dia). Só pude comparecer na sexta-feira, dia 07 de dezembro, último dia do evento. A seguir, um breve resumo do que assisti:

**Deep Dive no ASP.NET**: nessa apresentação, [Israel Aéce](http://www.israelaece.com/) mostrou algumas funcionalidades mais avançadas que estão disponíveis desde o ASP.NET 2.0 e que quase não são abordadas em palestras do assunto (e que poucas pessoas conhecem). Destaque para o [Client-Side Callbacks](http://www.linhadecodigo.com.br/Artigo.aspx?id=909), [páginas assíncronas](http://www.linhadecodigo.com.br/Artigo.aspx?id=831) (que apesar de não apresentar diferenças para o usuário final, pode melhorar a performance do lado servidor da aplicação), Control Adapters (que permitem customizar a renderização gerada pelos controles do ASP.NET, semelhante ao [CSS Control Adapters](http://www.asp.net/CSSAdapters/WhitePaper.aspx)), [Virtual Path Providers](http://support.microsoft.com/kb/910441) (um mecanismo para armazenar os arquivos e conteúdo de uma aplicação ASP.NET em um repositório diferente do sistema de arquivos, como por exemplo, em um banco de dados) e [Substitution Cache](http://weblogs.asp.net/scottgu/archive/2006/11/28/tip-trick-implement-donut-caching-with-the-asp-net-2-0-output-cache-substitution-feature.aspx) (define uma região dentro da área armazenada em cache que deve ser sempre atualizada).

**Programando com Microsoft Windows Communication Foundation**: não gostei muito desta palestra. Foram apresentados alguns conceitos básicos do WCF e SOA, e como desenvolver um serviço nessa plataforma. O problema é que muito código estava em *slides* e programação mesmo vimos pouca, apesar do título da palestra. Além disso, parece que essa apresentação era um tipo de segunda parte de uma outra palestra feita na quinta-feira, portanto, eu estava me sentindo um pouco perdido.

**Silverlight - Por uma web mais rica**: [Cezar Guimarães](http://blogs.msdn.com/cguimar/default.aspx) nos deu uma pequena amostra do que já é possível fazer com o Silverlight 1.0 no desenvolvimento de *Rich Internet Applications - RIA*. Nessa versão, o foco está em multimídia e javascript, muito javascript. Agora as atenções passam a se voltar para a versão 2.0 (antigamente chamada de 1.1), que vai permitir a execução de código .NET no browser do usuário e está prevista para ser lançada em 2008.

**ASP.NET AJAX - Otimizando e Estendendo**: o objetivo de [Fernando Cerqueira](http://www.fci.com.br/) foi mostrar os cuidados que devem ser tomados quando desenvolvemos aplicações AJAX no ASP.NET. Não basta simplesmente colocar um [UpdatePanel](http://ajax.asp.net/docs/overview/UpdatePanelOverview.aspx) na página e jogar todos os controles dentro dele, afinal, mesmo usando AJAX, as requisições ao servidor continuam sendo feitas por "debaixo dos panos". Assim, o uso de vários UpdatePanels e, em um cenário mais avançado, restringir o tráfego somente aos dados utilizando o formato [JSON](http://json.org/) pode contribuir significativamente para diminuir a quantidade de *bytes* trocada entre o servidor web e o browser. Para quem não conhece, a ferramenta utilizada para mostrar o que é trafegado entre o browser e o servidor web é o [Web Development Helper](http://projects.nikhilk.net/Projects/WebDevHelper.aspx).

Gostaria de ter assistido a outras paletras, como **Internet Information Services 7 para Desenvolvedores** e [ADO.NET Entity Framework](http://msdn2.microsoft.com/en-us/library/aa697427(VS.80).aspx), mas como elas aconteceram na quinta-feira, não foi possível. De qualquer maneira, foi um bom evento, de grande porte, como tem acontecido com os últimos Tech-Eds, no qual, além de poder aprender um pouco mais, podemos reencontrar os amigos.

