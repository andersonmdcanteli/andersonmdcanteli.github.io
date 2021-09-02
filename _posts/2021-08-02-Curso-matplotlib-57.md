---
title: "Curso matplotlib - Gráfico de barras horizontais (edição das barras)"
data: 2021-08-02
tags: []
header:
  image: "/images/chess.jpg"
  image_description: "Chess pieces"
excerpt: "matplotlib"
locale: "pt-br"
---

<br>

<h2><a style="color:black" id="altura-barra">Altura da barra</a></h2>

Para alterar a altura da barra, utilizamos o parâmetro `height` de forma similar ao parâmetro `width` do `plt.bar()`. Na prática, o parâmetro `height` no `plt.barh()` altera a espessura da barra, mas em relação ao eixo `y`.
{: .text-justify}

Por exemplo, para deixar todas as barras horizontais com uma altura igual de `0.2`, basta:

```python
plt.figure(figsize=(8,6))
plt.barh(frutas, precos, height=0.2)
plt.show()
```

*Figura 1* - Gráfico de barras horizontais com barras com altura diferente do padrão.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-barras-horizontais/57/grafico-barras-horizontais-01.png" alt="gráfico de barras horizontais desenhado com o matplotlib." >
{: .text-center}

<br>

Para deixar as barras horizontais com uma altura variada, basta passar uma `list` contendo números (`float` ou `int`) com o valor desejado para cada barra. Por exemplo:
{: .text-justify}

```python
altura_barras = [0.2, 0.3, 0.4, 0.5, 0.6]
plt.figure(figsize=(8,6))
plt.barh(frutas, precos, height=altura_barras)
plt.show()
```

*Figura 2* - Gráfico de barras horizontais com barras com altura variada.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-barras-horizontais/57/grafico-barras-horizontais-02.png" alt="gráfico de barras horizontais desenhado com o matplotlib." >
{: .text-center}

<br>


<h2><a style="color:black" id="posicao-inicial-barra">Posição inicial da barra</a></h2>

O parâmetro `left` determina a posição inicial da barra no eixo `x`. Ele recebe um número (`float` ou `int`) ou uma sequência de números indicando a posição em que a barra começar a ser preenchida (padrão `left = 0`). O `left` é o parâmetro análogo ao `bottom` de `plt.bar()`.
{: .text-justify}

**Exemplo:**

```python
altura_barras = [0.2, 0.3, 0.4, 0.5, 0.6]
plt.figure(figsize=(8,6))
plt.barh(frutas, precos, height=altura_barras, left = 10)
plt.show()
```

*Figura 3* - Gráfico de barras horizontais com barras com posição inicial deslocada.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-barras-horizontais/57/grafico-barras-horizontais-03.png" alt="gráfico de barras horizontais desenhado com o matplotlib." >
{: .text-center}

<br>


Também é possível variar a posição de início para cada barra, passando uma `list` com uma sequência contendo números (`int` ou `float`) que determinam a posição inicial de cada barra. Por exemplo:
{: .text-justify}


```python
altura_barras = [0.2, 0.3, 0.4, 0.5, 0.6]
posicao_left = [1, 2, 3, 4, 5]
plt.figure(figsize=(8,6))
plt.barh(frutas, precos, height=altura_barras, left = posicao_left)
plt.show()
```

*Figura 4* - Gráfico de barras horizontais com barras com posição inicial deslocada individualmente.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-barras-horizontais/57/grafico-barras-horizontais-04.png" alt="gráfico de barras horizontais desenhado com o matplotlib." >
{: .text-center}

<br>

<h2><a style="color:black" id="alinhamento">Alinhamento</a></h2>

Para ajustar a posição de alinhamento da barra no `plt.barh()` utilizamos o parâmetro `align` de forma similar ao `align` de `plt.bar()`. Este parâmetro recebe uma `string` com as opções `center` (padrão) ou `edge`, que irá posicionar a barra para cima.
{: .text-justify}

**Exemplo:**

```python
altura_barras = [0.2, 0.3, 0.4, 0.5, 0.6]
plt.figure(figsize=(8,6))
plt.barh(frutas, precos, height=altura_barras, align='edge')
plt.show()
```

*Figura 5* - Gráfico de barras horizontais com barras com alinhamento alterado.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-barras-horizontais/57/grafico-barras-horizontais-05.png" alt="gráfico de barras horizontais desenhado com o matplotlib." >
{: .text-center}

<br>

Para colocar a barra abaixo, basta passar um valor negativo para a altura das barras (`height`).

**Exemplo:**

```python
altura_barras = [0.2, 0.3, 0.4, -0.5, -0.6]
plt.figure(figsize=(8,6))
plt.barh(frutas, precos, height=altura_barras, align='edge')
plt.show()
```

*Figura 6* - Gráfico de barras horizontais com barras com alinhamento alterado.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-barras-horizontais/57/grafico-barras-horizontais-06.png" alt="gráfico de barras horizontais desenhado com o **matplotlib**." >
{: .text-center}

<br>

<h2><a style="color:black" id="outros-parametros">Outros parâmetros</a></h2>

Os demais parâmetros, como `color`, `edgecolor`, `linewidth`, `yerr`, `xerr`, `capsize`, etc, tem funcionamento idêntico ao visto em `plt.bar()`.
{: .text-justify}

<br>

<form id = "quiz" name = "quiz">

<p><strong>Qual é o parâmetro de plt.barh() que tem comportamento similar ao parâmetro width de plt.bar()?</strong></p>

<input type = "radio" id = "mc" name = "question1" value = "a"> <code>heigth</code>
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "b"> <code>size</code>
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "c"> <code>left</code>
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "d"> <code>align</code>
<p style="font-size: 50%"></p>
<p></p>
<input id = "button" type = "button" class="btn btn--info" value = "Enviar" onclick = "check();">
</form>

<div id = "after_submit">
<p style="font-size: 120%" id = "message"></p>
</div>

<br>

<p style="text-align: center">
  <a href="/Curso-matplotlib-56" class="btn btn--success">Anterior</a>
  <a href="/Curso-matplotlib-58" class="btn btn--success">Próximo</a>
</p>



<script>
function check(){
	var question1 = document.quiz.question1.value;
	var messages = [" 🎉 Correto! 🥳️ <br>",
  " 😔 Incorreto! 😔  <br> Não existe um parâmetro <code>size</code> em <code>plt.barh()</code>.",
  " Incorreto! 😔<br> O parâmetro <code>left</code> controla a posição inicial da barra em relação ao eixo <code>x</code>.",
  " 😔 Incorreto! <br> O parâmetro <code>align</code> controla a posição inicial da barra em relação ao valor de <code>y</code>.",
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
