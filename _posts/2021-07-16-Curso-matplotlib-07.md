---
title: "Curso matplotlib - Gráfico de dispersão (Tamanho do gráfico)"
data: 2021-07-16
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

O tamanho do gráfico pode ser alterado utilizando o método `plt.figure()`. Este método tem com função criar uma nova figura, e através desse método é possível alterar diversos parâmetros, como a cor de fundo do gráfico, cor das bordas, e o tamanho do gráfico.
{: .text-justify}

Para alterar o tamanho do gráfico, precisamos passar uma `tuple` com dois elementos para o parâmetro `figsize()`, da seguinte forma:
{: .text-justify}

```python
plt.figure(figsize=(width, height))
```
onde:

- O valor de `width` corresponde ao tamanho (em polegadas) da largura do eixo `x`.

- Já o valor de `height`, corresponde ao tamanho (em polegadas) da altura do eixo `y`.

Por padrão, o gráfico é criado com `6.4` polegadas de largura e `4.8` polegadas de altura.

```python
plt.figure(x,y, figsize=(6.4, 4.8))
```

[Documentação](https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.figure.html).

Para desenhar um gráfico **quadrado**, basta utilizar valores de `width` e `height` iguais:

```python
plt.figure(figsize=(8,8))
plt.scatter(x=x, y=y)
plt.show()
```

*Figura 1* - Gráfico de dispersão quadrado desenhado com o **matplotlib**.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/07/grafico-dispersao-01.png" alt="gráfico de dispersão desenhado utilizando o **matplotlib** " >
{: .text-center}


Para desenhar um gráfico mais largo, basta utilizar um valor de `width` **maior** do que o valor de `height`:


```python
plt.figure(figsize=(12,6))
plt.scatter(x=x, y=y)
plt.show()
```

*Figura 2* - Gráfico de dispersão mais largo desenhado com o **matplotlib**.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/07/grafico-dispersao-02.png" alt="gráfico de dispersão desenhado utilizando o **matplotlib** " >
{: .text-center}

E para desenhar um gráfico mais alto, basta utilizar um valor de `width` **menor** do que o valor de `height`:

```python
plt.figure(figsize=(6,12))
plt.scatter(x=x, y=y)
plt.show()
```

*Figura 3* - Gráfico de dispersão mais alto desenhado com o **matplotlib**.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/07/grafico-dispersao-03.png" alt="gráfico de dispersão desenhado utilizando o **matplotlib** " >
{: .text-center}


Observe a ordem em que os elementos foram adicionados:


```python
plt.figure(figsize=(6,12))
plt.scatter(x=x, y=y)
plt.show()
```

Inicialmente, criamos a figura, depois desenhamos os pontos, e por fim apresentamos o gráfico. A ideia é simular o desenho de um quadro, onde incialmente conseguimos a tela de desenho (ou o *canvas*), depois *pintamos* o quadro (adicionamos os elementos), e por fim *apresentamos o quadro* para outras pessoas (exportamos o gráfico).
{: .text-justify}

Esta estrutura ***sempre irá se repetir***, onde vamos adicionando mais elementos entre ***criar o canvas*** e ***apresentar a figura***.
{: .text-justify}



<form id = "quiz" name = "quiz">

<p><strong>Qual ordem correta para gerar um gráfico de dispersão no matplotlib?</strong></p>

<input type = "radio" id = "mc" name = "question1" value = "a"> criar canvas, adicionar elementos, apresentar o gráfico
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "b"> adicionar elementos, criar canvas, apresentar o gráfico
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "c"> adicionar elementos,  apresentar o gráfico, criar canvas
<p style="font-size: 50%"></p>
<p></p>
<input id = "button" type = "button" class="btn btn--info" value = "Enviar" onclick = "check();">
</form>

<div id = "after_submit">
<p style="font-size: 120%" id = "message"></p>
</div>

<br>

<form id = "quiz2" name = "quiz2">

<p><strong>Qual opção <i>NÃO</i> irá importar a parte gráfica da biblioteca matplotlib?</strong></p>

<input type = "radio" id = "mc" name = "question2" value = "a"> <code>from matplotlib import pyplot as plt</code>
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question2" value = "b"> <code>import matplotlib.pyplot as cafezinho</code>
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question2" value = "c"> <code>import matplotlib as mpl
</code>
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question2" value = "d"> <code>import pyplot.matplotlib as plt
</code>
<p style="font-size: 50%"></p>
<p></p>
<input id = "button2" type = "button" class="btn btn--info" value = "Enviar" onclick = "checkDois();">
</form>

<div id = "after_submit2">
<p style="font-size: 120%" id = "message2"></p>
</div>




<br>

<p style="text-align: center">
  <a href="/Curso-matplotlib-06" class="btn btn--success">Anterior</a>
  <a href="/Curso-matplotlib-08" class="btn btn--success">Próximo</a>
</p>



<script>
function check(){
	var question1 = document.quiz.question1.value;
	var messages = ["🥳️ Correto! 🎉 <br> Está é a ordem ideal para desenhar um gráfico utilizando o matplotlib",
  "Incorreto! 😔 <br> Apesar desta ordem gerar um gráfico, os parâmetros passados em <code>plt.figure()</code> não serão utilizados. ",
  "😔 Incorreto!  <br> Apesar desta ordem gerar um gráfico, os parâmetros passados em <code>plt.figure()</code>  não serão utilizados.",
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
	var question1 = document.quiz2.question2.value;
	var messages = ["Incorreto! 😔 <br> Apesar de não ser a forma mais usual, esta também é uma forma de importar a parte gráfica da biblioteca matplotlib!",
  "Incorreto! 😔 <br> Apesar do alias <code>cafezinho</code> não ter relação nenhuma com a geração de gráficos, esta forma irá importar a parte gráfica do matplotlib de forma correta! ",
  "😔 Incorreto!  <br> Embora seja uma forma pouco eficiente (pois será necessário escrever <code>mpl.pyplot</code> muitas vezes), esta forma irá importar a parte gráfica do matplotlib de forma correta!",
  "🎉 Correto! 🥳️ <br> A biblioteca <code>pyplot</code> não existe!",
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

	document.getElementById("after_submit2").style.visibility = "visible";
	document.getElementById("message2").innerHTML = messages[score];

};

</script>
