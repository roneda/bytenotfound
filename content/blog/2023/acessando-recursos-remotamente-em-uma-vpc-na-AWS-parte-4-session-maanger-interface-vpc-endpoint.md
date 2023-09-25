---
title: "Acessando recursos remotamente em uma VPC na AWS - parte 4 - AWS Systems Manager Session Manager com Interface VPC Endpoint"
date: 2023-09-24T10:48:58-03:00
draft: false
tags: ["aws", "vpc", "session manager", "aws systems manager", "acesso remoto", "infraestrutura", "segurança", "vpc endpoint", "privatelink"]
cover: 
  image: "/img/2023/AcessoRemotoAWS-4-sessionmanager-vpcendpoint.png"
---

No [post anterior dessa série]({{< relref "/blog/2023/acessando-recursos-remotamente-em-uma-vpc-na-AWS-parte-3.md">}}), vimos como utilizar o [**Session Manager**](https://docs.aws.amazon.com/systems-manager/latest/userguide/session-manager.html), um serviço gerenciado da AWS, para acessar uma instância EC2 remotamente em uma VPC, sem a necessidade de um Bastion Host e sem que a instância EC2 precisasse ficar em uma subnet pública. Para que isso funcione, é necessário que o [SSM Agent](https://docs.aws.amazon.com/systems-manager/latest/userguide/ssm-agent.html) esteja instalado na instância EC2, pois é ele que irá se comunicar com os serviços do Session Manager e do Systems Manager, conforme diagrama abaixo:

{{< figure src="/img/2023/AcessoRemotoAWS-3-sessionmanager.png" align="center" alt="Diagrama de arquitetura do cenário de acesso via Session Manager. O diagrama mostra um usuário acessando o serviço do Session Manager, através da Internet. O SSM Agent, instalado em uma instância EC2 com uma IAM Role configurada, também acessa o serviço do Session Manager e o serviço Systems Manager na AWS através dos enpoints públicos." >}}

No cenário demonstrado no post anterior, a comunicação às APIs dos serviços Session Manager e Systems Manager ocorria via endpoints públicos. Assim, a instância EC2 (que está em uma subnet privada) precisa de acesso de saída para Internet. Isso é fornecido através de um NAT Gateway na subnet pública, que por sua vez utiliza o Internet Gateway. Apesar da necessidade de saída para Internet, esse tráfego se mantém na rede da AWS, pois estão sendo acessados endpoints públicos da própria AWS.

> Aqui há um **ponto de atenção importante** que pode gerar confusão: nesse cenário, apesar do acesso a endpoints públicos e do tráfego passar pelo Internet Gateway, a AWS afirma que o tráfego **não deixa sua rede privada**. Dessa forma, como a origem e o destino do acesso ficam na própria AWS, **o tráfego não vai pela Internet**, apesar do destino ser um endpoint público acessível pela Internet e apesar de passar pelo Internet Gateway. Isso pode parecer um pouco confuso e contraintuivo, já que seria natural supor que essa comunicação ocorreria pela Internet, mas [em suas documentações](https://repost.aws/questions/QU4fn697qVTRWaB0rhGZfHZw/does-traffic-between-amazon-ec2-and-amazon-s3-really-go-over-the-internet) a AWS afirma que [isso não acontece na prática](https://aws.amazon.com/vpc/faqs/#Connectivity:~:text=Does%20traffic%20go%20over%20the%20internet%20when%20two%20instances%20communicate%20using%20public%20IP%20addresses%2C%20or%20when%20instances%20communicate%20with%20a%20public%20AWS%20service%20endpoint%3F).

Isso pode não ser um problema caso a aplicação já precise ter conectividade com a Internet por outros motivos. Entretanto, caso a aplicação não tenha essa necessidade, seríamos obrigados a prover essa conectividade com a Internet (com Internet Gateway e com NAT Gateway) somente para acessar os endpoints públicos dos serviços da AWS. Para esses cenários, em que não há necessidade ou não se quer acessar os serviços da AWS através de seus endpoints públicos, existe a possibilidade de acessá-los de forma privada através de **Interface VPC Endpoints**.

## Acesso remoto via AWS Systems Manager Session Manager com Interface VPC Endpoints

O **Interface VPC Endpoint** utiliza uma tecnologia da AWS chamada [PrivateLink](https://docs.aws.amazon.com/vpc/latest/privatelink/what-is-privatelink.html), que permite estabeler conectividade privada entre a VPC e os serviços da AWS suportados. Isso ocorre através da criação de uma ENI - Elastic Network Interface (uma placa de rede virtual) na subnet de uma VPC e que dá conectividade direta aos serviços. Na prática, é como se esses serviços da AWS estivessem na própria VPC. Dessa forma, a aplicação pode estar em uma VPC sem conectividade com a Internet e vai conseguir acessar o serviço AWS através do Interface VPC Endpoint, sem a necessidade de acesso ao endpoint público. O desenho de arquitetura a seguir representa como isso funciona no cenário de acesso remoto a uma instância EC2 através do Session Manager:


{{< figure src="/img/2023/AcessoRemotoAWS-4-sessionmanager-vpcendpoint.png" align="center" alt="Diagrama de arquitetura do cenário de acesso via Session Manager. O diagrama mostra um usuário acessando o serviço do Session Manager, através da Internet. O SSM Agent, instalado em uma instância EC2 e uma subnet privada com uma IAM Role configurada e sem acesso a Internet. O SSM Agent na instância EC2 acessa o serviço do Session Manager e o serviço Systems Manager na AWS através do Interface VPC Endpoint, que utiliza a tecnologia AWS PrivateLink. O tráfego passa por uma ENI - Elastic Network Interface criada na subnet." >}}


Pontos importantes:
* o servidor de aplicação (instância EC2) está em uma subnet privada, ou seja, sem acesso a Internet.
* a comunicação do servidor de aplicação com o Session Manager ocorre via [SSM Agent](https://docs.aws.amazon.com/systems-manager/latest/userguide/ssm-agent.html), que é um software instalado na instância EC2. Para seu correto funcionamento, o SSM Agent precisa se comunicar com os serviços do Session Manager e do Systems Manager. Nesse cenário, a comunicação ocorre através da ENI (placa de rede virtual) criada na subnet, que consegue acessar o serviço do Session Manager e o serviço Systems Manager de forma privada através do PrivateLink. Para a instância EC2 é como se as APIs desses serviços estivessem na VPC. Além disso, o SSM Agent precisa ter as devidas permissões para se comunicar com esses serviços. Para isso, a instância EC2 deve ser configurada com uma IAM Role que dê essas permissões.
* Toda comunicação, tanto do usuário com o Session Manager, quanto da instância EC2 com o Session Manager e o serviço Systems Manager, ocorre via HTTPS.

Para mais detalhes sobre Interface VPC Endpoint e PrivateLink, consulte [Acessando serviços AWS de forma privada com Interface VPC Endpoint/PrivateLink]({{< relref "/blog/2023/acessando-servicos-AWS-de-forma-privada-com-VPC-endpoints.md">}})

### Preparando o ambiente

> **Atenção**: A AWS oferece um nível gratuito para experimentação de seus produtos ([AWS Free Tier](https://aws.amazon.com/free/)) que pode ser utilizado para implementação dos exemplos, mas o leitor deve ficar atento para eventuais custos que possam ser gerados.


Para demonstrar como isso funciona na prática, foi criado um [template CloudFormation](https://github.com/roneda/exemplos-blog/blob/main/vpc-subnetprivada-ec2.yaml) que provisiona um ambiente inicial baseado no diagrama anterior. A stack será composta por:
* uma VPC;
* uma subnet privada;
* um security goup a ser utilizado nos Interface VPC Endpoints, que permite tráfego de entrada na porta 443 (lembre-se que o acesso aos endpoints da AWS ocorre via HTTPS através da ENI criada);
* uma instância EC2 que utiliza Amazon Linux 2023 (AMI baseada na região AWS de N. Virginia - us-east-1);
* uma IAM Role e um Instance Profile, que serão utilizados na instância EC2 e com permissões para acessar o Session Manager;

A partir desse ambiente base, serão feitas as configurações necessárias para permitir o uso do Session Manager.

Após fazer o [download do template CloudFormation](https://github.com/roneda/exemplos-blog/blob/main/vpc-subnetprivada-ec2.yaml) para seu computador, acesse sua conta na AWS e, no painel de gerenciamento do CloudFormation, clique no botão "**Create stack > With new resources (standard)**". Escolha a opção **"Upload a template file"** e faça o upload do arquivo de template CloudFormation. Na página seguinte, em **"Stack name"** preencha com um nome que achar melhor (ex: StackBase) e prossiga nas próximas páginas com os valores padrão, até iniciar a criação da stack. Após alguns minutos, a stack estará criada.

### Criando Interface VPC Endpoints para Session Manager

Quando estiver disponível, a instância EC2 estará em uma subnet privada, sem conectividade com a Internet e, consequentemente, sem acesso ao Session Manager. Para confirmar isso, acesse o painel de EC2 na console AWS, em seguida vá para a opção de menu **Instances** no lado esquerdo da página, selecione a instância **AppServer** e clique em **Connect** na parte de cima da página. Em seguida, escolha a opção **"Session Manager"**. Como esperado, o botão **Connect** estará desabilitado e aparecerá uma mensagem informando que não é possível se conectar à instância:

{{< figure src="/img/2023/AcessoRemotoAWS-4-sessionmanager-vpcendpoint-ec2-erro.png" align="center" alt="Página de acesso à instância EC2 via Session Manager na console AWS com mensagem de erro" >}}


Agora será criado o Interface VPC Endpoint para o serviço Systems Manager. Para isso, acesse o painel de VPC na console AWS. No menu do lado esquerdo, escolha a opção **"Virtual Private Cloud > Endpoints"**, clique no botão **"Create endpoint"** e informe os seguintes dados:
* Name: **SSMInterfaceEndpoint**
* Service Category: selecione **AWS Services**
* Service Name:  selecione **com.amazonaws.us-east-1.ssm**
* VPC: selecione **myVPC**
* Availability Zone: selecione **us-east-1a**
* Subnet ID: escolha a opção **mySubnet**
* Security Groups: selecione **VPCEndpointSecurityGroup**
* Clique em **"Create endpoint**

Repita o procedimento para criar o Interfa VPC Endpoint para o serviço Session Manager e informe os seguintes dados:
* Name: **SSMMessagesInterfaceEndpoint**
* Service Category: selecione **AWS Services**
* Service Name:  selecione **com.amazonaws.us-east-1.ssmmessages**
* VPC: selecione **myVPC**
* Availability Zone: selecione **us-east-1a**
* Subnet ID: escolha a opção **mySubnet**
* Security Groups: selecione **VPCEndpointSecurityGroup**
* Clique em **"Create endpoint**

Uma observação importante: esses são os Interface VPC Endpoints mínimos para poder utilizar o Session Manager. Dependendo do seu caso de uso, talvez sejam necessários outros Interface VPC Endpoints para uso de outras funcionalidades do  Systems Manager. Para mais informações, consulte [Creating VPC endpoints for Systems Manager](https://docs.aws.amazon.com/systems-manager/latest/userguide/setup-create-vpc.html#sysman-setting-up-vpc-create) e também [How do I create VPC endpoints so that I can use Systems Manager to manage private EC2 instances without internet access?](https://repost.aws/knowledge-center/ec2-systems-manager-vpc-endpoints) 

### Utilizando Session Manager via console AWS (browser)

Após o Interface VPC Endpoint ficar disponível, tente novamente acessar a instância EC2 pelo Session Manager. Para isso, acesse o painel de EC2 na console AWS, em seguida vá para a opção de menu **Instances** no lado esquerdo da página, selecione a instância **AppServer** e clique em **Connect** na parte de cima da página. Em seguida, escolha a opção **"Session Manager"**. Se tudo correu conforme o esperado, o botão **Connect** estará habilitado.

{{< figure src="/img/2023/AcessoRemotoAWS-4-sessionmanager-vpcendpoint-ec2.png" align="center" alt="Página de acesso à instância EC2 via Session Manager na console AWS com o botão Connect habilitado" >}}

> Talvez seja necessário aguardar de 5 a 10 minutos após a criação dos Interface VPC Endpoints para que a mensagem de erro na tela de acesso do Session Manager deixe de aparecer. 

Clicando nno botão **Connect**, será aberta uma janela no browser simulando um terminal na instância EC2. Os comando digitados nesse terminal serão executados na instância EC2.

{{< figure src="/img/2023/AcessoRemotoAWS-4-sessionmanager-vpcendpoint-ec2-terminal.png" align="center" alt="Imagem do terminal da instância EC2 aberto no browser pelo Session Manager" >}}

Para terminar a sessão, clique em **Terminate**.

Com essa configuração, também é possível acessar a instância EC2 através da linha de comando, utilizando o AWS CLI, como foi demonstrado em [Acessando recursos remotamente em uma VPC na AWS - parte 3 - AWS Systems Manager Session Manager]({{< relref "/blog/2023/acessando-recursos-remotamente-em-uma-vpc-na-AWS-parte-3.md#utilizando-session-manager-via-linha-de-comando-aws-cli">}})

Assim, além das vantagens citadas no post anterior (servidor de aplicação não precisar ficar exposto na Internet, uso de um serviço gerenciado da AWS que diminui a sobrecarga operacional, etc), o uso de Interface VPC Endpoint com o Session Manager faz com que a VPC não precise ter acesso a Internete para acessar as APIs da AWS. Assim, não é necessário ter o Internet Gateway e/ou NAT Gateway. 

É importante destacar que o custo do Interface VPC Endpoint é calculado por hora em que ele está provisionado em cada AZ e pelo tráfego processado por ele. Mais informações em [AWS PrivateLink Pricing](https://aws.amazon.com/privatelink/pricing/). Dessa forma, depois de finalizar os testes, não esqueça de excluir os Interface VPC Endpoints e apagar a stack de CloudFormation com os demais recursos.

No próximo post serão mostradas outras funcionalidades que o Session Manager fornece.


### Referências
* [How do I create VPC endpoints so that I can use Systems Manager to manage private EC2 instances without internet access?](https://repost.aws/knowledge-center/ec2-systems-manager-vpc-endpoints)
* [Creating VPC endpoints for Systems Manager](https://docs.aws.amazon.com/systems-manager/latest/userguide/setup-create-vpc.html#sysman-setting-up-vpc-create)
* [Acessando serviços AWS de forma privada com Interface VPC Endpoint/PrivateLink]({{< relref "/blog/2023/acessando-servicos-AWS-de-forma-privada-com-VPC-endpoints.md">}})
* [AWS Systems Manager Session Manager for Shell Access to EC2 Instances](https://aws.amazon.com/blogs/aws/new-session-manager/)
* [Connect to an Amazon EC2 instance by using Session Manager](https://docs.aws.amazon.com/prescriptive-guidance/latest/patterns/connect-to-an-amazon-ec2-instance-by-using-session-manager.html)
* [LAB 1: ELIMINATE BASTION HOSTS WITH SYSTEMS MANAGER](https://awscloudsecvirtualevent.com/workshops/module1/)
* [AWS MANAGEMENT AND GOVERNANCE TOOLS WORKSHOP - SESSION MANAGER](https://mng.workshop.aws/ssm/use-case-labs/sessionmanager.html)
* [AWS Systems Manager Session Manager](https://docs.aws.amazon.com/systems-manager/latest/userguide/session-manager.html)
* [Start a session](https://docs.aws.amazon.com/systems-manager/latest/userguide/session-manager-working-with-sessions-start.html#sessions-start-cli)