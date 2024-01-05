---
title: "Plano de estudo para certificação AWS Certified DevOps Engineer - Professional"
date: 2023-12-15T22:44:06-03:00
draft: false
tags: ["aws", "certificação", "devops"]
ShowToc: true
TocOpen: true
cover: 
  image: "/img/2023/AWS-DOP.png"
---

Em novembro/2023, passei na prova [AWS Certified DevOps Engineer - Professional](https://aws.amazon.com/certification/certified-devops-engineer-professional/). A seguir irei descrever como me preparei e dicas para quem estiver interessado em tirar essa certificação.

## Avisos

O conteúdo abaixo refere-se à versão DOP-C02 da prova, que passou a valer em março/2023. Apesar de não estar prevista uma nova versão da prova, dependendo de quando estiver lendo esse post, pode ser que o conteúdo esteja desatualizado. Então, fique atento.

Para que fique claro: lembro que o que funcionou para mim talvez não funcione para você. Cada pessoa tem uma forma diferente de estudar e aprender, e não há certo e nem errado. É importante que cada um conheça o que funciona melhor para si e faça os ajustes necessários. Eu, particularmente, gosto de misturar os vários formatos de conteúdo. Apesar de eu ter uma preferência por leitura, também gosto de complementar com vídeos. Também gosto de balancear a parte teórica com a prática. Enfim, avalie o que se adapta melhor ao seu estilo.

## Certificação vale a pena?

Certificação não é bala de prata e nem é perfeita. Mas ela oferece uma maneira estruturada de estudar um determinado campo do conhecimento. O valor da certificação não está no certificado propriamente dito, mas sim no processo de preparação e aprendizado. Nesse caso, passar na prova é uma consequência, e não o objetivo final. Se quiser saber mais o que penso sobre certificação valer a pena ou não, leia o que escrevi no post sobre a prova [AWS Solutions Architect Professional]({{< relref "/blog/2022/plano-de-estudo-para-certificacao-AWS-Solutions-Architect-Professional.md#certifica%C3%A7%C3%A3o-vale-a-pena" >}}).  

## A certificação AWS Certified DevOps Engineer - Professional

Segundo a AWS, essa certificação "*demonstra a experiência técnica de indivíduos em relação ao provisionamento, operação e gerenciamento de sistemas de aplicações distribuídas na plataforma da AWS, fornecendo maior confiança e credibilidade com colegas, partes interessadas e clientes.*". 

{{< figure src="/img/2023/AWS-DOP.png" align="center" alt="Logo da certificação AWS Certified DevOps Engineer - Professional" >}}

Como se trata de uma certificação do tipo *Professional*, espera-se um nível de dificuldade maior. Entretanto, não achei ela tão desgastante quanto a da AWS Solutions Architect Professional, que para mim continua sendo a mais exigente das provas que fiz até agora. Entretanto, isso não quer dizer que seja fácil, longe disso.

Principais pontos:
* escopo: possui um escopo mais limitado, ao contrário das provas de Solutions Architect (tanto Associate quanto Professional). Isso reflete em menos conteúdo para estudar. Por outro lado, é exigido um conhecimento mais detalhado de certos serviços da AWS. Se você já fez a prova de Solutions Architect Professional da AWS, conseguirá reaproveitar esse conhecimento. No meu caso, também consegui reaproveitar boa parte do conhecimento da prova AWS Certified Developer - Associate, [que havia feito em setembro/23]({{< relref "/blog/2023/plano-de-estudo-para-certificacao-AWS-Certified-Developer-Associate.md">}}). Isso ajudou bastante também
* complexidade e tamanho das questões: achei o nível de complexidade das questões um pouco menor do que a prova AWS Solutions Architect Professional. A maioria das questões foram de tamanho médio ou grande e, algumas poucas, com tamanho pequeno. Entretanto, não eram cenários ultra complexos envolvendo a combinação de muitos produtos. Foram perguntas mais diretas, podemos dizer
* quantidade de perguntas e tempo da prova: são 75 questões de múltipla escolha ou múltiplas respostas, das quais [65 é que valem pontos](https://d1.awsstatic.com/training-and-certification/docs-devops-pro/AWS-Certified-DevOps-Engineer-Professional_Exam-Guide.pdf). A duração é de 3 horas, mas para quem o Inglês não for o idioma nativo, é possível [solicitar um tempo extra de 30 minutos](https://aws.amazon.com/certification/policies/before-testing/?nc1=h_ls#Requesting_Accommodations). Na média, dá um pouco um pouco menos que 3 minutos por questão, o que pode ser pouco se não tomado o devido cuidado

Como toda prova, além do conhecimento técnico, também são validados sua capacidade de gestão de tempo e seu controle mental, para que fique no nível de atenção e foco adequados. Como sempre, algumas perguntas vão levar mais tempo para serem respondidas, e aí você precisa recuperar esse tempo gasto a mais nas perguntas que são menores e mais diretas. 

A prova pode ser feita em vários idiomas, mas ela ainda **não está disponível em Português**. Fiz a minha em Inglês (com o tempo extra de 30 minutos citado anteriormente).

Essa não é uma certificação barata, já que é de um nível mais avançado. O preço dela é de US$ 300. Se você já possui alguma certificação AWS, tem como benefício um desconto de 50% em outra prova. Nesse caso, o valor vai para US$ 150, que ainda é relativamente caro considerando o valor do dólar atualmente, mas é melhor do que o preço cheio. Como todas as demais certificações da AWS, ela tem validade de 3 anos e precisa ser renovada para ser mantida

Essa prova pode ser feito de forma on-line ou em um centro de exames. Como não gostei da experiência quando fiz a prova on-line da [AWS Security Specialty]({{< relref "/blog/2023/plano-de-estudo-para-certificacao-aws-certified-security-specialty.md" >}}), preferi fazer em um centro de exames. Como já disse em outro post, só volto a fazer prova de certificação on-line se não houver outra alternativa.


## Tempo de estudo

Estudei durante aproximadamente 45 dias, de 2 a 3 horas de estudo por dia. Lembrando que parte do conteúdo eu já conhecia por causa de outras provas da AWS, então para esses casos acabou sendo uma revisão. Pode ser que você precise de mais tempo caso esteja vendo o conteúdo pela primeira vez. Além disso, cada pessoa tem um ritmo e outros compromissos que acabam demandando tempo, então isso vai variar. O importante é manter a consistência e a disciplina.

## Materiais de estudo

Como nas outras provas, a maior parte do material apresentado aqui é paga. Antes de sair comprando material, se você assina alguma plataforma de cursos ou livros, vale verificar se ela já não oferece algo relativo a essa certificação.

### Leitura

Não encontrei livros da versão DOP-C02. Para essa prova, acabei focando nos *white papers* da AWS abaixo:

* [AWS Multi-Region Fundamentals](https://docs.aws.amazon.com/whitepapers/latest/aws-multi-region-fundamentals/aws-multi-region-fundamentals.html)
* [Disaster Recovery of Workloads on AWS: Recovery in the Cloud](https://docs.aws.amazon.com/whitepapers/latest/disaster-recovery-workloads-on-aws/disaster-recovery-workloads-on-aws.html)
* [Introduction to DevOps on AWS](https://docs.aws.amazon.com/whitepapers/latest/introduction-devops-aws/introduction-to-devops.html)
* [Practicing Continuous Integration and Continuous Delivery on AWS](https://docs.aws.amazon.com/whitepapers/latest/practicing-continuous-integration-continuous-delivery/welcome.html)
* [Overview of Deployment Options on AWS](https://docs.aws.amazon.com/whitepapers/latest/overview-deployment-options/welcome.html)
* [Running Containerized Microservices on AWS](https://docs.aws.amazon.com/whitepapers/latest/running-containerized-microservices/welcome.html)
    

### Vídeos

Atualmente, a maior parte dos materiais feitos para provas de certificação são cursos em vídeos. Assisti a dois cursos da Udemy. O do Zeal Vora achei muito repetitivo. Ele fazia uma aula teórica sobre o assunto e depois uma aula prática na qual repetia praticamente toda a parte teórica, o que acabou deixando o curso muito extenso desnecessariamente. Como já era de se esperar, o curso do Stephane Maarek é sem dúvidas o melhor e mais completo, com um nível de detalhamento muito bom. Se tivesse que escolher somente um curso para fazer, escolheria esse.  

* [AWS Certified DevOps Engineer Professional 2023 - DOP-C02](https://www.udemy.com/course/aws-certified-devops-engineer-professional-hands-on/) - Udemy - de Stephane Maarek
* [AWS Certified DevOps Engineer - Professional 2024](https://www.udemy.com/course/master-aws-certified-devops-engineer-professional/) - Udemy - de Zeal Vora



### Simulados

Os simulados são importantes pois é a experiência mais próxima que você terá da prova real. Os simulados listados abaixo possuem uma explicação detalhada da resposta de cada questão, o que é fonte importante de conhecimento para aprender coisas novas. Além disso, é comum aparecerem alguns tópicos que não haviam sido abordados nos cursos, o que acaba complementando o conhecimento. Todos os simulados abaixo possuem o mesmo nível, com ótima qualidade, mas o simulado oficial da AWS me surpreendeu positivamente. Uma curiosidade é que, das provas que já fiz, essa foi aquela onde apareceram mais perguntas parecidas com as perguntas dos simulados, de todos eles. Pode ser uma coincidência e nada garante que vá acontecer com outras pessoas, mas reforço uma dica que já dei em outras provas: quanto mais simulados você fizer, melhor.

* [Exam Prep Official Practice Exam: AWS Certified DevOps Engineer - Professional (DOP-C02 - English)](https://explore.skillbuilder.aws/learn/course/external/view/elearning/14810/aws-certified-devops-engineer-professional-official-practice-exam-dop-c02-english) - Oficial AWS
* [AWS Certified DevOps Engineer Professional Practice Exams DOP-C02 2023](https://portal.tutorialsdojo.com/courses/aws-certified-devops-engineer-professional-practice-exams/) - Tutorials Dojo - de Jon Bonso
* [Practice Exams | AWS Certified DevOps Engineer Professional](https://www.udemy.com/course/aws-certified-devops-engineer-professional-practice-exam-dop/) - Udemy - de Stephane Maarek e Abhishek Singh
* [AWS Certified DevOps Engineer Professional Practice Exams](https://www.udemy.com/course/aws-certified-devops-engineer-professional-practice-exams-course/) - Udemy - de Neal Davis

## Principais assuntos

Apareceram assuntos bem distribuídos, que faziam parte do escopo das outras provas: Arquitetura, Desenvolvimento, SysOps e Segurança, só que sob uma perspectiva de DevOps. Isso é, sob a perspectiva de alguém que irá criar automações, plataformas e serviços para que outras pessoas possam consumir e utilizar a AWS de forma governada e padronizada. Prepare-se para responder sobre estratégias de *deployment*, serviços de pipelines de CI/CD (CodeCommit, CodeBuild, CodeDeploy, CodePipeline), cenários envolvendo multiregião, CloudFormation, AWS Organizations, Control Tower, Service Control Policy (SCP) e AWS Config. Além disso, os recursos mais básicos da AWS, como VPC, AZs, Subnet, Route Rable, Security Group, Network ACL, EC2, EBS, ELB, S3, IAM também serão exigidos de uma forma ou de outra, mas sem um nível muito grande de profundidade. No meu caso, também caíram muitas perguntas de EventBridge e Auto Scaling. Deixando claro que o conteúdo vai variar a cada prova. Não necessariamente você encontrará os mesmos tópicos e mesma proporção na sua prova.

## Conclusão

Por se tratar de uma prova de nível Professional, é uma prova exigente mas não tão desgastante quando a de Solutions Architect Professional. Entretanto, é cobrado um nível de profundidade um pouco maior de alguns assuntos. A gestão do tempo é fundamental. Além disso, se você também fez outras provas da AWS, então irá reaproveitar muita do que estudou, o que é uma vantagem. Outro ponto que ajuda é experiência: se você trabalha com AWS há um tempo, provavelmente vai se deparar com perguntas de cenários pelos quais já passou no dia-a-dia. Deixando claro aqui que o que funcionou para mim não necessariamente vai funcionar para você. Espero ter ajudado. Boa sorte!