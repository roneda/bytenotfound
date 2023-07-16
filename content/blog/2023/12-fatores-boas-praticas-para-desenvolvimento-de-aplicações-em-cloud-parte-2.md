---
title: "12 Fatores: boas práticas para desenvolvimento de aplicações em Cloud - parte 2"
date: 2023-06-07T21:37:05-03:00
draft: false
tags: ["12 fatores", "arquitetura", "boa práticas", "cloud"]
---

> Esse texto foi originalmente publicado em [12 Fatores: conheça as boas práticas da metodologia de desenvolvimento de softwares](https://medium.com/itautech/12-fatores-conhe%C3%A7a-as-boas-pr%C3%A1ticas-da-metodologia-de-desenvolvimento-de-softwares-378f088f2330)

A metodologia 12 Fatores é composta por um conjunto de boas práticas para construção de aplicações para Cloud. Entre seus principais objetivos, ela visa explorar os benefícios das plataformas, favorecer a portabilidade máxima entre os ambientes de execução, aumentar a agilidade com atualizações frequentes, escalar sem causar mudanças significativas e diminuir o custo e tempo de onboarding de novas pessoas desenvolvedoras nos times.

Seus princípios estão organizados em 12 pilares:

1. Base de código
1. Dependências
1. Configurações
1. Serviços de apoio
1. Build, Release, Run
1. Processos
1. Port Binding
1. Concorrência
1. Descartabilidade
1. Paridade entre desenvolvimento e produção
1. Logs
1. Processos Administrativos

Na primeira parte, foram abordados os seis primeiros fatores e você pode encontrar mais detalhes em [12 Fatores: boas práticas para desenvolvimento de aplicações em Cloud - parte 1]({{< relref "/blog/2023/12-fatores-boas-praticas-para-desenvolvimento-de-aplicações-em-cloud-parte-1.md">}}). Nesse post, serão explorados os demais fatores.

### 7. Port binding

A aplicação deve expor seus serviços no ambiente em que é executada através de uma porta, que será utilizada para atender as requisições. Essa porta pode variar de acordo com o ambiente — e a aplicação não deve ser impactada por causa disso. O ideal é que as aplicações sejam completamente autocontidas, e que não dependam de nenhum middleware externo complexo (como application servers, web servers etc) para expor seus serviços.

Pensando em um ambiente em Cloud, as aplicações devem ser menores e mais leves para que sejam instanciadas ou encerradas rapidamente. As linguagens e plataformas de desenvolvimento mais modernas possuem servidores leves que podem ser embutidos nas próprias aplicações para que consigam expor seus serviços de forma autônoma, sem depender de algum servidor externo. Esse fator complementa o [fator 2 — Dependências]({{< relref "/blog/2023/12-fatores-boas-praticas-para-desenvolvimento-de-aplicações-em-cloud-parte-1.md#2-dependências">}}), no sentido de permitir ser uma aplicação autocontida, e o [fator 4 -Serviços de Apoio]({{< relref "/blog/2023/12-fatores-boas-praticas-para-desenvolvimento-de-aplicações-em-cloud-parte-1.md#4-serviços-de-apoio">}}), pois essa abordagem permite que uma aplicação se torne um serviço de apoio de outra aplicação.

### 8. Concorrência

Na computação, existem dois tipos de escalabilidade: vertical e horizontal. A escalabilidade vertical acontece quando as configurações de uma máquina ou servidor são melhoradas, aumentando assim seu tamanho com aumento de memória, aumento de disco, troca por um processador mais rápido etc.

Isso pode funcionar, mas existe um limite físico a partir do qual não é mais possível escalar. Esse modelo geralmente implica em desperdício, pois é comum que a máquina ou servidor fique ocioso boa parte do tempo, já que ele tem que estar preparado para o pico de demanda. A figura abaixo representa como funciona a escalabilidade vertical:

{{< figure src="/img/2023/12fatores-8-escvertical.gif" align="center" alt="Animação mostra um servidor que se torna maior gradativamente" >}}

Já a escalabilidade horizontal acontece quando aumentamos a quantidade de cópias da aplicação que estão sendo executadas ao mesmo tempo: aumento na quantidade de máquinas virtuais, na quantidade de containers, na quantidade de instâncias da aplicação etc.

Num ambiente de Cloud, é muito simples obter isso, já que é possível escalar quase que infinitamente. Além disso, é possível ter recursos com configurações menores (e mais baratos) e cujas quantidades variam conforme a demanda, fazendo uso mais eficiente e diminuindo a ociosidade desses recursos, o que evita ou reduz desperdícios. A figura a seguir mostra como funciona a escalabilidade horizontal:

{{< figure src="/img/2023/12fatores-8-eschorizontal.gif" align="center" alt="Animação mostra um servidor se multiplicando gradativamente em novas unidades" >}}

Esse fator determina que uma aplicação deve estar preparada para escalar horizontalmente, estando intimamente ligado com o [fator 6 — Processos]({{< relref "/blog/2023/12-fatores-boas-praticas-para-desenvolvimento-de-aplicações-em-cloud-parte-1.md#6-processos">}}), já que aplicações stateless escalam mais facilmente. Além disso, também deve-se atentar à forma como a aplicação é modularizada.

É comum que uma aplicação possua várias funcionalidades e que algumas sejam mais utilizadas que outras. Uma correta modularização da aplicação permite que as funcionalidades mais demandadas possam ser escaladas de forma independente das menos utilizadas, o que também ajuda a evitar desperdícios financeiros.

### 9. Descartabilidade
Uma aplicação na Cloud deve ser inicializada e encerrada rapidamente, a qualquer momento. O tempo de inicialização da aplicação deve ser o menor possível e seu encerramento deve ser confiável, liberando recursos corretamente, permitindo que os processamentos de curta duração em andamento terminem ou que processamentos de longa duração sejam interrompidos de forma que possam ser retomados posteriormente sem gerar inconsistências.

Os processos da aplicação e os recursos de infraestrutura utilizadas por ela devem ser tratados como descartáveis, pois o modelo elástico e sob demanda de Cloud permite que eles sejam facilmente repostos e substituídos. A arquitetura da aplicação precisa ser projetada para isso. Essa abordagem está ligada aos fatores [6-Processos]({{< relref "/blog/2023/12-fatores-boas-praticas-para-desenvolvimento-de-aplicações-em-cloud-parte-1.md#6-processos">}}), [7-Port Binding]({{< relref "#7-port-binding">}}) e [8-Concorrência,]({{< relref "#8-concorrência">}}) que em conjunto facilitam na escalabilidade rápida, na implantação de mudanças e na recuperação de falhas.

### 10. Paridade entre desenvolvimento e produção
Os ambientes de Desenvolvimento, Homologação, Produção e outros que possam existir devem ser os mais semelhantes possíveis. Além do aspecto mais óbvio disso, que é o técnico (as versões de tecnologias e ferramentas deveriam ser as mesmas em qualquer ambiente), esse fator também considera importante a paridade em duas outras perspectivas: tempo e pessoas.

O tempo entre o momento que o código da aplicação é versionado na base do código e sua implantação nos ambientes deve ser o menor possível. O objetivo é promover entregas frequentes, para evitar uma diferença muito grande entre o código-fonte que está na base de código e o código que está sendo executado em Produção. Em caso de problema na implantação de uma nova versão, vai ser mais fácil analisar, achar a causa e corrigir um código que acabou de ser alterado, pois as pessoas ainda estarão com o contexto da mudança.

Além disso, as pessoas que implementaram as alterações são as mais aptas a identificarem a causa de eventuais problemas e por isso devem acompanhar a implantação e monitoramento em produção. Equipes que trabalham no modelo de DevOps, no qual o time que desenvolve a aplicação também é responsável por sua operação, acabam tendo esse tipo de atuação naturalmente.

Além disso, esse fator em conjunto com o fator [5 -Build, Release, Run]({{< relref "/blog/2023/12-fatores-boas-praticas-para-desenvolvimento-de-aplicações-em-cloud-parte-1.md#5-build-release-run">}}), contribui para aumentar a confiança de que a aplicação vai funcionar em qualquer ambiente, facilitando o *Continuous Delivery e Continuous Deployment*.

### 11. Logs
Logs são uma sequência de eventos ordenados por tempo que são coletados das saídas dos processos da aplicação. A responsabilidade da aplicação é somente emitir o log na saída padrão (*stdout*), mas não deve se preocupar em armazenar ou gerir os logs produzidos. A captura, agregação, processamento, indexação e armazenamento dos logs devem ser feitos por mecanismos ou ferramentas providos pelo ambiente de execução, externos à aplicação, como por exemplo Logstash, Fluentd, Splunk, Elasticsearch, Kibana etc.

Esse desacoplamento permite que mudanças na maneira como logs são processados ou armazenados não provoquem alterações na aplicação.

### 12. Processos Administrativos
Processos Administrativos são aquelas atividades periféricas pontuais ou de manutenção que não fazem parte do núcleo da aplicação, como por exemplo: código que é executado uma única vez, migrações de bancos de dados, código executado periodicamente em horários pré-definidos etc.

Segundo esse fator, os Processos Administrativos devem ser executados de forma isolada das demais partes da aplicação e estão sujeitos aos mesmos fatores. Dessa forma, eles devem ter seu código-fonte versionado em uma base de código, declarando Dependências e utilizando as mesmas Configurações, além de passar pelos estágios de *Build, Release e Run*, etc.

Conforme explicado ao longo dos artigos, os 12 Fatores são um conjunto de princípios sobre organização de código, práticas de desenvolvimento, arquitetura e operações para construção de aplicações modernas.

Apesar do foco em aplicações executadas no ambiente de Cloud, qualquer aplicação pode seguir esses princípios. Além disso, não é obrigatório que toda aplicação que seja executada em Cloud siga esses fatores, mas é importante que essa seja uma decisão consciente, com base em requisitos e sabendo do que se está abrindo mão.

Para concluir, esses fatores são um ponto de partida, mas não são os únicos a serem considerados quando projetamos uma aplicação para ser executada em Cloud. Outros aspectos, como por exemplo segurança, processamento assíncrono, escalabilidade da camada de dados, consistência eventual, orientação a eventos, tolerância a falhas, estratégias de *deployment*, dentre outros, também são recomendáveis.