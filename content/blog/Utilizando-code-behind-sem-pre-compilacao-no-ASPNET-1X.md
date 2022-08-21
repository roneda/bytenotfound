
---
title: "Utilizando code-behind sem pré-compilação no ASP.NET 1.X"
date: 2006-03-05T19:45:00+08:00
lastmod: 2009-05-29T22:21:04+08:00
draft: false
categories: []
tags: ["asp.net", ".net framework", ]
---


Uma das grandes vantagens trazidas pelo ASP.NET foi o modelo de codificação batizado de *code-behind*, no qual o código *server-side* (por exemplo, C# ou VB.NET) fica separado do código HTML da página, ao contrário da abordagem do ASP tradicional, que misturava tudo e gerava muitos problemas, principalmente na hora da manutenção.

Com o lançamento do ASP.NET 2.0, o modelo de codificação foi aprimorado e o modelo de compilação padrão suportado pelo Visual Studio 2005 passou a ser o de tempo de execução, ou seja, é necessário enviar os arquivos *code-behind* para o servidor. O que muita gente não sabe é que este modelo também era suportado pelo ASP.NET 1.X, mas não era suportado pelo Visual Studio .NET 2002 ou 2003.

Vou demonstrar como isso é possível. Abra o Visual Studio .NET 2002 ou 2003 e crie um novo projeto do tipo ASP.NET Web Application chamado CodeBehind. Neste exemplo utilizarei a linguagem C#, mas poderia ser VB.NET, sem problema algum. Arraste um controle do tipo Label para o WebForm. No evento Page_Load do WebForm, adicione o seguinte código:

Label1.Text = "Olá Mundo sem pré-compilação!";


Agora, vá para a parte HTML da página WebForm1.aspx e acrescente o atributo *Scr* à diretiva *Page*, que deverá ficar parecida com o código abaixo:

<%@ Page language="c#" Codebehind="WebForm1.aspx.cs" AutoEventWireup="false" Inherits="CodeBehind.WebForm1" Src="WebForm1.aspx.cs"%>


Salve os arquivos mas NÃO compile sua aplicação. Abra o arquivo Global.asax no Notepad e exclua a propriedade *Inherits*. O arquivo deverá ficar assim:

<%@ Application Codebehind="Global.asax.cs" %>


Agora, vá ao browser de sua preferência e digite a URL da sua aplicação, que deve ser http://localhost/CodeBehind/WebForm1.aspx e perceba que a mensagem "Olá Mundo sem pré-compilação!" aparece no browser. Você perceberá que na primeira requisição há uma certa demora, pois a aplicação está sendo compilada. A partir da segunda requisição, não haverá mais esta demora, já que o *assemblie* já se encontra compilado. Verifique na pasta *bin* da sua aplicação que não há nenhuma DLL, que seria gerada caso utilizássemos a pré-compilação do Visual Studio. Não há DLL na pasta *bin* porque sua aplicação foi compilada em tempo de execução, ou seja, o *code-behind* foi compilado no momento em que a página foi acessada.

Mas você deve estar se perguntando: mas qual a utilidade disso? A principal vantagem é que quando não utilizamos pré-compilação, qualquer alteração no código é detectada, o que provoca uma nova compilação, mas a aplicação NÃO é reinicializada, ao contrário do que aconte quando geramos uma DLL através da pré-compilação do Visual Studio e a atualizamos com uma nova versão. Vamos a uma demonstração. Altere o código do evento Page_Load para:

 if (Session["numero"] != null)
 {
     Session["numero"] = Convert.ToInt32(Session["numero"]) + 1;
 }
 else
 {
     Session["numero"] = 1;
 }

 Label1.Text = "Olá Mundo sem pré-compilação!";
 Label1.Text += "  
" + Session["numero"].ToString() + " vezes";


Perceba que eu criei uma variável de sessão (objeto *Session*) chamada "numero", que funcionará como um contador de visitas para o usuário naquela sessão. Salve o arquivo e atualize a página no browser e perceba o contador funcionando. Agora, volte ao Visual Studio e altere a linha 10 para:

Label1.Text = "Olá Mundo sem pré-compilação alterado!";


Volte ao browser e atualize a página. Você deverá notar que o texto apresentado na página foi alterado mas o contador (e, portanto, a variável de sessão) não foi reinicilizado, ou seja, a aplicação não foi reinicilizada. Se tentarmos fazer isso utilizando a pré-compilação do Visual Studio, veremos que a cada vez que uma nova DLL é gerada, a aplicação é reinicializada e, conseqüentemente, as variáveis de sessão (objeto *Session*), de aplicação (objeto *Application*), etc, o que pode trazer problemas para a aplicação e os usuários.

A desvantagem é que precisamos enviar o código fonte da aplicação para o servidor, o que pode não ser interessante em termos de segurança. Cabe a você analisar as vantagens e desvantagens de cada modelo e escolher o que melhor atende suas necessidades.

Referências:  
[Web Forms Code Model](http://msdn.microsoft.com/library/default.asp?url=/library/en-us/vbcon/html/vbconwebformscodemodel.asp)  
[Meditating Upon the ASP.NET Code-Behind Model](http://www.codeguru.com/Csharp/.NET/net_general/code-behind/article.php/c4637/)

Ricardo Oneda.

