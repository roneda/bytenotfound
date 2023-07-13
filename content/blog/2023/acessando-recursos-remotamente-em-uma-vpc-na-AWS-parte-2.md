---
title: "Acessando recursos remotamente em uma VPC na AWS - parte 2"
date: 2023-07-10T21:10:58-03:00
draft: false
tags: ["aws", "vpc", "ssh", "acesso remoto", "infraestrutura", "segurança", "bastion host"]
---

Na [primeira parte]({{< relref "/blog/2023/acessando-recursos-remotamente-em-uma-vpc-na-AWS-parte-1.md">}}) dessa série de posts sobre opções existentes para acesso remoto a recurrsos de uma VPC na AWS, foi mostrada a forma mais básica e tradicional que é o acesso a instâncias EC2 com SSH. Apesar de funcionar, esse modelo possui pontos de atenção importantes, como a necessidade das instâncias EC2 ficarem expostas na Internet (o que aumenta a superfície de ataque) e a complexidade de gerenciamento das chaves privadas, utilizadas na autenticação do acesso. Isso torna-se mais crítico em cenários profissionais, onde provavelmente existirão várias pessoas precisando acessar várias instâncias EC2. Mais detalhes podem ser encontrados na [primeira parte]({{< relref "/blog/2023/acessando-recursos-remotamente-em-uma-vpc-na-AWS-parte-1.md">}}).

Nesse artigo, será mostrada uma outra opção que apresenta melhorias de alguns pontos do modelo discutido anteriormente.

## Acesso remoto via Bastion Host

Um **Bastion Host**, também conhecido como **Jump Box** ou **Jump Server**, é um servidor que funciona como um ponto único de acesso a uma rede privada a partir de uma rede externa. Por ser um componente crítico de segurança, esse servidor deve ter como único propósito ser um Bastion Host, não devendo ser utilizado para nenhuma outra finalidade. Assim, recursos e serviços que não estejam relacionados a essa finalidade devem ser desativados ou removidos para diminuir o risco de alguma vulnerabilidade ser explorada. 

No cenário de exemplo que será utilizado aqui, o Bastion Host será uma instância EC2 que ficará na subnet pública, exposta na Internet, enquanto as demais instâncias EC2, que representam os servidores de aplicação, ficarão isoladas em uma subnet privada. Portanto, o acesso às intâncias EC2 da subnet privada só poderá ser feito através do Bastion Host. O diagrama de arquitetura a seguir representa esse cenário.

{{< figure src="/img/2023/AcessoRemotoAWS-2-EC2-SSH-BastionHost.png" align="center" alt="Diagrama de arquitetura do cenário de acesso via Bastion Host. O diagrama mostra um usuário com uma chave privada acessando, através da Internet, uma instância EC2 que faz o papel de um Bastion Host em uma subnet pública de uma VPC na AWS, utilizando o protocolo SSH na porta 22. A partir do Bastion Host ocorrem os acessos às instâncias EC2 que se encontram na subnet privada, também via SSH na porta 22." >}}

É importante notar que:
* o acesso ao Bastion Host ocorre via Internet. Por isso ele deve ficar em uma subnet pública da VPC na AWS, para que possa aceitar conexões externas vindas da Internet. 
* o acesso às instâncias EC2 que representam os servidores de aplicação será feito somente a partir do Bastion Host. Dessa forma, essas instâncias EC2 estão localizadas em uma subnet privada, pois não precisam ficar expostas na Internet.
* tanto o acesso ao Bastion Host quanto aos servidores de aplicação serão através de SSH na porta 22. A diferença está na origem do acesso. O Security Group do Bastion Host deverá permitir conexões vindas da Internet para a porta 22. Já o Security Group dos servidores de aplicação deverão permitir conexões também na porta 22 mas vindas somente do Bastion Host. 
* o usuário que for acessar o Bastion Host terá que ter uma chave privada válida para se autenticar no SSH. Para isso, deverá ser gerado um par de chaves para ser utilizado nesse processo. O mesmo par de chaves será utilizado no acesso SSH que parte do Bastion Host para os servidores de aplicação. Entretanto, não se deve armazenar cópias de chaves privadas no Bastion Host, pois isso seria um risco de segurança. Para que o Bastion Host consiga acessar os servidores de aplicação sem que ele precise ter cópias da chave privada, será utilizado o recurso de **agent forwarding** do SSH.

> **Atenção**: A AWS oferece um nível gratuito para experimentação de seus produtos ([AWS Free Tier](https://aws.amazon.com/free/)) que pode ser utilizado para implementação dos exemplos, mas o leitor deve ficar atento para eventuais custos que possam ser gerados.

Para implementar esse cenário, acesse sua conta AWS através da console. O primeiro passo é criar uma VPC, uma subnet pública e uma subnet privada. A VPC padrão que toda conta AWS possui já vem com uma subnet pública e Internet Gateway configurados e é ela que iremos utilizar nesse exemplo. Caso queira, você pode começar do zero e criar uma nova VPC com uma nova subnet e configurar o Internet Gateway nela. Crie também uma subnet privada, ou seja, uma subnet cuja Route Table não possua roteamento para o Internet Gateway. Essa Route Table também deverá ser criada. 

No painel de gerenciamento de VPC, acesse a opção **Route tables** no menu do lado direito e depois clique no botão **"Create route table"**. Preencha os campos com os seguintes valores:
* Name: **PrivateRouteTable**
* VPC: selecione a VPC que será utilizada
* Clique em **"Create route table"**

Quando uma Route Table é criada, por padrão ela só possui uma rota que realiza roteamento local para dentro da VPC. É exatamente isso que queremos, pois essa Route Table será utilizada em uma subnet privada, sem acesso a Internet.

{{< figure src="/img/2023/AcessoRemotoAWS-2-rt.png" align="center" alt="Imagem da console AWS mostrando a configuração padrão de uma nova Route Table" >}}

Ainda no painel de gerenciamento de VPC, acesse o menu **Subnets** e depois clique no botão **"Create subnet"**, para criar a subnet privada com a seguinte configuração:
* VPC: escolha a VPC que será utilizada
* Subnet Name: **Private Subnet**
* Availability Zone: escolha uma zona de disponibilidade onde a subnet será criada
* IPv4 CIDR block: informe um bloco de endereços IP que seja válido na sua VPC
* Clique em **"Create subnet"**
* após a subnet ter sido criada, selecione-a e acesse a aba **Route table** no painel na parte debaixo da página. Perceba que a **Route Table** que essa subnet está utilizando é a **main**, que dá acesso a Internet. Temos que trocá-la pela Route Table que foi criada anteriormente. Para isso, clique no botão **"Edit route table association"**
* selecione a Route Table **PrivateRouteTable** e confirme que a única rota existente é para roteamento local. Clique em **Save**

{{< figure src="/img/2023/AcessoRemotoAWS-2-subnet.png" align="center" alt="Imagem da console AWS mostrando a associação da Route Table a uma subnet" >}}

O próximo passo é criar uma instância EC2 que fará o papel do Bastion Host. No painel de gerenciamento de EC2 na console da AWS, escolha a opção **"Launch Instance"**. Isso irá iniciar o guia de criação de EC2, que deve ser criada com as seguintes configurações:
* Name: **Bastion Host**
* Application and OS Images (Amazon Machine Image): **Amazom Linux - Amazon Linux 2023 AMI**
* Instance type: **t2.micro** (esse tipo de instância é elegível ao free tier da AWS)
* Key pair (login)
    * aqui precisamos criar um par de chaves pública/privada, que será utilizada para autenticação no acesso SSH tanto para o Bastion Host quanto para os servidores de aplicação. Clique no link **"Create new key pair"**, conforme imagem abaixo:
    {{< figure src="/img/2023/AcessoRemotoAWS-1-keypair.png" align="center" alt="Imagem da console AWS mostrando o link de criação de um novo par de chaves" >}}
    * em **"Key pair name"**, coloque **BastionKeyPair**
    * deixe as demais configurações conforme sugeridas e clique no botão **"Create key pair"**. Ao fazer isso, o par de chaves será gerado e o download da chave privada será feito automaticamente para o seu computador (arquivo **BastionKeyPair.pem**)
    * após a criação do par de chaves, ele deverá aparecer disponível para ser selecionado. Selecione-o para que a chave pública dele seja associada à instância EC2 que será criada.
* Network Settings:
    * Nesse item, devemos configurar a subnet a ser utilizada. Clique em **Edit**
    * VPC: escolha a VPC que será utilizada
    * Subnet: escolha uma subnet **pública** disponível, de preferência, na mesma zona de disponibilidade (AZ) onde foi criada a subnet privada
    * Firewall (security groups)
        * Mantenha a opção pré-selecionada **"Create security group"**, que como o nome indica, criará um novo security group
        * Security group name: para facilitar a identificação, preencha com **"Bastion Host Security Group"**
        * Inbound Security Group Rules: perceba que por padrão, esse security group será criado com a porta 22 do SSH aberta para a Internet. Isso está configurado nos campos **"Port range:22", "Source Type: Anywhere" e "Source: 0.0.0.0/0"**. É exatamente isso que queremos para o Bastion Host, não é necessário fazer nenhuma alteração.
        {{< figure src="/img/2023/AcessoRemotoAWS-2-sg-bastion.png" align="center" alt="Imagem da console AWS mostrando a configuração do Security Group do Bastion Host" >}}
* Deixe as demais configurações de EC2 com os valores padrão, pois não será necessário alterá-los para a demonstração que será feita. Clique em **"Launch Instance"** e aguarde a instância EC2 ficar disponível. 

O passo seguinte é criar uma instância EC2 que fará o papel do servidor de aplicação. Por se tratar de um cenário hipotético, será criada somente uma instância EC2, mas o mesmo procedimento poderia ser realizado mais vezes, caso houvesse mais de um servidor de aplicação.  No painel de gerenciamento de EC2 na console da AWS, escolha a opção **"Launch Instance"** e informe as seguintes configurações:
* Name: **AppServer**
* Application and OS Images (Amazon Machine Image): **Amazom Linux -Amazon Linux 2 AMI**. Perceba que essa AMI é uma versão do Amazon Linux diferente da utilizada no Bastion Host. Isso ajudará a deixar mais claro qual instância EC2 está sendo  acessada por SSH mais a frente.
* Instance type: **t2.micro** (esse tipo de instância é elegível ao free tier da AWS)
* Key pair (login): selecione o par de chaves pública/privada no passo anterior, **BastionKeyPair**, pois iremos utilizar o mesmo par de chaves tanto para o acesso ao servidor de aplicação quanto para o Bastion Host.
* Network Settings:
    * Nesse item, devemos configurar a subnet a ser utilizada. Clique em **Edit**
    * VPC: escolha a VPC que será utilizada
    * Subnet: escolha a subnet privada chamada **Private Subnet** criada anteriormente
    * Firewall (security groups)
        * Mantenha a opção pré-selecionada **"Create security group"**
        * Security group name: para facilitar a identificação, preencha com **"AppServer Security Group"**
        * Inbound Security Group Rules: perceba que por padrão, esse security group será criado com a porta 22 do SSH aberta para a Internet. Entretanto, o que queremos é que essa porta seja acessada somente pelo Bastion Host. Para fazer essa configuração, no campo **"Source type"** troque para a opção **Custom** e em seguida, no campo **Source**, escolha o security group **"Bastion Host Security Group"**. Com essa configuração, o acesso a essa instância EC2 na porta 22 será liberado para outras instâncias que utilizarem o security group **"Bastion Host Security Group"**, que no caso, é a instância do próprio Bastion Host.
        {{< figure src="/img/2023/AcessoRemotoAWS-2-sg-appserver.png" align="center" alt="Imagem da console AWS mostrando a configuração do Security Group do servidor da aplicação" >}}
* Deixe as demais configurações de EC2 com os valores padrão, pois não será necessário alterá-los para a demonstração que será feita. Clique em **"Launch Instance"** e aguarde a instância EC2 ficar disponível. 

Agora chegou o momento de acessar remotamente o servidor de aplicação. Para isso, são necessários dois acessos: o primeiro é o acesso para o Bastion Host para, a partir dele, realizar o segundo acesso que é para o servidor de aplicação na subnet privada. Ambos os acessos serão via SSH. Você deve se lembrar que as duas instâncias EC2 foram configuradas para utilizarem o mesmo par de chaves (**BastionKeyPair**). Isso significa que para os dois acessos, será utilizada a mesma chave privada para a autenticação. Entretanto, não será necessário ter uma cópia do arquivo com a chave privada armazenada no Bastion Host (isso seria um risco de segurança!). Através do recurso de **agent forwarding** do SSH, será possível acessar o servidor da aplicação utilizando a mesma chave privada usada para acessar o Bastion Host sem que o arquivo esteja presente nele. Dessa forma, o arquivo com a chave privda só precisa ficar no seu computador, de onde partirá o primeiro acesso, para ao Bastion Host.

Os comandos a seguir são válidos para o Windows 10 ou superior. Mas o mesmo conceito aplica-se também aos demais sistemas operacionais, como Linux ou MacOS, sendo necessárias as devidas adaptações nos comandos. 

Para utilizar o recurso de **agent forwarding** do SSH, o primeiro passo é habilitar o serviço **OpenSSH Authentication Agent**, também conhecido por **ssh-agent**. Você pode fazê-lo pela interface gráfica abrindo o [gerenciador de Serviços do Windows](https://www.softwaretestinghelp.com/open-windows-services-manager/), achando o serviço **OpenSSH Authentication Agent** e iniciando-o. Outra opção é abrir o **Windows Powershell** como **administrador** e executar os seguintes comandos, que configuram o serviço para início automático e em seguida o inicia:

```` powershell
Set-Service ssh-agent -StartupType Automatic
Start-Service ssh-agent
````
Em seguida, deve-se adicionar a chave privada ao **ssh-agent**, através do comando abaixo. Note que o caminho para o arquivo da chave privada deve ser adaptado para o seu cenário:

```` powershell
ssh-add C:\chaves\BastionKeyPair.pem
````

Para confirmar que a chave privada foi adicionada, pode ser utilizado o comando abaixo, que lista as chaves privadas cadastradas e disponíveis para o **ssh-agent**:

```` powershell
ssh-add -l
````

Agora está tudo pronto para utilizarmos o **agent forwarding** do SSH. O próximo passo é acessar o Bastion Host com o comando abaixo:

```` shell
ssh -A -i BastionKeyPair.pem ec2-user@host
````
Onde:
* o parâmetro **-A** habilita o uso do **agent forwarding**, que permitirá usar a mesma chave privada no acesso do Bastion Host ao servidor da aplicação, sem que ela precise estar presente no Bastion Host
* o parâmetro **"-i"** indica o arquivo com a chave privada que deve ser utilizado. Se o arquivo estiver em um diretório diferente de onde o comando está sendo executado, deve ser informado o caminho completo para o arquivo
* **ec2-user** é o usuário existente no servidor remoto que será autenticado pela chave privada. Como no exemplo a instância EC2 está instalada com o sistema operacional Amazon Linux, o usuário padrão é o **ec2-user**, mas isso vai mudar conforme o sistema operacional.
* **host** é o servidor Bastion Host ao qual será feito o acesso. Pode ser o endereço IP ou um nome DNS. Essa informação pode ser obtida no painel de gerenciamento de EC2 na console da AWS, selecionando a instância EC2 do Bastion Host e observando as informações **"Public IPv4 address"** ou **"Public IPv4 DNS"**

Após substituir os campos acima com os valores corretos e executar o comando, aparecerá a pergunta **"Are you sure you want to continue connecting (yes/no/[fingerprint])?"**. Digite **yes**.

Se após isso aparecer a mensagem de **"WARNING: UNPROTECTED PRIVATE KEY FILE!" -  "Permissions for 'BastionKeyPair.pem' are too open. It is required that your private key files are NOT accessible by others. This private key will be ignored."**, será necessário ajustar as permissões de acesso ao arquivo da chave privada. Essa mensagem é um mecanismo de segurança para evitar que seja utilizado um arquivo com permissões muito abertas. Para corrigir isso, deve-se limitar os usuários que possuem acesso a este arquivo. Siga os seguintes passos:
* abra o Windows Explorer e ache o diretório onde se encontra o arquivo **BastionKeyPair.pem**. Clique com o botão direito nele e escolha a opção **Properties**.
* Na janela que se abre, clique na aba **Security**
* Clique no botão **Advanced**
* Na janela que se abre, clique no botão **Disable inheritance**
* Escolha a opção **"Remove all inherited permissions from this object"**
* Adicione seu usuário local com a permissão de **Full control** e clique em **"Apply"**

Após essa configuração, execute novamente o comando **ssh** e se tudo estiver correto, você estará com um terminal Linux aberto no Bastion Host! Veja que no terminal aparece a mensagem de **"Amazon Linux 2023"**, que foi a AMI utilizada para o Bastion Host. Todos os comandos que você digitar a partir de agora serão executados na instância EC2 do Bastion Host remotamente.

O passo seguinte é acessar o servidor de aplicação. Para isso, a partir do Bastion Host, utilize o comando abaixo:

```` shell
ssh ssh ec2-user@ip-privado
````
Onde:
* **ec2-user** é o usuário existente no servidor remoto que será autenticado pela chave privada. Como no exemplo a instância EC2 está instalada com o sistema operacional Amazon Linux, o usuário padrão é o **ec2-user**, mas isso vai mudar conforme o sistema operacional.
* **ip-privado** é o endereço IP do servidor de aplicação ao qual será feito o acesso. Utilizaremos o endereço IP privado pois esse comando está sendo executado a partir do Bastion Host, que está localizado em uma VPC na AWS com acesso à subnet privada onde se encontra o servidor de aplicação. Essa informação pode ser obtida no painel de gerenciamento de EC2 na console da AWS, selecionando a instância EC2 do servidor de aplicação e observando a informação **"Private IPv4 addresses"**

Se tudo correr bem, você estará com um terminal Linux aberto no servidor de aplicação! Para confirmar, veja que no terminal aparece a mensagem de **"Amazon Linux 2"**, que foi a AMI utilizada para o Bastion Host. Todos os comandos que você digitar a partir de agora serão executados na instância EC2 do servidor de aplicação remotamente. 

Note que nesse segundo comando não foi necessário especificar nenhuma chave privada. Isso acontece por que o SSH está reutilizando a chave privada do primeiro acesso, através do **agent forwarding**, como era o esperado.

{{< figure src="/img/2023/AcessoRemotoAWS-2-sshagent.png" align="center" alt="Imagem dos comandos SSH com acesso remoto à instância EC2 do Bastion Host e posteriormente à instância EC2 do servidor de aplicação" >}}

Para voltar para sua máquina local, utilize o atalho **Ctrl + D** duas vezes: uma para voltar para o Bastion Host e outra para voltar para a linha de comando do seu computador local.

Em relação ao modelo utilizado no [post anterior](({{< relref "/blog/2023/acessando-recursos-remotamente-em-uma-vpc-na-AWS-parte-1.md">}})), essa opção possui como vantagem uma menor superfície de ataque, pois os servidores de aplicação não precisam ficar expostos diretamente para a Internet, podendo ficar isolados em uma subnet privada. Entretanto, o Bastion Host torna-se um componete crítico de segurança e traz algumas implicações. Ele precisa ficar exposto na Internet, o que o torna sujeito a tentativas de ataque, e para diminuir esse risco, deverá passar por um processo de *hardening*. Além disso, ele terá que ser devidamente gerenciado, mantido e atualizado, o que demanda esforço. Outra preocupação que deve ser tratada é quanto a alta disponibilidade dessa solução. Para fins didáticos, o Bastion Host encontra-se somente em uma zona de disponibilidade, mas para cenários críticos, isso não é suficiente. Para finalizar, a complexidade de gerenciamento e armazenamento das chaves privadas continua. 

Nas próximos posts da série serão exploradas mais alternativas de como melhorar a solução em relação a esses pontos.

### Referências
* [Securely Connect to Linux Instances Running in a Private Amazon VPC](https://aws.amazon.com/blogs/security/securely-connect-to-linux-instances-running-in-a-private-amazon-vpc/)
* [ssh-agent: How to configure ssh-agent, agent forwarding, & agent protocol](https://www.ssh.com/academy/ssh/agent)
* [An Illustrated Guide to SSH Agent Forwarding](http://unixwiz.net/techtips/ssh-agent-forwarding.html)
* [Key-based authentication in OpenSSH for Windows](https://learn.microsoft.com/en-us/windows-server/administration/openssh/openssh_keymanagement)


