
---
title: "Dica: Configurando o IIS para reconhecer aplicações ASP.NET"
date: 2005-02-28T03:13:00+08:00
lastmod: 2009-05-24T21:39:50+08:00
draft: false
categories: []
tags: ["asp.net", "dicas", "iis", ]
---


Quando o .NET Framework é instalado, são configurados mapeamentos entre as extensões de arquivos (.aspx, .ascx, etc) e o filtro ISAPI do ASP.NET para que o IIS - *Internet Information Service*, o servidor Web da Microsoft - execute corretamente este tipo de aplicação. Se no momento da instalação do .NET Framework o IIS não tiver sido instalado ou, se por algum motivo, o IIS tiver que ser reinstalado, esses mapeamentos não serão criados e ocorrerão problemas como mensagens de erro no momento da criação de uma nova aplicação ASP.NET no Visual Studio .NET ou a não visualização de controles (textbox, radio buttons, etc.) de páginas no browser.  

Para resolver este problema, basta executar a ferramenta de linha de comando **aspnet_regiis.exe**, também conhecida como *ASP.NET IIS Registration Tool*. Abra uma janela de linha de comando, digite a linha abaixo e tecle ENTER:  

**"*%windir%*\Microsoft.NET\Framework\*version*\aspnet_regiis.exe" -i  
**  
onde:

*   ***%windir%*** é o diretório onde foi instalado o Windows; 
*   ***version*** é o número da versão do .NET Framework instalado em seu computador; 
*   ***-i*** é o argumento que indica à ferramenta que os mapeamentos para o IIS devem ser criados para a versão corrente do .NET Framework;


Para saber sobre as demais opções de parâmetros desta ferramenta, execute o seguinte comando:

**"%windir%\Microsoft.NET\Framework\version\aspnet_regiis.exe" -?**  

Ricardo Oneda.  

