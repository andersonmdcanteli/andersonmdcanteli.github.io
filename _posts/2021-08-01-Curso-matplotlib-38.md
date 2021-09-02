---
title: "Curso matplotlib - Elementos auxiliares (reta vertical)"
data: 2021-08-01
tags: []
header:
  image: "/images/chess.jpg"
  image_description: "Chess pieces"
excerpt: "matplotlib"
locale: "pt-br"
---

<br>

Para desenhar uma reta vertical no gráfico, podemos utilizar tanto o `plt.axvline()` ou o `plt.vlines()`, que tem algumas pequenas diferenças entre si, mas é possível desenhar a mesma linha com estes dois elementos.
{: .text-justify}

<h2><a style="color:black" id="plt-axvline">Utilizando o plt.axvline()</a></h2>


Este elemento recebe três parâmetros:

- o ```x```, que é a posição em *x* que a linha vertical será desenhada (`float` ou `int`);

- o ```ymin```, que é a distância entre a base do gráfico e o início da reta (`int` ou `float`). Este valor deve estar entre 0 e 1;

- o ```ymax```, que é a distância entre a base do gráfico e o fim da reta (`int` ou `float`). Este valor deve estar entre 0 e 1;

**Exemplo:**

```python
plt.figure(figsize=(8,6))
plt.scatter(x,y)
plt.axvline(x=2.5, ymin=0, ymax=1)
plt.show()
```

*Figura 1* - Gráfico de dispersão com reta adicionada utilizando o `plt.axvline()`.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-elementos-auxiliares/38/grafico-elementos-auxiliares-01.png" alt="gráfico de dispersão genérico desenhado com o **matplotlib**, como uma reta inserida  " >
{: .text-center}

<br>

**Exemplo:**

```python
plt.figure(figsize=(8,6))
plt.scatter(x,y)
plt.axvline(x=2.5, ymin=0.2, ymax=1)
plt.show()
```

*Figura 2* - Gráfico de dispersão com reta adicionada utilizando o `plt.axvline()`.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-elementos-auxiliares/38/grafico-elementos-auxiliares-02.png" alt="gráfico de dispersão genérico desenhado com o **matplotlib**, como uma reta inserida  " >
{: .text-center}

<br>

**Exemplo:**

```python
plt.figure(figsize=(8,6))
plt.scatter(x,y)
plt.axvline(x=2.5, ymin=0.2, ymax=0.8)
plt.show()
```

*Figura 3* - Gráfico de dispersão com reta adicionada utilizando o `plt.axvline()`.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-elementos-auxiliares/38/grafico-elementos-auxiliares-03.png" alt="gráfico de dispersão genérico desenhado com o **matplotlib**, como uma reta inserida  " >
{: .text-center}

<br>


Mais detalhes sobre o `plt.axvline()` na [documentação](https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.axvline.html).


<h2><a style="color:black" id="plt-vlines">Utilizando o plt.vlines()</a></h2>

Este elemento também recebe três parâmetros:

- o primeiro (```x```), que é a posição em `x` que a linha vertical será desenhada (`float` ou `int`), podendo também ser uma sequência para desenhar várias retas;

- o segundo (```ymin```), que o valor onde a reta começa (`int` ou `float`), podendo também ser uma sequência indicando o inicio de cada reta;

- o terceiro (```ymax```), que o valor onde a reta termina (`int` ou `float`), podendo também ser uma sequência indicando o fim de cada reta;

**Exemplo:**

```python
plt.figure(figsize=(8,6))
plt.scatter(x,y)
plt.vlines(2.5, 0.2, 0.8)
plt.show()
```

*Figura 4* - Gráfico de dispersão com reta adicionada utilizando o `plt.vlines()`.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-elementos-auxiliares/38/grafico-elementos-auxiliares-04.png" alt="gráfico de dispersão genérico desenhado com o matplotlib, como uma reta inserida  " >
{: .text-center}

<br>

**Exemplo:**

```python
plt.figure(figsize=(8,6))
plt.scatter(x,y)
plt.vlines([1.5, 2.5, 3.5], 0.2, 0.8)
plt.show()
```

*Figura 5* - Gráfico de dispersão com reta adicionada utilizando o `plt.vlines()`.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-elementos-auxiliares/38/grafico-elementos-auxiliares-05.png" alt="gráfico de dispersão genérico desenhado com o matplotlib, como uma reta inserida  " >
{: .text-center}

<br>

**Exemplo**:

```python
plt.figure(figsize=(8,6))
plt.scatter(x,y)
plt.vlines([1.5, 2.5, 3.5], [0.2, 0.1, 0.4], 0.8)
plt.show()
```

*Figura 6* - Gráfico de dispersão com reta adicionada utilizando o `plt.vlines()`.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-elementos-auxiliares/38/grafico-elementos-auxiliares-06.png" alt="gráfico de dispersão genérico desenhado com o matplotlib, como uma reta inserida  " >
{: .text-center}

<br>

**Exemplo:**

```python
plt.figure(figsize=(8,6))
plt.scatter(x,y)
plt.vlines([1.5, 2.5, 3.5], [0.2, 0.1, 0.4], [0.8, 3.5, 2])
plt.show()
```

*Figura 7* - Gráfico de dispersão com reta adicionada utilizando o `plt.vlines()`.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-elementos-auxiliares/38/grafico-elementos-auxiliares-07.png" alt="gráfico de dispersão genérico desenhado com o matplotlib, como uma reta inserida  " >
{: .text-center}

<br>

Maiores detalhes na [documentação](https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.vlines.html#matplotlib.pyplot.vlines).


<br>

<form id = "quiz" name = "quiz">

<p><strong>Qual é a principal diferença entre o plt.axvline() e o plt.vlines()</strong></p>

<input type = "radio" id = "mc" name = "question1" value = "a"> O <code>plt.axvline()</code> utiliza a porcentagem do eixo <code>y</code> para a reta, enquanto que o <code>plt.vlines()</code> utiliza os valores do eixo <code>y</code>
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "b"> O <code>plt.vlines()</code> utiliza a porcentagem do eixo y para a reta, enquanto que o <code>plt.axvline()</code> utiliza os valores do eixo <code>y</code>
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "c"> Não existe diferença entre os dois elementos
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "d"> O <code>plt.axvline()</code> utiliza a porcentagem do eixo <code>x</code> para a reta, enquanto que o <code>plt.vlines()</code> utiliza os valores do eixo <code>x</code>
<p style="font-size: 50%"></p>
<p></p>
<input id = "button" type = "button" class="btn btn--info" value = "Enviar" onclick = "check();">
</form>

<div id = "after_submit">
<p style="font-size: 120%" id = "message"></p>
</div>

<br>

<p style="text-align: center">
  <a href="/Curso-matplotlib-37" class="btn btn--success">Anterior</a>
  <a href="/Curso-matplotlib-39" class="btn btn--success">Próximo</a>
</p>


<script>
function check(){
	var question1 = document.quiz.question1.value;
	var messages = [" 🎉 Correto! 🥳️  <br> Esta é a principal diferença!",
  " 😔 Incorreto! 😔  <br> É o <code>plt.axvline()</code> que utiliza a porcentagem do gráfico, não o <code>plt.vlines()</code>",
  " Incorreto! 😔  <br>  O <code>plt.axvline()</code> utiliza a porcentagem do eixo <code>y</code> para a reta, enquanto que o <code>plt.vlines()</code> utiliza os valores do eixo <code>y</code>. Portanto, existe diferença entre estes elementos",
  " 😔 Incorreto! <br> Tanto o <code>plt.vlines()</code> como o <code>plt.axvline()</code> utilizam valores do eixo <code>y</code>, não do eixo <code>x</code>",
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
