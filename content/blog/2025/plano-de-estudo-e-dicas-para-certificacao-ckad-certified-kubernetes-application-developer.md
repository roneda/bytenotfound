---
title: "Plano de estudo e dicas para certificação CKAD - Certified Kubernetes Application Developer"
date: 2025-05-19T21:23:06-03:00
draft: false
tags: ["kubernetes", "certificação", "ckad", "linux foundation", "cncf"]
ShowToc: true
TocOpen: true
cover: 
  image: "/img/2023/AWS-DOP.png"
---

No começo de abril de 2025, passei na prova [CKAD - Certified Kubernetes Application Developer](https://training.linuxfoundation.org/certification/certified-kubernetes-application-developer-ckad/). Vou compartilhar como me preparei para a prova, com dicas para quem estiver interessado.


## A certificação CKAD - Certified Kubernetes Application Developer

A CKAD é uma das certificações de Kubernetes oferecidas pela Linux Foundation e CNCF - Cloud Native Computing Foundation. Como o próprio nome indica, o público dessa certificação são pessoas desenvolvedoras. Entretanto, o objetivo não é avaliar o desenvolvimento de aplicações propriamente dito, e sim o que uma pessoa desenvolvedora deve conhecer de Kubernetes para usar e operar uma aplicação que será executada nesse ambiente. 

Segundo a [página oficial da certificação](https://training.linuxfoundation.org/certification/certified-kubernetes-application-developer-ckad/), "*o exame certifica que os candidatos podem projetar, construir e implantar aplicações cloud-native em Kubernetes*". 

{{< figure src="/img/2025/ckad.png" align="center" alt="Logo da certificação CKAD - Certified Kubernetes Application Developer" >}}

No escopo da prova, estão quase todos recursos do Kubernetes, o que é bastante coisa. Espere questões sobre Deployment, Pod, Service, Ingress, CronJob, Configmap, Secrets, containers, estratégias de deployment, Service Account, depreciação de APIs, Probes, etc. O conteúdo mais detalhado pode ser consultado no [currículo da prova](https://github.com/cncf/curriculum).

Uma característica importante do exame é que ele é totalmente prático, ao contrário da maioria das certificações, cujos exames são baseados em perguntas teóricas de múltipla escolha. Durante o exame, o candidato terá acesso remoto a ambientes Kubernetes onde deverá executar os comandos necessários para atingir os objetivos esperados de cada questão. Achei excelente esse modelo de exame, pois avalia a capacidade do candidato para resolver problemas na prática. Isso também ajuda você a saber se acertou ou não a questão, pois dá para validar na hora se o que foi feito gerou ou não o resultado esperado. Além disso, no ambiente remoto você também poderá consultar a documentação oficial do Kubernetes e de outras tecnologias se a pergunta exigir isso. No próprio enunciado da questão aparecem links para as documentações.

No meu caso, foram 16 questões, para um perído de 2 horas de duração da prova. Eu dividiria o nível de complexidade das questões em 3 com base na quantidade de tarefas exigidas de cada questão: simples (questões mais diretas), média complexidade (questões com um nível maior de tarefas para serem concluídas) e alta complexidade (questões com várias tarefas necessárias para serem concluídas). Em torno de 70% das questões foram de simples ou média complexidade, sendo os 30% restante as mais complexas. Cada questão é independente, ou seja, você não precisa concluir uma questão para conseguir responder outra. Mas dentro de uma questão, as tarefas que a compõem possuem dependência entre si na maior parte das vezes. 

Essa é uma prova bem cara. Recentemente, houve um reajuste do preço e, no momento que escrevo esse post, ela está custando US$ 445. Vale a pena ficar de olho no site da Linux Foundation, pois em algumas épocas do ano eles costumam fazer promoções com 40% ou 50% de desconto, o que ajuda bastante. Nesse valor está incluso a possibilidade de um *retake*, ou seja, se você não passar na primeira tentativa, tem direito a uma segunda chance sem custo adicional. Também está incluso o acesso a duas sessões de um simulado (Exam Simulator) na plataforma [Killer Shell](https://killer.sh/). Uma vez iniciada uma das sessões do simulado, ela ficará disponível somente por 36 horas. Durante esse período, é possível fazer o simulado quantas vezes você quiser. No geral, achei que a dificuldade do simulado da CKAD foi um pouco maior do que a prova verdadeira. Então, se você for bem no simulado, é um bom indicativo de que está preparado para a prova. Se você quiser, também é possível adquirir esse simulado diretamente na plataforma Killer Shell, mas você terá que pagar por isso, além do custo da prova.

A CKAD tem validade de 2 anos e precisa de renovação se quiser ser mantida. Fiz a prova em Inglês (**o Português não é uma opção de idioma disponível**). A pontuação mínima para ser aprovado é de 66%. Essa prova só pode ser feita de forma on-line, não existindo ainda a opção de fazê-la centros de exames. Procuro evitar esse modelo de prova, pois não tive uma boa experiência quando fiz o exame da [AWS Security Specialty]({{< relref "/blog/2023/plano-de-estudo-para-certificacao-aws-certified-security-specialty.md" >}}). Como essa é a única opção, não teve jeito. Para meu alívio, não tive nenhuma surpresa desagradável e tanto o processo de check-in quanto o decorrer da prova foram bem tranquilos. Você precisa instalar um aplicativo da PSI em seu computador, que é a plataforma usada para a realização da prova. 

## Materiais de estudo
Utilizei os seguintes materiais para me preparar para a prova:
* curso [Kubernetes Certified Application Developer (CKAD) with Tests](https://www.udemy.com/course/certified-kubernetes-application-developer/) - Udemy - de Mumshad Mannambeth: se você tiver que escolher uma única opção, este é o curso a ser escolhido. É bem completo e detalhado, explica os porquês de como algumas coisas são feitas e funcionam no Kubernetes. Além disso, você também ganha acesso a ambientes de laboratórias na plataforma [KodeKloud](https://kodekloud.com/), o que é muito importante, já que essa é uma prova prática. Se você for assinante da KodeKloud, esse curso já está incluso e não é necessário comprá-lo na Udemy.
* livro [Kubernetes: Up and Running, 3rd Edition](https://learning.oreilly.com/library/view/kubernetes-up-and/9781098110192/): apesar de não ser um livro voltado para a prova de certificação, com ele você ganhará conhecimentos gerais sobre Kubernetes. 
* livro [Certified Kubernetes Application Developer (CKAD) Study Guide, 2nd Edition](https://learning.oreilly.com/library/view/certified-kubernetes-application/9781098152857/): apesar de ser um livro voltado especificamente para o exame CKAD, não é tão completo e nem tão profundo quando o curso da Udemy que sugeri anteriormente. Se você for assinante da O'Reilly, poderá fazer os labs que são um complemento desse livro, disponíveis em [Certified Kubernetes Application Developer (CKAD) Exam Prep Labs](https://learning.oreilly.com/playlists/2e9fe6dc-2a05-47fe-ae0a-34d6485287cc/). Uma ótima oportunidade para exercitar o conhecimento, considerando que é um exame prático.


## Dicas
Vamos às dicas:
* gestão do tempo: ponto crítico para o sucesso na prova, ainda mais por ser prática. Você tem que ter uma estratégia muito bem definida para gerenciar bem seu tempo. 2 horas é uma quantidade de tempo bem apertada para o número de questões. A estratégia que adotei, e que sugiro, é que sempre que você se deparar com uma questão que seja mais complexa ou que aborde um assunto que você não domine, marque a questão para revisão e vá para a próxima. Você tem que tomar essa decisão rapidamente. Não gaste tempo em questões que vão exigir mais tempo para serem resolvidas sem passar por todas questões antes. Resolva primeiro as questões mais simples ou de média complexidade dos temas que você conhece mais, e deixe as mais complexas e de assuntos que você não domina para o final. Com isso, você tem mais chance de pontuar nas questões de assuntos que tem mais domínio antes do tempo acabar. Quando tiver passado por todas questões, retorne para aquelas que você marcou para revisão, começando novamente por aquelas que você acha que tem mais chance de concluir ou que vai levar menos tempo dentre aquelas que restaram. Repita esse ciclo até conseguir responder todas ou até terminar o tempo. No meu caso, terminei a última questão faltando apenas 2 minutos para o tempo acabar. 
* a maioria das questões é composta de mais de uma tarefa. Mesmo que não saiba responder completamente uma questão, faça as tarefas que souber, pois perguntas parcialmente respondidas também contribuem para a pontuação final.
* use todas técnicas disponíveis para ganhar tempo, como configuração de alias, atalhos, etc. Qualquer coisa que economize tempo ou que evite digitar teclas desnecessariamente faz diferença. Por exemplo, ao invés de digitar o comando **kubectl**, use o alias **"k"**, que já vem configurado no ambiente da prova. Assim, ao invés de digitar:
  ```` shell
  kubectl get pod
  ````
  use
  ```` shell
  k get pod
  ````
  Pode parecer uma coisa boba, mas se você lembrar que terá que digitar esse comando dezenas ou centenas de vezes, a cada vez você economiza 6 teclas digitadas, o que vai economizar muito tempo. Além disso, você pode criar seus próprios alias ou variáveis de ambiente. Eu, por exemplo, configurei o seguinte alias e variável de ambiente:
  ```` shell
  alias ka="k apply -f"
  export dry="--dry-run=client -o yaml"
  ````
  que usava da seguinte forma
  ```` shell
  # para gerar um template yaml de um comando
  k run pod --image=nginx $dry > pod.yaml

  # para aplicar um template yaml
  ka pod.yaml
  ````
  Esses são comandos bastante exigidos na prova e, se usados dessa maneira, ajudam a otimizar o tempo. Avalie outros comandos que você ache interessante usar essa estratégia. 
  Já o comando abaixo configura um *namespace* padrão. Dessa forma, nas questões em que você tem que trabalhar com um *namespace* diferente do *default*, não é necessário ficar especificando o nome do *namespace* a cada comando, o que vai resultar em menos digitação e, consequentemente, menos tempo gasto:
  ```` shell
  k config set-context --current --namespace <NOME_NAMESPACE>
  ````
* o ambiente remoto onde a prova é realizada é um ambiente Linux. Portanto, você deve saber usá-lo muito bem. Não é necessário que você seja um especialista em Linux, mas você tem que ficar bem a vontade usando-o. Além disso, certamente você precisará editar algum objeto do Kubernetes ou editar algum arquivo yaml durante a prova. Portanto, você tem que dominar o editor de texto. Se não tiver fluência no **vim** (como é o meu caso), use outro editor em que se sinta à vontade e no qual você seja mais produtivo. Eu utilizei o **nano**. Para mudar o editor de texto padrão usado para edição de objetos do Kubernetes, configure a variável de ambiente conforme abaixo. Dessa forma, sempre que você der o comando **kubectl edit**, será aberto o editor de texto configurado:
  ```` shell
  export KUBE_EDITOR=nano
  ````
* apesar de ser uma prova com consulta liberada à documentação oficial do Kubernetes, use somente em último caso, pois isso consome tempo. Preferencialmente, você deve ter decorado os principais comandos dos principais objetos do Kubernetes. Se não decorou, use o help nativo do próprio **kubectl**, que normalmente vêm com exemplos que ajudam bastante. Se precisar de um arquivo yaml, prefira gerar através do **kubectl**, que é mais rápido (configure uma variável de ambiente para agilizar isso, conforme explicado anteriormente). Somente use a documentação do site para os objetos do Kubernetes que não podem ser criados ou gerado o yaml através do **kubectl**. Para isso, você precisa saber quais objetos do Kubernetes podem ser criados a partir do **kubectl** e quais só podem ser criados de forma declarativa (com arquivo yaml). Para os casos em que não houver outra alternativa a não ser consultar a documentação (por exemplo, para obter um exemplo de arquivo yaml de determinado objeto), saiba como chegar na documentação e conheça-a muito bem. A última coisa que você vai querer fazer durante a prova é buscar na documentação algo que você nunca pesquisou antes.
* pratique, pratique e pratique. Muito mesmo. Esteja bem afiado. Você só vai saber que tipo de tarefa vai levar mais ou menos tempo se praticar. Você só vai saber quais atalhos e alias serão mais úteis se praticar. Você só vai dominar o editor de texto e o mínimo necessário de Linux para a prova se praticar. Você só vai conhecer e saber quando usar a documentação do site ou não se praticar. Desenvolva essas habilidades e conhecimentos enquanto estiver estudando e praticando para a prova. Ter um ambiente onde você pode exercitar isso é obrigatório, seja no seu computador ou em algum laboratório remoto de alguma plataforma ou ambiente *sandbox*. Você tem que chegar na prova com essas técnicas dominadas.


## Conclusão

A CKAD é uma prova exigente, para a qual a gestão do tempo é primordial. É exigido conhecimento de uma ampla quantidade de assuntos relacionados a Kubernetes. Praticar é a melhor maneira para se preparar para a prova. Espero que ajude!