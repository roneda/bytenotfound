---
title: "Plano de estudo para certificação AWS Certified Developer - Associate"
date: 2023-10-23T20:44:06-03:00
draft: false
tags: ["aws", "certificação", "desenvolvimento"]
ShowToc: true
TocOpen: true
cover: 
  image: "/img/2023/AWS-CDA.png"
---

No mês passado (setembro/2023), passei na prova [AWS Certified Developer - Associate](https://aws.amazon.com/certification/certified-developer-associate/). Aqui irei compartilhar como me preparei e dicas para quem estiver interessado em fazer essa prova.

## Avisos

O conteúdo abaixo refere-se à versão DVA-C02 da prova, que passou a valer em fevereiro/2023. Apesar de não estar prevista uma nova versão da prova, dependendo de quando estiver lendo esse post, pode ser que o conteúdo esteja desatualizado. Então, fique atento.

Quero lembrar que o que funcionou para mim talvez não funcione para você. Cada pessoa tem uma forma diferente de estudar e aprender, e não há certo e nem errado. É importante que cada um conheça o que funciona melhor para si e faça os ajustes necessários. Eu, particularmente, gosto de misturar os vários formatos de conteúdo. Apesar de eu ter uma preferência por leitura, também gosto de complementar com vídeos. Também gosto de balancear a parte teórica com a prática. Enfim, avalie o que se adapta melhor ao seu estilo.

## Certificação vale a pena?

Já dei minha opinião sobre certificação valer a pena ou não no post sobre a prova [AWS Solutions Architect Professional]({{< relref "/blog/2022/plano-de-estudo-para-certificacao-AWS-Solutions-Architect-Professional.md#certifica%C3%A7%C3%A3o-vale-a-pena" >}}). Não vou ser repetitivo aqui, mas em resumo, certificação não é bala de prata e nem é perfeita. Entretanto, ela oferece uma maneira estruturada de estudar um determinado campo do conhecimento. O valor da certificação não está no certificado propriamente dito, mas sim no processo de preparação e aprendizado. Nesse caso, passar na prova é uma consequência, e não o objetivo final.

## A certificação AWS Certified Developer - Associate

Segundo a AWS, essa certificação "*demonstra conhecimento e compreensão dos principais produtos da AWS, usos e práticas recomendadas básicas de arquitetura da AWS e proficiência no desenvolvimento, implantação e debugging de aplicações baseadas em nuvem usando a AWS*". 

{{< figure src="/img/2023/AWS-CDA.png" align="center" alt="Logo da certificação AWS Certified Developer - Associate" >}}

Como se trata de uma certificação do tipo *Associate*, espera-se um nível de dificuldade médio. Assim, como é esperado, ela não é nem de perto tão desgastante quanto a da AWS Solutions Architect Professional e possui um nível de dificuldade um pouco menor que a [AWS Security Specialty]({{< relref "/blog/2023/plano-de-estudo-para-certificacao-aws-certified-security-specialty.md" >}}). Isso não significa que você não precisa se preparar. 

Principais pontos:
* escopo: possui um escopo mais limitado, ao contrário das provas de Solutions Architect (tanto Associate quanto Professional), que cobrem uma infinidade de produtos e serviços da AWS. O foco acaba sendo um domínio de conhecimento específico, no caso, Desenvolvimento na AWS. Isso reflete em menos conteúdo para estudar. Por outro lado, é exigido um conhecimento mais detalhado de certos serviços da AWS que fazem sentido quando falamos de desenvolvedores. Se você já fez algumas das provas de Solutions Architect da AWS, conseguirá reaproveitar esse conhecimento, o que irá facilitar
* complexidade e tamanho das questões: no geral, classificaria o nível de complexidade das questões como intermediário. Não houve perguntas gigantes, que fosse necessário rolar a tela para conseguir ler por completo. A maioria das questões foram de tamanho médio e, algumas poucas, com tamanho pequeno. Fiquei surpreso com algumas perguntas que eram bem diretas e fáceis. Isso me causou desconfiança, pois pensei que pudesse ser algum tipo de "pegadinha", mas relendo atentamente confirmei que eram perguntas simples mesmo. De todo modo, foram poucas perguntas assim
* quantidade de perguntas e tempo da prova: são 65 questões de múltipla escolha ou múltiplas respostas, para 2 horas e 10 minutos de duração da prova. Para quem o Inglês não for o idioma nativo, é possível [solicitar um tempo extra de 30 minutos](https://aws.amazon.com/certification/policies/before-testing/?nc1=h_ls#Requesting_Accommodations). Na média, dá um pouco mais que 2 minutos por questão. 

Como toda prova, além do conhecimento técnico, também são validados sua capacidade de gestão de tempo e seu controle mental, para que fique no nível de atenção e foco adequados. Como sempre, algumas perguntas vão levar mais tempo para serem respondidas, e aí você precisa recuperar esse tempo gasto a mais nas perguntas que são menores e mais diretas. 

A prova pode ser feita em vários idiomas, inclusive Português do Brasil. Fiz a minha em Inglês (com o tempo extra de 30 minutos citado anteriormente), pois todo material de estudo que utilizei foi em Inglês. Prefiri assim pois queria evitar qualquer surpresa que fizesse eu gastar tempo, por exemplo, tentando entender o que uma eventual tradução "estranha" de algum termo técnico queria dizer. Mas de qualquer modo, a prova pode ser feita em Português para quem não se sentir confortável com Inglês.

O preço dessa certificação é de US$ 150. Se você já possui alguma certificação AWS, tem como benefício um desconto de 50% em outra prova. Nesse caso, o valor vai para US$ 75, que é um valor médio. Como todas as demais certificações da AWS, ela tem validade de 3 anos e precisa ser renovada para ser mantida.

Essa prova pode ser feito de forma on-line ou em um centro de exames. Como não gostei da experiência quando fiz a prova on-line da [AWS Security Specialty]({{< relref "/blog/2023/plano-de-estudo-para-certificacao-aws-certified-security-specialty.md" >}}), preferi fazer em um centro de exames. Só volto a fazer prova de certificação on-line novamente se não houver outra alternativa.


## Tempo de estudo

Estudei durante aproximadamente 45 dias, de 2 a 3 horas de estudo por dia. Lembrando que parte do conteúdo eu já conhecia por causa de outras provas da AWS, então para esses casos acabou sendo uma revisão. Pode ser que você precise de mais tempo caso esteja vendo o conteúdo pela primeira vez. Além disso, cada pessoa tem um ritmo e outros compromissos que acabam demandando tempo, então isso vai variar. O importante é manter a consistência e a disciplina.

## Materiais de estudo

Como nas outras provas, a maior parte do material apresentado aqui é paga. Antes de sair comprando material, se você assina alguma plataforma de cursos ou livros, vale verificar se ela já não oferece algo relativo a essa certificação. No meu caso, por exemplo, assino a [O'Reilly](https://www.oreilly.com/) e [A Cloud Guru](https://acloudguru.com/), e acabei lendo livros e fazendo cursos que encontrei lá.

### Leitura

Não encontrei livros da versão DVA-C02. Acabei lendo alguns capítulos de dois livros da versão DVA-C01 da prova (que estão disponíveis na O’Reilly). Como é um material de certa forma desatualizado, preferi focar em capítulos de assuntos que são mais cobrados na prova de AWS Developer Associate e que eu não dominava, de forma a não gastar muito tempo neles. O plano seria complementar e revisar esse conteúdo com os demais materiais, teoricamente mais atualizados.

Além disso, também li também alguns *white papers* da AWS. 

Abaixo, a lista de materiais de leitura que utilizei:

* livro [AWS Certified Developer Associate All-in-One Exam Guide (Exam DVA-C01)](https://www.amazon.com/Certified-Developer-Associate-Guide-DVA-C01/dp/1260460177/)
* livro [AWS Certified Developer Official Study Guide, Associate Exam](https://www.amazon.com/Certified-Developer-Official-Study-Guide/dp/1119508193/)
* White Papers
    * [Practicing Continuous Integration and Continuous Delivery on AWS](https://docs.aws.amazon.com/whitepapers/latest/practicing-continuous-integration-continuous-delivery/welcome.html)
    * [Overview of Deployment Options on AWS](https://docs.aws.amazon.com/whitepapers/latest/overview-deployment-options/welcome.html)
    * [Running Containerized Microservices on AWS](https://docs.aws.amazon.com/whitepapers/latest/running-containerized-microservices/welcome.html)
    * [Implementing Microservices on AWS](https://docs.aws.amazon.com/whitepapers/latest/microservices-on-aws/microservices-on-aws.html)
    * [Optimizing Enterprise Economics with Serverless Architectures](https://docs.aws.amazon.com/whitepapers/latest/optimizing-enterprise-economics-with-serverless/optimizing-enterprise-economics-with-serverless.html)
    * [Serverless Applications Lens AWS Well-Architected Framework](https://docs.aws.amazon.com/wellarchitected/latest/serverless-applications-lens/welcome.html)
    

### Vídeos

Atualmente, a maior parte dos materiais feitos para provas de certificação são cursos em vídeos. Assisti aos cursos do A Cloud Guru e da Udemy. O do A Cloud Guru e o do Neal Davis, da Udemy, achei superificiais em vários tópicos. O curso do Neal Davis foi o que mais me decepcionou, pois não manteve o nível de profundidade que eu já havia visto em outros cursos dele. Um reflexo disso é o tempo de duração desse treinamento, que é praticamente a metade dos outros dois. O do Stephane Maarek, também da Udemy, é sem dúvidas o melhor e mais completo, com um nível de detalhamento muito bom. Se tivesse que escolher somente um curso para fazer, escolheria esse.  

* [Ultimate AWS Certified Developer Associate 2023 NEW DVA-C02](https://www.udemy.com/course/aws-certified-developer-associate-dva-c01/) - Udemy - de Stephane Maarek
* [AWS Certified Developer Associate Exam Training DVA-C02](https://www.udemy.com/course/aws-certified-developer-associate-exam-training/) - Udemy - de Neal Davis
* [AWS Certified Developer - Associate (DVA-C02)](https://www.pluralsight.com/cloud-guru/courses/aws-certified-developer-associate-dva-c02) - A Cloud Guru - de Faye Ellis


### Simulados

Os simulados são importantes pois é a experiência mais próxima que você terá da prova real. Os simulados listados abaixo possuem uma explicação detalhada da resposta de cada questão, o que é fonte importante de conhecimento para aprender coisas novas. Além disso, é comum aparecerem alguns tópicos que não haviam sido abordados nos cursos, o que acabava complementando o conhecimento. Os melhores simulados, na minha opinião, são do Jon Bonso (Tutorials Dojo) e do Stephane Maarek. Uma dica que dou é: quanto mais simulados você fizer, melhor.

* [AWS Certified Developer Associate DVA-C02 Practice Exams 2023](https://portal.tutorialsdojo.com/courses/aws-certified-developer-associate-practice-exams/) - Tutorials Dojo - de Jon Bonso
* [Practice Exams | AWS Certified Developer Associate 2023](https://www.udemy.com/course/aws-certified-developer-associate-practice-tests-dva-c01/) - Udemy - de Stephane Maarek
* [AWS Certified Developer Associate Practice Exam Questions](https://www.udemy.com/course/aws-developer-associate-practice-exams/) - Udemy - de Neal Davis

## Principais assuntos

Por se tratar de uma prova voltada para desenvolvedores, você tem que dominar temas relacionados a serviços de pipelines de CI/CD (CodeCommit, CodeBuild, CodeDeploy, CodePipeline) e estratégias de *deployment*, serviços serverless utilizados em desenvolvimento de aplicações (Lambda, DynamoDB, API Gateway, Cognito, SQS, SNS, Step Functions) e infraestrutura como código com CloudFormation. Também se prepare para responder sobre Kinesis, Elastic Beanstalk e X-Ray. Além disso, os recursos mais básicos da AWS, como VPC, AZs, Subnet, Route Rable, Security Group, Network ACL, EC2, EBS, ELB, S3, também serão exigidos de uma forma ou de outra, mas sem um nível muito grande de profundidade. No meu caso, caíram muitas perguntas de API Gateway e X-Ray. Para minha surpresa, não houve nenhuma questão pedindo para calcular o RCU ou WCU de uma tabela DynamoDB! Eu tinha "certeza" que haveria pelo menos uma pergunta dessas, mas a AWS deve ter mudado isso com a nova versão da prova, já que essa deveria ser uma das perguntas mais manjadas. Lembrando que isso vai variar a cada prova. Não necessariamente você encontrará os mesmos tópicos na sua prova.

## Conclusão

Como expliquei antes, por se tratar de uma prova de nível Associate e com foco em Desenvolvimento na AWS, o escopo fica limitado em termos de quantidade de assuntos, resultando em menos conteúdo para estudar quando comparada com outras provas, principalmente as de Solutions Architect. Entretanto, é exigido um nível de profundidade um pouco maior dos assuntos. Além disso, se você também fez outras provas da AWS, então irá reaproveitar muita do que estudou, o que é uma vantagem. Deixando claro aqui que o que funcionou para mim não necessariamente vai funcionar para você. Espero que esse plano de estudo contribua na sua preparação. Boa prova!