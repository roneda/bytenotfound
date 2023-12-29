---
title: "Acessando recursos remotamente em uma VPC na AWS - parte 5 - AWS Systems Manager Session Manager com Port Forwarding"
date: 2023-11-22T10:48:58-03:00
draft: false
tags: ["aws", "vpc", "session manager", "aws systems manager", "acesso remoto", "infraestrutura", "segurança", "vpc endpoint", "privatelink", "port forwarding"]
cover: 
  image: "/img/2023/AcessoRemotoAWS-5-sessionmanager-portforwarding.png"
---

Nessa série de posts, tenho mostrado algumas possíveis formas de acessar recursos remotamente em uma VPC na AWS, suas vantagens e desvantagens. Desde formas mais simples como [SSH]({{< relref "/blog/2023/acessando-recursos-remotamente-em-uma-vpc-na-AWS-parte-1.md">}}), passando pelo uso de [Bastion Host]({{< relref "/blog/2023/acessando-recursos-remotamente-em-uma-vpc-na-AWS-parte-2.md">}}), evoluindo até formas mais seguras com o uso do serviço [Session Manager]({{< relref "/blog/2023/acessando-recursos-remotamente-em-uma-vpc-na-AWS-parte-3.md">}}) da AWS e com [Interface VPC Endpoint]({{< relref "/blog/2023/acessando-recursos-remotamente-em-uma-vpc-na-AWS-parte-4-session-maanger-interface-vpc-endpoint.md">}}).

Em todos os exemplos, o recurso acessado sempre foi uma instância EC2. Ou seja, foi mostrado como acessar o terminal de uma instância EC2 e executar comandos remotamente. Entretanto, uma solução na AWS normalmente envolve muitos outros recursos além de instâncias EC2. Não seria bom se conseguíssemos acessar remotamente outros recursos disponíveis na VPC (por exemplo, um banco de dados RDS ou outros serviços da AWS), como se fossem recursos locais, de forma segura? Isso é possível e demonstrarei como fazer isso nesse artigo!

## Acesso remoto via AWS Systems Manager Session Manager com Port Forwarding

O **Port Forwarding** (ou encaminhamento de porta) é uma funcionalidade do Session Manager que possibilita que o tráfego de rede destinado a uma porta local seja redirecionado para um destino remoto. Em outras palavras, uma porta é aberta no computador local e é estabelecido um túnel com um outro computador remoto. Todo tráfego enviado para a porta local é encaminhado para o computador remoto através do túnel. O princípio é o mesmo do [SSH Port Forwarding](https://www.ssh.com/academy/ssh/tunneling) (também conhecido como [SSH Tunneling](https://www.ssh.com/academy/ssh/tunneling-example)), com a vantagem de que com o uso do Session Manager não é preciso gerenciar pares de chaves públicas e privadas e nem expor a porta 22 do SSH para acesso. 

A grande vantagem dessa abordagem é que ela permite o uso de um recurso remoto como se fosse local. Um desenvolvedor poderia desenvolver, executar, testar e "debugar" uma aplicação localmente acessando recursos remotos em uma VPC na AWS (bancos de dados, servidores de cache, etc), sem a necessidade de ter todos os componentes da solução instalados no seu computador. Ou seja, o desenvolvedor acessa um endereço local que, através do port forwarding, encaminha o tráfego para o recurso remoto de forma transparente.

Além de recursos que são provisionados na VPC, também é possível acessar remotamente de forma privada serviços gerenciados da AWS que, a princípio, são públicos, como SQS, SNS, S3, etc, ou seja, serviços que não são provisionados na VPC. Isso é possível através do uso do Interface VPC Endpoint, que cria uma ENI (placa de rede virtual) na VPC e é através dela que se tem acesso ao serviço gerenciado da AWS através Private Link.

Para mais detalhes sobre Interface VPC Endpoint e PrivateLink, consulte [Acessando serviços AWS de forma privada com Interface VPC Endpoint/PrivateLink]({{< relref "/blog/2023/acessando-servicos-AWS-de-forma-privada-com-VPC-endpoints.md">}})

No exemplo desse post, será utilizado o Session Manager com Port Forwarding para acesso remoto a um banco de dados RDS (sem que ele precise ficar exposto para a Internet) e também a uma fila SQS com o tráfego passando pela VPC. Perceba que o RDS e SQS são somente exemplos. Ou seja, o acesso remoto poderia ser feito a qualquer outro recurso que fosse acessível a partir da VPC, como por exemplo, um cluster do ElastiCache, um servidor Web, um bucket S3 ou qualquer outro recurso que possua um endereço IP da VPC. O diagrama abaixo mostra o ambiente que será criado para essa demonstração:


{{< figure src="/img/2023/AcessoRemotoAWS-5-sessionmanager-portforwarding.png" align="center" alt="Diagrama de arquitetura do cenário de acesso a um banco de dados RDS e uma fila SQL via Session Manager com Port Forwarding." >}}


Pontos importantes:
* no computador local há duas portas abertas (1212 e 1213) que mantêm um túnel com o Session Manager. O tráfego destinado a essas portas locais será redirecionado para o banco de dados RDS e para a fila SQS, respectivamente.
* existe uma instância EC2 na VPC que vai funcionar como um **jump server**. Isso significa que é essa instância EC2 que permitirá a conectividade com os recursos desejados da VPC, no caso, o banco de dados RDS e a fila SQS.
* tanto o jump server quando o banco de dados RDS estão em uma subnet privada, sem acesso a Internet. Na VPC não há nenhuma subnet pública.
* o acesso à fila SQS ocorre através da ENI (placa de rede virtual) criada na subnet, que consegue acessar o serviço do SQS de forma privada através do PrivateLink. Isso é necessário pois a VPC não possui acesso a Internet e, portanto, não possui acesso ao endpoint público do serviço.
* a comunicação do jump server com o Session Manager ocorre via [SSM Agent](https://docs.aws.amazon.com/systems-manager/latest/userguide/ssm-agent.html), que é um software instalado na instância EC2. Para seu correto funcionamento, o SSM Agent precisa se comunicar com os serviços do Session Manager e do Systems Manager. Nesse cenário, a comunicação ocorre através da ENI (placa de rede virtual) criada na subnet, que consegue acessar o serviço do Session Manager e o serviço Systems Manager de forma privada através do PrivateLink. Para a instância EC2 é como se as APIs desses serviços estivessem na VPC. Isso é necessário pois não há acesso a Internet a partir da VPC. Além disso, o SSM Agent precisa ter as devidas permissões para se comunicar com esses serviços. Para isso, a instância EC2 deve ser configurada com uma IAM Role que dê essas permissões.
* Toda comunicação, tanto do usuário com o Session Manager, quanto da instância EC2 com o Session Manager, o serviço Systems Manager e o serviço SQS, ocorre via HTTPS.



### Preparando o ambiente

> **Atenção**: A AWS oferece um nível gratuito para experimentação de seus produtos ([AWS Free Tier](https://aws.amazon.com/free/)) que pode ser utilizado para implementação dos exemplos, mas o leitor deve ficar atento para eventuais custos que possam ser gerados.


Para demonstrar como isso funciona na prática, foi criado um [template CloudFormation](https://github.com/roneda/exemplos-blog/blob/main/vpc-subnetprivada-ec2-sessionmanager-rds-sqs.yaml) que provisiona um ambiente  baseado no diagrama anterior. A stack será composta por:
* uma VPC;
* duas subnets privadas;
* uma instância EC2 que utiliza Amazon Linux 2023 (AMI baseada na região AWS de N. Virginia - us-east-1) e que fará papel do jump server;
* uma IAM Role e um Instance Profile, que serão utilizados na instância EC2 e com permissões para acessar o Session Manager;
* dois Interface VPC Endpoints para acessar os endpoints do Session Manager. Como a EC2 ficará em uma subnet sem conectividade com a Internet, o acesso aos endpoints do Session Manager da AWS ocorrerá através desses Interface VPC Endpoints;
* um Interface VPC Endpoint para acessar o endepoint do SQS. Como a EC2 ficará em uma subnet sem conectividade com a Internet, o acesso aos endpoints do Session Manager da AWS ocorrerá através desses Interface VPC Endpoints;
* um security goup a ser utilizado nos Interface VPC Endpoints, que permite tráfego de entrada na porta 443 (lembre-se que o acesso aos endpoints da AWS ocorre via HTTPS através das ENIs criadas);
* um security group a ser utilizado no jump server;
* um security group a ser utilizado no banco de dados RDS, que permite tráfego originado do jump server;


Após fazer o [download do template CloudFormation](https://github.com/roneda/exemplos-blog/blob/main/vpc-subnetprivada-ec2-sessionmanager-rds-sqs.yaml) para seu computador, acesse sua conta na AWS e, no painel de gerenciamento do CloudFormation, clique no botão "**Create stack > With new resources (standard)**". Escolha a opção **"Upload a template file"** e faça o upload do arquivo de template CloudFormation. 

Na página seguinte, em **"Stack name"** preencha com um nome que achar melhor (ex: myStack) e informe um nome do usuário master e a respectiva senha para acesso ao banco de dados. Prossiga nas próximas páginas com os valores padrão, até iniciar a criação da stack. Após alguns minutos, a stack estará criada. Na aba **Output** da stack de CloudFormation estarão disponíveis alguns dados que serão utilizados nos próximos passos. 

### Utilizando Session Manager com Port Forwarding para acesso ao RDS

Agora será demonstrado como acessar os recursos remotamente pelo Session Manager através da linha de comando, utilizando o AWS CLI. Para isso, é preciso ter instalado e configurado o [AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html) e o [Session Manager plugin for the AWS CLI](https://docs.aws.amazon.com/systems-manager/latest/userguide/session-manager-working-with-install-plugin.html). Acesse os respectivos links caso não os tenha instalados.

O exemplo a seguir será feito utilizando o Windows 10 ou superior. Entretanto, o mesmo pode ser reproduzido em outro sistema operacional. Abra o Windows Powershell ou o Command Prompt e execute o comando abaixo:

```` shell
aws ssm start-session --target <JumpServerInstanceID> --document-name AWS-StartPortForwardingSessionToRemoteHost --parameters host="<RDSEndpoint>",portNumber="3306",localPortNumber="1213"
````
Onde:
* **JumpServerInstanceID** é o identificador da instância EC2 que funcionará como jump server. Esse dado, pode ser obtido no **Output** da stack de CloudFormation criada anteriormente.
* **host** é o endereço do recurso que se quer acessar remotamente. Deve ser um nome ou endereço IP acessível pela VPC onde está o jump server. Nesse caso, é o endereço da instância RDS (**RDSEndpoint**), que pode ser obtido no **Output** da stack de CloudFormation criada anteriormente.
* **portNumber** é a porta do recurso remoto (host) que se quer acessar. Nesse caso, como se trata de um banco de dados MySql, a porta padrão é a 3306, mas esse valor varia dependendo do recurso remoto a ser acessado.
* **localPortNumber** é a porta que será aberta no computador local e através da qual o tráfego será recebido para ser encaminhado para o recurso remoto. Nesse exemplo está sendo utilizada a porta 1213, mas poderia ser qualquer porta disponível.

O que esse comando faz é abrir a porta 1213 no computador local, ficar escutando o tráfego que chega nela e estabelecer um túnel com o serviço Session Manager. Todo o tráfego que essa porta receber será encaminhado para o serviço Session Manager, que por sua vez utilizará a instância EC2 como ponte para chegar ao host remoto na porta 3306. Após a execução do comando, será apresentada a tela conforme abaixo. Deixe esse terminal aberto, pois o comando precisa estar em execução para que o acesso funcione.

{{< figure src="/img/2023/AcessoRemotoAWS-5-sessionmanager-portforwarding-rds.png" align="center" alt="Imagem do terminal com a sessão aberta com o Session Manager fazendo port forwarding para o RDS" >}}

Para demonstrar o acesso ao banco de dados, será utilizada o [DBeaver](https://dbeaver.io/), que é uma ferramenta gráfica para gerenciamento de banco de dados. Você pode utilizar qualquer outra ferramenta ou aplicação de sua preferência.

Abra o DBeaver e crie uma nova conexão, escolhendo **MySql** como banco de dados.

{{< figure src="/img/2023/AcessoRemotoAWS-5-sessionmanager-portforwarding-dbeaver1.png" align="center" alt="Tela de criação de conexão do DBeaver" >}}

Na tela de configuração da conexão, em **Server Host** informe **localhost** e em **Port** coloque 1213 ou a porta local que você utilizou para fazer o port forwarding. Note que, do ponto de vista do DBeaver, o acesso será feito para o computador local (localhost) e o encaminhamento para o verdadeiro servidor de banco de dados será feito de forma transparente. Em **Username** e **Password** informe o nome do usuário master e a respectiva senha que foram utilizados na criação de stack de CloudFormation.

{{< figure src="/img/2023/AcessoRemotoAWS-5-sessionmanager-portforwarding-dbeaver2.png" align="center" alt="Tela de configuração de conexão com o banco de dados" >}}

Ao finalizar a configuração da conexão com o banco de dados será possível acessá-lo através do DBeaver, como se estivéssemos trabalhando com ele localmente. Entretanto, esse banco de dados está em uma VPC na AWS.

{{< figure src="/img/2023/AcessoRemotoAWS-5-sessionmanager-portforwarding-dbeaver3.png" align="center" alt="Tela do DBeaver acessando o banco de dados RDS" >}}

### Utilizando Session Manager com Port Forwarding para acesso ao SQS

Agora será demonstrado como acessar um fila SQS remotamente através da VPC. Abra uma nova janela do Windows Powershell ou do Command Prompt e execute o comando abaixo:

```` shell
aws ssm start-session --target <JumpServerInstanceID> --document-name AWS-StartPortForwardingSessionToRemoteHost --parameters host="sqs.us-east-1.amazonaws.com",portNumber="443",localPortNumber="1313"
````

Onde:
* **JumpServerInstanceID** é o identificador da instância EC2 que funcionará como jump server. Esse dado, pode ser obtido no **Output** da stack de CloudFormation criada anteriormente. É o mesmo jump server utilizado para o acesso ao RDS.
* **host** é o endereço do recurso que se quer acessar remotamente. Deve ser um nome ou endereço IP acessível pela VPC onde está o jump server. Nesse caso, é o endereço do endpoint público do SQS na região de N. Virgínia (onde foi criada a fila SQS). Apesar de ser o endereço do endpoint público do SQS, o acesso ocorrerá por dentro da VPC, pois nela foi criado o Interface VPC Endpoint para SQS.
* **portNumber** é a porta do recurso remoto (host) que se quer acessar. Nesse caso, como o SQS é um serviço gerenciado da AWS, o acesso a suas APIs é via HTTPS e por isso a porta utilizada é a 443. 
* **localPortNumber** é a porta que será aberta no computador local e através da qual o tráfego será recebido para ser encaminhado para o recurso remoto. Nesse exemplo está sendo utilizada a porta 1313, mas poderia ser qualquer porta disponível.

O que esse comando faz é abrir a porta 1313 no computador local, ficar escutando o tráfego que chega nela e estabelecer um túnel com o serviço Session Manager. Todo o tráfego que essa porta receber será encaminhado para o serviço Session Manager, que por sua vez utilizará a instância EC2 como ponte para chegar ao serviço SQS na porta 443 através do Interface VPC Endpoint. Após a execução do comando, será apresentada a tela conforme abaixo. Deixe esse terminal aberto, pois o comando precisa estar em execução para que o acesso funcione.

{{< figure src="/img/2023/AcessoRemotoAWS-5-sessionmanager-portforwarding-sqs1.png" align="center" alt="Imagem do terminal com a sessão aberta com o Session Manager com port forwarding para o SQS" >}}

Abra mais uma janela do Windows Powershell ou do Command Prompt e execute o comando abaixo da AWS CLI abaixo para enviar uma mensagem para a fila SQS (substitua “URL da fila” pela URL gerada na criação da fila na stack de CloudFormation):

```` shell
aws sqs send-message --queue-url <SQSQueueURL> --message-body "Olá mundo!" --endpoint-url https://localhost:1313 --no-verify-ssl
````

Onde:
* **SQSQueueURL** é a URL da fila SQS para onde será enviada a mensagem e que pode ser encontrada no **Output** da stack de CloudFormation criada anteriormente. 
* **endpoint-url** é o endereço do endpoint que será utilizado para fazer essa chamada de API. Nesse caso, a chamada será feita para o computador local (localhost) na porta que foi aberta anteriormente (1313).
* o parâmetro **no-verify-ssl** desabilita a validação do certificado digital utilizado no endepoint do serviço da AWS. Isso é necessário pois o endereço de endpoint que estamos acessando (localhost) é diferente do endereço que consta no certificado digital, que é o endereço público do serviço SQS (sqs.us-east-1.amazonaws.com). Caso essa validação do certificado digital não seja desabilitada, essa diferença entre os nomes provoca um erro. Essa validação não deve ser desabilitada em cenários produtivos.

O comando acima enviará uma mensagem para a fila SQS criada anteriormente através de uma URL que aponta para o computador local (localhost) na porta 1313, ao invés da URL pública padrão do SQS. O resultado será algo parecido com a imagem abaixo. Note que é exibida uma mensagem de alerta sobre a desabilitação da validação do certificado digital.

{{< figure src="/img/2023/AcessoRemotoAWS-5-sessionmanager-portforwarding-sqs2.png" align="center" alt="Imagem do terminal mostrando que a mensagem foi enviada para fila SQS" >}}

Por fim, confirme o recebimento da mensagem na fila SQS. Na console da AWS, acesse o painel do SQS e selecione a **FilaTeste**. Clique em **“Send and receive messages”**, depois clique em **“Poll for messages”** e veja que aparece a mensagem. Clicando nela é exibido o corpo da mensagem com o texto que foi enviado pelo comando da AWS CLI:

{{< figure src="/img/2023/AcessoRemotoAWS-5-sessionmanager-portforwarding-sqs3.png" align="center" alt="Imagem mostrando o texto 'Olá mundo!' no corpo da mensagem da fila SQS" >}}


Dessa forma, é possível se conectar a qualquer recurso acessível pela VPC de forma remota. Isso se aplica a produtos que são provisionados na VPC, como bancos de dados RDS, clusters de cache do ElastiCache, etc, e também a serviços gerenciados da AWS, que não ficam na VPC dos usuários, como S3, SQS, SNS, etc. Nesse caso, é necessário o uso de Interface VPC Endpoint para que o acesso seja feito pela VPC. 

Esse tipo de abordagem facilita e agiliza bastante o desenvolvimento de aplicações, pois permite que recursos na Cloud possam ser acessados através de um endereço local, sem que esses recursos precisem ficar expostos e sem que seja necessário ter um ambiente local replicando todos os recursos que compõem a solução. Como foi mostrado, para cada recurso que se deseja acessar remotamente é necessário utilizar uma porta local diferente e estabelecer uma sessão com o Session Manager, que deve permanecer aberta enquanto o acesso for necessário. 


Depois de finalizar os testes, para fechar a sessão, utilize **Ctrl + C**. Além disso, não esqueça de apagar a stack de CloudFormation para que não ocorra cobranças desnecessárias.

### Referências
* [Use port forwarding in AWS Systems Manager Session Manager to connect to remote hosts](https://aws.amazon.com/blogs/mt/use-port-forwarding-in-aws-systems-manager-session-manager-to-connect-to-remote-hosts/)
* [Securely connect to an Amazon RDS or Amazon EC2 database instance remotely with your preferred GUI](https://aws.amazon.com/blogs/database/securely-connect-to-an-amazon-rds-or-amazon-ec2-database-instance-remotely-with-your-preferred-gui/)
* [New – Port Forwarding Using AWS System Manager Session Manager](https://aws.amazon.com/blogs/aws/new-port-forwarding-using-aws-system-manager-sessions-manager/)
* [Starting a session (port forwarding to remote host)](https://docs.aws.amazon.com/systems-manager/latest/userguide/session-manager-working-with-sessions-start.html#sessions-remote-port-forwarding)
* [SSH Tunneling](https://www.ssh.com/academy/ssh/tunneling)
* [SSH Tunneling: Examples, Command, Server Config](https://www.ssh.com/academy/ssh/tunneling-example)
* [Acessando serviços AWS de forma privada com Interface VPC Endpoint/PrivateLink]({{< relref "/blog/2023/acessando-servicos-AWS-de-forma-privada-com-VPC-endpoints.md">}})
