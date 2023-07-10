---
title: "Plano de estudo para certificação AWS Certified Security - Specialty"
date: 2023-03-30T20:20:06-03:00
draft: false
tags: ["aws", "certificação", "segurança"]
ShowToc: true
TocOpen: true
---

No final de 2022, passei na prova [AWS Certified Security - Specialty](https://aws.amazon.com/certification/certified-security-specialty/?nc1=h_ls). Nesse post, vou compartilhar um pouco sobre como me preparei e minha experiência, pois essa foi a primeira vez que fiz a prova on-line, remotamente.

## Avisos

O conteúdo abaixo refere-se à versão SCS-C01 da prova. Apesar de não estar prevista uma nova versão da prova, dependendo de quando estiver lendo esse post, pode ser que o conteúdo esteja desatualizado. Então, fique atento.

Também quero deixar claro que o que funcionou para mim talvez não funcione para você. Cada pessoa tem uma forma diferente de estudar e aprender, e não há certo e nem errado. É importante que cada um conheça o que funciona melhor para si e faça os ajustes necessários. Eu, particularmente, gosto de misturar os vários formatos de conteúdo. Apesar de eu ter uma preferência por leitura, também gosto de complementar com vídeos. Também gosto de balancear a parte teórica com a prática. Enfim, avalie o que se adapta melhor ao seu estilo.

## Certificação vale a pena?

Já dei minha opinião sobre certificação valer a pena ou não no post sobre a prova [AWS Solutions Architect Professional]({{< relref "/blog/2022/plano-de-estudo-para-certificacao-AWS-Solutions-Architect-Professional.md#certifica%C3%A7%C3%A3o-vale-a-pena" >}}). Não vou ser repetitivo aqui, mas em resumo, certificação não é bala de prata e nem é perfeita. Entretanto, ela oferece uma maneira estruturada de estudar um determinado campo do conhecimento. O valor da certificação não está no certificado propriamente dito, mas sim no processo de preparação e aprendizado. Nesse caso, passar na prova é uma consequência, e não o objetivo final.

## A certificação AWS Security - Specialty

Segundo a AWS, essa certificação "*valida a experiência em segurança de dados e workloads na Nuvem AWS*". Como se trata de uma certificação do tipo *Specialty*, espera-se um nível de dificuldade mais avançado, semelhante às certificações do nível *Professional*.

{{< figure src="/img/2023/AWS-SCS.png" align="center" alt="Logo da certificação AWS Certified Security - Specialty" >}}

Entretanto, não achei a prova da AWS Security Specialty tão desgastante quanto a da AWS Solutions Architect Professional. Isso ocorreu devido aos seguintes motivos:
* escopo: ao contrário da prova AWS Solutions Architect Professional, que cobre uma infinidade de produtos e serviços da AWS, a prova AWS Security Specialty tem o seu escopo limitado. Isso é natural, pois como o próprio nome diz, o foco é em uma especialidade, no caso, Segurança. O resultado é que há menos conteúdo para estudar. Por falar em conteúdo...
* conteúdo reaproveitado: todo o conteúdo de Segurança estudado e conhecimento adquirido para a prova AWS Solutions Architect Professional é reaproveitado na prova AWS Security Specialty. Essa é uma grande vantagem. Claro que na prova AWS Security Specialty é exigido um conhecimento mais profundo e detalhado de alguns produtos e serviços, já que é uma prova de especialidade. Mas são conhecimentos complementares à base adquirida anteriormente, o que facilita bastante
* complexidade e tamanho das questões: achei o nível de complexidade das questões um pouco menor do que a prova AWS Solutions Architect Professional (o que não significa que é fácil). Não houve perguntas gigantes, que fosse necessário rolar a tela para conseguir ler por completo. A maioria das questões foram médias e, algumas poucas, com tamanho pequeno. Pelo que lembro, foi a prova em que menos vi perguntas do tipo "pegadinha"
* quantidade de perguntas e tempo da prova: são 65 questões de múltipla escolha ou múltiplas respostas, para 2 horas e 50 minutos de duração da prova. Para quem o Inglês não for o idioma nativo, é possível [solicitar um tempo extra de 30 minutos](https://aws.amazon.com/certification/policies/before-testing/?nc1=h_ls#Requesting_Accommodations). Na média, dá um pouco mais que 3 minutos por questão. Na prova AWS Solutions Architect Professional são 75 questões, e o tempo médio por pergunta acaba sendo menor.

Como toda prova, além do conhecimento técnico, também são validados sua capacidade de gestão de tempo e seu controle mental, para que fique no nível de atenção e foco adequados. Como sempre, algumas perguntas vão levar mais tempo para serem respondidas, e aí você precisa recuperar esse tempo gasto a mais nas perguntas que são menores e mais diretas. 

A prova pode ser feita em vários idiomas, inclusive Português do Brasil. Fiz a minha em Inglês (com o tempo extra de 30 minutos citado anteriormente), pois todo material de estudo que utilizei foi em Inglês. Prefiri assim pois queria evitar qualquer surpresa que fizesse eu gastar tempo, por exemplo, tentando entender o que uma eventual tradução "estranha" de algum termo técnico queria dizer. Mas de qualquer modo, a prova pode ser feita em Português para quem não se sentir confortável com Inglês.

Essa não é uma certificação barata, já que é de um nível mais avançado. O preço dela é de US$ 300. Se você já possui alguma certificação AWS, tem como benefício um desconto de 50% em outra prova. Nesse caso, o valor vai para US$ 150, que ainda é relativamente caro considerando o valor do dólar atualmente, mas é melhor do que o preço cheio. Como todas as demais certificações da AWS, ela tem validade de 3 anos e precisa ser renovada para ser mantida.

Particularmente, gostei bastante de estudar o conteúdo para essa prova. Ele mostra em detalhes como funcionam muitos serviços estruturantes de Segurança na AWS. Segurança é um assunto que permeia tudo quando falamos em Cloud e ter um bom entendimento sobre isso é primordial. Como a própria AWS gosta de dizer, [Segurança é "job zero"](https://aws.amazon.com/pt/blogs/enterprise-strategy/security-at-aws/), ou seja, é o tema mais prioritário e que precisa ser considerado em tudo, desde o início. Diria até que essa é uma certificação que qualquer profissional que trabalha com AWS deveria fazer, independentemente de trabalhar diretamente com Segurança ou não.

### Prova on-line

Como se tornou padrão com a pandemia de COVID-19 e as regras de distanciamento social, é possível fazer essa prova de certificação de forma on-line ou presencialmente em um centro de exames. Como eu queria fazer a prova ainda em 2022 e e as datas disponíveis em centros de exame eram somente para a segunda quinzena de janeiro de 2023, decidi por fazer a prova on-line. Nunca havia feito esse modelo de prova e, particularmente, não gostei da experiência. 

Primeiro, você precisa tirar várias fotos do local onde você vai fazer a prova e do seu documento. Eu tive que tirar uma seis versões de fotos do meu documento até que ficasse adequada aos critérios da Pearson VUE, que é a responsável pela prova. Quando você está preocupado com a prova, a última coisa que você quer é se preocupar com fotos de documentos. Em segundo lugar, você é filmado pela webcam durante toda a prova. Em determinado momento, fiz um movimento mais brusco para me ajeitar na cadeira e fui acionado pelo chat avisando que eu poderia me movimentar mas de maneira que meu rosto sempre ficasse visível na câmera. Ficar preocupado com esses detalhes secundários é muito ruim quando sua verdadeira preocupação deveria ser com a prova.

Além disso, eu também tinha preocupações com imprevistos como uma eventual falta de energia elétrica, problemas na conexão com Internet ou barulhos na vizinhança de casa que atrapalhassem a prova. Felizmente, nada disso aconteceu e acabou dando tudo certo. Dessa forma, não pretendo fazer uma prova de certificação on-line novamente, a não ser que não haja alternativa.

## Tempo de estudo

Estudei durante aproximadamente 45 dias, entre 2 e 3 horas de estudo por dia, e um pouco mais aos finais de semana (4 a 5 horas por dia). Lembrando que boa parte do material eu já conhecia por causa da prova AWS Solutions Architect Professional, então para esses casos acabou sendo uma revisão. Pode ser que você precise de mais tempo caso esteja vendo o conteúdo pela primeira vez. Além disso, cada pessoa tem um ritmo e outros compromissos que acabam demandando tempo, então isso vai variar. O importante é manter a consistência e a disciplina.

## Materiais de estudo

A maior parte do material apresentado aqui é paga. Antes de sair comprando material, se você assina alguma plataforma de cursos ou livros, vale verificar se ela já não oferece algo relativo a essa certificação. No meu caso, por exemplo, assino a [O'Reilly](https://www.oreilly.com/) e [A Cloud Guru](https://acloudguru.com/), e acabei lendo livros e fazendo cursos que encontrei lá.

### Leitura

Basicamente, li um livro (que está disponível na O'Reilly) e alguns *white papers* da AWS. Alguns estão marcados como "arquivados" pela AWS, o que significa que podem estar desatualizados, então é bom ficar atento. Mas de forma geral ainda possuem conteúdo que pode ajudar.

Abaixo, a lista de materiais de leitura que utilizei:

* livro [AWS Certified Security Specialty All-in-One Exam Guide (Exam SCS-C01)](https://www.amazon.com/Certified-Security-Specialty-Guide-SCS-C01/dp/1260461726)
* White Papers
    * [Security Pillar - AWS Well-Architected Framework](https://docs.aws.amazon.com/wellarchitected/latest/security-pillar/welcome.html)
    * [AWS Key Management Service Best Practices](https://d1.awsstatic.com/whitepapers/aws-kms-best-practices.pdf)
    * [AWS Key Management Service - AWS KMS Cryptographic Details](https://docs.aws.amazon.com/kms/latest/cryptographic-details/intro.html)
    * [AWS Best Practices for DDoS Resiliency](https://docs.aws.amazon.com/whitepapers/latest/aws-best-practices-ddos-resiliency/welcome.html)
    * [AWS Security Best Practices](https://d1.awsstatic.com/whitepapers/Security/AWS_Security_Best_Practices.pdf)
    * [Security at Scale: Logging in AWS](https://d0.awsstatic.com/whitepapers/compliance/AWS_Security_at_Scale_Logging_in_AWS_Whitepaper.pdf)
    * [Organizing Your AWS Environment Using Multiple Accounts](https://docs.aws.amazon.com/whitepapers/latest/organizing-your-aws-environment/organizing-your-aws-environment.html) 
    * [AWS Multiple Account Security Strategy - How do I manage multiple AWS accounts for security purpose?](https://d1.awsstatic.com/aws-answers/AWS_Multi_Account_Security_Strategy.pdf)
    * [Building a Scalable and Secure Multi-VPC AWS Network Infrastructure](https://docs.aws.amazon.com/whitepapers/latest/building-scalable-secure-multi-vpc-network-infrastructure/welcome.html)


### Vídeos

Atualmente, a maior parte dos materiais feitos para provas de certificação são cursos em vídeos. Assisti aos cursos do A Cloud Guru e da Udemy. Os dois são bons e bem completos, com vantagem para o da Udemy. Não deixe a aparência "caseira" e "independente" do curso da Udemy te enganar (se você assistir vai entender o que eu quero dizer): o instrutor é bem didático, se preocupando em explicar os "porquês" em detalhes. Surpreendeu-me positivamente! O da AWS é bem curto e dá algumas dicas, mas não espere nada além disso. 

* [AWS Certified Security Specialty](https://www.udemy.com/course/aws-certified-security-specialty/) - Udemy - de Zeal Vora
* [AWS Certified Security - Specialty 2020](https://acloudguru.com/course/aws-certified-security-specialty) - A Cloud Guru - de Ryan Kroonenburg e Faye Ellis
* [Exam Readiness: AWS Certified Security - Specialty](https://explore.skillbuilder.aws/learn/course/external/view/elearning/97/exam-readiness-aws-certified-security-specialty?ss=sec&sec=prep) - AWS - gratuito

### Simulados

Os simulados são importantes pois é a experiência mais próxima que você terá da prova real. Os simulados listados abaixo possuem uma explicação detalhada da resposta de cada questão, o que é fonte importante de conhecimento para aprender coisas novas. Além disso, é comum aparecer alguns tópicos que não haviam sido abordados nos cursos, o que acabava complementando o conhecimento. Os melhores simulados, na minha opinião, são do Jon Bonso (Tutorials Dojo).
* [AWS Certified Security Specialty Practice Exams 2023](https://portal.tutorialsdojo.com/courses/aws-certified-security-specialty-practice-exams/) - Tutorials Dojo - Jon Bonso
* [SCS-C01: AWS Certified Security – Specialty Practice Exams](https://www.udemy.com/course/new-aws-certified-security-specialty-exams/) - Udemy - Viktor Afimov
* [AWS Certified Security - Specialty Sample Questions](https://d1.awsstatic.com/training-and-certification/docs-security-spec/AWS-Certified-Security-Speciality_Sample-Questions.pdf) - AWS - Gratuito
* [AWS Certified Security - Specialty Official Practice Question Set](https://explore.skillbuilder.aws/learn/course/external/view/elearning/12473/aws-certified-security-specialty-practice-question-set-scs-c01-english?ss=sec&sec=prep) - AWS - Gratuito
* [The AWS Certification Quiz Show: Security - Specialty exam, Episode 1](https://explore.skillbuilder.aws/learn/course/external/view/elearning/353/the-aws-certification-quiz-show-security-specialty-exam-episode-1) - AWS - Gratuito
* [The AWS Certification Quiz Show: Security - Specialty exam, Episode 2](https://explore.skillbuilder.aws/learn/course/external/view/elearning/323/the-aws-certification-quiz-show-security-specialty-exam-episode-2) - AWS - Gratuito
* [The AWS Certification Quiz Show: Security - Specialty exam, Episode 3](https://explore.skillbuilder.aws/learn/course/external/view/elearning/300/the-aws-certification-quiz-show-security-specialty-exam-episode-3) - AWS - Gratuito
* [The AWS Certification Quiz Show | Episode 13 | AWS Certified Security - Specialty](https://www.twitch.tv/aws/video/467770461) - AWS - Gratuito

## Principais assuntos

Por se tratar de uma prova de nível de especialidade em Segurança, você tem que dominar temas relacionados a IAM (como os vários tipos de policies, IAM Roles, Cross-account IAM Roles, SSO, etc), KMS, CloudHSM, tipos de criptografias (server-side, client-side, em trânsito, em repouso, simétrica, assimétrica, etc), segurança de infraestrutura (NACL, Security Groups), serviços como Guard Duty, AWS Shield, Cloud Trail.  Obviamente que isso vai variar a cada prova. Não necessariamente você encontrará os mesmos tópicos na sua prova.

## Conclusão

Como disse anteriormente, por se tratar de uma prova de especialidade, no caso Segurança, o escopo fica limitado, resultando em menos conteúdo para estudar quando comparada com a prova AWS Solutions Architect Professional. Além disso, se você também fez essa última prova, então irá reaproveitar muita do que estudou, o que é uma vantagem. Lembrando que o que funcionou para mim não necessariamente vai funcionar para você. Expero que esse plano de estudo possa contribuir de alguma forma com a preparação de outras pessoas para a prova. Bons estudos!