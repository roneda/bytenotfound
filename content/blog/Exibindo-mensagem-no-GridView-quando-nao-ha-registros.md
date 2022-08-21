
---
title: "Exibindo mensagem no GridView quando não há registros"
date: 2006-02-05T19:52:00+08:00
lastmod: 2009-05-29T21:55:04+08:00
draft: false
categories: []
tags: ["dicas", "asp.net", ]
---


O controle GridView do ASP.NET 2.0 trouxe duas propriedades que permitem exibir uma mensagem quando a fonte de dados a qual o GridView está vinculado não retornar dados: *EmptyDataTemplate* (permite utilizar um *template* com a mensagem) e *EmptyDataText* (um simples texto que será exibido). Irei fazer um pequeno exemplo de como utilizar estas propriedades.

Para isso, utilizarei o Visual Studio 2005 e o SQL Server 2005 Express com o banco de dados de exemplo Northwind. Apesar da Microsoft recomendar o uso do banco de dados de exemplo [AdventureWorks](http://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&DisplayLang=en), que foi criado especialmente para o SQL Server 2005, optei por utilizar o Northwind, pois ele é mais conhecido e também porque permitirá que pessoas com o SQL Server 2000 possam utilizá-lo. Caso você não tenha o Northwind, você pode fazer o seu [download](http://www.microsoft.com/downloads/details.aspx?FamilyID=06616212-0356-46a0-8da2-eebc53a68034&DisplayLang=en). Após baixar o arquivo *SQL2000SampleDb.msi* e executá-lo, será criada uma pasta em "C:\SQL Server 2000 Sample Databases" com os scripts e arquivos MDF e LDF dos banco de dados Northwind e Pubs. Abra o SQL Express Manager e execute o comando abaixo para *attachar* o Northwind à instância do SQL Express:

EXEC sp_attach_db N'Northwind',N'C:\SQL Server 2000 Sample Databases\NORTHWND.MDF'


Agora vá ao Visual Studio 2005 e crie um novo Web Site chamado *GridViewVazio*. No Server Explorer (menu *View > Server Explorer*), clique com o botão direito em *Data Connections* e escolha a opção *Add Connection*. Na tela que é apresentada, iremos definir nossa fonte de dados (*Data So*urce). Escolha *Microsoft SQL Server* e clique no botão *Continue*. Na próxima tela, entre com o nome da instância onde está rodando o SQL Express (no padrão NOME_MAQUINA\SQLEXPRESS) e selecione o banco de dados Northwind. Você deve ver uma tela parecida com a da imagem abaixo. Clique no botão *Test Connection* para verificar se está tudo certo e depois em *OK*.

![](/img/2006/GridViewVazio01.gif)

Vá para o *design* da página *Default.aspx* e arraste um *TextBox* e um *Button* para ela. Logo abaixo, a partir do *Server Explorer*, arraste a tabela *Products* do banco de dados Northwind. Perceba que foram criados um controle *GridView* e um *SqlDataSource*. Você deve ter uma tela parecida com a figura abaixo.

![](/img/2006/GridViewVazio02.gif)

Agora, vamos fazer com que os produtos sejam exibidos no GridView de acordo com o que digitarmos no TextBox, funcionando como uma pesquisa. Selecione o SqlDataSource e clique na seta no canto superior direito para termos acesso a sua* SmartTag*. Selecione a opção *Configure Data Source*. Não altere nada na primeira tela e clieque em *Next*. Na próxima tela é apresentada nossa query T-SQL que desejamos alterar. Clique no botão *WHERE*. Em *Column*, escolha o campo *ProductName*. Em *Operator* escolha o operador *LIKE* do T-SQL. Em *Source*, escolha *Control*, já que nosso parâmetro será digitado no controle TextBox. Em *ControlID*, selecione *TextBox1*, que é o ID do nosso controle TextBox.

![](/img/2006/GridViewVazio03.gif)

Clique em *Add* e depois em *OK*. Na próxima tela, clique em *Next* e, finalmente, em *Finish*. Também podemos mudar o *layout* de nosso GridView, clicando em *AutoFormat* a partir de sua *SmartTag*. Escolha um formato de sua preferência. Selecione o GridView e exiba a janela de propriedades (*View > Propertie Window*). Altere o valor a propriedade *EmptyDataText* para "*Não foram encontrados registros para a busca.*"

Execute a aplicação e perceba que a mensagem de que "*Não foram encontrados registros para a busca.*" é exibida, já que não há nada digitado no caixa de texto. 

![](/img/2006/GridViewVazio04.gif)

Digite algum texto que exista na tabela de produtos e veja que o GridView vem preenchido.

![](/img/2006/GridViewVazio05.gif)

Outra maneira de se exibir uma mensagem é utilizando o *EmptyDataTemplate*, que lhe dá mais flexibilidade, já que podemo definir um *template* (trecho de código HTML personalizado). Volte ao Visual Studio 2005, selecione o GridView e, a partir de sua *SmartTag*, selecione a opção *Edit Templates*. O *EmptyDataTemplate* é então aberto para que possamos editá-lo. Neste exemplo, utilizei a frase "*Não foram encontrados registros para a busca.*" em negrito e na cor vermelha. Fiz uma simples personalização, mas perceba que poderia fazer algo mais complexo.

![](/img/2006/GridViewVazio06.gif)

Na *SmartTag* do *EmptyDataTemplate*, selecione *End Template Editing* para retornar ao *design* da página *Default.aspx*. Se você visualizar o fonte da página *Default.aspx*, encontrará a definição do template utilizado no *EmptyDataTemplate*:

    <EmptyDataTemplate>
        <span style="color: red"><strong>Não foram encontrados registros para a busca.</strong></span>
    </EmptyDataTemplate>


Execute a aplicação e perceba que agora a mensagem exibida é aquela definda pelo *EmptyDataTemplate*.

![](/img/2006/GridViewVazio07.gif)

Espero que tenham gostado e até a próxima.

Ricardo Oneda

