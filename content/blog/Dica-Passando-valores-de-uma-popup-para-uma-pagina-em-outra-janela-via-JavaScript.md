
---
title: "Dica: Passando valores de uma popup para uma página em outra janela via JavaScript"
date: 2005-10-30T18:15:00+08:00
lastmod: 2009-05-28T22:38:33+08:00
draft: false
categories: []
tags: ["javascript", "dicas", ]
---


É comum termos a situação de retornar um valor selecionado em uma janela popup para a página que abriu esta popup. Isso só é possível através de JavaScript, pois são eventos que ocorrem no lado cliente. Para conseguir isso, você poderia utilizar o seguinte bloco de código JavaScript na sua popup:

<script language="javascript">
function selecionaValor(valor)
{
  window.opener.document.forms[0].NOME_CONTROLE.value = valor;
  window.close();
}
</script>


onde:  
<span style="background-color: #ffffff; color: #0000ff;">window.opener</span> é uma referência à janela que abriu a popup;  
<span style="color: #0000ff;">document.forms[0]</span> é uma referência ao formulário (neste caso, o primeiro, cujo índice é 0) da janela que abriu a popup;  
<span style="color: #0000ff;">NOME_CONTROLE</span> é o nome do controle HTML do formulário da janela que abriu a popup, para o qual você vai passar o valor selecionado;  
<span style="color: #0000ff;">valor</span> é o novo valor que será atribuído ao controle da página que abriu a popup;  

E para chamar a função:  

<a href="javascript:selecionaValor('novo valor');">seu link</a>


Obs: a palavra "java script" acima deve ser escrita sem espaços; o theSpoke está bloqueando este tipo de escrita, provavelmente por questões de segurança, o que me obrigou a escrevê-la com um espaço em branco no meio. É por essas e outra que tem tanta gente abandonando o theSpoke...

Ricardo Oneda

