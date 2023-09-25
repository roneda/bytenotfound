---
title: "Acessando recursos remotamente em uma VPC na AWS - parte 3 - AWS Systems Manager Session Manager"
date: 2023-07-23T10:01:58-03:00
draft: false
tags: ["aws", "vpc", "session manager", "aws systems manager", "acesso remoto", "infraestrutura", "segurança"]
---

No [post anterior]({{< relref "/blog/2023/acessando-recursos-remotamente-em-uma-vpc-na-AWS-parte-2.md">}}), foi mostrado como um Bastion Host com SSH é utilizado como ponto único de acesso remoto aos recursos de uma VPC. Dessa forma, somente o Bastion Host precisa ficar exposto para a Internet, enquanto que os demais servidores podem ficar em uma subnet privada. Isso reduz a superfície de ataque e aumenta a segurança em relação à alternativa apresentada no [primeiro post da série]({{< relref "/blog/2023/acessando-recursos-remotamente-em-uma-vpc-na-AWS-parte-1.md">}}). Apesar disso, o uso do Bastion Host traz outras preocupações, como o esforço para ser mantido e gerenciado, a necessidade de se pensar em alta disponibilidade, complexidade para gerenciar as chaves privadas utilizadas na autenticação e maior custo.

Nesse post, será mostrado como o uso de um serviço gerenciado da AWS, o Session Manager, endereça esses problemas.

## Acesso remoto via AWS Systems Manager Session Manager

O [**Session Manager**](https://docs.aws.amazon.com/systems-manager/latest/userguide/session-manager.html) é um serviço gerenciado da AWS que faz parte do "guarda-chuvas" do produto **AWS Systems Manager**. O Session Manager permite acessar os recursos de uma VPC remotamente sem a necessidade de um Bastion Host e sem que os recursos precisem ficar em uma subnet pública. O controle de acesso é integrado com o serviço de IAM da AWS, ou seja, o usuário se autentica com as mesmas credenciais de acesso à AWS, não sendo necessário o uso e gerenciamento de pares de chaves. Por ser um serviço gerenciado, não é preciso se preocupar e gastar esforço em manter uma infraestrutura adicional. Além disso, [não há custos adicionais para uso do Session Manager](https://www.amazonaws.cn/en/systems-manager/pricing/) em si, (mas há custo para a infraestrutura envolvida). O diagrama a seguir mostra o cenário de exemplo que será implementado.

{{< figure src="/img/2023/AcessoRemotoAWS-3-sessionmanager.png" align="center" alt="Diagrama de arquitetura do cenário de acesso via Session Manager. O diagrama mostra um usuário acessando o serviço do Session Manager, através da Internet. O SSM Agent, instalado em uma instância EC2 com uma IAM Role configurada, também acessa o serviço do Session Manager e o serviço Systems Manager na AWS." >}}

Note que:
* O usuário acessa via Internet somente o Session Manager, que é o serviço gerenciado da AWS. Não há acesso direto à instância EC2. O acesso do usuário pode ser tanto via console de gerenciamento da AWS ou por linha de comando, conforme será mostrado adiante.
* A comunicação do servidor de aplicação com o Session Manager ocorre via [SSM Agent](https://docs.aws.amazon.com/systems-manager/latest/userguide/ssm-agent.html), que é um software instalado na instância EC2. Para seu correto funcionamento, o SSM Agent precisa se comunicar com os serviços do Session Manager e do Systems Manager. Nesse cenário, a comunicação ocorre via endpoints públicos desses serviços. Além disso, o SSM Agent precisa ter as devidas permissões para se comunicar com esses serviços. Para isso, a instância EC2 deve ser configurada com uma IAM Role que dê essas permissões.
* A instância EC2 encontra-se em uma subnet privada. Como o SSM Agent necessita se comunicar com os serviços do Session Manager e do Systems Manager através de seus endpoints públicos, a instância EC2 precisa de acesso de saída para Internet. Isso é fornecido através de um NAT Gateway na subnet pública. Apesar da necessidade de saída para Internet, esse tráfego se mantém na rede da AWS, pois estão sendo acessados endpoints públicos da própria AWS. É sempre o SSM Agent que inicia a conexão com os serviços do Session Manager e do Systems Manager.
* Toda comunicação, tanto do usuário com o Session Manager, quanto da instância EC2 com o Session Manager e o serviço Systems Manager, ocorre via HTTPS.

### Preparando o ambiente

> **Atenção**: A AWS oferece um nível gratuito para experimentação de seus produtos ([AWS Free Tier](https://aws.amazon.com/free/)) que pode ser utilizado para implementação dos exemplos, mas o leitor deve ficar atento para eventuais custos que possam ser gerados.

Para implementar esse cenário, acesse sua conta AWS através da console. O primeiro passo é criar uma VPC, uma subnet pública, uma subnet privada e um NAT Gateway. A VPC padrão que toda conta AWS possui já vem com uma subnet pública e Internet Gateway configurados e é ela que iremos utilizar nesse exemplo. Caso queira, você pode começar do zero e criar uma nova VPC com uma nova subnet e configurar o Internet Gateway nela. Crie também uma subnet privada, ou seja, uma subnet cuja Route Table não possua roteamento para o Internet Gateway, mas com roteamento para o NAT Gateway. Essa Route Table e o NAT Gateway também deverão ser criados. 


No painel de gerenciamento de VPC, acesse a opção **NAT gateways** no menu do lado esquerdo e depois clique no botão **"Create NAT Gateway"**. Preencha os campos com os seguintes valores:
* Name: **MeuNATGateway**
* Subnet: selecione uma subnet **pública**
* Elastic IP allocation ID: clique em **"Allocate Elastic IP"** para que um Elastic IP seja criado e depois selecione-o.
* Clique em **"Create NAT Gateway"**


No painel de gerenciamento de VPC, acesse a opção **Route tables** no menu do lado esquerdo e depois clique no botão **"Create route table"**. Preencha os campos com os seguintes valores:
* Name: **PrivateRouteTable**
* VPC: selecione a VPC que será utilizada
* Clique em **"Create route table"**

Quando uma Route Table é criada, por padrão ela só possui uma rota que realiza roteamento local para dentro da VPC. Para que o servidor de aplicação que será criado na subnet privada tenha saída para Internet, será necessário adicionar uma outra rota que direcione as conexões diferentes das locais para o NAT Gateway. Para isso, selecione a Route Table, clique em **Routes** e depois em **"Edit routes"**. Na página que se abre, clique em **"Add route"** e preencha:
* Destination: **0.0.0.0/0** para indicar qualquer conexão para um destino que não se enquadre nas demais regras de rotas
* Target: **NAT Gateway > MeuNATGateway**
* Clique em **"Save changes"**


{{< figure src="/img/2023/AcessoRemotoAWS-3-rt.png" align="center" alt="Imagem da console AWS mostrando a configuração de uma Route Table com roteamento para NAT Gateway" >}}

Ainda no painel de gerenciamento de VPC, acesse o menu **Subnets** e depois clique no botão **"Create subnet"**, para criar a subnet privada com a seguinte configuração:
* VPC: escolha a VPC que será utilizada
* Subnet Name: **Private Subnet**
* Availability Zone: escolha uma zona de disponibilidade (AZ) onde a subnet será criada, de preferência, a mesma AZ onde foi criado o NAT Gateway
* IPv4 CIDR block: informe um bloco de endereços IP que seja válido na sua VPC
* Clique em **"Create subnet"**
* após a subnet ter sido criada, selecione-a e acesse a aba **Route table** no painel na parte debaixo da página. Perceba que a **Route Table** que essa subnet está utilizando é a **main**, que dá acesso a Internet. Temos que trocá-la pela Route Table que foi criada anteriormente. Para isso, clique no botão **"Edit route table association"**
* selecione a Route Table **PrivateRouteTable** e confirme a existência das rotas para roteamento local e para o NAT Gateway. Clique em **Save**

{{< figure src="/img/2023/AcessoRemotoAWS-3-subnet.png" align="center" alt="Imagem da console AWS mostrando a associação da Route Table a uma subnet" >}}

Agora será criada a IAM Role que depois vai ser configurada na instância EC2. Essa IAM Role deverá ter as políticas necessárias para o SSM Agent conseguir acessar os serviços do Session Manager e do Systems Manager. Vá para o painel de gerenciamento de IAM na console AWS, escolha a opção **Access management > Roles** no menu a esquerda e depois clique em **"Create role"**. Preencha os campos conforme a seguir:
* Trusted entity type: **AWS Service**
* Use case: **EC2**
* Clique em **Next**
* Na página de escolha da política, selecione a **AmazonSSMManagedInstanceCore**, que é uma política gerenciada da AWS já com as permissões necessárias. Clique em **Next**.
* Role Name: **EC2_SSM_Role**
* Clique em **"Create Role"**

O passo seguinte é criar uma instância EC2 que fará o papel do servidor de aplicação. Por se tratar de um cenário hipotético, será criada somente uma instância EC2, mas o mesmo procedimento poderia ser realizado mais vezes, caso houvesse mais de um servidor de aplicação. Vá para o painel de gerenciamento de EC2 na console da AWS, escolha a opção **"Launch Instance"** e informe as seguintes configurações:
* Name: **AppServer**
* Application and OS Images (Amazon Machine Image): **Amazom Linux -Amazon Linux 2023 AMI**. Essa AMI já possui o SSM Agent instalado por padrão. A lista de AMIs que possuem o SSM Agent instalado por padrão encontra-se em [Amazon Machine Images (AMIs) with SSM Agent preinstalled](https://docs.aws.amazon.com/systems-manager/latest/userguide/ami-preinstalled-agent.html).
* Instance type: **t2.micro** (esse tipo de instância é elegível ao free tier da AWS)
* Key pair (login): selecione a opção **"Proceed without a key pair (Not recommended)"**, pois o acesso à instância EC2 será através do Session Manager, que não necessita de par de chaves.
* Network Settings:
    * Nesse item, devemos configurar a subnet a ser utilizada. Clique em **Edit**
    * VPC: escolha a VPC que será utilizada
    * Subnet: escolha a subnet privada chamada **Private Subnet** criada anteriormente
    * Firewall (security groups)
        * Mantenha a opção pré-selecionada **"Create security group"**
        * Security group name: para facilitar a identificação, preencha com **"AppServer Security Group"**
        * Inbound Security Group Rules: perceba que por padrão, esse security group será criado com a porta 22 do SSH aberta para a Internet. Entretanto, não iremos utilizar SSH para acessar a instância, já que utilizaremos o Session Manager. Nesse caso, podemos clicar em **Remove** para remover essa regra. Dessa maneira, esse security group não terá nenhuma regra que permita exposição de qualquer porta.
        {{< figure src="/img/2023/AcessoRemotoAWS-3-sg.png" align="center" alt="Imagem da console AWS mostrando a configuração do Security Group do servidor da aplicação" >}}
* Advanced details:
    * IAM instance profile: escolha a opção **EC2_SSM_Role**, que é a IAM Role criada anteriormente e que contém as permissões necessárias para o SSM Agent conseguir se comunicar com os serviços Session Manager e Systems Manager.
* Deixe as demais configurações de EC2 com os valores padrão, pois não será necessário alterá-los para a demonstração que será feita. Clique em **"Launch Instance"** e aguarde a instância EC2 ficar disponível. 

### Utilizando Session Manager via console AWS (browser)

Agora é possível acessar a instância EC2 remotamente através do Session Manager. Primeiro, será desmonstrado como fazer isso pela console da AWS, ou seja, via browser. Há duas opções: através do painel de EC2 ou através do painel do Systems Manager. 

Para iniciar uma sessão no Session Manager pelo painel de EC2 na console AWS, acesse a opção de menu **Instances** no lado esquerdo da página, selecione a instância **AppServer** e clique em **Connect** na parte de cima da página. Em seguida, escolha a opção **"Session Manager"**. Se tudo correu conforme o esperado, o botão **Connect** estará habilitado e clicando nele será aberta uma janela no browser simulando um terminal na instância EC2. Os comando digitados nesse terminal serão executados na instância EC2.

{{< figure src="/img/2023/AcessoRemotoAWS-3-sessionmanager-ec2.png" align="center" alt="Imagem do terminal da instância EC2 aberto no browser pelo Session Manager" >}}

Para iniciar uma sessão no Session Manager pelo painel de Systems Manager na console AWS, acesse a opção de menu **"Session Manager"** no lado esquerdo da página. Será mostrada uma página com todas as sessões ativas no momento. Clique no botão **"Start session"**, selecione a instância **AppServer**, clique em **Next** duas vezes e em seguida em **"Start session"**. Novamente será aberta uma janela no browser simulando um terminal na instância EC2. Os comando digitados nesse terminal serão executados na instância EC2.

O painel do Systems Manager, além de mostrar as sessões do Session Manager ativas no momento, também permite consultar o histórico de todas as sessões já abertas, acessando a opção **"Session history"**.

{{< figure src="/img/2023/AcessoRemotoAWS-3-sessionmanager-sessionhistory.png" align="center" alt="Imagem que mostra o histórico de sessões do Session Manager" >}}

Para terminar a sessão, clique em **Terminate**.

### Utilizando Session Manager via linha de comando (AWS CLI)

Agora será demonstrado como acessar a instância EC2 remotamente pelo Session Manager através da linha de comando, utilizando o AWS CLI. Para isso, é preciso ter instalado e configurado o [AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html) e o [Session Manager plugin for the AWS CLI](https://docs.aws.amazon.com/systems-manager/latest/userguide/session-manager-working-with-install-plugin.html). Acesse os respectivos links caso não os tenha instalados.

O exemplo a seguir será feito utilizando o Windows 10 ou superior. Entretanto, o mesmo pode ser reproduzido em outro sistema operacional. Abra o Windows Powershell ou o Command Prompt e execute o comando abaixo:

```` shell
aws ssm start-session --target instance-id
````
Onde:
* **instance-id** é o identificador da instância EC2 que se quer acessar. Para obter esse dado, acesse o painel de EC2 na console AWS (pelo browser) e veja o valor do campo  **"Instance ID"** da instância EC2 desejada.

Se tudo estiver correto, você estará com um terminal Linux aberto no servidor remoto usando AWS CLI com o Session Manager. Todos os comandos que você digitar serão executados na instância EC2 remotamente. Perceba que a experiência de uso é praticamente a mesma da que se estivesse utilizando SSH, mas sem as desvantagens desse.

{{< figure src="/img/2023/AcessoRemotoAWS-3-sessionmanager-cli.png" align="center" alt="Imagem que mostra o terminal da instância EC2 aberto na linha de comando usando AWS CLI com Session Manager" >}}

Note que as sessões do Session Manager abertas pela linha de comando também aparecem na lista de sessões ativas e no histórico de sessões no painel do Systems Manager, na console AWS (browser).

Para voltar para sua máquina local, digite **exit** e tecle **ENTER** ou então utilize o atalho **Ctrl + D**.

A opção apresentada possui uma série de vantagens em relação ao que havia sido mostrado nos posts anteriores:
* os servidores de aplicação não precisam ficar expostos na Internet. 
* não é preciso ter Bastion Host. Isso diminui a superfície de ataque e diminui os custos da solução.
* o Session Manager é um serviço gerenciado da AWS, o que faz com que a responsabilidade de manutenção seja da AWS e não precisamos nos preocupar com isso.
* o controle de acesso é integrado com o IAM da AWS, não sendo necessário o uso e gerenciamento de pares de chaves.

Apesar de ser uma solução menos complexa, mais segura, com menor sobrecarga operacional e mais barata, ainda há pontos que podem ser melhorados. No próximo post será mostrado o que mais pode ser evoluído na solução.

### Referências
* [AWS Systems Manager Session Manager for Shell Access to EC2 Instances](https://aws.amazon.com/blogs/aws/new-session-manager/)
* [Connect to an Amazon EC2 instance by using Session Manager](https://docs.aws.amazon.com/prescriptive-guidance/latest/patterns/connect-to-an-amazon-ec2-instance-by-using-session-manager.html)
* [LAB 1: ELIMINATE BASTION HOSTS WITH SYSTEMS MANAGER](https://awscloudsecvirtualevent.com/workshops/module1/)
* [AWS MANAGEMENT AND GOVERNANCE TOOLS WORKSHOP - SESSION MANAGER](https://mng.workshop.aws/ssm/use-case-labs/sessionmanager.html)
* [AWS Systems Manager Session Manager](https://docs.aws.amazon.com/systems-manager/latest/userguide/session-manager.html)
* [Start a session](https://docs.aws.amazon.com/systems-manager/latest/userguide/session-manager-working-with-sessions-start.html#sessions-start-cli)