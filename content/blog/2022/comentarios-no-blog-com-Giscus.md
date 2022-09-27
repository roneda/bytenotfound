---
title: "Comentários no blog com giscus"
date: 2022-09-27T20:05:56-03:00
draft: false
tags: ["blog", "hugo", "giscus"]
---

Utilizar um gerador de site estático como o [Hugo](https://gohugo.io/), que eu [adotei aqui no blog]({{< relref "/blog/2022/migrando-o-blog-para-Hugo.md" >}} "Migrando do BlogEngine.NET para para Hugo"), trás alguns desafios. Como nesse modelo não existe uma aplicação sendo executada no servidor, já que todas as páginas do site ficam prontas para serem acessadas (por isso se chama site estático!), não há onde armazenar conteúdos dinâmicos, como são os comentários de um blog. Para isso, é necessário utilizar algum serviço separado.

O Hugo trás [suporte nativo](https://gohugo.io/content-management/comments/) ao [Disqus](https://disqus.com/), que é uma plataforma de comentários bem popular. Entretanto, o uso dele implicaria em alguns aspectos que não me deixam confortável, como a exibição de anúncios no plano gratuito, o que também gera preocupações com privacidade.

Analisando as alternativas, acabei descobrindo o [giscus](https://giscus.app/), que é um sistema de comentários baseado no [GitHub Discussions](https://docs.github.com/pt/discussions/collaborating-with-your-community-using-discussions/about-discussions). Assim, todos os comentários do blog ficam armazenados no GitHub. Como o código-fonte do meu blog [também está no GitHub](https://github.com/roneda/bytenotfound), acabou fazendo muito sentido! Cada post no blog tem sua própria "discussão" no GitHub Discussions, com suporte a funcionalidades como respostas e reações. Para comentar, a pessoa só precisa ter uma conta no GitHub e autorizar o uso da aplicação do giscuss em sua conta. Tudo isso sem anúncios ou preocupações com privacidade. Uma solução bem elegante!