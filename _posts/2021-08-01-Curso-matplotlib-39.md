---
title: "Curso matplotlib - Elementos auxiliares (reta horizontal)"
data: 2021-08-01
tags: []
header:
  image: "/images/chess.jpg"
  image_description: "Chess pieces"
excerpt: "matplotlib"
locale: "pt-br"
---

<br>

Para desenhar uma reta horizontal no gráfico, podemos utilizar o ```plt.axhline()``` ou o ```plt.hlines()``` que tem algumas pequenas diferenças entre si, mas é possível desenhar a mesma linha com estes dois elementos. Contudo, é muito semelhante ao que foi visto para a inserção de uma reta vertical.
{: .text-justify}

<h2><a style="color:black" id="plt-axhline">Utilizando o plt.axhline()</a></h2>

Este elemento recebe três parâmetros:

- o ```y```, que é a posição em `y` que a linha horizontal será desenhada (`float` ou `int`);

- o ```xmin```, que é a distância entre a base do gráfico e o início da reta (`int` ou `float`). Este valor deve estar entre 0 e 1;

- o ```xmax```, que é a distância entre a base do gráfico e o fim da reta (`int` ou `float`). Este valor deve estar entre 0 e 1;

**Exemplo:**

```python
plt.figure(figsize=(8,6))
plt.scatter(x,y)
plt.axhline(y=1, xmin=0.1, xmax=0.5)
plt.show()
```

*Figura 1* - Gráfico de dispersão com reta adicionada utilizando o `plt.axhline()`.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-elementos-auxiliares/39/grafico-elementos-auxiliares-01.png" alt="gráfico de dispersão genérico desenhado com o matplotlib, como uma reta inserida  " >
{: .text-center}

<br>

**Exemplo:**

```python
plt.figure(figsize=(8,6))
plt.scatter(x,y)
plt.axhline(y=2.5, xmin=0.4, xmax=0.9)
plt.show()
```

*Figura 2* - Gráfico de dispersão com reta adicionada utilizando o `plt.axhline()`.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-elementos-auxiliares/39/grafico-elementos-auxiliares-02.png" alt="gráfico de dispersão genérico desenhado com o matplotlib, como uma reta inserida  " >
{: .text-center}

<br>

Maiores informações na [documentação](https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.axhline.html#matplotlib.pyplot.axhline).

<br>

<h2><a style="color:black" id="plt-hlines">Utilizando o plt.hlines()</a></h2>

Este elemento também recebe três parâmetros:

- o primeiro (```y```), que é a posição em *y* que a linha vertical será desenhada (`float` ou `int`), podendo também ser uma sequência para desenhar várias retas;

- o segundo (```xmin```), que o valor onde a reta começa (`int` ou `float`), podendo também ser uma sequência indicando o inicio de cada reta;

- o terceiro (```xmax```), que o valor onde a reta termina (`int` ou `float`), podendo também ser uma sequência indicando o fim de cada reta;

**Exemplo:**

```python
plt.figure(figsize=(8,6))
plt.scatter(x,y)
plt.hlines(y=2.5, xmin=0.4, xmax=0.9)
plt.show()
```

*Figura 3* - Gráfico de dispersão com reta adicionada utilizando o `plt.hlines()`.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-elementos-auxiliares/39/grafico-elementos-auxiliares-03.png" alt="gráfico de dispersão genérico desenhado com o matplotlib, como uma reta inserida  " >
{: .text-center}

<br>

**Exemplo:**

```python
plt.figure(figsize=(8,6))
plt.scatter(x,y)
plt.hlines(y=[2.5, 1.5, 3.5], xmin=0.4, xmax=0.9)
plt.show()
```

*Figura 4* - Gráfico de dispersão com reta adicionada utilizando o `plt.hlines()`.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-elementos-auxiliares/39/grafico-elementos-auxiliares-04.png" alt="gráfico de dispersão genérico desenhado com o matplotlib, como uma reta inserida  " >
{: .text-center}

<br>

**Exemplo:**

```python
plt.figure(figsize=(8,6))
plt.scatter(x,y)
plt.hlines(y=[2.5, 1.5, 3.5], xmin=0.4, xmax=[0.9, 4, 3.5])
plt.show()
```

*Figura 5* - Gráfico de dispersão com reta adicionada utilizando o `plt.hlines()`.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-elementos-auxiliares/39/grafico-elementos-auxiliares-05.png" alt="gráfico de dispersão genérico desenhado com o matplotlib, como uma reta inserida  " >
{: .text-center}

<br>

**Exemplo:**

```python
plt.figure(figsize=(8,6))
plt.scatter(x,y)
plt.hlines(y=[2.5, 1.5, 3.5], xmin=[0.4, 2, 1.5], xmax=[0.9, 4, 3.5])
plt.show()
```

*Figura 6* - Gráfico de dispersão com reta adicionada utilizando o `plt.hlines()`.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-elementos-auxiliares/39/grafico-elementos-auxiliares-06.png" alt="gráfico de dispersão genérico desenhado com o matplotlib, como uma reta inserida  " >
{: .text-center}

<br>

Maiores informações na [documentação](https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.hlines.html#matplotlib.pyplot.hlines).

<br>

<form id = "quiz" name = "quiz">

<p><strong>Qual seria um método adequado para inserir uma linha paralela ao eixo x?</strong></p>

<input type = "radio" id = "mc" name = "question1" value = "a"> <code>plt.hlines()</code>
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "b"> <code>plt.axvline()</code>
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "c"> <code>plt.axline()</code>
<p style="font-size: 50%"></p>
<p></p>
<input id = "button" type = "button" class="btn btn--info" value = "Enviar" onclick = "check();">
</form>

<div id = "after_submit">
<p style="font-size: 120%" id = "message"></p>
</div>

<br>

<p style="text-align: center">
  <a href="/Curso-matplotlib-38" class="btn btn--success">Anterior</a>
  <a href="/Curso-matplotlib-40" class="btn btn--success">Próximo</a>
</p>


<script>
function check(){
	var question1 = document.quiz.question1.value;
	var messages = [" 🎉 Correto! 🥳️ <br> Esta é uma das formas de inserir uma reta horizontal no gráfico!",
  " Incorreto! 😔 <br> O <code>plt.axvline()</code> é utilizado para inserir uma reta vertical, não uma reta horizontal. ",
  " 🎉 Correto! 🥳 <br> Apesar de não ser a melhor escolha para desenhar uma reta <i>paralela</i> ao eixo x, o <code>plt.axline()</code> também é uma alternativa!",
  "☕️"];
	var score;

	if (question1 == "a") {
		score = 0;
	}	else if (question1 == "b") {
		score = 1;
	} else if (question1 == "c") {
    score = 2;
  } else {
    score = 3;
  }

	document.getElementById("after_submit").style.visibility = "visible";
	document.getElementById("message").innerHTML = messages[score];

};
