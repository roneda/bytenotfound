
---
title: "Dica: Filtro de extensões de arquivos para upload"
date: 2007-02-21T01:17:00+08:00
lastmod: 2009-06-20T15:17:21+08:00
draft: false
categories: []
tags: ["dicas", "javascript", ]
---


Uma dúvida que aparece freqüentemente nos [fóruns do MSDN Brasil](http://forums.microsoft.com/MSDN-BR/default.aspx?SiteID=21 "Fóruns de discussão do MSDN Brasil") é sobre como restringir o upload a determinados tipos de arquivos. A idéia é que, por exemplo, se uma aplicação web disponibiliza a funcionalidade de upload de imagens, não se deveria deixar que fosse feito o upload de um arquivo com extensão .doc.

Podemos fazer essa verificação no servidor. O problema desta abordagem é que uma requisição deve ser feita ao servidor web para que este possa fazer a validação. O ideal seria fazer essa restrição no momento em que o usuário está escolhendo o arquivo, ainda no lado cliente da aplicação.

Apesar da especificação do HTML do W3C [prever o atributo **accept**](http://www.w3.org/TR/html4/interact/forms.html#adef-accept), que especifica uma lista de tipos permitidos para upload de arquivos, parece que nenhum browser implementou essa característica. Pesquisando na Internet, encontrei um [código javascript](http://javascript.internet.com/forms/upload-filter.html "Upload Filter") que permite especificar as extensões de arquivos permitidas para upload. Caso o arquivo escolhido não possua uma das extensões informadas, uma mensagem de aviso é exibida e o upload não é feito.

Algumas observações sobre o script: ele não limita a escolha de arquivo às extensões pré-definidas. Ou seja, na caixa de diálogo para escolha do arquivo, pode-se escolher qualquer um. A consistência é feita somente no momento em que o formulário for submetido ao servidor. Outra ponto que deve ser notado é que, por se tratar de um script que roda no lado cliente da aplicação, não se deve confiar totalmente nele, pois pode ser burlado. Assim, é importante que a validação também seja feita no servidor. Por último, nada impediria que alguém renomeasse um arquivo qualquer para uma das extensões permitidas, mesmo que a nova extensão não tivesse nada a ver com o conteúdo do arquivo.

Também sugiro ler uma [FAQ](http://www.faqts.com/knowledge_base/index.phtml/fid/177) que encontrei, com as principais dúvidas relativas a upload de arquivos em aplicações web.

