---
title: "Curso matplotlib - Gráfico de barras verticais (barras de erro)"
data: 2021-08-02
tags: []
header:
  image: "/images/chess.jpg"
  image_description: "Chess pieces"
excerpt: "matplotlib"
locale: "pt-br"
---

<br>

É possível adicionar barras de erro para cada barra, o que é feito passando o parâmetro `yerr` (para barras de erro no eixo `y`) ou `xerr` (para barras de erros no eixo `x`), de forma muito semelhante ao que vimos <a href="/Curso-matplotlib-27/">anteriormente</a>.
{: .text-justify}

Estes dois parâmetros podem ser alterados de duas formas. A primeira, e geralmente a mais utilizada, é passando uma constante (`int` ou `float`) ou uma sequência de números.
{: .text-justify}

Ao utilizar uma constante para todas as barras, um mesmo valor será utilizado para as barras de erro de todas as barras.
{: .text-justify}

```python
espessuras = [0.5, .7, 0.8, 0.3, -0.2]
espessura_borda = [1, 2, 3, 4, 5]
cores = ['r', 'g', 'k', 'w', 'y']
cores_borda = ['g', 'm', 'k', 'y', 'b']
inicio = [0, 1, 2, 3, 4,]
plt.figure(figsize=(8,6))
plt.bar(frutas, precos, width=espessuras, align='edge', bottom=inicio, color=cores, edgecolor=cores_borda,
       linewidth=espessura_borda, yerr=0.5)
plt.show()
```

*Figura 1* - Gráfico de barras verticais com barras de erro de mesmo tamanho.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-barras-verticais/50/grafico-barras-verticais-01.png" alt="gráfico de barras verticais desenhado com o matplotlib." >
{: .text-center}

<br>

Ao utilizar uma sequência de valores (como uma  `list` por exemplo), cada valor dessa sequencia será utilizada para as cada barra de erro (o tamanho dessa sequência deve ser igual ao tamanho da sequência passada para o parâmetro `x`).
{: .text-justify}


```python
std_y = [0.5, 0.6, 0.1, 0.2, 1]
espessuras = [0.5, .7, 0.8, 0.3, -0.2]
espessura_borda = [1, 2, 3, 4, 5]
cores = ['r', 'g', 'k', 'w', 'y']
cores_borda = ['g', 'm', 'k', 'y', 'b']
inicio = [0, 1, 2, 3, 4,]
plt.figure(figsize=(8,6))
plt.bar(frutas, precos, width=espessuras, align='edge', bottom=inicio, color=cores, edgecolor=cores_borda,
       linewidth=espessura_borda, yerr=std_y)
plt.show()
```

*Figura 2* - Gráfico de barras verticais com barras de erro de tamanho variado.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-barras-verticais/50/grafico-barras-verticais-02.png" alt="gráfico de barras verticais desenhado com o matplotlib." >
{: .text-center}

<br>

Observe que o tamanho da barra de erro adicionado foi exatamente o tamanho passado, tanto para cima, como para baixo do topo de cada barra. Esta é a forma mais comum de adicionar estas barras, pois na maioria das vezes elas representam o **desvio padrão** ou o **intervalo de confiança** de uma observação/medida.
{: .text-justify}

A outra forma que temos é especificar qual o tamanho para cima e para baixo no topo da barra. Isto é feito passando uma sequência de duas dimensões para o ```yerr```, que deve conter os valores para cada barra.
{: .text-justify}

Por exemplo, ao passar ```yerr = [[1, 1, 1, 1, 1], [2, 2, 2, 2, 2]]```, obtemos:

```python
espessuras = [0.5, .7, 0.8, 0.3, -0.2]
espessura_borda = [1, 2, 3, 4, 5]
cores = ['r', 'g', 'k', 'w', 'y']
cores_borda = ['g', 'm', 'k', 'y', 'b']
inicio = [0, 1, 2, 3, 4,]
plt.figure(figsize=(8,6))
plt.bar(frutas, precos, width=espessuras, align='edge', bottom=inicio, color=cores, edgecolor=cores_borda,
       linewidth=espessura_borda, yerr=[[1, 1, 1, 1, 1], [2, 2, 2, 2, 2]])
plt.show()
```

*Figura 3* - Gráfico de barras verticais com barras de erro com limites diferentes.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-barras-verticais/50/grafico-barras-verticais-03.png" alt="gráfico de barras verticais desenhado com o **matplotlib**." >
{: .text-center}

<br>

Repare que a barra acima do topo é duas vezes maior do que a barra abaixo do topo. Dessa forma, é possível personalizar as barras de erros de forma bem simples. Também é possível que estes valores variem entre cada barra. Por exemplo:
{: .text-justify}

```python
std_y = [[0.4, 0.4, 0.4, 2, 0.5],[0.1, 0.2, 0.3, 0.4, 0.1]]
espessuras = [0.5, .7, 0.8, 0.3, -0.2]
espessura_borda = [1, 2, 3, 4, 5]
cores = ['r', 'g', 'k', 'w', 'y']
cores_borda = ['g', 'm', 'k', 'y', 'b']
inicio = [0, 1, 2, 3, 4,]
plt.figure(figsize=(8,6))
plt.bar(frutas, precos, width=espessuras, align='edge', bottom=inicio, color=cores, edgecolor=cores_borda,
       linewidth=espessura_borda, yerr=std_y)
plt.show()
```

*Figura 4* - Gráfico de barras verticais com barras de erro com limites variados.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-barras-verticais/50/grafico-barras-verticais-04.png" alt="gráfico de barras verticais desenhado com o matplotlib." >
{: .text-center}

<br>


É possível utilizar a mesma lógica para barras de erro no eixo `x`, utilizando o parâmetro `xerr` ao invés de `yerrr`, com a diferença de que é necessário especificar todos os valores. Alguns exemplos:
{: .text-justify}

```python
std_x = [0.1, 0.2, 0.3, 0.4, 1]
espessuras = [0.5, .7, 0.8, 0.3, -0.2]
espessura_borda = [1, 2, 3, 4, 5]
cores = ['r', 'g', 'k', 'w', 'y']
cores_borda = ['g', 'm', 'k', 'y', 'b']
inicio = [0, 1, 2, 3, 4,]
plt.figure(figsize=(8,6))
plt.bar(frutas, precos, width=espessuras, align='edge', bottom=inicio, color=cores, edgecolor=cores_borda,
       linewidth=espessura_borda, xerr=std_x)
plt.show()
```

*Figura 5* - Gráfico de barras verticais com barras de erro no sentido do eixo `x`.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-barras-verticais/50/grafico-barras-verticais-05.png" alt="gráfico de barras verticais desenhado com o matplotlib." >
{: .text-center}

<br>

```python
std_x = [[0.1, 0.2, 0.3, 0.4, 1],[0.4, 0.4, 0.4, 0.4, .4]]
espessuras = [0.5, .7, 0.8, 0.3, -0.2]
espessura_borda = [1, 2, 3, 4, 5]
cores = ['r', 'g', 'k', 'w', 'y']
cores_borda = ['g', 'm', 'k', 'y', 'b']
inicio = [0, 1, 2, 3, 4,]
plt.figure(figsize=(8,6))
plt.bar(frutas, precos, width=espessuras, align='edge', bottom=inicio, color=cores, edgecolor=cores_borda,
       linewidth=espessura_borda, xerr=std_x)
plt.show()
```

*Figura 6* - Gráfico de barras verticais com barras de erro no sentido do eixo `x`.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-barras-verticais/50/grafico-barras-verticais-06.png" alt="gráfico de barras verticais desenhado com o matplotlib." >
{: .text-center}

<br>


<h2><a style="color:black" id="cor-barra-erro">Cor da barra de erro</a></h2>

Para alterar a cor da barra de erro, basta passar uma  `str` ou uma sequência de `str` com o(s) nome(s) das cores desejadas através do parâmetro `ecolor`.
{: .text-justify}

**Exemplo:**

```python
std_y = [0.5, 0.6, 0.1, 0.2, 1]
espessuras = [0.5, .7, 0.8, 0.3, -0.2]
espessura_borda = [1, 2, 3, 4, 5]
cores = ['r', 'g', 'k', 'w', 'y']
cores_borda = ['g', 'm', 'k', 'y', 'b']
inicio = [0, 1, 2, 3, 4,]
plt.figure(figsize=(8,6))
plt.bar(frutas, precos, width=espessuras, align='edge', bottom=inicio, color=cores, edgecolor=cores_borda,
       linewidth=espessura_borda, yerr=std_y, ecolor='m')
plt.show()
```

*Figura 7* - Gráfico de barras verticais com barras de erro na cor magenta.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-barras-verticais/50/grafico-barras-verticais-07.png" alt="gráfico de barras verticais desenhado com o matplotlib." >
{: .text-center}

<br>


```python
cor_barra_erro = ['g', 'm', 'b', 'k', 'y']
std_y = [0.5, 0.6, 0.1, 0.2, 1]
espessuras = [0.5, .7, 0.8, 0.3, -0.2]
espessura_borda = [1, 2, 3, 4, 5]
cores = ['r', 'g', 'k', 'w', 'y']
cores_borda = ['g', 'm', 'k', 'y', 'b']
inicio = [0, 1, 2, 3, 4,]
plt.figure(figsize=(8,6))
plt.bar(frutas, precos, width=espessuras, align='edge', bottom=inicio, color=cores, edgecolor=cores_borda,
       linewidth=espessura_borda, yerr=std_y, ecolor=cor_barra_erro)
plt.show()
```

*Figura 8* - Gráfico de barras verticais com barras de erro com cores variadas.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-barras-verticais/50/grafico-barras-verticais-08.png" alt="gráfico de barras verticais desenhado com o matplotlib." >
{: .text-center}

<br>


<h2><a style="color:black" id="cap">Cap</a></h2>

É possível adicionar uma barrinha nas extremidades da barra de erro, o que é muito comum de ser observado neste tipo apresentação do erro. Para adicionar esta barra, basta passar um número (`float`) através do parâmetro `capsize`.
{: .text-justify}

**Exemplo:**

```python
std_y = [0.5, 0.6, 0.1, 0.2, 1]
espessuras = [0.5, .7, 0.8, 0.3, -0.2]
espessura_borda = [1, 2, 3, 4, 5]
cores = ['r', 'g', 'k', 'w', 'y']
cores_borda = ['g', 'm', 'k', 'y', 'b']
inicio = [0, 1, 2, 3, 4,]
plt.figure(figsize=(8,6))
plt.bar(frutas, precos, width=espessuras, align='edge', bottom=inicio, color=cores, edgecolor=cores_borda,
       linewidth=espessura_borda, yerr=std_y, ecolor='m', capsize=5)
plt.show()
```
<br>

<form id = "quiz" name = "quiz">

<p><strong>Qual a diferença entre os parâmetros xerr e yerr?</strong></p>

<input type = "radio" id = "mc" name = "question1" value = "a"> Não tem diferença
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "b"> O parâmetro <code>xerr</code> insere barras de erro na vertical, enquanto que o parâmetro <code>yerr</code> insere barras de erro na horizontal.
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "c"> O parâmetro <code>xerr</code> insere barras de erro na vertical, enquanto que o parâmetro <code>yerr</code> insere barras de erro na horizontal.
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "d"> O parâmetro <code>xerr</code> desenha um gráfico de barras verticais, enquanto que o parâmetro <code>yerr</code> desenha um gráfico de barras na horizontal.
<p style="font-size: 50%"></p>
<p></p>
<input id = "button" type = "button" class="btn btn--info" value = "Enviar" onclick = "check();">
</form>

<div id = "after_submit">
<p style="font-size: 120%" id = "message"></p>
</div>



<br>

<p style="text-align: center">
  <a href="/Curso-matplotlib-49" class="btn btn--success">Anterior</a>
  <a href="/Curso-matplotlib-51" class="btn btn--success">Próximo</a>
</p>



<script>
function check(){
	var question1 = document.quiz.question1.value;
	var messages = [" Incorreto! 😔 <br> Os parâmetros <code>yerr</code> e <code>xerr</code> controlam o tamanho das barras de erro, na vertical e na horizontal, respectivamente.",
  " 😔 Incorreto! 😔  <br> O parâmetro <code>xerr</code> insere barras de erro na <i>horizontal</i>, enquanto que o parâmetro <code>yerr</code> insere barras de erro na <i>vertical</i>",
  "🎉 Correto! 🥳️ <br> Esta é a diferença entre estes dois parâmetros. ",
  " 😔 Incorreto! <br> Para desenhar um gráfico de barra na vertical, utilizamos o método <code>plt.bar()</code>, e para desenhar um gráfico de barras na horizontal, utilizamos o método <code>plt.barh()</code>. Os parâmetros <code>yerr</code> e <code>xerr</code> não tem relação com o posicionamento das barras, mas com o posicionamento das <i>barras de erro</i>.",
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
