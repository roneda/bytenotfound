
---
title: "Dica: Queries parametrizadas com OLE DB e ODBC .NET Data Providers"
date: 2005-03-08T16:08:00+08:00
lastmod: 2009-05-26T00:47:38+08:00
draft: false
categories: []
tags: ["dicas", "ado.net", ]
---


Uma dúvida muito comum que aparece no [fóruns do MSDN Brasil](http://social.msdn.microsoft.com/Forums/pt-BR/categories "Fórum do MSDN Brasil") é quanto à utilização de parâmetros em queries SQL quando se utiliza o OLE DB ou ODBC .NET Data Providers. Na maioria dos casos, o problema está no fato de que a pessoa não sabe que, ao contrário do SQL Server Data Provider, o OLE DB e o ODBC Data Providers não suportam parâmetros nomeados em uma instrução SQL. Os parâmetros, nestes casos, são representados pelo sinal "**?**" (ponto de interrogação). Assim, uma instrução SQL que com SQL Server Data Provider fosse:

SELECT Nome FROM Clientes WHERE Codigo = @ID AND Cidade = @Cid


No OLE DB ou ODBC .NET Data Providers ficaria assim:

SELECT Nome FROM Clientes WHERE Codigo = ? AND Cidade = ?


Note que no caso de haver mais de um parâmetro no comando SQL, é importante que os parâmetros sejam adicionados ao objeto *Command* na mesma ordem em que aparecem na   
instrução SQL, já que não será possível mapeá-los através de nomes.

Vale lembrar que o SQL Server Data Provider não aceita este tipo de representação de parâmetros por ponto de interrogação.  

Ricardo Oneda.

