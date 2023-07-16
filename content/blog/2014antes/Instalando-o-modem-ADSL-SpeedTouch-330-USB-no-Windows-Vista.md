
---
title: "Instalando o modem ADSL SpeedTouch 330 USB no Windows Vista"
date: 2007-07-31T01:40:00+08:00
lastmod: 2009-06-20T20:27:14+08:00
draft: false
categories: []
tags: ["dicas", "windows", "hardware", ]
---


Se você utiliza banda larga com o modem SpeedTouch 330 via USB, encontrará problemas no Windows Vista. Isso porque o mesmo não é reconhecido automaticamente pelo novo sistema operacional. Notem que estou me referindo ao modem conectado à porta USB, e não ao modem que é conectado à saída da placa de rede Ethernet. Esse, pelo que fiquei sabendo, o Windows Vista reconhece normalmente, e é isso que, provavelmente, o pessoal do suporte técnico da empresa que vende o serviço de banda larga vai lhe falar. O fato é que a versão USB desse modem é quase uma anomalia (são poucos os *felizardos* que o possuem), tanto que este modelo nem está mais disponível.

Ao tentar instalar a aplicação que vem no CD (que não foi feita para o Vista), tudo aparentemente vai bem, até o momento do *boot*. Neste instante, a instalação é interrompida e aparece uma mensagem de erro dizendo que "O cliente PPoE não foi instalado". Neste ponto, apesar da instalação não ter sido concluída, os drivers do modem já foram copiados para o HD e já é possível instalar o modem manualmente. Apesar de assim termos acesso à Internet, não é uma solução muito bonita, pois estamos utilizando uma versão de driver antiga e a mensagem de erro sempre aparece quando inicializamos o computador.

Pesquisando um pouco na Internet, descobri que várias pessoas estavam enfrentando o mesmo problema. Também descobri que, recentemente, a Thomson, fabricante do produto, disponibilizou em seu [site uma versão do driver para Windows Vista](http://www.thomson.net/globalenglish/deliver/in-home-digital-distribution/telco-isp/dsl-modems-gateways/windows_vista_support/Pages/default.aspx). Para instalá-lo, siga o seguinte procedimento:

1.  desligue o modem da porta USB;  
2.  caso tenha instalado alguma versão anterior do driver, desinstale-a; 
3.  dê um boot no computador; 
4.  execute o arquivo copiado do site com os novos drivers; 
5.  quando solicitado, conecte o modem à porta USB;


Em minhas pesquisas sobre o assunto, achei um [post de um blog brasileiro que explica um outro procedimento](http://www.sykey.net/2007/02/06/instalando-e-configurando-o-modem-speedtouch-usb-no-windows-vista/). Não cheguei a testá-lo, mas fica aqui a referência, caso alguém precise.

