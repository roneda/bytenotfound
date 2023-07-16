
---
title: "Entendendo os Bookmarklets"
date: 2006-07-06T15:31:00+08:00
lastmod: 2009-06-13T15:43:29+08:00
draft: false
categories: []
tags: ["código", "javascript", "browsers", ]
---


[Bookmarklets](http://www.bookmarklets.com/) são pequenos trechos de código javascript armazenados no Bookmarks, também conhecido como Favoritos no Internet Explorer. Uma vez armazenado, podemos colocar esse atalho em uma barra de ferramentas do browser e acionar o código com um único clique. O conceito, pelo que andei lendo, parece ser antigo, mas só vim a descobri-lo há pouco tempo, e achei a idéia bem interessante. Caso você não saiba, é possível executar código javascript a partir da barra de endereços do browser. Tente copiar o código abaixo na barra de endereços do seu browser, tecle ENTER e veja o alert sendo mostrado:

javascript:(function(){alert('Hello World!'); })()


Agora imagine escrever código que interaja com a página que está sendo exibida ou então que automatize uma determinada tarefa repetitiva. Pesquisei um pouco por aí e achei coisas [bem interessantes](http://www.imilly.com/bm.htm). Por exemplo, um bookmarklet que faz uma pesquisa no Google sem que você tenha que passar pela página inicial:

javascript:q = "" + (window.getSelection ? window.getSelection() : document.getSelection ? document.getSelection() : document.selection.createRange().text); if (!q) q = prompt("Search terms? ... ", ""); if (q!=null) location="http://www.google.com/search?q=" + escape(q).replace(/ /g, "+"); void 0


Talvez você já tenha a barra de ferramentas do Google ou então utilize algum browser que já oferece o campo de busca integrado. Nestes casos, o bookmarklet acima não seria muito útil. Mas se você realiza buscas através do Google limitando o escopo da pesquisa em determinado site, poderia colocar essa configuração em um bookmarklet. O exemplo a seguir realiza uma pesquisa no site KB (Knowledge Base) da Microsoft através do Google:

javascript:q = "" + (window.getSelection ? window.getSelection() : document.getSelection ? document.getSelection() : document.selection.createRange().text); if (!q) q = prompt("Search terms? ... ", ""); if (q!=null) location="http://www.google.com/search?&q=site:support.microsoft.com+" + escape(q).replace(/ /g, "+"); void 0


Aproveitei a idéia e criei um bookmarklet com minha assinatura para os [fóruns do MSDN Brasil](http://forums.microsoft.com/MSDN-BR/default.aspx?SiteID=21). Se você constuma utilizar os fóruns, deve ter percebido que o campo de assinatura não permite código HTML. Entretanto, nada impede que você deixe este campo em branco e coloque, manualmente, sua assinatura, digamos, mais elaborada, em cada post. Isso traz alguns problemas: ou você digita sua assinatura todas as vezes ou então salva-a em um arquivo e, todas as vezes que for postar algo, abre o arquivo, copia o texto e cola. Com o bookmarklet abaixo, eu simplesmente clico no atalho, copio o texto que é mostrado e colo no post:

java script:(function(){var a='<p> </p><hr size="1" />Ricardo Oneda<br /><a href="+unescape(" target="_blank">http://thespoke.net/blogs/oneda/default.aspx </a><p> </p>';prompt("Assinatura",a); })()


Por algum motivo que não pude identificar, não consegui fazer com que a assinatura fosse adicionada automaticamente ao campo de edição da mensagem, sem a necessiadade do copiar e colar, mas mesmo assim, já ajudou. Enfim, as possibilidades são inúmeras.

Ricardo Oneda.

