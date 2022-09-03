---
title: "Migrando o blog para Hugo"
date: 2022-09-03T16:59:25-03:00
draft: false
tags: ["blog", "hugo"]
---

Como eu disse no [post anterior]({{< relref "/blog/2022/reativando-o-blog.md" >}} "Reativando o blog"), essa é a quarta versão do meu blog. Meu [primeiro post]({{< relref "/blog/Apresentacao.md" >}} "Apresentação") foi em 2005, no theSpoke.net, que era uma plataforma da Microsoft. 

Em 2006, [migrei para um domínio "próprio"]({{< relref "/blog/blog-novo-vida-nova.md" >}} "Blog novo, vida nova"). Coloco entre aspas pois eu não era o dono, já que meu blog ficava hospedado no [MVPs.org](https://mvps.org/), que era um espaço mantido por alguns MVPs da Microsoft e fornecido gratuitamente para MVPs. Lá, cada um era responsável por criar seu próprio site e manter as ferramentas que quisesse usar. Comecei usando o Community Server como base do meu blog, já que era uma plataforma relativamente conhecida pois era a mesma que a Microsoft utilizava em seus blogs. Depois, migrei para o [BlogEngine.NET](https://blogengine.io/), que era mais leve e simples, e o utilizei desde então. 

Tanto o Community Server quanto o BlogEngine.NET podem ser considerados Sistemas de Gerenciamento de Conteúdo (CMS - Content Management System) tradicionais, semelhantes ao [WordPress](https://wordpress.com/). Nesse modelo, há um software que é executado no servidor e que é utilizado tanto para a criação do conteúdo (no meu caso, publicação de posts no blog) quanto para servir o conteúdo. Geralmente, o conteúdo fica armazenado em um banco de dados, apesar de que no caso do BlogEngine.NET o conteúdo fica armazenado em arquivos XML gravados no servidor. Quando alguém acessa o site, a página é gerada dinamicamente pelo CMS com base nas configurações e no conteúdo armazenado (no banco de dados ou em arquivos em disco).

Esse modelo de CMS tradicional tem algumas características: exige processamento no servidor (o que aumenta o tempo para carregar a página e também aumenta o custo da solução) e é necessário dedicar um certo esforço na manutenção, já que o software precisa ser atualizado e ser mantido seguro. Isso pode valer a pena para sites que sejam dinâmicos e que mudem de acordo com a pessoa que está acessando. Mas para sites simples e com conteúdos que são os mesmos para todo mundo que acessa (como é o caso de um blog), essas características são desvantagens.

É aí que entram os Geradores de Sites Estáticos (SSG - Static Site Generator). Os SSGs são ferramentas que geram as páginas de um site previamente. Dessa forma, ao acessar o site, todo o seu conteúdo já está lá pronto para ser consumido, não sendo necessário que cada página seja gerada dinamicamente no servidor, no momento do acesso. Fazendo uma analogia com o desenvolvimento de software, é como se houvesse uma etapa de "compilação" do site, na qual os templates (as partes que são comuns no site e que definem a formatação do conteúdo) são mesclados com as configurações e com os conteúdos propriamente ditos, tendo como resultado final páginas HTML, imagens, arquivos Javascript e CSS. Isso traz uma série de vantagens em relação ao modelo de CMS tradicional:

* O site fica mais leve, pois as páginas estão prontas para serem acessadas, não há necessidade de serem processadas e geradas dinamicamente. Isso deixa o acesso mais rápido
* Não é mais preciso ter uma aplicação CMS rodando em um servidor e nem um banco de dados. Um simples servidor web é suficiente. E na verdade, nem é preciso ter um servidor, se o site ficar hospedado em um bucket S3, por exemplo
* Por não haver necessidade de ter uma aplicação rodando no servidor, a solução fica mais barata e a manutenção fica bastante simplificada
* A segurança também aumenta, pois a superfície de ataque diminui consideravelmente, já que o conteúdo é estático e não há aplicação no servidor com risco de bugs

Outra vantagem é que o conteúdo do site pode ser tratado como código, como se fosse uma aplicação. Ele pode ser armazenado em um repositório git (o desse blog está em um [repositório no GitHub](https://github.com/roneda/bytenotfound)) e passar por um processo de build e deploy, com testes e validações, como se fosse uma aplicação. 


{{< figure src="/img/2022/hugo-logo.svg" alt="Logo do Hugo" >}}


Existem vários [geradores de sites estáticos](https://jamstack.org/generators/) disponíveis. O que estou utilizando nesse blog é o [Hugo](https://gohugo.io/). A migração para ele foi relativamente simples. Como eu tinha um backup do meu blog anterior baseado no BlogEngine.NET, só foi necessário converter o conteúdo para [Markdown](https://pt.wikipedia.org/wiki/Markdown), que é o formato utilizado pelo Hugo. Felizmente, existe uma ferrramenta chamada [BlogML to Hugo](https://github.com/jijiechen/BlogML2Hugo) que faz exatamente isso. Como o BlogEngine.NET suporta o formato [BlogML](https://en.wikipedia.org/wiki/BlogML), bastou exportar o conteúdo para esse formato, fazer alguns ajustes na forma como [imagens são referenciadas para se adequadar ao modelo do Hugo](https://brianpeek.com/migrating-blogengine-net-to-ghost/), executar a ferramenta para gerar os arquivos Markdown e copiá-los para a pasta de conteúdo na estrutura de pastas do Hugo. Criar um site com Hugo também é muito simples. Seguindo [os passos da documentação oficial](https://gohugo.io/getting-started/quick-start/) você já tem um site funcional. Depois é só fazer os ajustes, escolher um tema mais adequado e aplicar as configurações que faça sentido.

Para hospedar meu blog, estou utilizando a [Netlify](https://www.netlify.com/), que é uma empresa que oferece uma plataforma para desenvolvimento e hospedagem de sites através de uma CDN - Content Delivery Network, com várias funcionalidades, como processo de build e deploy automatizado a partir de um commit no repositório do GitHub, certificado digital gratuito integrado com [Let's Encrypt](https://letsencrypt.org/pt-br/) e possiblidade de uso de domínio próprio. Tudo isso no plano gratuito. O único custo que tenho é do registro do domínio. 

Além da Netlify, existem outras opções gratuitas para hospedagem de sites estáticos, sendo as mais conhecidas o  [GitHub Pages](https://pages.github.com/) e [Azure Static Web Apps](https://docs.microsoft.com/en-us/azure/static-web-apps/overview).

Dessa forma, consegui um bom ponto de equilíbrio entre ter o controle do conteúdo (não dependendo de uma plataforma para criar e publicar o conteúdo), um baixo esforço de manutenção (não precisando me importar com instalação e atualização de aplicações em servidores) e com baixo custo.