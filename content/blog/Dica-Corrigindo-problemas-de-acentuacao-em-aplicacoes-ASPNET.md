
---
title: "Dica: Corrigindo problemas de acentuação em aplicações ASP.NET"
date: 2005-10-02T19:15:00+08:00
lastmod: 2009-05-27T22:24:31+08:00
draft: false
categories: []
tags: ["asp.net", "dicas", ]
---


Muitas vezes, encontramos problemas no desenvolvimento de aplicações ASP.NET relacionados à  exibição incorreta de letras acentuadas ou na formatação de datas e/ou valores monetários. Isso acontece porque as configurações regionais do servidor estão configuradas com a cultura/idioma diferente do que a aplicação realmente necessita, que no nosso caso é o Português do Brasil. Para resolver este problema, basta acrescentar a seguinte linha no arquivo de configuração web.config:  

 <globalization requestEncoding="iso-8859-1" responseEncoding="iso-8859-1" culture="pt-BR"/>   
Este código faz com que a aplicação utilize a cultura brasileira em vez da que está definida nas configurações regionais do servidor.  

Se você quiser saber mais sobre como funcionam as codificações de caracteres (ASCII, Unicode, etc), sugiro ler o seguinte artigo (muito bem humorado, por sinal):

[The Absolute Minimum Every Software Developer Absolutely, Positively Must Know About Unicode and Character Sets (No Excuses!)](http://www.joelonsoftware.com/articles/Unicode.html)  

Ricardo Oneda.

