---
title: "Acessando serviços AWS de forma privada com Interface VPC Endpoint/PrivateLink"
date: 2023-08-10T20:09:40-03:00
draft: false
tags: ["aws", "vpc endpoint", "vpc", "infraestrutura", "privatelink"]
cover: 
  image: "/img/2023/AcessoPrivadoAWS-1-interface-vpc-endpoint.png"
---

Como sabemos, a AWS possui uma série de produtos que são oferecidos como serviços (ex: SQS, SNS, S3, DynamoDB, etc). Esses serviços são acessados através de **endpoints** que, por padrão, são "públicos", ou seja, são acessados pela Internet. É através desses endpoints públicos que é possível interagir com as APIs dos serviços da AWS pela Internet usando, por exemplo, a linha de comando (AWS CLI) em nossos computadores pessoais.

Os endpoints são basicamente URLs e no geral seguem o padrão abaixo:

```
protocolo://[código-do-serviço].[código-da-região].amazonaws.com
```

Por exemplo, o endpoint do SQS da região N.Virginia da AWS é:

````
https://sqs.us-east-1.amazonaws.com
````

Mais informações em [AWS service endpoints](https://docs.aws.amazon.com/general/latest/gr/rande.html).

Aplicações que são executadas na AWS certamente precisam acessar um ou mais desses serviços da AWS. Como os endpoints por padrão são públicos, isso significa que as aplicações precisam estar em uma VPC que tenha conectividade com a Internet para conseguir acessar os endpoints e usar esses serviços. Na prática, isso se traduz na necessidade de se ter um Internet Gateway na VPC. Se a aplicação estiver em uma subnet privada, também será necessário um NAT Gateway. O diagrama abaixo representa esse cenário, em que a aplicação em uma instância EC2 em uma subnet privada precisa acessar uma fila SQS na AWS.

{{< figure src="/img/2023/AcessoPrivadoAWS-1-endpoint-publico.png" align="center" alt="Diagrama de arquitetura do cenário de acesso ao endpoint público de um serviço AWS. O diagrama mostra uma aplicação em uma instância EC2 em uma subnet privada de uma VPC AWS fazendo acesso a uma fila SQS pelo endpoint público desse serviço. O tráfego passa por um NAT Gateway e por um Internet Gateway antes de chegar na fila SQS." >}}

Aqui há um **ponto de atenção importante** que pode gerar confusão: nesse cenário, apesar do acesso a endpoints públicos e do tráfego passar pelo Internet Gateway, a AWS afirma que o tráfego **não deixa sua rede privada**. Dessa forma, como a origem e o destino do acesso ficam na própria AWS, **o tráfego não vai pela Internet**, apesar do destino ser um endpoint público acessível pela Internet e apesar de passar pelo Internet Gateway. Isso pode parecer um pouco confuso e contraintuivo, já que seria natural supor que essa comunicação ocorreria pela Internet, mas [em suas documentações](https://repost.aws/questions/QU4fn697qVTRWaB0rhGZfHZw/does-traffic-between-amazon-ec2-and-amazon-s3-really-go-over-the-internet) a AWS afirma que [isso não acontece na prática](https://aws.amazon.com/vpc/faqs/#Connectivity:~:text=Does%20traffic%20go%20over%20the%20internet%20when%20two%20instances%20communicate%20using%20public%20IP%20addresses%2C%20or%20when%20instances%20communicate%20with%20a%20public%20AWS%20service%20endpoint%3F).

Isso pode não ser um problema caso a aplicação já precise ter conectividade com a Internet por outros motivos. Entretanto, caso a aplicação não tenha essa necessidade, seríamos obrigados a prover essa conectividade com a Internet (com Internet Gateway e talvez com o NAT Gateway) somente para acessar os endpoints públicos dos serviços da AWS. Para esses cenários, em que não há necessidade ou não se quer acessar os serviços da AWS através de seus endpoints públicos, existe a possibilidade de acessá-los de forma privada através de **VPC Endpoints**.

## VPC Endpoints

Existem três tipos de VPC Endpoints: o Gateway, o Gateway Load Balancer e o Interface. O **Gateway VPC Endpoint** suporta somente dois serviços da AWS (S3 e DynamoDB), funciona através da criação de regras na Route Table e é gratuito. Entretanto, esse tipo de VPC Endpoint não recebe mais evolução da AWS.

O **Gateway Load Balancer VPC Endpoint** serve para enviar tráfego de forma privada para *appliances* virtuais de terceiros, geralmente para inspeções de segurança ou outros serviços de rede. Ele também é configurado através da criação de regras na Route Table.

Os VPC Endpoints do tipo Gateway e Gateway Load Balancer não serão abordados nesse artigo. Mais informações sobre podem ser encontradas em [Gateway endpoints](https://docs.aws.amazon.com/vpc/latest/privatelink/gateway-endpoints.html) e [Access virtual appliances through AWS PrivateLink](https://docs.aws.amazon.com/vpc/latest/privatelink/vpce-gateway-load-balancer.html).


O **Interface VPC Endpoint** [suporta uma gama muito maior de serviços da AWS](https://docs.aws.amazon.com/vpc/latest/privatelink/aws-services-privatelink-support.html) (que são atualizados conforme novos produtos são lançados) e utiliza uma tecnologia da AWS chamada [PrivateLink](https://docs.aws.amazon.com/vpc/latest/privatelink/what-is-privatelink.html), que permite estabeler conectividade privada entre a VPC e os serviços da AWS suportados. Isso ocorre através da criação de uma ENI - Elastic Network Interface (uma placa de rede virtual) na subnet de uma VPC e que dá conectividade direta aos serviços. Na prática, é como se esses serviços da AWS estivessem na própria VPC. Dessa forma, a aplicação pode estar em uma VPC sem conectividade com a Internet e vai conseguir acessar o serviço AWS através do Interface VPC Endpoint, sem a necessidade de acesso ao endpoint público. O desenho de arquitetura a seguir representa como isso funciona considerando o mesmo exemplo anterior, ou seja, uma aplicação em uma instância EC2 em uma subnet privada acessando uma fila SQS na AWS:

{{< figure src="/img/2023/AcessoPrivadoAWS-1-interface-vpc-endpoint.png" align="center" alt="Diagrama de arquitetura do cenário de acesso ao serviço AWS de forma privada. O diagrama mostra uma aplicação em uma instância EC2 em uma subnet privada de uma VPC AWS fazendo acesso a uma fila SQS pelo Interface VPC Endpoint, que utiliza a tecnologia AWS PrivateLink. O tráfego passa por uma ENI - Elastic Network Interface criada na subnet." >}}


É importante notar que:
* a aplicação está em uma subnet privada, ou seja, sem acesso a Internet.
* o acesso acontece através da ENI (placa de rede virtual) criada na subnet, que consegue acessar a fila SQS de forma privada através do PrivateLink. Para a aplicação é como se a fila SQS estivesse na VPC.
* o acesso ao serviço AWS pode ser feito através da mesma URL do endpoint público. Quando o Interface VPC Endpoint é criado, automaticamente é feita uma configuração no DNS que resolve a URL do endpoint público para o endereço IP privado da ENI na VPC ao invés do endereço IP público (essa é uma técnica chamada [*split-horizon DNS*](https://en.wikipedia.org/wiki/Split-horizon_DNS)). Dessa forma, o uso do Interface VPC Endpoint é transparente para a aplicação, que não precisa ser alterada. Mais detalhes em [DNS Resolution](https://docs.aws.amazon.com/vpc/latest/privatelink/privatelink-access-aws-services.html#interface-endpoint-dns-resolution).

### Preparando o ambiente

> **Atenção**: A AWS oferece um nível gratuito para experimentação de seus produtos ([AWS Free Tier](https://aws.amazon.com/free/)) que pode ser utilizado para implementação dos exemplos, mas o leitor deve ficar atento para eventuais custos que possam ser gerados.

Para demonstrar como isso funciona na prática, foi criado um [template CloudFormation](https://github.com/roneda/exemplos-blog/blob/main/vpc-subnetprivada-ec2-sessionmanager.yaml) que provisiona um ambiente inicial baseado no diagrama anterior. A stack será composta por:
* uma VPC;
* uma subnet privada;
* dois Interface VPC Endpoints para acessar os endpoints do [Session Manager]({{< relref "/blog/2023/acessando-recursos-remotamente-em-uma-vpc-na-AWS-parte-3.md">}}). Utilizaremos o Session Manager para ter acesso ao shell da EC2 para demonstrar o funcionamento do Interface VPC Endpoint. Como a EC2 ficará em uma subnet sem conectividade com a Internet, o acesso aos endpoints do Session Manager da AWS ocorrerá através desses Interface VPC Endpoints;
* um security goup a ser utilizado nos Interface VPC Endpoints, que permite tráfego de entrada na porta 443 (lembre-se que o acesso aos endpoints da AWS ocorre via HTTPS através da ENI criada);
* uma instância EC2 que utiliza Amazon Linux 2023 (AMI baseada na região AWS de N. Virginia - us-east-1);
* uma IAM Role e um Instance Profile, que serão utilizados na instância EC2 e com permissões para acessar o SQS e o Session Manager;
* uma fila SQS;

A partir desse ambiente base, serão feitas as configurações necessárias para permitir o acesso da EC2 à fila SQS de forma privada.

Faça o [download do template CloudFormation](https://github.com/roneda/exemplos-blog/blob/main/vpc-subnetprivada-ec2-sessionmanager.yaml) para seu computador. Acesse sua conta na AWS e, no painel de gerenciamento do CloudFormation, clique no botão "**Create stack > With new resources (standard)**". Escolha a opção **"Upload a template file"** e faça o upload do arquivo de template CloudFormation obtido anteriormente. Na página seguinte, em **"Stack name"** preencha com um nome que achar melhor (ex: StackBase) e prossiga nas próximas páginas com os valores padrão, até iniciar a criação da stack. Após alguns minutos, a stack estará criada.

Na aba **Resources**, encontre a fila SQS criada e anote o valor da coluna **"Physical ID"**, que contém a URL da fila SQS a ser utilizada posteriormente.

### Utilizando Interface VPC Endpoint

Quando estiver disponível, a instância EC2 estará em uma subnet privada, sem conectividade com a Internet e nem com o SQS. Para confirmar isso, acesse o painel de EC2 na console AWS, em seguida vá para a opção de menu **Instances** no lado esquerdo da página, selecione a instância **AppServer** e clique em **Connect** na parte de cima da página. Em seguida, escolha a opção **"Session Manager"**. Se tudo correu conforme o esperado, o botão **Connect** estará habilitado e clicando nele será aberta uma janela no browser simulando um terminal na instância EC2.

Digite o comando abaixo para tentar acessar um site na Internet com um timeout de 15 segundos:

```` shell
curl -I https://example.com --connect-timeout 15
````

Note que após 15 segundos, aparece uma mensagem de erro informando que não foi possível se conectar ao servidor. Isso confirma que a instância EC2 não consegue acessar a Internet. Agora, execute o comando da AWS CLI abaixo para tentar enviar uma mensagem para a fila SQS (substitua **"URL da fila"** pela URL gerada na criação da fila na stack de CloudFormation)

```` shell
aws sqs send-message --queue-url <URL da fila> --message-body "Olá mundo!" 
```` 

Após um tempo, aparece uma mensagem de timeout indicando que não foi possível realizar a operação. Em seguida, execute o comando abaixo que deveria retornar o endereço IP do endpoint do serviço SQS na região de N. Virginia da AWS:

```` shell
dig sqs.us-east-1.amazonaws.com +short
````

O endereço IP retornado é o público, e não um endereço IP privado da VPC. A figura abaixo mostra os resultados dos comandos apresentados:

{{< figure src="/img/2023/AcessoPrivadoAWS-1-sessionmanager-1.png" align="center" alt="Imagem do terminal da instância EC2 aberto no browser pelo Session Manager com o resultado de erro dos comandos" >}}

Agora faremos a criação do Interface VPC Endpoint para o serviço SQS. Para isso, acesse o painel de VPC na console AWS. No menu do lado esquerdo, escolha a opção **"Virtual Private Cloud > Endpoints"**, clique no botão **"Create endpoint"** e informe os seguintes dados:
* Name: **SQSVPCEndpoint**
* Service Category: selecione **AWS Services**
* Service Name:  selecione **com.amazonaws.us-east-1.sqs**
* VPC: selecione **myVPC**
* Availability Zone: selecione **us-east-1a (use1-az4)**
* Subnet ID: escolha a opção **mySubnet**
* Security Groups: selecione **VPCEndpointSecurityGroup**
* Clique em **"Create endpoint**

Após o Interface VPC Endpoint ficar disponível, selecione-o e na parte de baixo da página, na aba **Subnets**, role a tela para a direita até encontar o campo **"Network Interface ID"**. Clique no link para abrir a página onde é possível ver a ENI - Elastic Network Interface que foi criada na subnet, através da qual será possível acessar o endpoint do SQS de forma privada.

{{< figure src="/img/2023/AcessoPrivadoAWS-1-eni.png" align="center" alt="Imagem que mostra a ENI criada na subnet junto com o Interface VPC Endpoint" >}}

Volte para o terminal do Session Manager e reexecute os três comandos acima. O primeiro, que tenta acessar um site na Internet, continua a não funcionar. Esse é o comportamento esperado, pois a subnet continua sem conectividade com a Internet. Entretanto, os dois comandos seguintes, um que envia uma mensagem para a fila SQS e o outro que retorna o endereço IP do endpoint do serviço SQS agora funcionam. Note que o endereço IP retornado no último comando é um endereço IP privado da faixa de IPs da VPC, que é o mesmo endereço IP associado a ENI:

{{< figure src="/img/2023/AcessoPrivadoAWS-1-sessionmanager-2.png" align="center" alt="Imagem do terminal da instância EC2 aberto no browser pelo Session Manager com o resultado de sucesso dos comandos" >}}

Por fim, confirme o recebimento da mensagem na fila SQS. Na console da AWS, acesse o painel do SQS e selecione a **FilaTeste**. Clique em **"Send and receive messages"**, depois clique em **"Poll for messages"** e veja que  aparece a mensagem. Clicando nela é exibido o corpo da mensagem com o texto que foi enviado pelo comando da AWS CLI:

{{< figure src="/img/2023/AcessoPrivadoAWS-1-sqs.png" align="center" alt="Imagem mostrando o texto 'Olá mundo!' no corpo da mensagem da fila SQS" >}}

É importante destacar que o custo do Interface VPC Endpoint é baseado por hora em que ele está provisionado em cada AZ e pelo tráfego processado por ele. Mais informações em [AWS PrivateLink Pricing](https://aws.amazon.com/privatelink/pricing/). Dessa forma, depois de finalizar os testes, não esqueça de excluir o Interface VPC Endpoint para o SQS e apagar a stack de CloudFormation com os demais recursos.

Nesse artigo foi mostrado como é possível acessar serviços da AWS de forma privada, a partir de uma VPC que não tenha conectividade com a Internet. Outro ponto interessante é que esse modelo não se aplica somente aos serviços AWS. Ou seja, ele também pode ser utilizado para acessar serviços customizados ou de terceiros de forma privada através de VPC Endpoints Services, mas isso é assunto para um próximo post. 

## Referências

* [What is AWS PrivateLink?](https://docs.aws.amazon.com/vpc/latest/privatelink/what-is-privatelink.html)
* [Access AWS services through AWS PrivateLink](https://docs.aws.amazon.com/vpc/latest/privatelink/privatelink-access-aws-services.html)
* [Does traffic between Amazon EC2 and Amazon S3 really go over the internet?](https://repost.aws/questions/QU4fn697qVTRWaB0rhGZfHZw/does-traffic-between-amazon-ec2-and-amazon-s3-really-go-over-the-internet)
* [Does traffic go over the internet when two instances communicate using public IP addresses, or when instances communicate with a public AWS service endpoint?](https://aws.amazon.com/vpc/faqs/#Connectivity:~:text=Does%20traffic%20go%20over%20the%20internet%20when%20two%20instances%20communicate%20using%20public%20IP%20addresses%2C%20or%20when%20instances%20communicate%20with%20a%20public%20AWS%20service%20endpoint%3F)
* [Reduce Cost and Increase Security with Amazon VPC Endpoints](https://aws.amazon.com/blogs/architecture/reduce-cost-and-increase-security-with-amazon-vpc-endpoints/)
* [VPC Endpoint Workshop](https://catalog.us-east-1.prod.workshops.aws/workshops/25daa7f1-11a5-4c96-8923-9b0e333acc59/en-US)