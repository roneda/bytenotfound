---
title: "ATENÇÃO: Sua conta na AWS pode ficar mais cara em 2024"
date: 2024-01-10T20:20:06-03:00
draft: false
tags: ["aws", "finops", "ipv4", "eks", "rds", "aurora", "mysql", "postgresql", "suporte estendido"]
cover: 
  image: "/img/2024/custos_cloud.jpg"
---

{{< figure src="/img/2024/custos_cloud.jpg" align="center" alt="Desenho de uma nuvem com um cifrão e com notas de dólar voando no céu" >}}



Não é novidade que custo é um assunto muito importante quando falamos de Cloud. A facilidade que uma plataforma de Cloud oferece para criarmos recursos rapidamente e escalar conforme a necessidade pode gerar descontrole e resultar em supresas nada agradáveis para o bolso quando a conta chegar. O tema é tão importante que até existe uma disciplina ([FinOps](https://www.finops.org/)) dedicada a como fazer uso de Cloud sem desperdícios financeiros, com o máximo de eficiência possível. É um trabalho contínuo, que exige acompanhamento e ajustes constantes.

A AWS também reconhece a importância do assunto. Tanto é que um dos pilares do AWS Well-Architected Framework é o de [Otimização de Custos](https://docs.aws.amazon.com/wellarchitected/latest/cost-optimization-pillar/welcome.html?ref=wellarchitected-wp), que contém orientações e boas práticas de como utilizar os produtos da AWS de forma eficiente e com o menor custo possível. 

Além disso, a AWS gosta bastante de divulgar que repassa para seus clientes reduções nos preços de seus produtos, reflexo de suas constantes melhorias em eficiência. E realmente é um histórico impressionante. Segundo dados de 2022 da própria AWS, [já houve 115 reduções de preços desde quando ela começou em 2006](https://docs.aws.amazon.com/wellarchitected/latest/cost-optimization-pillar/cost_cloud_financial_management_scheduled.html#:~:text=As%20of%20April%202022%2C%20AWS%20has%20reduced%20prices%20115%20times%20since%20it%20was%20launched%20in%202006). Inclusive, boa parte do [histórico de anúncios de reduções de preços pode ser consultada](https://aws.amazon.com/blogs/aws/category/price-reduction/). 

Entretanto, no segundo semestre de 2023 a AWS fez alguns anúncios que vão impactar diretamente no custo de seus clientes em 2024, se não forem tomadas as devidas precauções. É uma nova cobrança e um novo "serviço" que poderão ser cobrados automaticamente caso não sejam tomadas ações. 


## Cobrança de endereços IPv4 públicos

A partir de 1º de Fevereiro de 2024, todos endereços IPv4 públicos em uso serão cobrados pela AWS. Isso **NÃO se limita** ao Elastic IP. Ou seja, uma instância EC2 (ou qualquer outro recurso) que tenha um endereço IPv4 público associado diretamente a ela, sem o uso do Elastic IP, passará a sofrer cobrança. Atualmente, somente Elastic IPs que não estão em uso são cobrados.

Essa é uma forma indireta da AWS "incentivar" a adoção de IPv6, já que segundo ela os preços de IPv4 aumentaram bastante nos últimos tempos devido à escassez. Portanto, é bom rever os recursos que estão em subnets públicas e se eles podem ser transferidos para subnets privadas ou então passarem a utilizar IPv6.

Mais informações sobre a nova cobrança você encontra em [New – AWS Public IPv4 Address Charge + Public IP Insights](https://aws.amazon.com/blogs/aws/new-aws-public-ipv4-address-charge-public-ip-insights/) 

E para sugestões de como fazer melhor uso de endereços IPv4 públicos, você pode ler [Identify and optimize public IPv4 address usage on AWS](https://aws.amazon.com/blogs/networking-and-content-delivery/identify-and-optimize-public-ipv4-address-usage-on-aws/)


## Serviço de suporte estendido para EKS e RDS

Softwares comerciais e *open source* trabalham com ciclo de vida. Isso significa que quando uma nova versão é lançada, ela será suportada e receberá correções durante um determinado período. Até o término desse período, espera-se que o software seja atualizado para versões mais atualizadas. Caso isso não aconteça, o usuário desse software assume o risco de utilizar uma versão antiga, sujeita a *bugs* e vulnerabilidades de segurança.

A AWS anunciou o serviço de suporte estendido para EKS, o serviço gerenciado de Kubernetes da AWS, e para RDS, o serviço de banco de dados relacional da AWS. No caso do RDS, o suporte estendido será para MySQL e PostgreSQL, inclusive para Aurora. Com esse serviço, a AWS passará a fornecer suporte e correções de segurança para versões que não são mais suportadadas oficialmente pelas comunidades. E claro, isso terá um custo. O suporte estendido de EKS ainda está em **preview** e por enquanto não será cobrado, mas a previsão é que isso mude em algum momento do início de 2024. Já para o MySQL, a cobrança começa em março de 2024, e para o PostegreSQL, em abril de 2024.

Na prática, isso significa que quem estiver utilizando uma versão antiga de Kubernetes, MySQL e PostegreSQL, fora do período do suporte padrão, entrará **automaticamente** no suporte estendido da AWS. Ou seja, isso acarretará no aumento de custos automaticamente. Para evitar essa cobrança, os usuários precisarão atualizar os produtos para versões mais novas antes do término do período de suporte padrão. 

Para saber mais informações sobre o serviço de suporte estendido, suas condições e restrições, leia:
* [Amazon EKS extended support for Kubernetes versions available in preview](https://aws.amazon.com/blogs/containers/amazon-eks-extended-support-for-kubernetes-versions-available-in-preview/)
* [Your MySQL 5.7 and PostgreSQL 11 databases will be automatically enrolled into Amazon RDS Extended Support](https://aws.amazon.com/blogs/aws/your-mysql-5-7-and-postgresql-11-databases-will-be-automatically-enrolled-into-amazon-rds-extended-support/)