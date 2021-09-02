---
title: "Gráfico de pizza (labels das fatias)"
data: 2021-08-08
tags: []
header:
  image: "/images/chess.jpg"
  image_description: "Chess pieces"
excerpt: "matplotlib"
locale: "pt-br"
---


<br>

<h2><a style="color:black" id="nomes-fatias">Nomes nas fatias</a></h2>

Para adicionar nomes (os labels) em cada fatia da pizza, basta passar uma sequência contendo `str` através do parâmetro `labels`.
{: .text-justify}

**Exemplo:**

```python
plt.figure(figsize=(8,8))
plt.pie(quantidade_vendas, labels = sabor)
plt.show()
```

*Figura 1* - Gráfico de pizza com labels nas fatias.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-pizza/70/grafico-pizza-01.png" alt="gráfico de pizza desenhado com matplotlib com labels nas fatias." >
{: .text-center}

<br>


<h2><a style="color:black" id="distancia-centro-label">Distância entre o centro da pizza e o seu label</a></h2>

Para controlar a distância entre o centro da pizza e o seu `label`, basta passar um número (`int` ou `float`) através do parâmetro `labeldistance` para o `plt.pie()`. O valor padrão é `1.1`.
{: .text-justify}

**Exemplo:**

```python
plt.figure(figsize=(8,8))
plt.pie(quantidade_vendas, labels = sabor, labeldistance = 1.2)
plt.show()
```

*Figura 2* - Gráfico de pizza com labels nas fatias.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-pizza/70/grafico-pizza-02.png" alt="gráfico de pizza desenhado com matplotlib com labels nas fatias." >
{: .text-center}

<br>

Caso utilize `labeldistance = 0`, todos os labels serão desenhados no centro da pizza:

```python
plt.figure(figsize=(8,8))
plt.pie(quantidade_vendas, labels = sabor, labeldistance = 0)
plt.show()
```

*Figura 3* - Gráfico de pizza com labels nas fatias.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-pizza/70/grafico-pizza-03.png" alt="gráfico de pizza desenhado com matplotlib com labels nas fatias." >
{: .text-center}

<br>

Por padrão, o raio da pizza é igual a `1.0`. Então, caso deseje que os labels sejam desenhados no limite externo da borda, basta passar `labeldistance = 1`:
{: .text-justify}

```python
plt.figure(figsize=(8,8))
plt.pie(quantidade_vendas, labels = sabor, labeldistance = 1)
plt.show()
```

*Figura 4* - Gráfico de pizza com labels nas fatias.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-pizza/70/grafico-pizza-04.png" alt="gráfico de pizza desenhado com matplotlib com labels nas fatias." >
{: .text-center}

<br>


<h2><a style="color:black" id="labels-rotacao">Rotacionando os labels</a></h2>


Para rotacionar os nomes das fatias podemos alterar o parâmetro `rotatelabels` de `False` (padrão) para `True`. A rotação fará com que o texto acompanhe o ângulo da fatia, e deixe de estar na horizontal.
{: .text-justify}


```python
plt.figure(figsize=(8,8))
plt.pie(quantidade_vendas, labels = sabor, rotatelabels=True)
plt.show()
```

*Figura 5* - Gráfico de pizza com labels nas fatias.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-pizza/70/grafico-pizza-05.png" alt="gráfico de pizza desenhado com matplotlib com labels nas fatias." >
{: .text-center}

<br>

<form id = "quiz" name = "quiz">

<p><strong>Qual é a função do parâmetro labeldistance?</strong></p>

<input type = "radio" id = "mc" name = "question1" value = "a"> Controlar a distância entre o centro da pizza e o limite mais próximo dos labels
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "b"> Controlar o raio da pizza
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "c"> Controlar a distância entre o centro da pizza e o limite mais distânte dos labels
<p style="font-size: 50%"></p>
<p></p>
<input id = "button" type = "button" class="btn btn--info" value = "Enviar" onclick = "check();">
</form>

<div id = "after_submit">
<p style="font-size: 120%" id = "message"></p>
</div>


<br>


<p style="text-align: center">
  <a href="/Curso-matplotlib-69" class="btn btn--success">Anterior</a>
  <a href="/Curso-matplotlib-71" class="btn btn--success">Próximo</a>
</p>


<script>
function check(){
	var question1 = document.quiz.question1.value;
	var messages = [" 🎉 Correto! 🥳️ <br> Esta é a função do parâmetro <code>labeldistance</code>!",
  " 😔 Incorreto! <br> Para controlar o raio pizza é utilizado o parâmetro <code>radius</code>.",
  " Incorreto 😔 ! <br> O parâmetro <code>labeldistance</code> controla a distância entre o centro da pizza e o limite mais próximo dos labels, não o mais distante.",
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
