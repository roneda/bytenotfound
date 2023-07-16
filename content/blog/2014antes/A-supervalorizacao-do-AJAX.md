
---
title: "A supervalorização do AJAX"
date: 2006-01-29T22:57:00+08:00
lastmod: 2009-05-29T21:31:58+08:00
draft: false
categories: []
tags: ["divagações", "ajax", ]
---


Se você não esteve em Marte no último ano, então já deve ter ouvido falar sobre [AJAX](http://www.adaptivepath.com/publications/essays/archives/000385.php) (Asynchronous JavaScript and XML), que também atende pelos nomes de [Remote Scripting ou Script Callback](http://www.eggheadcafe.com/articles/20050709.asp), uma técnica de desenvolvimento de aplicações Web que permite, basicamente, que uma página faça requisições ao servidor Web via JavaScript, sem a necessidade de atualizar a página inteira, o que pode tornar uma aplicação web mais rica, rápida, interativa e dinâmica para o usuário, deixando-a mais parecida com uma aplicação desktop, o que proporciona uma melhor usabilidade.

Mas qual o segredo do AJAX? Bem, não há segredo algum. Ele utiliza tecnologias que já estão por aí há um bom tempo, como JavaScript, DHTML, XML e [XMLHttpRequest](http://developer.apple.com/internet/webcontent/xmlhttpreq.html), responsável pelo envio e recebimento de dados do servidor. Na verdade, nem o uso de XMLHttpRequest é necessário, já que poderíamos obter um resultado parecido utilizando-se [iframes](http://developer.apple.com/internet/webcontent/iframe.html). Como se vê, são tecnologias que qualquer desenvolvedor web que se preze conhece (ou pelo menos deveria conhecer). Assim, AJAX é mais uma arquitetura do que uma novidade.

Então, por que tanta badalação em torno desta sigla? Ao meu ver, são dois os principais motivos: o primeiro é que agora todos os browsers mais recentes (IE, FireFox, Netscape, Opera, Konqueror, Safari, etc) de todas plataformas (Windows, Unix, Mac, etc) suportam a utilização do objeto XMLHttpRequest, que originalmente foi criado pela Microsoft como um componente ActiveX e que, antigamente, era exclusivo do IE. Aliás, a Microsoft [anunciou recentemente](http://blogs.msdn.com/ie/archive/2006/01/23/516393.aspx) que, a partir do IE 7.0, o objeto XMLHttpRequest será exposto como um objeto de script nativo, ou seja, não será mais um controle ActiveX, o que tornará o IE mais compatível com os outros browsers. O segundo motivo é a utilização maciça que o Google vem fazendo em seus produtos (como o [Google Maps](http://maps.google.com/), [GMail](http://gmail.google.com/) e [Google Suggest](http://www.google.com/webhp?complete=1&hl=en), entre outros), que deu uma visibilidade grande para a técnica.

O grande problema que vejo quando há muito *hype* em torno de alguma tecnologia nova é que a coisa foge do controle e logo começa a aparecer muita besteira sobre o assunto. Com o AJAX não poderia ser diferente e já se vê por aí o efeito negativo da superexposição. Um exemplo disso é a matéria publicada neste mês na [Info Exame](http://www.infoexame.com.br/) (sobre a qual já escrevi minha opinião em outro [post](/blog/post/2005/02/07/Porque-a-Info-nao-e-uma-boa-revista.aspx)), que tem o Google como matéria de capa, e cujo o título é "AJAX dá dinheiro?". A conclusão da matéria é que o AJAX ainda não é uma mina de dinheiro, mas é possível ganhar, em média, entre e 20% e 25% a mais ou, segundo um funcionário de uma consultoria, o profissional que domina o AJAX pode até mesmo dobrar seu salário! Além disso, 2006 deve deixar o mercado aquecido para os conhecedores do AJAX. E lá se vão as ovelhinhas aprender a última moda...

Percebam aí que há uma combinação explosiva: um assunto da moda, uma publicação cuja credibilidade é duvidosa, pessoas desinformadas e pronto! A besteira está feita! Será que alguém realmente acredita que o fato de "saber" AJAX (que utiliza tecnologias que um desenvolvedor web já domina há um bom tempo) irá trazer milhares de propostas de emprego e rios de dinheiro? E as empresas que procuram por especialistas em AJAX, será que realmente sabem o que essa sigla significa e sabem o que querem ou somente estão seguindo um modismo e depois de algum tempo irão perceber o quanto foram ignorantes? E as consultorias, ao invés de ajudarem seus clientes a entender o que tudo isso significa, não estariam interessadas na ignorância dos mesmos para que assim consigam "vender" mais consultores e ganhar mais dinheiro? Tudo termina da seguinte maneira: a empresa finge que sabe o que quer e se sente moderna por "estar utilizando" uma tecnologia da moda e o profissional finge que conhece e todos vivem felizes... e assim caminha a humanidade.

Não estou criticando o AJAX, e acho que o mesmo tem o seu valor e muitas das idéias que ele traz, de fato, irão contribuir para melhorar a experiência do usuário em relação às aplicações web. O que me deixa preocupado é quantidade de pessoas que não sabem o que falam.

Ricardo Oneda.

