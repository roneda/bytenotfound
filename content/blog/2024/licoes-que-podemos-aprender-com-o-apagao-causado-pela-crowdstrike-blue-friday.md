---
title: "Lições que podemos aprender com o apagão causado pela CrowdStrike (Blue Friday)"
date: 2024-07-21T16:56:02-03:00
draft: true
tags: ["", ]
cover: 
  image: "/img/2024/bsod.png"
---

Na sexta-feira, dia 19/07/2024, aconteceu o que provavelmente é o maior incidente tecnológico da história em termos de abrangência: o apagão causado por uma atualização no software Falcon, da empresa de segurança CrowdStrike, que provocou a famigerada "tela azul da morte" (em inglês, *Blue Screen Of Death - BSOD*) em computadores com Windows ao redor do mundo (*Blue Friday*).

{{< figure src="/img/2024/bsod.png" align="center" alt="Imagem da tela azul da morte do Windows" >}}

Diversos serviços e negócios ficaram indisponíveis, nos mais variados setores, como companhias aéreas e aeroportos, instituições financeiras, serviços de emergência, sistemas de saúde, empresas de telecomunicação, de varejo, etc, gerando transtornos nas vidas de milhões de pessoas. Os impactos sociais e econômicos certamente são de uma escala gigantesca. Nesse momento em que escrevo, muita gente ainda deve estar trabalhando para normalizar a situação, o que deve se estender nos próximos dias. A Microsoft [estima que foram afetados em torno de 8,5 milhões de dispositivos Windows](https://blogs.microsoft.com/blog/2024/07/20/helping-our-customers-through-the-crowdstrike-outage/). Isso é menos de um por cento de todas as máquinas Windows do mundo, mas é um número absoluto muito grande.

Apesar de somente computadores com Windows terem sido afetados dessa vez, [problemas semelhantes haviam ocorrido pouco meses antes com algumas distribuições Linux](https://www.neowin.net/news/crowdstrike-broke-debian-and-rocky-linux-months-ago-but-no-one-noticed/), obviamente sem o mesmo alcance que agora. Isso mostra que esse não foi um caso isolado, parecendo ser algo recorrente, o que gera uma série de questionamentos sobre (a falta de) práticas e testes da CrowdStrike para atualizações de seus softwares. 

Você pode encontrar o pronunciamento oficial da CrowdStrike sobre o incidente e os passos necessários para a correção do problema em [REMEDIATION AND GUIDANCE HUB: FALCON CONTENT UPDATE FOR WINDOWS HOSTS](https://www.crowdstrike.com/falcon-content-update-remediation-and-guidance-hub/).

Podemos aproveitar acontecimentos como esse para refletir um pouco e tirar (ou relembrar) algumas lições importantes.

## Não há somente um único culpado
Incidentes dessa magnitude não são culpa de uma pessoa somente. Claro que alguém programou o código que continha o bug, mas a responsabilidade não é somente dessa pessoa. Entre um código ser escrito e ser distribuído para uso, existe uma série de oportunidades e etapas nas quais problemas como esse deveriam ser identificados antes de serem liberados: revisão de código, ferramentas de análise de código, esteiras de CI/CD, testes dos mais variados tipos, estratégias de deployment progressivo (canary, blue/green, ring, etc), observabilidade, etc. A falha na identificação desse tipo de bug é resultado de um problema estrutural, da organização e da forma como ela opera, que falhou em utilizar práticas de engenharia de software para um componente tão crítico e que não possui os processos adequados. Bugs existem e vão continuar existindo, por melhor que seja o engenheiro de software e por mais bem intencionado que seja. Deve haver mecanismos para impedir ao máximo que esses bugs sejam liberados para produção. E quanto mais crítico o componente, maiores devem ser os cuidados.

## Está tudo interconectado
Que temos uma dependência absurda da tecnologia no nosso dia-a-dia é claro para todos nós. Nossas vidas pessoal e profissional dependem de produtos e serviços tecnológicos e a tendência é que isso só aumente. Mas o que acabamos esquecendo (e que a maioria das pessoas leigas não sabem até que eventos como esse aconteçam), é como essa tecnologia é baseada em uma rede complexa de dependências de componentes críticos que, ao menor sinal de desestabilizção, pode fazer tudo ruir como num castelo de cartas. A figura abaixo representa bem isso:

{{< figure src="/img/2024/dependency.png" align="center" alt="Imagem de um meme mostrando a fragilidade de nossa infraestrutura digital" >}}
Fonte: [Dependency](https://xkcd.com/2347) 

Softwares dependendo de frameworks e bibliotecas, open-source ou proprietários, que dependem de runtimes, que dependem de sistemas operacionais, que podem ser executados em uma infraestrutura de cloud de um outro fornecedor, que dependem de serviços que são acessados através de rede e que nem ao menos sabemos onde estão, que por sua vez dependem de outros e assim sucessivamente. Isso sem falar nas dependências e componentes de hardware. Camadas em cima de camadas, abstrações em cima de outras abstrações formam uma rede intrincada de componentes que ninguém (mesmo que seja profissional de TI) é capaz de mapear por completo e nem de saber a extensão do impacto que a falha em uma dessas peças pode causar.

Às vezes, dá a impressão de que tudo está preso por um barbante e prestes a desmoronar. E o mais incrível mesmo é que tudo isso funciona na maior parte do tempo. Chega a ser quase um "milagre" que um apagão desses não tenha acontecido antes. E algo me diz que esse não será o último.


## Você é responsável pelo seu produto (mesmo que terceiros causem problemas)
Achei curioso a forma como algumas reportagens e boa parte das pessoas em redes sociais se referiram ao problema como sendo de responsabilidade da Microsoft, como se ela tivesse causado e como se ela devesse corrigi-lo. Claro, isso aconteceu porque é o Windows que apresentava a tela azul, então é natural que os usuários e leigos em geral acreditem que esse seja um "problema do Windows". A imagem da Microsoft e do Windows também saiu um pouco arranhada, principalmente  para quem não é da área de TI. 

Isso pode ser injusto e nem pode parecer o correto, mas na prática é assim que funciona a percepção das pessoas pela opinião pública. Não importa que tecnicamente seu produto (no caso o Windows) teve problema por causa de terceiros (CrowdStrike). O fato é que ele ficou indisponível e o responsável pelo produto final será cobrado por isso. Essa regra se aplica para qualquer produto ou serviço prestado por empresas de qualquer ramo. Se o produto ou serviço ficar indisponível, seus clientes irão cobrá-lo, mesmo que a "culpa" do problema seja de terceiros. O fato é que seus clientes não estão conseguindo usar seu produto e você deveria ter pensado em formas para evitar isso.

Não tenho informações privilegiadas, mas aposto que no mesmo dia em que esse apagão aconteceu, o time do Windows na Microsoft já deve ter começado a pensar em mecanismos para melhorar a forma como gerenciar drivers de terceiros e mitigar problemas semelhantes a esses no futuro.