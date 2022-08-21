
---
title: "Dica: Melhore a navegação de sua aplicação ASP.NET com o SmartNavigation"
date: 2005-04-22T01:27:00+08:00
lastmod: 2009-05-27T00:38:04+08:00
draft: false
categories: []
tags: ["asp.net", "dicas", ]
---


O ASP.NET possui uma característica chamada **Smart Navigation** que permite uma melhor navegação em sua aplicação Web. Ela possibilita as seguintes melhorias:  

- mantém a posição da página na tela e o foco no controle entre cada *postback*, evitando que a página volte para seu início após o retorno do servidor. Isso é especialmente útil em, por exemplo, páginas grandes de cadastros;  
- evita o efeito da "piscada" da página entre os *postbacks*;  
- impede que cada postback seja salvo na lista de histórico do browser, mantendo somente uma única entrada;  

Para habilitar o Smart Navigation em uma página, basta configurar a propriedade **SmartNavigation** do WebForm para **true**. Caso deseje habilitá-lo em toda sua aplicação, adicione a tag <pages> no arquivo web.config, que deverá ficar parecido com:

<configuration>
    <system.web>
        <pages smartNavigation=”true”/>
        .....
    </system.web>
</configuration>


Mas nem tudo são flores...esta propriedade só funciona para browsers Internet Explorer 5.5 ou superior, e mesmo assim são comuns os relatos de problemas com CSS, entre outros. Mas uma aplicação web deveria rodar em qualquer plataforma, independentemente do browser e, mesmo que houvesse a dependência do browser, não deveria ocorrer erros, certo? Bem, nestes casos, existem algumas alternativas que "simulam" o comportamento da propriedade SmartNavigation através de JavaScript e HTML, que no fundo, é o que o SmartNavigation também faz, só que de forma automática (lembra que eu [disse](/blog/post/2005/03/28/ASPNET-x-JavaScript.aspx "ASP.NET x JavaScript") que ainda é importante saber JavaScript?). Se ficou interessado nestas alternativas, sugiro uma visita nos seguintes endereços:  

[How to persist the scroll position of an ASP.NET page without using SmartNavigation](http://blogs.prenia.com/cathi/PermaLink.aspx?guid=c634ab31-bab6-467e-a838-3790af0b1041 "How to persist the scroll position of an ASP.NET page without using SmartNavigation")  
[Crossbrowser SmartNavigation Alternative](http://www.codeproject.com/aspnet/lili.asp "Crossbrowser SmartNavigation Alternative")  
[Crossbrowser SmartNavigation Alternative II](http://www.codeproject.com/aspnet/lili2.asp "Crossbrowser SmartNavigation Alternative II")  

Ricardo Oneda.

