---
title: "Curso matplotlib - Gráfico com barras de erros (edição da barra de erro)"
data: 2021-07-31
tags: []
header:
  image: "/images/chess.jpg"
  image_description: "Chess pieces"
excerpt: "matplotlib"
locale: "pt-br"
---

<br>


<h2><a style="color:black" id="cor-linha-barra">Cor da linha da barra</a></h2>

Para alterar a cor da linhas das barras de erro, basta passar o parâmetro `ecolor` com a cor desejada para `plt.errorbar()`. A lista de cores disponível é a mesma vista <a href="/Curso-matplotlib-08#cor-marcadores">anteriormente</a>.
{: .text-justify}

Por exemplo, para deixar a cor das barras vermelha:
{: .text-justify}

```python
plt.figure(figsize=(8,6))
plt.errorbar(dias, media, yerr=desv_pad, ecolor='red')
plt.show()
```

*Figura 1* - Gráfico de erros relacionando a temperatura média na cidade de Birigui-SP em três dias diferentes do ano de 2021 - barras na cor vermelha.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-erros/30/grafico-erros-01.png" alt="gráfico de dispersão desenhado com o **matplotlib** relacionando o dia e a temperatura média do dia, com as barras na cor vermelha" >
{: .text-center}

<br>

<h2><a style="color:black" id="espessura-barra-erro">Espessura da barra de erro</a></h2>

A espessura da barra de erro pode ser controlada através do parâmetro `elinewidth`, passando um número (`float` ou `int`) com a espessura desejada.
{: .text-justify}

Por exemplo:

```python
plt.figure(figsize=(8,6))
plt.errorbar(dias, media, yerr=desv_pad, ecolor='red', elinewidth=4)
plt.show()
```

*Figura 2* - Gráfico de erros relacionando a temperatura média na cidade de Birigui-SP em três dias diferentes do ano de 2021 - barras espessas na cor vermelha.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-erros/30/grafico-erros-02.png" alt="gráfico de dispersão desenhado com o **matplotlib** relacionando o dia e a temperatura média do dia, com as barras espessas na cor vermelha" >
{: .text-center}

<br>

<h2><a style="color:black" id="capsize">Caps</a></h2>

Para adicionar uma barra horizontal nas extremidades da barra de erro, basta passar o tamanho desejado (`float` ou `int`) para esta barra para o parâmetro `capsize`. Por padrão, `capsize=0.0`, e por isto ele não apareceu nos gráficos anteriores.
{: .text-justify}

Por exemplo:

```python
plt.figure(figsize=(8,6))
plt.errorbar(dias, media, yerr=desv_pad, ecolor='red', elinewidth=4, capsize=10)
plt.show()
```

*Figura 3* - Gráfico de erros relacionando a temperatura média na cidade de Birigui-SP em três dias diferentes do ano de 2021 - barras espessas na cor vermelha com cap.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-erros/30/grafico-erros-03.png" alt="gráfico de dispersão desenhado com o **matplotlib** relacionando o dia e a temperatura média do dia, com as barras espessas na cor vermelha com cap" >
{: .text-center}

<br>

Observe que por padrão o cap tem tamanho igual a `0.0` e por este motivo ele não é apresentado no gráfico. Contudo, o elemento cap existe mesmo quando `capsize = 0.0`.
{: .text-justify}

<h3><a style="color:black" id="espessura-capsize">Espessura do cap</a></h3>


Para alterar a espessura do `cap`, basta passar um número (`float` ou `int`) para o parâmetro `capthick`. Por exemplo:

```python
plt.figure(figsize=(8,6))
plt.errorbar(dias, media, yerr=desv_pad, ecolor='red', elinewidth=4, capsize=10, capthick=5)
plt.show()
```

*Figura 4* - Gráfico de erros relacionando a temperatura média na cidade de Birigui-SP em três dias diferentes do ano de 2021 - barras espessas na cor vermelha com cap espesso.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-erros/30/grafico-erros-04.png" alt="gráfico de dispersão desenhado com o **matplotlib** relacionando o dia e a temperatura média do dia, com as barras espessas na cor vermelha com cap espesso" >
{: .text-center}

<br>

É fortemente recomendado que a espessura do cap seja igual a espessura da barra de erro.

<br>

<h2><a style="color:black" id="posicao-barra">Posição da barra</a></h2>

Nos gráficos anteriores, a barra de erro foi desenha ***por cima*** da linha. Entretanto, é possível alterar sua posição em relação ao elemento. Para isto, basta passar o parâmetro `barsabove` como `True` (por padrão `barsabove = False`). Por exemplo:
{: .text-justify}

```python
plt.figure(figsize=(8,6))
plt.errorbar(dias, media, yerr=desv_pad, ecolor='red', elinewidth=4, capsize=10, capthick=5, barsabove=True)
plt.show()
```

*Figura 5* - Gráfico de erros relacionando a temperatura média na cidade de Birigui-SP em três dias diferentes do ano de 2021 - barras espessas na cor vermelha com cap espesso com a barra por cima do ponto.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-erros/30/grafico-erros-05.png" alt="gráfico de dispersão desenhado com o **matplotlib** relacionando o dia e a temperatura média do dia, com as barras espessas na cor vermelha com cap espesso com a barra por cima do ponto" >
{: .text-center}

<br>

<form id = "quiz" name = "quiz">

<p><strong>Qual das opções abaixo irá inserir um cap com espessura igual a 2?</strong></p>

<input type = "radio" id = "mc" name = "question1" value = "a"> <code>plt.errorbar(x, y, yerr=desv_pad, ecolor='blue', elinewidth=4, capsize=10)</code>
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "b"> <code>plt.errorbar(x, y, yerr=desv_pad, ecolor='blue', capsize=10, capthick=2)</code>
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "c"> <code>plt.errorbar(x, y, yerr=desv_pad, ecolor='blue', elinewidth=4, capthick=2)</code>
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "d"> <code>plt.errorbar(x, y, ecolor='blue', elinewidth=4, capsize=10, capthick=2)</code>
<p style="font-size: 50%"></p>
<p></p>
<input id = "button" type = "button" class="btn btn--info" value = "Enviar" onclick = "check();">
</form>

<div id = "after_submit">
<p style="font-size: 120%" id = "message"></p>
</div>

<br>

<p style="text-align: center">
  <a href="/Curso-matplotlib-29" class="btn btn--success">Anterior</a>
  <a href="/Curso-matplotlib-31" class="btn btn--success">Próximo</a>
</p>


<script>
function check(){
	var question1 = document.quiz.question1.value;
	var messages = [" Incorreto! 😔 <br> Esta faltando passar o parâmetro <code>capthick=2</code>!",
  " 🎉 Correto! 🥳️ <br> Esta sequência de parâmetros irá inserir um cap com espessura igual a 2!",
  " 😔 Incorreto! 😔 <br> Esta faltando passar o parâmetro <code>capsize</code>! ",
  " 😔 Incorreto! <br> Esta faltando passar o parâmetro <code>yerr</code>! ",
  "☕️"];
	var score;

	if (question1 == "a") {
		score = 0;
	}	else if (question1 == "b") {
		score = 1;
	} else if (question1 == "c") {
    score = 2;
  } else if (question1 == "d") {
    score = 3;    
  } else {
    score = 4;
  }

	document.getElementById("after_submit").style.visibility = "visible";
	document.getElementById("message").innerHTML = messages[score];

};

</script>
