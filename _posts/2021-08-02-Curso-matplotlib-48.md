---
title: "Curso matplotlib - Gráfico de barras verticais (Edição das barras)"
data: 2021-08-02
tags: []
header:
  image: "/images/chess.jpg"
  image_description: "Chess pieces"
excerpt: "matplotlib"
locale: "pt-br"
---

<br>

<h2><a style="color:black" id="espessura-barras">Espessura da barra</a></h2>


Para alterar a espessura das barras, é necessário passar o parâmetro `width`. Este parâmetro pode receber um único valor (`float` ou `int`) ou uma `list` contendo os valores especificados de espessura para cada coluna (o valor padrão é `0.8`).
{: .text-justify}

Por exemplo, para alterar a espessura de cada barra para `0.5`:
{: .text-justify}

```python
plt.figure(figsize=(8,6))
plt.bar(frutas, precos, width = 0.5)
plt.show()
```

*Figura 1* - Gráfico de barras verticais com barras mais finas (que o padrão).
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-barras-verticais/48/grafico-barras-verticais-01.png" alt="gráfico de barras verticais desenhado com o **matplotlib**." >
{: .text-center}

<br>

Para alterar a espessura das barras individualmente, basta passar uma `list` da seguinte forma:
{: .text-justify}

```python
espessuras = [0.5, 1.0, 0.8, 0.3, 0.2]
plt.figure(figsize=(8,6))
plt.bar(frutas, precos, width=espessuras)
plt.show()
```

*Figura 2* - Gráfico de barras verticais com barras de espessura variada.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-barras-verticais/48/grafico-barras-verticais-02.png" alt="gráfico de barras verticais desenhado com o matplotlib." >
{: .text-center}

<br>

<h2><a style="color:black" id="alinhamento-barras">Alinhamento das barras</a></h2>

Podemos alterar o alinhamento das barras, ou seja, a posição em relação ao *tick* de cada barra, o que é feito através do parâmetro `align`. Este parâmetro recebe uma `str` que pode ser:
{: .text-justify}

- `'center'`: alinha de acordo com as posições de `x` (padrão);

ou

- `'edge'`: alinha aos limites esquerdos em relação as posições `x`;

Por exemplo:

```python
espessuras = [0.5, .7, 0.8, 0.3, 0.2]
plt.figure(figsize=(8,6))
plt.bar(frutas, precos, width=espessuras, align='edge')
plt.show()
```

*Figura 3* - Gráfico de barras verticais com alinhamento à direita.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-barras-verticais/48/grafico-barras-verticais-03.png" alt="gráfico de barras verticais desenhado com o matplotlib." >
{: .text-center}

<br>


Para alinhar à esquerda, basta passar um valor negativo para o parâmetro `width`. Por exemplo:
{: .text-justify}

```python
espessuras = [0.5, .7, 0.8, 0.3, -0.2]
plt.figure(figsize=(8,6))
plt.bar(frutas, precos, width=espessuras, align='edge')
plt.show()
```

*Figura 4* - Gráfico de barras verticais com o último elemento alinhado à esquerda.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-barras-verticais/48/grafico-barras-verticais-04.png" alt="gráfico de barras verticais desenhado com o matplotlib." >
{: .text-center}

<br>

Observe que a última barra (`'Mamão Formosa'`) ficou alinhada à esquerda do *tick*, enquanto que as demais colunas seguem à direita do *tick*.
{: .text-justify}


<h2><a style="color:black" id="posicao-eixo-y">Posição inicial da barra em relação ao eixo y</a></h2>

Podemos alterar a posição onde a barra começa no eixo `y` através do parâmetro `bottom`, que recebe um número (`int` ou `float`) ou uma sequência (`list`, `tuple`, `ndarray`, etc).
{: .text-justify}

Por exemplo, para alterar todas as barras igualmente, iniciando em `2`:
{: .text-justify}

```python
espessuras = [0.5, .7, 0.8, 0.3, -0.2]
plt.figure(figsize=(8,6))
plt.bar(frutas, precos, width=espessuras, align='edge', bottom=2)
plt.show()
```

*Figura 5* - Gráfico de barras verticais com o as barras iniciando em `y = 2`.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-barras-verticais/48/grafico-barras-verticais-05.png" alt="gráfico de barras verticais desenhado com o matplotlib." >
{: .text-center}

<br>

Para alterar a posição de início de cada barra individualmente precisamos passar uma `list` contendo os valores desejados. Por exemplo:

```python
espessuras = [0.5, .7, 0.8, 0.3, -0.2]
inicio = [0, 1, 2, 3, 4,]
plt.figure(figsize=(8,6))
plt.bar(frutas, precos, width=espessuras, align='edge', bottom=inicio)
plt.show()
```

*Figura 6* - Gráfico de barras verticais com o as barras iniciando em posições variadas de `y`.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-barras-verticais/48/grafico-barras-verticais-06.png" alt="gráfico de barras verticais desenhado com o matplotlib." >
{: .text-center}

<br>


<form id = "quiz" name = "quiz">

<p><strong>Como desenhar a barra à esquerda do <i>tick</i> em plt.bar()?</strong></p>

<input type = "radio" id = "mc" name = "question1" value = "a"> Passando o parâmetro <code>left=True</code>.
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "b"> Passando o parâmetro <code>align='edge'</code>.
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "c"> Passando o parâmetro <code>align='left'</code> e passando um valor de espessura negativa para o parâmetro <code>width</code>.
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "d"> Passando o parâmetro <code>align='edge'</code> e passando um valor de espessura negativa para o parâmetro <code>width</code>.
<p style="font-size: 50%"></p>
<p></p>
<input id = "button" type = "button" class="btn btn--info" value = "Enviar" onclick = "check();">
</form>

<div id = "after_submit">
<p style="font-size: 120%" id = "message"></p>
</div>

<br>



<p style="text-align: center">
  <a href="/Curso-matplotlib-47" class="btn btn--success">Anterior</a>
  <a href="/Curso-matplotlib-49" class="btn btn--success">Próximo</a>
</p>




<script>
function check(){
	var question1 = document.quiz.question1.value;
	var messages = [" Incorreto! 😔 <br> O método <code>plt.bar()</code> não tem um parâmetro <code>left</code>!",
  " 😔 Incorreto! 😔  <br> Ao passar o parâmetro <code>align='edge'</code>, as barras serão alinhadas à direita, não à esquerda.",
  "  😔 Incorreto!<br> O parâmetro <code>align</code> tem apenas as opções <code>'center'</code> e <code>'edge'</code>",
  "🎉 Correto! 🥳️ <br> Desta forma, a barra será desenhada à esquerda do <i>tick</i>!",
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
