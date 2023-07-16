
---
title: "Server Controls no ASP.NET MVC Framework"
date: 2008-02-27T01:33:00+08:00
lastmod: 2009-06-28T23:47:53+08:00
draft: false
categories: []
tags: ["asp.net", "mvc", ]
---


Enquanto a atualização do [ASP.NET MVC Framework](http://www.linhadecodigo.com.br/Artigo.aspx?id=1634) não é lançada, temos que conviver com pequenos *bugs* da plataforma (o que é normal e até mesmo esperado, já que estamos falando de uma versão CTP). Os *Server Controls* que dependem da infra-estrutura do modelo de *WebForms* (como *Viewstate* e *Postback*) não são suportados no MVC Framework. Já os *Server Controls* que não dependem dela, como o *Repeater* e o *ListView*, podem ser utilizados. Entretanto, se você adicionar, por exemplo, um *Repeater* a uma *View* e tentar acessá-lo através do *code-behind*, irá notar que o mesmo não será reconhecido. Para corrigir esse bug, basta clicar com o botão direito do mouse sobre a página ASPX e escolher a opção *Convert to Web Application*.

![](/img/2008/MVCbug1.png)

Ao fazer isso, será criado um arquivo com extensão **.designer.cs**, responsável por conter a declaração dos *Server Controls* utilizados na *View*.

![](/img/2008/MVCbug2.png)

Agora é possível acessá-lo normalmente através do *code-behind*.

