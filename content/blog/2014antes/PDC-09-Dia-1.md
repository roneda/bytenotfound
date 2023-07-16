
---
title: "PDC 09 - Dia 1"
date: 2009-11-19T03:35:00+08:00
lastmod: 2009-11-19T12:50:40+08:00
draft: false
categories: []
tags: ["eventos", "pdc", ]
---


Na terça-feira, 17/11, o PDC 09 começou oficialmente. O dia iniciou com os *keynotes* de Ray Ozzie, *Chief Software Architect* e substituto de Bill Gates na Microsoft, e Bob Muglia, presidente da divisão de *Server and Tools* (inclusive, já é possível [assistir à gravação ou fazer o download do keynote no site do evento](http://microsoftpdc.com/Sessions/KEY01)). Como não poderia ser diferente, o assunto principal foi Windows Azure e* Cloud Computing*, ou computação na nuvem. Definitivamente, esse é a grande tendência do momento (se é que restava alguma dúvida em relação a isso) já que não só a Microsoft, mas todas as grandes empresas de tecnologia possuem alguma iniciativa nesse campo, como Google, Amazon, IBM, etc.

Se dividirmos a história da informática em “eras”, estamos atualmente em seu quinto estágio. O primeiro durou até o fim dos anos 70 e era dominado pelos Mainframes. Nos anos 80 veio a segunda era, com a popularização dos PCs e o surgimento da arquitetura cliente-servidor. Nos anos 90, apareceu, para as massas, uma coisa chamada Internet, que mudaria a vida de todos, principalmente através da web. Na virada do século, veio o quarto estágio, no qual ficou estabelecido o conceito de serviços/SOA. Por fim, entra o estágio no qual estamos atualmente, representado pela nuvem, onde os serviços ficam disponíveis e a infra-estrutura é tratada como se fosse eletricidade, de forma transparente, fazendo com que até mesmo nos esqueçamos que ela existe.

Pode parecer algo ainda distante para muitos, mas já existem empresas implantando sistemas em produção e aproveitando-se das vantagens que a nuvem oferece. E durante o *keynote*, foram mostrados vários casos que já estão utilizando o Windows Azure, apesar dele só começar a ser comercializado em 2010. O principal benefício é ter uma infra-estrutura de TI dimensionada exatamente para as necessidades do negócio, nem mais e nem menos, pagando somente por que é utilizado. Assim, evita-se que haja uma infra-estrutura superdimensionada só para atender aumentos temporários de demanda, o que caracteriza desperdício, e também se evita a indisponibilidade do serviço caso ocorra um aumento de demanda não previsto. Foi mostrado o exemplo da empresa [Kelley Blue Book](http://www.kbb.com/), que comercializa carros. Eles possuíam dois *datacenters*, sendo que um deles ficava totalmente ocioso, funcionando como *backup* para alguma eventualidade. Com o Azure, esse tipo de custo foi eliminado. Além disso, antigamente, levavam 6 semanas para disponibilizar novo hardware para o site deles. Agora, aproveitando-se da capacidade elástica da nuvem, são necessários apenas 6 minutos para aumentar a capacidade de processamento. E quando a mesma não é mais necessária, volta-se a situação anterior rapidamente.

![A nuvem do Azure](/img/2009%2f11%2fPDC09_1.JPG)

Esse tipo de infra-estrutura exigirá um novo modelo de gerenciamento e de aplicação, que são diferentes do que temos atualmente. Questões como escalabilidade, orientação a serviços, disponibilidade, elasticidade, entre outras, devem ser consideradas.

Também foram anunciados novos serviços e produtos, como o [Microsoft Pinpoint](http://pinpoint.microsoft.com/), uma espécie de marketplace para profissionais e empresas de TI oferecerem seus produtos; o [Microsoft Dallas](http://pinpoint.microsoft.com/en-US/Dallas), que dá acesso a conjuntos de dados, quaisquer que sejam eles, pagos ou não, para serem utilizados nas aplicações; e o Projeto Sydney, que fornecerá a conectividade entre a nuvem do Azure e o ambiente interno das empresas. Aliás, essa é uma característica muito importante para que o conceito de computação na nuvem decole. Na minha opinião, o futuro será formado por um ambiente misto, com parte da infra-estrutura e dados mantidos internamente na empresa e parte suportado por uma nuvem pública como o Azure.

Saindo do assunto Windows Azure, outra sessão que achei interessante e que vale alguns comentários foi sobre o futuro do ASP.NET. Em linhas gerais, o que estão avaliando para as próximas versões do ASP.NET são: utilização do pattern [ActiveRecord](http://en.wikipedia.org/wiki/Active_record_pattern) para acesso a dados no ASP.NET MVC e WebForms; suporte a funcionalidades do HTML 5, como vídeo, *drag and drop* e armazenamento de dados *offline*; melhorias na manipulação de imagens; envio automático de e-mail para confirmação de cadastro em um site, útil para se certificar que o e-mail é válido; notificação sobre progresso de *upload* de arquivos; melhor suporte a [CSS Sprites](http://www.alistapart.com/articles/sprites). Aliás, esse é um conceito interessante: com os CSS Sprites é possível, através de CSS,  agrupar vários arquivos de imagens e tratá-los como se fossem uma única imagem. A vantagem é que o browser só necessita de uma única conexão com o servidor para obter o arquivo, ao invés do que aconteceria caso essa técnica não fosse aplicada (seria necessária uma conexão para cada uma das imagens). Isso aumenta a velocidade com que os elementos da página são baixados, tornando a navegação mais ágil.

Abaixo, seguem links para posts sobre o primeiro dia do PDC, com mais informações sobre o que está acontecendo, escritos por outros brasileiros que também estão aqui em Los Angeles:

*   <div class="MsoNormal" style="text-align: justify; margin: 0cm 0cm 10pt;">[Dia 1 do PDC 2009](http://unplugged.giggio.net/unplugged/post/Dia-1-do-PDC-2009.aspx) – por Giovanni Bassi</div>

*   <div class="MsoNormal" style="text-align: justify; margin: 0cm 0cm 10pt;">[pdc09: primeiro dia de evento!](http://blogs.msdn.com/wcamb/archive/2009/11/17/pdc09-primeiro-dia-de-evento.aspx) – por Waldemir Cambiucci</div>

*   <div class="MsoNormal" style="text-align: justify; margin: 0cm 0cm 10pt;">[PDC 2009 – Dia 1](http://blogs.msdn.com/conde/archive/2009/11/18/pdc-2009-dia-1.aspx) – por Luciano Condé</div>



Logo mais escreverei sobre como foi o segundo dia do PDC 09. Houve muitas novidades sobre o Silverlight. Se você quiser saber o que está acontecendo no PDC 09 em tempo real, [acompanhe-me pelo twitter](http://twitter.com/roneda).

