---
title: "Curso matplotlib - Gráfico de linhas (edição das linhas)"
data: 2021-07-29
tags: []
header:
  image: "/images/chess.jpg"
  image_description: "Chess pieces"
excerpt: "matplotlib"
locale: "pt-br"
---

<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/generico/banner.png" alt="banner provisório " >
{: .text-center}

<br>


<h2><a style="color:black" id="cor-linha">Cor da linha</a></h2>

Para alterar a cor da linha desenhada utilizando o `plt.plot()`, basta passar uma `str` com o nome da cor desejada através do parâmetro `c` ou o parâmetro `color` . Por exemplo, para deixar a cor da linha vermelha, precisamos passar a `str` `'r'` para o parâmetro `color`:
{: .text-justify}

```python
plt.figure(figsize=(12,6))
plt.plot(horario,temperatura, color='r')
plt.show()
```

*Figura 1* - Linhas na cor vermelha.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-linhas/20/grafico-linhas-01.png" alt="gráfico de linhas desenhado com o matplotlib relacionando o horário e a temperatura ambiente com linha vermelha" >
{: .text-center}

<br>

As opções de cores são as mesmas que estudamos <a href="/Curso-matplotlib-08#cor-marcadores">anteriormente</a>.

<br>

<h2><a style="color:black" id="espessura-linha">Espessura da linha</a></h2>

Para alterar a espessura da linha desenhada utilizando o `plt.plot()` basta passar um número (`int` ou `float`) com a espessura desejada através do parâmetro `linewidth`:
{: .text-justify}

```python
plt.figure(figsize=(12,6))
plt.plot(horario,temperatura, color='r', linewidth=3.5)
plt.show()
```

*Figura 3* - Linhas na cor vermelha mais espessa.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-linhas/20/grafico-linhas-02.png" alt="gráfico de linhas desenhado com o matplotlib relacionando o horário e a temperatura ambiente com linha vermelha mais espessa" >
{: .text-center}

<br>



<h2><a style="color:black" id="estilo-linha">Estilo da linha</a></h2>

<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/generico/banner.png" alt="banner provisório " >
{: .text-center}


Para alterar o estilo da linha, utilizamos o parâmetro `linestyle`, passando uma `str` com o **nome do estilo**, ou uma `tuple` contendo **estilos parametrizados**.
{: .text-justify}

<h3><a style="color:black" id="estilo-padrao">Estilo padrão</a></h3>

Para utilizar apenas o nome do estilo, temos de passar uma `str` com uma das quatro opções abaixo:
{: .text-justify}

- `'solid'` (sólido);
- `'dotted'` (pontos);
- `'dashed'` (traços);
- `'dashdot'` (traço-ponto);

Visualmente:

*Figura 4* - Exemplo de estilos de linhas.
{: .text-center}
<img src="https://raw.githubusercontent.com/andersonmdcanteli/matplotlib-course/main/auxiliary-scripts/matplotli-all-linestyles/matplotlib_linestyles.png" alt="Exemplos visuais de como são renderizados os diferentes tipos de linhas">
{: .text-center}

<br>

Observe que também temos a opção de deixar a linha vazia, utilizando o `'None'`, ou `''` ou `' '`, e por isso as três primeiras linhas da imagem acima não aparecem. Você encontra o script desenvolvido para gerar o gráfico acima [clicando aqui](https://github.com/andersonmdcanteli/matplotlib-course/blob/main/auxiliary-scripts/matplotli-all-linestyles/matplotlib-all-linestyles.ipynb).
{: .text-justify}

Por exemplo, para deixar a linha com estilo traço-ponto, basta passar o `linestyle='dashdot'`:
{: .text-justify}

```python
plt.figure(figsize=(12,6))
plt.plot(horario, temperatura, c='red', linewidth=3.5, linestyle='dashdot')
plt.show()
```

*Figura 5* - Linhas na cor vermelha mais espessa - traço ponto.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-linhas/20/grafico-linhas-03.png" alt="gráfico de linhas desenhado com o matplotlib relacionando o horário e a temperatura ambiente com linha vermelha mais espessa com estilo traço ponto" >
{: .text-center}

<br>

<h3><a style="color:black" id="estilo-personalizado">Estilos personalizados</a></h3>

Para utilizar estilos personalizados (parametrizados), é preciso passar uma `tuple` com 2 elementos:

- o primeiro elemento é o número 0;

- o segundo elemento é uma outra `tuple`, que aceita vários parâmetros, mas sempre em dupla:


    + o primeiro parâmetro dessa `tuple` se refere ao tamanho do marcador que irá compor a linha. Por exemplo, o número 1 se refere a um ponto. O número 2 se refere a dois pontos, e assim por diante.


    + o segundo valor desse `tuple` se refere a distância entre cada ponto que compõe a linha.


**Exemplo**: A `tuple` `(0, (1, 10))` irá gerar uma "linha" com pontos (primeiro elemento) e separada em 10 unidades (segundo elemento)

```python
plt.figure(figsize=(12,6))
plt.plot(horario, temperatura, c='red', linewidth=3.5, linestyle=(0, (1,10)))
plt.show()
```

*Figura 6* - Linhas na cor vermelha mais espessa - estilo personalizado.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-linhas/20/grafico-linhas-04.png" alt="gráfico de linhas desenhado com o **matplotlib** relacionando o horário e a temperatura ambiente com linha vermelha mais espessa com estilo personalizado" >
{: .text-center}

<br>

**Exemplo**: A `tuple` `(0, (5, 10))` irá gerar uma "linha" com 5 pontos juntos, formando um traço (primeiro elemento) e separada em 10 unidades (segundo elemento)

```python
plt.figure(figsize=(12,6))
plt.plot(horario, temperatura, c='red', linewidth=3.5, linestyle=(0, (5,10)))
plt.show()
```

*Figura 7* - Linhas na cor vermelha mais espessa - estilo personalizado.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-linhas/20/grafico-linhas-05.png" alt="gráfico de linhas desenhado com o **matplotlib** relacionando o horário e a temperatura ambiente com linha vermelha mais espessa com estilo personalizado" >
{: .text-center}

<br>


**Exemplo**: A `tuple` `(0, (5, 10, 1, 4))` irá gerar uma "linha", onde o primeiro marcador da linha será um traço (5 unidades) espaçada em 10 unidades do próximo ponto. O segundo marcador será um ponto (uma unidade) espaçada em 4 unidades do próximo ponto. Este padrão irá se repetir até que todo o intervalo seja preenchido.
{: .text-justify}

```python
plt.figure(figsize=(12,6))
plt.plot(horario, temperatura, c='red', linewidth=3.5, linestyle=(0, (5,10, 1, 4)))
plt.show()
```

*Figura 8* - Linhas na cor vermelha mais espessa - estilo personalizado.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-linhas/20/grafico-linhas-06.png" alt="gráfico de linhas desenhado com o **matplotlib** relacionando o horário e a temperatura ambiente com linha vermelha mais espessa com estilo personalizado" >
{: .text-center}

<br>

Este tipo de formatação permite uma edição complexa do estilo da linha. Entretanto, dê preferências para os estilos mais comuns, pois os leitores estão acostumados com eles, e irão perceber as diferenças entre as linhas de forma mais rápida. Outros exemplos e detalhes você encontra na [documentação](https://matplotlib.org/stable/gallery/lines_bars_and_markers/linestyles.html)
{: .text-justify}


<br>

<form id = "quiz" name = "quiz">

<p><strong>Como alterar o estilo de linha para pontilhado?</strong></p>

<input type = "radio" id = "mc" name = "question1" value = "a"> Passando o parâmetro <code> linestyle = ":"</code>
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "b"> Passando o parâmetro <code> linewidth = ":"</code>
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "c"> Passando o parâmetro <code>linestyle = ".."</code>
<p style="font-size: 50%"></p>
<p></p>
<input id = "button" type = "button" class="btn btn--info" value = "Enviar" onclick = "check();">
</form>

<div id = "after_submit">
<p style="font-size: 120%" id = "message"></p>
</div>


<br>

<form id = "quiz" name = "quiz2">

<p><strong>Qual é a função do parâmetro <code>linewidth</code>?</strong></p>

<input type = "radio" id = "mc" name = "question1" value = "a"> Alterar a cor da linha
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "b"> Alterar a espessura da linha
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "c"> Alterar o estilo da linha
<p style="font-size: 50%"></p>
<p></p>
<input id = "button" type = "button" class="btn btn--info" value = "Enviar" onclick = "checkDois();">
</form>

<div id = "after_submit_dois">
<p style="font-size: 120%" id = "message_dois"></p>
</div>

<br>

<p style="text-align: center">
  <a href="/Curso-matplotlib-19" class="btn btn--success">Anterior</a>
  <a href="/Curso-matplotlib-21" class="btn btn--success">Próximo</a>
</p>





<script>
function check(){
	var question1 = document.quiz.question1.value;
	var messages = [" 🥳️  Correto 🎉! <br> Esta é a forma correta de alterar o estilo da linha para pontilhado!",
  "😔 Incorreto! ️ <br> O parâmetro <code>linewidth</code> é utilizado para alterar a espessura da linha, e não o seu estilo. Além disto, o <code>linewidth</code> aceita apenas números. ",
  "Incorreto! 😔  <br> O valor a ser passado para alterar o estilo da linha para pontilhado é o <code>':'</code> e não o <code>'..'</code>. Além disto, o parâmetro <code>linestyle</code> não tem a opção <code>'..'</code>. ",
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


<script>
function checkDois(){
	var question1 = document.quiz2.question1.value;
	var messages = ["😔 Incorreto! <br> O parâmetro utilizado para alterar a cor da linha é o parâmetro <code>color</code> ou o parâmetro <code>c</code>",
  "🥳️  Correto 🎉! <br> É através do parâmetro <code>linewidth</code> que se altera a espessura da linha!",
  "😔 Incorreto!  <br> O parâmetro utilizado para alterar a estilo da linha é o parâmetro <code>linestyle</code> ",
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

	document.getElementById("after_submit_dois").style.visibility = "visible";
	document.getElementById("message_dois").innerHTML = messages[score];

};

</script>
