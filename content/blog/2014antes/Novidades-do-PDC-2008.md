
---
title: "Novidades do PDC 2008"
date: 2008-11-09T19:05:00+08:00
lastmod: 2009-07-08T02:00:30+08:00
draft: false
categories: []
tags: [".net framework", "visual studio", "windows", ]
---


O [PDC 2008](http://www.microsoftpdc.com/) aconteceu no final de outubro. Não estive lá, mas tentei acompanhar o evento a distância, principalmente lendo blogs e sites de notícias. Os vídeos das apresentações também estão disponíveis gratuitamente para [download](http://channel9.msdn.com/pdc2008/), mas confesso que ainda não consegui assiti-los. Segue um pequeno resumo daquilo que li - não espere nada muito detalhado; os comentários a seguir são baseados na primeira impressão que tive sobre os principais assuntos abordados:

[Windows Azure](http://www.microsoft.com/azure/windowsazure.mspx): foi o grande lançamento e assunto do evento (eu achava que seria o [Windows 7](/blog/post/2008/10/12/Windows-7.aspx)). Foi definido como o sistema operacional da Microsoft para a computação em nuvem. Percebi que essa definição causou muita confusão. É bom deixar claro alguns pontos: o Windows Azure não vai ser a próxima versão do Windows e nem estará disponível para ser comprado e instalado em casa ou nas empresas. Além disso, não substituirá a instalação do Windows ou algum outro sistema operacional nos computadores. A melhor definição que li sobre o Windows Azure foi a do blog [Negócio de Risco](http://blogs.technet.com/risco/archive/2008/10/29/como-assim-um-sistema-operacional-na-nuvem.aspx), da Microsoft Brasil:

*"Nos últimos dois anos a Microsoft trabalhou para montar um super-computador, formado por centenas de milhares de CPUs operando conjuntamente e conectados a terabytes de memória e petabytes de armazenamento. Esta estrutura toda está fisicamente espalhados por quase uma dezena de datacenters mas opera como uma única e gigantesca máquina, talvez a maior existente no mundo. O Windows Azure é o sistema operacional que roda nesta máquina.*

*Em termos conceituais o Windows Azure faz as mesmas funções que qualquer outro sistema operacional. Ele gerencia a alocação dos recursos da máquina, intermedia o acesso ao hardware, oferece aos desenvolvedores uma plataforma que permita a eles escrever aplicações para a máquina, gerentia a comunicação entre as aplicações, cuida da interface com o usuário,  etc. A diferença fundamental entre o Windows Azure e os outros Windows é que ele não roda no seu PC e sim no super-computador da Microsoft."* 

![](/img/2008/azure.jpg) 

Resumidamente, o Windows Azure é o sistema operacional que controlará uma espécie de serviço de *hosting* a ser oferecido pela Microsoft. Teoricamente faz sentido que essa infra-estrutura não fique com a empresa que contrata esse tipo serviço. As empresas estão preocupadas com seus negócios, e não com parafernálias técnicas. Entretanto, na prática, não sei se as coisas funcionam assim. Há ainda pontos importantes a serem analisados, principalmente os referentes à disponibilidade, privacidade e segurança.

**Windows 7**: acabou sendo ofuscado pelo Windows Azure e também porque não trouxe nada de [revolucionário](http://blogs.zdnet.com/Bott/?p=575) (aliás, como já era previsto). A Microsoft adotou a política de fazer melhorias no que já se tem ao invés de entupir o sistema operacional com funcionalidades que muitas vezes nem são utilizadas - e que podem causar mais dor de cabeça do que benefícios. Os avanços do Windows 7 parecem ter se concentrados em campos como usabilidade, diminuição do tempo de *boot* e número de serviços carregados por padrão, redução no consumo de memória, melhorias no consumo de baterias de notebook, além de suporte a *multi-touch*. Como podem notar, foram focados aspectos básicos, o que, na minha opinião, está corretíssimo. Na maior parte das vezes, menos é mais. Segundo relatos, o sistema parece estar mais leve, tanto que será possível instalá-lo em [netbooks](http://en.wikipedia.org/wiki/Netbook), aqueles computadores ultra-portáteis, móveis e de baixo custo que se tornaram a coqueluche do momento e que basicamente são utilizados para acesso a Internet e escrita de textos (o que, para muita gente, é mais do que suficiente). Outra novidade é que arquivos do tipo VHD (*Virtual Hard Disk*) serão reconhecidos automaticamente, ou seja, não será necessário instalar o Virtual PC para rodar máquinas virtuais. A primeira versão beta do Windows 7 será lançada em dezembro de 2008 ou janeiro de 2009. A versão final está prevista para início de 2010, mas muitos já comentam que poderá ser antecipada para o final de 2009, já que final de ano é uma época em que muitos computadores são vendidos e o novo sistema operacional poderia ser um estímulo para aumentar as vendas (ainda mais em tempos de crise).

**Web Office**: sim, depois de muito tempo e especulação, a Microsoft finalmente apresentou uma primeira versão do Office para a web. Com ela, será possível utilizar uma versão mais enxuta do Word, Excel, PowerPoint e OneNote através de qualquer browser. Resta saber qual será o modelo de negócios a ser adotado, pois a Microsoft não vai querer canibalizar a suíte Office, que é a maior fonte de receitas da empresa juntamente com o Windows.

**Visual Studio 2010 e .NET 4.0**: durante o evento, foi liberada a versão CTP do [Visual Studio 2010 e .NET Framework 4.0](http://go.microsoft.com/fwlink/?LinkId=129231). Entre as novidades, está o maior suporte ao desenvolvimento de aplicações para aproveitar a arquitetura *multicore* dos computadores atuais - *Parallel Computing*. Um ponto que me chamou a atenção é que algumas funcionalidades do Visual Studio 2010 serão feitas com WPF (se eu não me engano, o WPF também será utilizado em alguns lugares do Widows 7). Acho que o fato da própria Microsoft começar a utilizar essa tecnologia em seus produtos (já não era tempo!) pode ajudar a aumentar a adoção da mesma pelo mercado, já que este terá mais confiança em apostar em algo novo.

![](/img/2008/vs2010.jpg) 

O que mais me impressiona, e até certo ponto me deixa um pouco frustrado, é que nem acabamos de digerir completamente as novidades do Visual Studio 2008 (e não se esqueçam do [Service Pack 1](/blog/post/2008/08/11/Visual-Studio-2008-e-NET-Framework-35-Service-Pack-1.aspx)), e uma nova versão já está no horizonte. Eu mesmo já escrevi sobre isso [algumas](/blog/post/2005/02/09/A-insanidade-das-atualizacoes-tecnologicas.aspx) [vezes](/blog/post/2007/07/11/Data-de-lancamento-do-Visual-Studio-2008.aspx), e percebo que [outras](http://blogs.windowsclient.net/sameh/archive/2008/09/30/visual-studio-2010-and-net-framework-4-0-announced.aspx) [pessoas](http://silverlight.net/blogs/jesseliberty/archive/2008/10/23/so-much-technology-so-little-time.aspx) também têm a mesma sensação. Vejam um exemplo de desabafo:

*"I think we will be lusting our breaths for a long time with the .NET technologies, it's just a few weeks since the .NET 3.5 SP1 release and here they are announcing the 4.0 version. Although, it is a good thing to have more and more technologies that makes your life easier, but I think that we will spend the rest of our life just learning the .NET technologies without having the chance to use it."* 

Pois é, tenho a mesma sensação de que ficaremos loucos se tentarmos estudar tudo o que está sendo lançado. E tenho a impressão de que a velocidade tende a aumentar...

Ricardo Oneda.

