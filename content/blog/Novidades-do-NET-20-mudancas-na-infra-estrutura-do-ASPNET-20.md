
---
title: "Novidades do .NET 2.0: mudanças na infra-estrutura do ASP.NET 2.0"
date: 2005-11-04T01:45:00+08:00
lastmod: 2009-05-28T23:54:08+08:00
draft: false
categories: []
tags: [".net framework", "asp.net", ]
---


Além de vários novos controles adicionados, as principais mudanças do ASP.NET  2.0 foram introduzidas em sua infra-estrutura. Mudanças drásticas foram feitas:

*   no modelo de codificação, no qual anteriormente havia uma relação de herança entre a página ASPX e o arquivo de código (*code-behind*), e agora faz uso de classes *partial*, ou seja, tanto a página ASPX quanto o código fazem parte da mesma classe, que são combinados em tempo de execução; isso também faz com que o arquivo *code-behind* fique mais claro e menor do que o modelo antigo; 
*   na compilação: agora, o padrão do ASP.NET é compilar a aplicação em tempo execução. Isso implica em copiar os arquivos *code-behind* para o servidor. Entretanto, por questões de segurança e/ou privacidade, nem sempre podemos ou queremos enviar o código com toda nossa lógica para o servidor. Nestes casos, podemos utilizar o que foi chamado de *Precompilation for Deployment*, que consiste em pré-compilar o site em *assemblies*, que então serão copiados para o servidor. Este tipo de pré-compilação faz com que nem mesmo o código fonte de páginas ASPX fique disponível. Também foi desenvolvido um outro tipo de pré-compilação chamado *In-Place Precompilation*, cujo objetivo, é ganhar performance, já que não será necessária a compilação das página na primeira vez em que ela for solicitada, que é o que ocorre se não for feita a pré-compilação. Ambos os tipos de pré-compilação são feitos com o utilitário de linha de comando *aspnet_compiler.exe*;


Também vale citar as mudanças na estrutura do *ViewState*. O *ViewState* é uma técnica utilizada pelo ASP.NET para manter o estado de controles de uma página. Isso é feito através de um campo *HIDDEN* (oculto) da página chamado __VIEWSTATE e, dependendo de como fosse utilizado, poderia causar um sério problema de performance, pois seu tamanho poderia aumentar significantemente, o que aumentaria também o tamanho da página. Foram feitas alterações no formato de serialização deste campo, o que proporcionou a redução do seu tamanho em quase 50%, em um dos testes feitos.  

Referências:

[ASP.NET 2.0 Internals](http://msdn.microsoft.com/en-us/library/ms379581.aspx)  
<span id="nsrTitle">[ASP.NET Web Site Precompilation Overview](http://msdn2.microsoft.com/en-us/library/399f057w.aspx)</span>  
[ASP.NET Page Class Overview](http://msdn2.microsoft.com/en-us/library/ms178138.aspx)  
[Speed Up Your Site with the Improved View State in ASP.NET 2.0](http://msdn.microsoft.com/en-us/magazine/cc163901.aspx)  

Ricardo Oneda

