---
title: "Plano de estudo para certificação AWS Solutions Architect - Professional"
date: 2022-09-12T20:09:25-03:00
draft: false
tags: ["aws", "certificação"]
ShowToc: true
TocOpen: true
---

Em julho de 2022, passei na prova [AWS Certified Solutions Architect - Professional](https://aws.amazon.com/certification/certified-solutions-architect-professional/?nc1=h_ls). Nesse post, vou compartilhar um pouco da minha experiência e como me preparei.

## Avisos

Algumas informações importantes. O conteúdo abaixo refere-se à versão SAP-C01 da prova. A AWS já anunciou uma nova versão da prova, a SAP-C02, que passará a valer a partir de 15 de novembro de 2022. As informações da nova versão  já estão disponíveis no [site da AWS](https://aws.amazon.com/certification/coming-soon/). Haverá uma pequena mudança nas áreas de conhecimento avaliadas e vários novos produtos passarão a fazer parte do escopo da nova versão da prova. Mais detalhes podem ser encontrados em [What’s New with the SAP-C02 AWS Certified Solutions Architect Professional exam this 2022](https://tutorialsdojo.com/whats-new-with-the-sap-c02-aws-certified-solutions-architect-professional-exam-this-2022-sap-c03/). Quando uma nova versão de qualquer prova de certificação é lançada, é natural que se leve um certo tempo até que o conteúdo dos cursos e simulados sejam completamente atualizados. Portanto, se você já iniciou os estudos ou pretende fazer a prova em breve, sugiro que se planeje para que faça a versão atual.

Também quero deixar claro que o que funcionou para mim talvez não funcione para você. Cada pessoa tem uma forma diferente de estudar e aprender, e não há certo e nem errado. É importante que cada um conheça o que funciona melhor para si e faça os ajustes necessários. Eu, particularmente, gosto de misturar os vários formatos de conteúdo. Apesar de eu ter uma leve preferência por leitura, também gosto de complementar com vídeos. Também gosto de balancear a parte teórica com a prática. Enfim, avalie o que se adapta melhor ao seu estilo.

## Certificação vale a pena?

Certificação em TI é um assunto polêmico. Há quem defenda e há quem critique, com bons argumentos para ambos os lados. Se eu fiz a prova, então você já pode imaginar que eu ache que vale a pena. A certificação oferece uma maneira estruturada de estudar um determinado escopo de conhecimento. É perfeita? Claro que não, nada é perfeito. Uma pessoa certificada significa que ela seja competente? Não necessariamente. É possível ser um ótimo profissional sem ter certificação? Claro que sim, conheço vários. 

Para mim, o valor da certificação não está no certificado propriamente dito, mas sim no processo de preparação e aprendizado. O valor da certificação é obtido de como e do quê você aprendeu ao estudar. Se você se preparar somente para passar na prova, tentando decorar dados e sem entender o porquê das coisas, o valor vai ser baixo. Agora, se você realmente estudou os assuntos e entendeu os motivos, o valor vai ser alto (e aqui não estou falando de valor monetário, e sim do nível de aproveitamento e do quanto isso vai contribuir para sua vida profissional). Nesse caso, passar na prova vai uma consequência, e não o objetivo final.

## A certificação AWS Solutions Architect - Professional

Pegando emprestado o que está escrito no site da AWS, essa certificação "*valida a capacidade de projetar, implantar e avaliar aplicações na AWS com requisitos variados e complexos*". Se você ler os comentários a respeito dela pela Internet, vai encontrar pessoas falando que essa é uma das provas mais "desafiadoras" da AWS. É algo esperado, já que se trata de uma [certificação de nível mais avançado da AWS](https://aws.amazon.com/certification/?nc1=h_ls).

{{< figure src="/img/2022/AWS-SAP.png" align="center" alt="Logo da certificação AWS Solutions Architect - Professional" >}}

A dificuldade se dá por uma combinação de fatores: 
* escopo muito amplo: a AWS possui uma infinidade de produtos e serviços, com vários recursos e funcionalidades, que só aumentam com o passar do tempo. Boa parte deles faz parte do escopo da prova
* complexidade e tamando das questões: a maior parte das questões fala de cenários que envolvem a combinação de vários produtos da AWS. Muitas vezes, duas ou mais alternativas funcionam tecnicamente, mas você tem que decidir qual é a **melhor alternativa** para o que está sendo pedido para **aquele cenário**. Então, nada de parar na primeira alternativa tecnicamente correta, pois pode ser que alguma depois dela também seja tecnicamente correta e a mais adequada para aquele cenário. Muito se fala também sobre o tamanho das questões e das alternativas, que muitas delas você tem que rolar a tela para conseguir ler por completo. No meu caso, apareceram algumas questões com esse tamanho grande, mas somente uma pequena parte. A grande maioria foram de questões médias e, algumas poucas, com tamanho pequeno e mais diretas. Particularmente, pelos comentários que li e pelo que eu havia conversado com algumas pessoas, eu esperava algo pior. Mas claro que isso pode variar para cada pessoa, portanto, o que aconteceu comigo não necessariamente vai acontecer com você
* quantidade de perguntas e tempo da prova: são 75 questões de múltipla escolha ou múltiplas respostas, para 3 horas de duração da prova. Para quem fizer a prova em Inglês e esse idioma não for o seu nativo, é possível [solicitar um tempo extra de 30 minutos](https://aws.amazon.com/certification/policies/before-testing/?nc1=h_ls#Requesting_Accommodations). Mesmo assim, na média, dá menos que 3 minutos por questão, o que pode ser pouco, já que são perguntas de tamanho médio ou grande, conforme dito anteriormente

Considerando tudo isso, é uma prova cansativa e desgastante. Ela não só avalia o conhecimento técnico, mas também sua capacidade de gestão de tempo e seu controle mental, para que fique no nível de atenção e foco adequados, sem se desesperar e nem relaxar demais. Naturalmente, algumas perguntas vão levar mais tempo para serem respondidas, e aí você precisa recuperar esse tempo gasto a mais nas perguntas que são menores e mais diretas (que são a minoria). No meu caso, as primeiras questões acabaram tomando mais tempo do que deviam, mas depois fui controlando a ansiedade e aumentando a confiança. Assim, consegui manter um bom ritmo e no final ainda sobrou um pouco de tempo para repassar pelas questões que eu havia marcado para revisão. Mas é comum relatos de pessoas que ficam sem tempo para revisão e até mesmo ter a prova encerrada devido ao tempo esgotado, sem ter conseguido passar por todas as questões. 

A AWS afirma que essa prova é destinada para quem tem dois ou mais anos de experiência prática com sua Cloud. Realmente, isso faz todo sentido. Se você começou a trabalhar ou estudar AWS há pouco tempo, sugiro fortemente que não pule etapas. Comece pela [AWS Solutions Architect - Associate](https://aws.amazon.com/certification/certified-solutions-architect-associate/?ch=sec&sec=rmg&d=1), adquira mais experiência e bagagem, e só depois faça a versão Professional. Tem coisas que só são adquiridas com tempo. Uma pessoa com pouco experiência em AWS até pode conseguir passar na prova  Professional, mas terá mais dificuldade e não conseguirá aproveitar o conhecimento da mesma forma que alguém que já tem mais tempo de estrada.

A prova pode ser feita em vários idiomas, inclusive Português do Brasil. Fiz a minha em Inglês (com o tempo extra de 30 minutos citado anteriormente), pois todo material de estudo que utilizei foi em Inglês. Prefiri assim pois queria evitar qualquer surpresa que fizesse eu gastar tempo, por exemplo, tentando entender o que uma eventual tradução "estranha" de algum termo técnico queria dizer. A prova é complexa e já possui fatores suficientes para se preocupar e não queria que esse fosse mais um. Mas de qualquer modo, a prova pode ser feita em Português para quem não se sentir confortável com Inglês.

Essa não é uma certificação barata, já que é de um nível mais avançado. O preço dela é de US$ 300. Se você já possui alguma certificação AWS, tem como benefício um desconto de 50% em outra prova. Nesse caso, o valor vai para US$ 150, que ainda é relativamente caro considerando o valor do dólar atualmente, mas é melhor do que o preço cheio. Como todas as demais certificações da AWS, ela tem validade de 3 anos e precisa ser renovada para ser mantida.

Com a pandemia de COVID-19 e as regras de distanciamento social, tornou-se comum a realização de provas de certificação de forma on-line, a partir de casa. Como estamos num cenário bem melhor, com a pandemia relativamente controlada, optei por fazer a prova em um centro de exames. Achei que essa seria a melhor decisão, pois não queria que imprevistos como uma eventual falta de energia elétrica, problemas na conexão com Internet ou barulhos na vizinhança de casa atrapalhassem a prova. Como disse anteriormente, queria manter o foco na prova, e não ficar me preocupando com aspectos, de certa forma, secundários. Mas a prova on-line continua sendo uma opção para quem quiser.

## Tempo de estudo

Quando comecei a me organizar para estudar, levantei todo o material que iria utilizar (mais sobre isso na próxima seção) e o quanto de tempo por dia eu pretendia estudar. Com base nisso, cheguei a uma previsão de até 3 meses para estudar para a prova, considerando entre 2 e 3 horas de estudo por dia, e um pouco mais (em torno de 5 horas por dia) aos finais de semana. Como já disse e volto a repetir, cada pessoa tem um ritmo e outros compromissos que acabam demandando tempo, então isso vai variar. O importante é manter a consistência e a disciplina. O tempo que você utiliza estudando e se preparando acaba sento até "mais caro" que o valor monetário da prova.

## Materiais de estudo

A maior parte do material apresentado aqui é paga. Antes de sair comprando material, se você assina alguma plataforma de cursos ou livros, vale verificar se ela já não oferece algo relativo a essa certificação. No meu caso, por exemplo, assino a [O'Reilly](https://www.oreilly.com/) e [A Cloud Guru](https://acloudguru.com/), e acabei lendo livros e fazendo cursos que encontrei lá.

### Leitura

Não encontrei livros "confiáveis" da prova AWS Solutions Architect - Professional. Acabei lendo dois livros da certificação Associate (que estão disponíveis na O'Reilly), pois apesar de serem provas de níveis de dificuldade diferentes, grande parte do conteúdo acaba sendo a mesma no que se refere aos produtos e serviços da AWS. O que não fosse abordado nesses livros, seria coberto nos cursos em vídeos e simulados. Além disso, seria uma oportunidade para revisar e fortalecer os conceitos.

Li também alguns *white papers* da AWS, de assuntos que percebi que eram mais cobrados nos simulados ou em temas em que eu sentia maior necessidade de detalhamento. Alguns estão marcados como "arquivados", o que significa que podem estar desatualizados, então é bom ficar atento. Mas de forma geral ainda possuem conteúdo que pode ajudar.

Uma dica que normalmente é dada por aí é a leitura das FAQs dos produtos da AWS. Sinceramente, sair lendo a FAQ de todos os produtos não é produtivo. Realmente as FAQs dos produtos AWS são bem completas e provavelmente boa parte das respostas das questões das provas estão de uma forma ou de outra nas FAQs. Entretanto, as FAQs são extensas e existem centenas de produtos da AWS. É irreal achar que será possível ler todas as FAQs e ainda lembrar de todo o conteúdo. Acredito que as FAQs possam ser utilizadas pontualmente, para algum caso que você sinta maior necessidade de entendimento.

Abaixo, a lista de materiais de leitura que utilizei:

* livro [AWS Certified Solutions Architect Study Guide: Associate SAA-CO2 Exam](https://www.amazon.com/Certified-Solutions-Architect-Study-Guide/dp/1119713080/)
* livro [AWS Certified Solutions Architect Associate All-in-One Exam Guide, Second Edition](https://www.amazon.com/Certified-Solutions-Architect-Associate-SAA-C02/dp/1260470180/)
* White Papers
    * [Organizing Your AWS Environment Using Multiple Accounts](https://docs.aws.amazon.com/whitepapers/latest/organizing-your-aws-environment/organizing-your-aws-environment.html) 
    * [AWS Multiple Account Security Strategy - How do I manage multiple AWS accounts for security purpose?](https://d1.awsstatic.com/aws-answers/AWS_Multi_Account_Security_Strategy.pdf)
    * [AWS Migration Whitepaper](https://d1.awsstatic.com/whitepapers/Migration/aws-migration-whitepaper.pdf)
    * [Building a Scalable and Secure Multi-VPC AWS Network Infrastructure](https://docs.aws.amazon.com/whitepapers/latest/building-scalable-secure-multi-vpc-network-infrastructure/welcome.html)
    * [Amazon Virtual Private Cloud Connectivity Options](https://d1.awsstatic.com/whitepapers/aws-amazon-vpc-connectivity-options.pdf)
    * [Single Region Multi-VPC Connectivity - How do I connect multiple VPCs within the same AWS Region?](https://d0.awsstatic.com/aws-answers/AWS_Single_Region_Multi_VPC_Connectivity.pdf)
    * [Multiple Region Multi-VPC Connectivity - How do I connect multiple VPCs in different AWS Regions?](https://d0.awsstatic.com/aws-answers/AWS_Multiple_Region_Multi_VPC_Connectivity.pdf)
    * [Disaster Recovery of Workloads on AWS: Recovery in the Cloud](https://docs.aws.amazon.com/whitepapers/latest/disaster-recovery-workloads-on-aws/disaster-recovery-workloads-on-aws.html)


### Vídeos

A maior parte dos materiais feitos especificamente para a certificação que você vai encontrar são cursos em vídeos. Dos que assisti, todos assumem que o aluno já tem experiência com AWS. Portanto, a abordagem não é introdutória, o máximo que é feito é uma revisão rápida para alguns assuntos mais comuns (lembre-se que é uma certificação de nível Professional, que assume que a pessoa tem alguns anos de experiência com AWS). Dos que estão listados abaixo, o curso do A Cloud Guru é o que percebo hoje que talvez tenha feito a menor diferença. O curso é bom, mas a abrangência deixa a desejar, não sendo abordados vários tópicos importantes. Os outros dois são mais completos e acabam se complementando em alguns aspectos.

* [AWS Certified Solutions Architect - Professional 2020](https://acloudguru.com/course/aws-certified-solutions-architect-professional) - A Cloud Guru - de Scott Pletcher
* [AWS Certified Solutions Architect Professional SAP-C01 2022](https://www.udemy.com/course/aws-certified-solutions-architect-professional-training/) - Udemy - de Neal Davis
* [Ultimate AWS Certified Solutions Architect Professional 2022](https://www.udemy.com/course/aws-solutions-architect-professional/) - Udemy - de Stephane Maarek
* [Exam Readiness: AWS Certified Solutions Architect – Professional](https://explore.skillbuilder.aws/learn/course/external/view/elearning/34/exam-readiness-aws-certified-solutions-architect-professional?sap=sec&sec=prep) - AWS - gratuito


### Laboratórios

Os laboratórios são importantes para colocar em prática o que foi aprendido na parte teórica. Não diria que os laboratórios são essenciais para essa prova, mas se você é uma pessoa que aprende melhor colocando a mão na massa, isso pode fazer a diferença. Eles também podem ajudar a consolidar o conhecimento. 

Tanto o curso do A Cloud Guru quanto o do Neal Davis, da Udemy (citados anteriormente), contém alguns exercícios práticos. No caso do A Cloud Guru, a assinatura dá direito a ambientes de *sandbox* nos provedores de Cloud mais conhecidos, e assim você consegue fazer os exercícios em uma conta temporária da AWS. 

Também cheguei a fazer os laboratórias da [Whizlabs](https://www.whizlabs.com/), mas não recomendo. Apesar de ser uma quantidade grande de laboratórios, a qualidade variava demais, e alguns deles chegaram a não funcionar. Alguns também eram muito simplórios, não compatíveis com o nível Professional. 

### Simulados

Os simulados são importantes para você ter uma ideia do que lhe aguarda na prova real. Além disso, os simulados que fiz e que estão listados abaixo apresentam uma explicação detalhada da resposta de cada questão. Era comum eu gastar mais tempo lendo as explicações das respostas do que com a pergunta propriamente dita. Sempre é possível aprender algo a mais nas explicações, mesmo nos casos em que se acerta a resposta. Além disso, também apareciam perguntas relacionadas a alguns tópicos que não haviam sido abordados nos cursos, o que acabava complementando o conhecimento.

* [Practice Exam AWS Certified Solutions Architect Professional](https://www.udemy.com/course/practice-exam-aws-certified-solutions-architect-professional/) - Udemy -  de Stephane Maarek
* [AWS Certified Solutions Architect Professional Practice Exam](https://www.udemy.com/course/aws-certified-solutions-architect-professional-aws-practice-exams/) - Udemy - de Neal Davis
* [AWS Certified Solutions Architect Professional Practice Exam](https://www.udemy.com/course/aws-solutions-architect-professional-practice-exams-sap-c02/) - Udemy - de Jon Bonso
* [AWS Certified Solutions Architect - Professional Sample Questions](https://d1.awsstatic.com/training-and-certification/docs-sa-pro/AWS-Certified-Solutions-Architect-Professional_Sample-Questions.pdf) - AWS - gratuito
* [AWS Certified Solutions Architect - Professional Official Practice Question Set](https://aws.amazon.com/certification/certified-solutions-architect-professional/?nc1=h_ls) - AWS - gratuito

## Principais assuntos

Por se tratar de uma prova de nível avançado, você tem que dominar os recursos mais básicos da AWS, como VPC, AZs, Subnet, Route Rable, Security Group, Network ACL, EC2, EBS, ELB, S3, etc. Além disso, no meu caso apareceram várias perguntas relacionadas à migração para Cloud, Direct Connect, AWS Organizations, Service Control Policy (SCP) e Cross-account IAM Roles. Além disso, é comum aparecer uma ou duas perguntas sobre produtos e serviços menos conhecidos da AWS, que talvez você nem tenha estudado ou ouvido falar. Obviamente que isso vai variar a cada prova. Não necessariamente você encontrará os mesmos tópicos na sua prova.

## Conclusão

Como disse anteriormente, essa é uma prova cansativa e que aborda uma quantidade imensa de conhecimento. A gestão do tempo e da ansiedade é vital. O que funcionou para mim não necessariamente vai funcionar para você. Quis passar minhas percepções a partir da experiência que tive e, assim, poder contribuir de alguma forma com a preparação de outras pessoas para a prova. Acredito que muitas das dicas apresentadas aqui podem ajudar nisso. Boa sorte!