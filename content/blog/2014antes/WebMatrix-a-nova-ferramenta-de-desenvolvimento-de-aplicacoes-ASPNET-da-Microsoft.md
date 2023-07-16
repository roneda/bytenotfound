
---
title: "WebMatrix: a nova ferramenta de desenvolvimento de aplicações ASP.NET da Microsoft"
date: 2010-07-06T23:46:00+08:00
lastmod: 2010-07-07T05:50:40+08:00
draft: false
categories: []
tags: ["iis", "asp.net", "webmatrix", ]
---


Nesses [10 anos de existência do .NET Framework](http://reddevnews.com/articles/2010/06/28/happy-bithday-dotnet-framework.aspx "Happy Birthday .NET Framework!"), o ASP.NET se consolidou como uma das mais importantes plataformas de desenvolvimento de aplicações web. Inicialmente concebido com um modelo de desenvolvimento muito próximo ao que era utilizado no desenvolvimento de aplicações *desktop*, cujo objetivo era facilitar a transição dos profissionais que estavam acostumados a desenvolver aplicações *desktop* mas nunca haviam programado para web, muita coisa mudou desde a versão 1.0. A cada nova versão, características mudaram e muitos recursos foram adicionados. Um novo modelo de desenvolvimento, o [ASP.NET MVC](/blog/post/2008/01/13/Desvendando-o-ASPNET-MVC-Framework.aspx "Desvendando o ASP.NET MVC Framework"), apareceu como alternativa ao modelo WebForms. Além disso, nesse meio tempo, vários paradigmas surgiram nas aplicações Web, como Ajax e RIA, que foram devidamente incorporados à plataforma ASP.NET.  Apesar desses novos recursos proporcionarem ganhos de produtividade na medida em que foram incorporados pelo ASP.NET, paradoxalmente, eles também adicionaram um certo nível de complexidade para os novatos, que estão sendo apresentados agora para o ASP.NET e que não acompanharam toda a evolução da plataforma. Apesar da abundância de informação e documentação sobre ASP.NET na Internet e em outros meios (revistas, livros, CDs de treinamento, etc) e ferramentas disponíveis para aprendizado, como a [versão trial do Visual Studio 2010](http://www.microsoft.com/downloads/details.aspx?familyid=5414E4C0-C1F8-473E-8E9D-A1A7BE786141&displaylang=en "Microsoft Visual Studio 2010 Professional Trial - ISO") ou então as versões [Express do Visual Studio](http://www.microsoft.com/express/downloads/ "Visual Studio 2010 Express") que são gratuitas, para alguém que está começando a aprender sobre desenvolvimento de aplicações web, é complicado saber por onde começar.

Se você acompanha esse blog regularmente, deve se lembrar que no [último post que escrevi](/blog/post/2010/07/04/Aconteceu-no-Twitter-23-270610-a-030710.aspx "Aconteceu no Twitter 23 - 27/06/10 a 03/07/10"), comentei sobre algumas novidades do ASP.NET que foram anunciadas na semana passada. Relembrando, foram anunciados os seguintes produtos:

*   <div style="text-align: justify;">[IIS Express](http://learn.iis.net/page.aspx/868/iis-developer-express-overview/ "IIS Developer Express Overview"): um servidor web gratuito, totalmente compatível com o IIS da versão *server* do Windows, e sem as limitações do Cassini, que é o servidor web que vem atualmente embutido no Visual Studio. A vantagem é que o desenvolvedor terá uma versão de servidor web muito mais próxima do que se encontra em ambientes reais de produção, sem a necessidade de se ter uma versão *server* do Windows para executá-lo, já que o IIS Express funcionará em qualquer versão de Windows a partir do XP, e será muito mais fácil de instalar e configurar;</div>

*   <div style="text-align: justify;">[SQL Server Compact Edition com suporte ao ASP.NET](http://weblogs.asp.net/scottgu/archive/2010/06/30/new-embedded-database-support-with-asp-net.aspx "New Embedded Database Support with ASP.NET"): um banco de dados leve, gratuito, baseado em arquivo e compatível com o SQL Server. Basta copiar o arquivo de banco de dados com extensão *.sdf* que o ASP.NET conseguirá acessá-lo, sem necessidade de instalação e/ou configuração;</div>

*   <div style="text-align: justify;">[Razor](http://weblogs.asp.net/scottgu/archive/2010/07/02/introducing-razor.aspx "Introducing “Razor” – a new view engine for ASP.NET "): é o codinome do novo *view engine* do ASP.NET e que será o padrão a partir do ASP.NET MVC 3, que está em desenvolvimento. O objetivo dele é simplificar a codificação das *views* do ASP.NET MVC, facilitando a geração de código HTML;</div>




<table border="0">
<tbody>
<tr>
<td>


Se você prestou atenção, percebeu que todos os produtos acima possuem em comum o desejo de **simplificar** a vida dos desenvolvedores, seja no momento da codificação, seja na hora de se montar o ambiente de desenvolvimento. Dentro desse mesmo objetivo, de simplificação, hoje foi anunciada a versão beta do [WebMatrix](http://www.microsoft.com/web/webmatrix/ "WebMatrix"), que é uma nova IDE de desenvolvimento de aplicações web com ASP.NET, voltada para os inciantes que estão começando a dar seus primeiros passos no mundo do desenvolvimento web. O WebMatrix, além do editor de código, também integrará os produtos citados acima (IIS Express, SQL Server Compact Edition e Razor) e mais uma ferramenta de publicação, em um mesmo pacote, fornecendo de uma única vez tudo que um desenvolvedor iniciante precisa para começar a aprender ASP.NET, de maneira rápida e fácil.

</td>
<td>


[![WebMatrix](/img/2010%2f7%2fwebx-brand.png)](http://www.microsoft.com/web/webmatrix/ "WebMatrix")

</td>
</tr>
</tbody>
</table>


Vale ressaltar que, se você não é um iniciante e já utiliza o Visual Studio como ferramenta de desenvolvimento (seja a versão completa ou a Express), tanto o IIS Express, quanto o SQL Server Compact Edition e o Razor também estarão disponíveis para você através de uma atualização a ser lançada futuramente, ou seja, para utilizar qualquer uma dessas tecnologias não será obrigatório o uso do WebMatrix.

Quando um novo site é criado a partir do zero no WebMatrix, você logo percebe a diferença em relação a uma aplicação ASP.NET criada pelo Visual Studio. Para começar, existe uma nova extensão de arquivo, que varia de acordo com a linguagem utilizada: *.cshtml* (código C#) ou *.vbhtml* (código VB.NET) . Arquivos com essas extensões são chamados de *ASP.NET Web Pages*, que utilizam a nova sintaxe do Razor. Quando criado um arquivo desse tipo, inicialmente ele só contém código HTML, diferentemente de uma página ASP.NET tradicional (arquivo com extensão *.aspx*). Assim, por exemplo, nos arquivos que utilizam Razor, não existe a diretiva *Page*. Isso torna a página bem mais limpa. Nesse ponto, há uma semelhança muito grande com o que havia de simplicidade nas páginas ASP clássicas. Além disso, quando o site é criado, não há arquivo *web.config*.

Outra facilidade que o WebMatrix traz são alguns *helpers*, que permitem integração fácil com serviços como Twitter, Facebook, Google Analytics, geração de *captchas*, gráficos, etc. Esses *helpers* também estarão disponíveis futuramente para quem utiliza Visual Studio, ou seja, não é uma funcionalidade exclusiva do WebMatrix.

Concluindo, o WebMatrix é uma ferramenta voltada para o público iniciante, para aplicações de pequeno e médio porte, cujo objetivo é diminuir o atrito de quem está começando a conhecer o desenvolvimento para a plataforma web com ASP.NET, facilitando vários aspectos que uma pessoa nesse estágio de aprendizado, normalmente, ainda não tem condições de conhecer. Também vejo essa ferramenta como uma porta de entrada para profissionais de outras plataformas, principalmente PHP, pois o WebMatrix oferece um ambiente mais próximo daquele e evita que, em um primeiro momento, o profissional tenha que se familiarizar com conceitos exclusivos do ASP.NET. Além disso, a Microsoft está tento cuidado para que todo (ou pelo menos a maior parte do)  conhecimento adquirido no WebMatrix possa ser reaproveitado quando a pessoa decidir mudar para uma plataforma mais profissional, e nesse sentido, há uma tendência para que se opte pelo ASP.NET MVC.

Fiquem ligados no blog, pois pretendo abordar mais detalhes do WebMatrix nos próximos dias.

*Obs: se você acompanha a evolução do .NET Framework desde o início, deve ter se lembrado que já existiu uma ferramenta da Microsoft chamada WebMatrix, também voltada para aplicações ASP.NET, muito semelhante a essa em seus objetivos. Isso foi antes das versões Express existirem. Apesar do mesmo nome, esse novo WebMatrix trata-se de uma ferramenta totalmente diferente. Parece que as opções de nomes para produtos estão acabando na Microsoft ![Wink](http://oneda.mvps.org/blog/editors/tiny_mce3/plugins/emotions/img/smiley-wink.gif "Wink").*

Referências:

[Site oficial do WebMatrix](http://www.microsoft.com/web/webmatrix/)

[Introducing WebMatrix](http://weblogs.asp.net/scottgu/archive/2010/07/06/introducing-webmatrix.aspx)

[Microsoft WebMatrix in Context and Deploying your first site](http://www.hanselman.com/blog/MicrosoftWebMatrixInContextAndDeployingYourFirstSite.aspx)

