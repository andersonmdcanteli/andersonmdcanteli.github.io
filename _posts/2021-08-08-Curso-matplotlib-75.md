---
title: "Gráfico de pizza (propriedades das fatias)"
data: 2021-08-08
tags: []
header:
  image: "/images/chess.jpg"
  image_description: "Chess pieces"
excerpt: "matplotlib"
locale: "pt-br"
---


<br>

É possível alterar propriedades da fatias, como a cor das bordas, cor da linha das bordas, estilo das linhas, entre outros. Para fazer estas alterações, passamos um `dict` com o nome da propriedade que será alterada como `key`, e o novo valor como `value` da `key`, para o `plt.pie()` através do parâmetro `wedgeprops`.
{: .text-justify}

<h2><a style="color:black" id="cor-linha-fatias">Cor das linhas</a></h2>

Para alterar a cor da linha das fatias, basta passar a cor, utilizando seu nome (`str`), como valor através da chave `edgecolor`.
{: .text-justify}

**Exemplo:**

```python
explode = (0, 0.1, 0, 0, 0)
plt.figure(figsize=(8,6))
plt.pie(quantidade_vendas, labels = sabor, autopct='%.1f%%', startangle=90, explode=explode,
       wedgeprops = {'edgecolor': 'k'})
plt.show()
```

*Figura 1* - Gráfico de pizza com as linhas na cor preta.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-pizza/75/grafico-pizza-01.png" alt="gráfico de pizza desenhado com matplotlib com as linhas na cor preta" >
{: .text-center}

<br>

<h2><a style="color:black" id="espessura-borda-fatias">Espessura das bordas</a></h2>

De forma similar, para alterar a espessura das bordas basta passar a nova espessura (número `int` ou `float`) como `value` para a `key` `linewidth`.
{: .text-justify}

**Exemplo:**

```python
explode = (0, 0.1, 0, 0, 0)
plt.figure(figsize=(8,6))
plt.pie(quantidade_vendas, labels = sabor, autopct='%.1f%%', startangle=90, explode=explode,
       wedgeprops = {'edgecolor': 'k', 'linewidth': 3})
plt.show()
```

*Figura 2* - Gráfico de pizza com as linhas na cor preta e mais espessas.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-pizza/75/grafico-pizza-02.png" alt="gráfico de pizza desenhado com matplotlib com as linhas na cor preta e mais espessas" >
{: .text-center}

<br>

<h2><a style="color:black" id="estilo-linha-fatias">Estilo da linha</a></h2>

Para alterar o estilo das linhas das fatias, basta passar o novo estilo como `value` para a `key` `linestyle`. Os estilos de linha disponíveis são os mesmos vistos <a href="/Curso-matplotlib-20/#estilo-linha">anteriormente</a>.
{: .text-justify}

**Exemplo:**

```python
explode = (0, 0.1, 0, 0, 0)
plt.figure(figsize=(8,6))
plt.pie(quantidade_vendas, labels = sabor, autopct='%.1f%%', startangle=90, explode=explode,
       wedgeprops = {'edgecolor': 'k', 'linewidth': 3, 'linestyle': '--'})
plt.show()
```

*Figura 3* - Gráfico de pizza com as linhas com estilo tracejado, na cor preta e mais espessas.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-pizza/75/grafico-pizza-03.png" alt="gráfico de pizza desenhado com matplotlib com as linhas com estilo tracejado, na cor preta e mais espessas" >
{: .text-center}

<br>

<h2><a style="color:black" id="suavizada-fatias">Suavizada</a></h2>

Dentre as demais opções, temos a opção de deixar a pizza com um estilo mais suave, o que é feito passando como `value` o `bool` `True` para a `key` `antialiased`.  Este parâmetro é mais perceptível em gráficos de pizzas mais complexas.
{: .text-justify}

**Exemplo:**

```python
explode = (0, 0.1, 0, 0, 0)
plt.figure(figsize=(8,6))
plt.pie(quantidade_vendas, labels = sabor, autopct='%.1f%%', startangle=90, explode=explode,
       wedgeprops = {'edgecolor': 'k', 'linewidth': 3, 'linestyle': '--', 'antialiased': True})
plt.show()
```

*Figura 4* - Gráfico de pizza com estilo suavizado.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-pizza/75/grafico-pizza-04.png" alt="gráfico de pizza desenhado com matplotlib com estilo suavizado" >
{: .text-center}

<br>

<h2><a style="color:black" id="grafico-rosquinha">Espessura da pizza (gráfico de rosquinha)</a></h2>

Uma forma *muito interessante* de apresentar o gráfico de pizza, é transformando ele em um gráfico de ***rosquinha*** (*donut*). Estes gráficos são caracterizados com um buraco no centro, dando uma outra percepção ao gráfico de pizza, e lembram uma rosquinha.
{: .text-justify}


Para transformar o gráfico de pizza em um gráfico de rosquinha, basta passar um número (`int` ou `float`) como `value` para a `key` `width`. Este número corresponde ao raio do buraco da rosquinha, e deve ser *menor* do que o raio da pizza (`radius`).
{: .text-justify}


**Exemplo:**

```python
plt.figure(figsize=(8,6))
plt.pie(quantidade_vendas, labels = sabor, autopct='%.1f%%', startangle=90, pctdistance=0.75,
       wedgeprops = {'edgecolor': 'k', 'linewidth': 3, 'antialiased': True, 'width': 0.5})
plt.show()
```

*Figura 5* - Gráfico de rosquinha.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-pizza/75/grafico-pizza-05.png" alt="gráfico de rosquinha desenhado com matplotlib " >
{: .text-center}

<br>

<form id = "quiz" name = "quiz">

<p><strong>Como alterar as propriedades das fatias do gráfico de pizza?</strong></p>

<input type = "radio" id = "mc" name = "question1" value = "a"> Passando os parâmetros edgecolor, linestyle, linewidth, etc, diretamente para o plt.pie()
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "b"> Passando os parâmetros edgecolor, linestyle, linewidth, etc, como value, e o respectivo valor como key para o parâmetro wedgeprops
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "c"> Passando os parâmetros edgecolor, linestyle, linewidth, etc, como key, e o respectivo valor como value para o parâmetro wedgeprops
<p style="font-size: 50%"></p>
<p></p>
<input id = "button" type = "button" class="btn btn--info" value = "Enviar" onclick = "check();">
</form>

<div id = "after_submit">
<p style="font-size: 120%" id = "message"></p>
</div>


<br>

<p style="text-align: center">
  <a href="/Curso-matplotlib-74" class="btn btn--success">Anterior</a>
  <a href="/Curso-matplotlib-76" class="btn btn--success">Próximo</a>
</p>


<script>
function check(){
	var question1 = document.quiz.question1.value;
	var messages = [" Incorreto! 😔 <br> É necessário passar estes parâmetros <i>através</i> do parâmetro <code>wedgeprops</code>.",
  " 😔 Incorreto! <br> Estes os parâmetros <code>linestyle</code>, <code>linewidth</code>, etc, devem ser utilizados como <code>key</code>, não como <code>value</code>",
  " 🎉 Correto! 🥳️ ",
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
