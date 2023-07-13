---
title: "Acessando recursos remotamente em uma VPC na AWS - parte 1"
date: 2023-07-09T09:51:39-03:00
draft: false
tags: ["aws", "vpc", "ssh", "acesso remoto", "infraestrutura", "segurança"]
---

Esse é o primeiro de uma série de posts nos quais falarei sobre como podemos acessar remotamente recursos de infraestrutura (ex: instâncias EC2, bancos de dados RDS, etc) que se encontram localizados em uma VPC na AWS. Se você conhece ou trabalha com AWS, já sabe que é possível alcançar determinado resultado de várias maneiras. O objetivo dessa série de posts é mostrar de forma prática as principais opções que podemos utilizar para acessar remotamente, a partir do seu computador, um componente de infraestrutura em uma VPC. Serão mostradas várias alternativas, desde a mais tradicional até a mais sofisticada, com variados graus de complexidade, segurança e custo. 

Você precisa ter conhecimentos básicos de AWS e se quiser implementar na prática os cenários apresentados, será necessária uma conta AWS. A AWS oferece um nível gratuito para experimentação de seus produtos ([AWS Free Tier](https://aws.amazon.com/free/)) que pode ser utilizado para implementação dos exemplos, mas o leitor deve ficar atento para eventuais custos que possam ser gerados.

## Acessando uma instância EC2 com SSH

A primeira opção a ser apresentada é a mais básica e tradicional. Como exemplo, imagine o cenário em que temos uma aplicação sendo executada em instâncias EC2 na AWS e que precisamos acessar essas instâncias EC2 para realizar algum tipo de atividade, como manutenção no servidor ou investigação de algum problema. Podemos fazer isso através do SSH. O [SSH](https://en.wikipedia.org/wiki/Secure_Shell), ou Secure Shell, é um protocolo de redes seguro que permite o acesso remoto a servidores e outros dispositivos. No nosso cenário de exemplo, iremos acessar uma instância EC2 com SSH, através da Internet e utilizando autenticação baseada em chave pública. O diagrama de arquitetura abaixo representa esse cenário.

{{< figure src="/img/2023/AcessoRemotoAWS-1-EC2-SSH.png" align="center" alt="Diagrama de arquitetura do cenário de acesso a uma instância EC2 com SSH. O diagrama mostra um usuário com uma chave privada acessando, através da Internet, uma instância EC2 em uma subnet pública de uma VPC na AWS, utilizando o protocolo SSH na porta 22" >}}

Observe os seguintes pontos:
* o acesso será feito via Internet. Dessa forma, a instância EC2 precisa estar em uma subnet pública da VPC na AWS, para que ela possa aceitar conexões externas vindas da Internet. Na AWS, uma subnet é considerada pública quando possui uma Route Table configurada com uso de um Internet Gateway. 
* o acesso será através da porta 22, que é a porta padrão de SSH no servidor. Portanto, teremos que configurar o Security Group da instância EC2 para permitir conexões vindas da Internet para essa porta.
* o usuário que for acessar a instância EC2 terá que ter uma chave privada válida para se autenticar no SSH. Para isso, deverá ser gerado um par de chaves para ser utilizado nesse processo.

Para implementar esse cenário, acesse sua conta AWS através da console. O primeiro passo é criar uma VPC e uma subnet pública. A VPC padrão que toda conta AWS possui já vem com uma subnet pública e Internet Gateway configurados e é ela que iremos utilizar nesse exemplo. Caso queira, você pode começar do zero e criar uma nova VPC com uma nova subnet e configurar o Internet Gateway nela.

Em seguida, crie uma instância EC2 que irá fazer o papel do servidor de aplicação. No painel de gerenciamento de EC2 na console da AWS, escolha a opção **"Launch Instance"**. Isso irá iniciar o guia de criação de EC2, que deve ser criada com as seguintes configurações:
* Name: **AppServer**
* Application and OS Images (Amazon Machine Image): **Amazom Linux - Amazon Linux 2023 AMI**
* Instance type: **t2.micro** (esse tipo de instância é elegível ao free tier da AWS)
* Key pair (login)
    * aqui precisamos criar um par de chaves pública/privada, que será utilizada para autenticação no acesso SSH da instância EC2. Clique no link **"Create new key pair"**, conforme imagem abaixo:
    {{< figure src="/img/2023/AcessoRemotoAWS-1-keypair.png" align="center" alt="Imagem da console AWS mostrando o link de criação de um novo par de chaves" >}}
    * em **"Key pair name"**, coloque **AppServerKeyPair**
    * deixe as demais configurações conforme sugeridas e clique no botão **"Create key pair"**. Ao fazer isso, o par de chaves será gerado e o download da chave privada será feito automaticamente para o seu computador (arquivo **AppServerKeyPair.pem**)
    * após a criação do par de chaves, ele deverá aparecer disponível para ser selecionado. Selecione-o para que a chave pública dele seja associada à instância EC2 que será criada.
    {{< figure src="/img/2023/AcessoRemotoAWS-1-keypair-2.png" align="center" alt="Imagem da console AWS mostrando a seleção do par de chaves criado" >}}
* Network Settings:
    * Nesse item, devemos configurar a subnet a ser utilizada. Clique em **Edit**
    * VPC: escolha a VPC que será utilizada
    * Subnet: escolha uma subnet pública disponível
    * Firewall (security groups)
        * Mantenha a opção pré-selecionada **"Create security group"**, que como o nome indica, criará um novo security group
        * Security group name: para facilitar a identificação, preencha com **"AppServer Security Group"**
        * Inbound Security Group Rules: perceba que por padrão, esse security group será criado com a porta 22 do SSH aberta para a Internet. Isso está configurado nos campos **"Port range:22", "Source Type: Anywhere" e "Source: 0.0.0.0/0"**. É exatamente isso que queremos, não é necessário fazer nenhuma alteração.
        {{< figure src="/img/2023/AcessoRemotoAWS-1-sg.png" align="center" alt="Imagem da console AWS mostrando a configuração do Security Group" >}}
* Deixe as demais configurações de EC2 com os valores padrão, pois não será necessário alterá-los para a demonstração que será feita. Clique em **"Launch Instance"** e aguarde a instância EC2 ficar disponível. 

Agora chegou o momento de acessar remotamente a instância EC2 via SSH. Para isso, é preciso um **cliente SSH**. O Windows, a partir da versão 10, já vem com um **cliente SSH** por padrão e é ele que será utilizado nessa demonstração. Entretanto, você pode utilizar qualquer outro **cliente SSH** seja no Windows ou em outro sistema operacional. 

Abra o **Windows Powershell** ou o **Command Prompt** e execute o comando SSH abaixo:

```` shell
ssh -i AppServerKeyPair.pem ec2-user@host
````

Onde:
* o parâmetro **"-i"** indica o arquivo com a chave privada que deve ser utilizado. Se o arquivo estiver em um diretório diferente de onde o comando está sendo executado, deve ser informado o caminho completo para o arquivo
* **ec2-user** é o usuário existente no servidor remoto que será autenticado pela chave privada. Como no exemplo a instância EC2 está instalada com o sistema operacional Amazon Linux, o usuário padrão é o **ec2-user**, mas isso vai mudar conforme o sistema operacional.
* **host** é o servidor ao qual será feito o acesso. Pode ser o endereço IP ou um nome DNS. Essa informação pode ser obtida no painel de gerenciamento de EC2 na console da AWS, selecionando a instância EC2 desejada e observando as informações **"Public IPv4 address"** ou **"Public IPv4 DNS"**

Após substituir os campos acima com os valores corretos e executar o comando, aparecerá a pergunta **"Are you sure you want to continue connecting (yes/no/[fingerprint])?"**. Digite **yes**.

Se após isso aparecer a mensagem de **"WARNING: UNPROTECTED PRIVATE KEY FILE!" -  "Permissions for 'AppServerKeyPair.pem' are too open. It is required that your private key files are NOT accessible by others. This private key will be ignored."**, será necessário ajustar as permissões de acesso ao arquivo da chave privada. Essa mensagem é um mecanismo de segurança para evitar que seja utilizado um arquivo com permissões muito abertas. Para corrigir isso, deve-se limitar os usuários que possuem acesso a este arquivo. Siga os seguintes passos:
* abra o Windows Explorer e ache o diretório onde se encontra o arquivo **AppServerKeyPair.pem**. Clique com o botão direito nele e escolha a opção **Properties**.
* Na janela que se abre, clique na aba **Security**
* Clique no botão **Advanced**
* Na janela que se abre, clique no botão **Disable inheritance**
* Escolha a opção **"Remove all inherited permissions from this object"**
* Certique que seu usuário de seu computador local esteja na lista remanescente e clique em **"Apply"**

Após essa configuração, execute novamente o comando **ssh** e se tudo estiver correto, você estará com um terminal Linux aberto no servidor remoto. Todos os comandos que você digitar serão executados na instância EC2 remotamente.

{{< figure src="/img/2023/AcessoRemotoAWS-1-ssh.png" align="center" alt="Imagem do comando SSH com acesso remoto à instância EC2 pelo terminal Linux" >}}

Para voltar para sua máquina local, digite **exit** e tecle **ENTER** ou então utilize o atalho **Ctrl + D**.

A opção apresentada, apesar de funcionar, possui alguns pontos de atenção importantes:
* o servidor da aplicação precisa estar em uma subnet pública para que possa ser acessado pela Internet. Ao expô-la na Internet, a instância EC2 sofrerá tentativas de invasão e ataques, no mínimo, na porta 22. Se a aplicação não tiver nenhuma outra funcionalidade que justifique ser exposta na Internet, o servidor terá que ficar exposto somente por causa do SSH. Isso amplia a superfície de ataque desnecessariamente.
* da maneira que foi feita, se a solução for composta por várias instâncias EC2, cada uma delas deverá ficar exposta na Internet para que possam ser acessadas remotamente, ampliando ainda mais a superfície de ataque.
* esse modelo pode funcionar para cenários muito simples ou em testes rápidos, mas quando se trata de uso profissional e corporativo, é complexo de escalar. Imagine uma situação em que várias pessoas precisam ter acesso a vários servidores diferentes. Isso vai exigir um grande número de pares de chave públicas e privadas, que precisarão ser gerenciadas e armazenadas em local seguro. Se uma dessas chaves privadas for comprometida ela poderá dar acesso a alguém com intenções maliciosas.Para evitar isso todos os servidores acessíveis por essa chave privada precisarão ter a respectiva chave pública removida deles.

Nas próximos posts da série, serão mostradas opções de como tratar esses pontos e melhorar a solução.

