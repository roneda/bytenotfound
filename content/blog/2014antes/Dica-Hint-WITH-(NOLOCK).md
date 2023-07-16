
---
title: "Dica: Hint WITH (NOLOCK)"
date: 2005-09-22T03:03:00+08:00
lastmod: 2009-05-27T22:15:20+08:00
draft: false
categories: []
tags: ["dicas", "sql server", ]
---


<div> </div>
<div>O SQL Server 2000 dá suporte a uma série de hints que podem ser utilizadas para sobrepor o nível de isolamento da transação atual. Apesar do Query Optmizer fazer automaticamente a escolha do tipo de lock a ser aplicado na query, às vezes pode ser interessante termos controle sobre este tipo de configuração. A hint WITH (NOLOCK) permite melhorar o desempenho de uma consulta, pois, quando ela é utilizada, não é aplicado nenhum shared lock e os exclusive locks das outras transações são ignorados.</div>
<div> </div>
<div>Abaixo segue um exemplo de utilização da hint WITH (NOLOCK), utilizando-se o banco de dados de exemplo Pubs:</div>


SELECT au_lname FROM authors WITH (NOLOCK)


<div> </div>
<div>
<div>Note que quando essa hint for utilizada, é possível que ocorra a leitura de dados de uma transação que ainda não foi concluída, as chamadas Dirty Reads. Assim, seu uso não é recomendável nos casos em que a exatidão e precisão da consulta forem importantes. Nos demais casos, ela pode ser utilizada, já que seu uso evita o gasto de recursos que normalmente é envolvido no gerenciamento de locks.</div>
<div> </div>
<div>Ricardo Oneda.</div>
</div>

