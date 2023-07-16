
---
title: "Dica: Diminuindo o tempo de carregamento de uma página web através do download paralelo de arquivos"
date: 2011-11-22T21:06:00+08:00
lastmod: 2011-11-22T21:18:56+08:00
draft: false
categories: []
tags: ["dicas", "html", "browsers", "javascript", "performance", ]
---


Na semana passada, o Cleber Dantas publicou em seu blog um *post* com uma dica bem interessante sobre o uso de [cookie-free domains](http://www.cleberdantas.com/2011/11/cuidado-com-os-cookies-cookie-free-domains/ "Cuidado com os Cookies, use cookie-free domains"). Basicamente, a idéia é armazenar arquivos estáticos do site, como imagens, arquivos CSS e JavaScript, que não precisam ter acesso aos *cookies,* em um subdomínio diferente do site principal. Assim, quando o *browser* fizer as requisições desses arquivos, os *cookies* não serão trafegados e, consequentemente, economizaremos no consumo de banda de rede, tornando o processo mais rápido.

Além da vantagem citada no artigo do Cleber, essa abordagem possibilita outro ganho, que é paralelizar o *download* de arquivos que compõem uma página HTML, tornando seu carregamento mais rápido. O protocolo HTTP 1.1 especifica que os *browsers* devem permitir duas conexões concorrentes por *hostname*, no máximo. Ou seja, segundo a especificação, os *browsers* só poderiam fazer *download* de dois arquivos simultaneamente de um mesmo *hostname*. Apesar dessa especificação, a maioria dos *browsers* mais recentes estabelece [valores padrões maiores para o número máximo de conexões](http://www.browserscope.org/?category=network) e podem ser configurados para outros valores. De qualquer modo, existe um limite. Como uma página HTML normalmente é composta por mais arquivos (considere os arquivos de imagem, CSS, JavaScript, etc), se essa página e todos os recursos que a compõem estiverem em um mesmo *hostname*, quando se atinge esse limite de requisições simultâneas, o *browser* enfilera as requisições pendentes até que alguma requisição executada anteriormente termine, e assim possa realizar as demais requisições de forma sequencial.

Ao distribuirmos os arquivos estáticos em múltiplos subdomínios, o limite de conexões simultâneas do *browser* será aplicado a cada subdomínio, ou seja, se antes uma página e seus elementos ficavam armazenados em somente um *hostname* e o *browser* limitava a N conexões simultâneas, com o uso dessa técnica o número de requisições possíveis simultâneas passa a ser N multiplicado pelo número de subdomínios utilizados. Isso torna possível que mais arquivos sejam baixados em paralelo pelo browser, diminuindo assim a fila de requisições de arquivos e o tempo para carregamento da página e de todos seus recursos.

Apesar do ganho poder ser grande, deve-se tomar cuidado com o uso exagerado de subdomínios, pois múltiplas conexões concorrentes aumentam o uso de CPU pelo *browser*, além de ser necessário estabelecer uma conexão TCP com cada subdomínio e resolver seu nome por DNS, o que pode causar o efeito oposto ao desejado, ou seja, fazer com que a página demore mais para carregar. O número ideal depende de vários fatores e características do site, mas estudos mostram que um número entre 2 e 4 subdomínios é o indicado. Mais informações sobre os ganhos e cuidados com o uso dessa abordagem podem ser encontradas nos links de referência a seguir:

*   [Parallelize downloads across hostnames](http://code.google.com/speed/page-speed/docs/rtt.html#ParallelizeDownloads "Parallelize downloads across hostnames")
*   [Optimizing Page Load Time](http://www.die.net/musings/page_load_time/ "Optimizing Page Load Time")
*   [Performance Research, Part 4: Maximizing Parallel Downloads in the Carpool Lane](http://yuiblog.com/blog/2007/04/11/performance-research-part-4/ "Performance Research, Part 4: Maximizing Parallel Downloads in the Carpool Lane")
*   [Circumventing browser connection limits for fun and profit](http://www.ajaxperformance.com/2006/12/18/circumventing-browser-connection-limits-for-fun-and-profit/ "Circumventing browser connection limits for fun and profit")


