
---
title: "Imagens amareladas no Windows Photo Gallery do Windows Vista"
date: 2007-09-02T19:20:00+08:00
lastmod: 2009-06-21T19:09:36+08:00
draft: false
categories: []
tags: ["windows", "dicas", "outros", ]
---


Outro dia percebi que as imagens abertas no Windows Photo Gallery, do Windows Vista, estavam aparecendo com uma tonalidade de amarelo, como no exemplo abaixo (clique na imagem para vê-la em tamanho maior):

[![](/img/2007/foto_amarelo_p.jpg)](/img/2007/foto_amarelo_g.jpg) 

Note que não somente a imagem aparece amarelada, mas também boa parte da janela do Windows Photo Gallery. Isso ocorria para qualquer arquivo de imagem. O mais estranho é que se aberta em algum outro programa, a imagem era apresentada com as cores corretas.

O problema estava no *profile* de cor utilizado pelo monitor. Para corrigir o problema, clique com o botão direito do mouse sobre o *desktop* > escolha *Personalize* > *Display Settings* > clique no botão *Advanced Settings* > vá à guia *Color Management* > clique em *Color Management* > na janela que se abre, selecione a opção *Use my settings for this device* > clique no botão *Add *> selecione o profile **sRGB IEC61966-2.1** e clique *Ok* > selecione o *profile* que acabou de ser incluído e clique em *Set as Default Profile*. A tela deverá ficar parecida com a imagem abaixo:

![](/img/2007/color.jpg) 

Reinicialize o computador e tente visualizar alguma imagem no Windows Photo Gallery. Se tudo deu certo, a imagem será mostrada com suas cores corretas, conforme figura abaixo (clique na imagem para vê-la em tamanho maior):

[![](/img/2007/foto_normal_p.jpg)](/img/2007/foto_normal_g.jpg) 

Perceba a diferença em relação a imagem anterior. O problema parece ser causado por alguma atualização de *driver* feita pelo Windows Update, segundo infomações que li. Seguem alguns links utilizados como referência:

*   <div>[Windows Vista Photo Gallery Yellow Tint Background Problem](http://www.mydigitallife.info/2007/07/11/windows-vista-photo-gallery-yellow-tint-background-problem/ "Windows Vista Photo Gallery Yellow Tint Background Problem")</div>

*   <div>[Microsoft Photography & Video Blog FAQ](http://blogs.msdn.com/pix/pages/faq.aspx#q6 "Why do my photos have an odd color cast in Vista (but look fine in XP and IE)?") </div>


