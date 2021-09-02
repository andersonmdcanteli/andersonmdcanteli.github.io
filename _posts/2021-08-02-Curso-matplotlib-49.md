---
title: "Curso matplotlib - Gráfico de barras verticais (Cores das barras)"
data: 2021-08-02
tags: []
header:
  image: "/images/chess.jpg"
  image_description: "Chess pieces"
excerpt: "matplotlib"
locale: "pt-br"
---

<br>

<h2><a style="color:black" id="">Cor das barras</a></h2>

Para alterar a cor das barras passamos uma `str` através do parâmetro `color` com o nome da cor desejada. As cores disponíveis são as mesmas vistas <a href="/Curso-matplotlib-08#cor-marcadores">anteriormente</a>. Por exemplo:
{: .text-justify}


```python
espessuras = [0.5, .7, 0.8, 0.3, -0.2]
inicio = [0, 1, 2, 3, 4,]
plt.figure(figsize=(8,6))
plt.bar(frutas, precos, width=espessuras, align='edge', bottom=inicio, color='yellow')
plt.show()
```

*Figura 1* - Gráfico de barras verticais com barras na cor amarela.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-barras-verticais/49/grafico-barras-verticais-01.png" alt="gráfico de barras verticais desenhado com o matplotlib." >
{: .text-center}

<br>

Também é possível passar uma sequência de nomes de cores através de uma `list`, o que altera a cor das barras individualmente. Por exemplo:
{: .text-justify}

```python
espessuras = [0.5, .7, 0.8, 0.3, -0.2]
cores = ['r', 'g', 'k', 'w', 'y']
inicio = [0, 1, 2, 3, 4,]
plt.figure(figsize=(8,6))
plt.bar(frutas, precos, width=espessuras, align='edge', bottom=inicio, color=cores)
plt.show()
```

*Figura 2* - Gráfico de barras verticais com barras com cores variadas.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-barras-verticais/49/grafico-barras-verticais-02.png" alt="gráfico de barras verticais desenhado com o matplotlib." >
{: .text-center}

<br>

<h2><a style="color:black" id="cor-bordas">Cor das bordas das barras</a></h2>

Também podemos alterar a cor das bordas das barras, o que é feito através do parâmetro `edgecolor`, passando uma `str` ou uma sequência (`list`, `tuple`, `ndarray`, etc) contendo as `str` com o nome das cores desejadas. Por exemplo, para deixar todas as bordas na cor preta:
{: .text-justify}

```python
espessuras = [0.5, .7, 0.8, 0.3, -0.2]
cores = ['r', 'g', 'k', 'w', 'y']
inicio = [0, 1, 2, 3, 4,]
plt.figure(figsize=(8,6))
plt.bar(frutas, precos, width=espessuras, align='edge', bottom=inicio, color=cores, edgecolor='k')
plt.show()
```

*Figura 3* - Gráfico de barras verticais com barras com cores variadas com bordas na cor preta.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-barras-verticais/49/grafico-barras-verticais-03.png" alt="gráfico de barras verticais desenhado com o matplotlib." >
{: .text-center}

<br>


Também é possível alterar a cor das bordas de cada barra individualmente, passando uma `list` com os nomes das cores. Por exemplo:
{: .text-justify}

```python
espessuras = [0.5, .7, 0.8, 0.3, -0.2]
cores = ['r', 'g', 'k', 'w', 'y']
cores_borda = ['g', 'm', 'k', 'y', 'b']
inicio = [0, 1, 2, 3, 4,]
plt.figure(figsize=(8,6))
plt.bar(frutas, precos, width=espessuras, align='edge', bottom=inicio, color=cores, edgecolor=cores_borda)
plt.show()
```

*Figura 4* - Gráfico de barras verticais com barras com cores variadas e com bordas com cores variadas.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-barras-verticais/49/grafico-barras-verticais-04.png" alt="gráfico de barras verticais desenhado com o matplotlib." >
{: .text-center}

<br>


<h2><a style="color:black" id="espessura-bordas-barras">Espessura das bordas das barras</a></h2>

Para alterar a espessura das bordas basta passar um número (`int` ou `float`) ou uma sequência de números através do parâmetro `linewidth`. Por exemplo:
{: .text-justify}

```python
espessuras = [0.5, .7, 0.8, 0.3, -0.2]
cores = ['r', 'g', 'k', 'w', 'y']
cores_borda = ['g', 'm', 'k', 'y', 'b']
inicio = [0, 1, 2, 3, 4,]
plt.figure(figsize=(8,6))
plt.bar(frutas, precos, width=espessuras, align='edge', bottom=inicio, color=cores, edgecolor=cores_borda,
       linewidth=2)
plt.show()
```

*Figura 5* - Gráfico de barras verticais com barras com cores variadas e com bordas mais espessas e com cores variadas.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-barras-verticais/49/grafico-barras-verticais-05.png" alt="gráfico de barras verticais desenhado com o matplotlib." >
{: .text-center}

<br>

Também é possível alterar a espessura de cada barra individualmente, passando a espessura desejada para cada barra em uma `list` para o parâmetro `linewidth`. Por exemplo:
{: .text-justify}

```python
espessuras = [0.5, .7, 0.8, 0.3, -0.2]
espessura_borda = [1, 2, 3, 4, 5]
cores = ['r', 'g', 'k', 'w', 'y']
cores_borda = ['g', 'm', 'k', 'y', 'b']
inicio = [0, 1, 2, 3, 4,]
plt.figure(figsize=(8,6))
plt.bar(frutas, precos, width=espessuras, align='edge', bottom=inicio, color=cores, edgecolor=cores_borda,
       linewidth=espessura_borda)
plt.show()
```

*Figura 6* - Gráfico de barras verticais com barras com cores variadas e com bordas de espessuras variadas e com cores variadas.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-barras-verticais/49/grafico-barras-verticais-06.png" alt="gráfico de barras verticais desenhado com o matplotlib." >
{: .text-center}

<br>

<form id = "quiz" name = "quiz">

<p><strong>Qual a diferença entre o plt.scatter() e o plt.bar() em relação as cores disponíveis para serem utilizadas?</strong></p>

<input type = "radio" id = "mc" name = "question1" value = "a"> O <code>plt.bar()</code> aceita apenas cores no estilo RGB.
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "b"> <code>plt.bar()</code> não aceita cores no estilo RGB.
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "c"> Nenhuma diferença
<p style="font-size: 50%"></p>
<p></p>
<input id = "button" type = "button" class="btn btn--info" value = "Enviar" onclick = "check();">
</form>

<div id = "after_submit">
<p style="font-size: 120%" id = "message"></p>
</div>

<br>


<p style="text-align: center">
  <a href="/Curso-matplotlib-48" class="btn btn--success">Anterior</a>
  <a href="/Curso-matplotlib-50" class="btn btn--success">Próximo</a>
</p>


<script>
function check(){
	var question1 = document.quiz.question1.value;
	var messages = [" Incorreto! 😔 <br> O <code>plt.bar()</code> aceita várias outras opções de cores, não apenas cores RGB.",
  " 😔 Incorreto! 😔  <br> O <code>plt.bar()</code> também aceita cores no estilo RGB!",
  "🎉 Correto! 🥳️ <br> As cores disponíveis são exatamente as mesmas ",
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

</script>
