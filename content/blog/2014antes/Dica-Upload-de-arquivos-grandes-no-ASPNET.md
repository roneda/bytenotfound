
---
title: "Dica: Upload de arquivos grandes no ASP.NET"
date: 2005-02-18T05:29:00+08:00
lastmod: 2009-05-26T00:52:25+08:00
draft: false
categories: []
tags: ["dicas", "asp.net", ]
---


O ASP.NET limita o tamanho de arquivos para upload em até 4096 KB (ou 4 MB). Para aumentar este limite, devemos incluir o elemento **<httpRuntime>** da seguinte maneira no arquivo** web.config** da aplicação:

<configuration>
   <system.web>
      <httpRuntime  maxRequestLength="8192"/>
       ...


O valor do atributo **maxRequestLength** indica o tamanho máximo do arquivo em KB. Caso se deseje alterar este valor para todas as aplicações do servidor, o parâmetro deverá ser alterado no arquivo **machine.config**  

Ricardo Oneda.

