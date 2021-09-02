---
title: "Gráfico de pizza (estilos)"
data: 2021-08-08
tags: []
header:
  image: "/images/chess.jpg"
  image_description: "Chess pieces"
excerpt: "matplotlib"
locale: "pt-br"
---


<br>

<h2><a style="color:black" id="sombra">Shadow</a></h2>

Através do parâmetro `shadow` podemos adicionar uma sombra as fatias, o que fornece uma percepção de profundidade à fatia da pizza. O parâmetro `shadow` aceita apenas valores `bool`, sendo que `False` (padrão) não insere a sombra, e `True` insere a sombra.
{: .text-justify}

**Por exmplo:**

```python
explode = (0, 0.1, 0.5, 0.3, 0.2)
plt.figure(figsize=(8,6))
plt.pie(quantidade_vendas, labels = sabor, autopct='%.1f%%', startangle=90, explode=explode, shadow=True)
plt.show()
```

*Figura 1* - Gráfico de pizza com sombra.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-pizza/74/grafico-pizza-01.png" alt="gráfico de pizza desenhado com matplotlib com sombra" >
{: .text-center}

<br>

<h2><a style="color:black" id="cor-fatias">Cor das fatias</a></h2>

Para alterar a cor das fatias, é necessário passar uma sequência (`list`, `tuple`, etc) com o nome da cor que será utilizada em cada fatia, para o `plt.bar()` através do parâmetro `colors`. Observe que, ao contrário dos outros elementos, aqui utilizamos `colors` com `s` e não `color` sem o `s`. Entretanto, as cores disponíveis são as mesmas vistas <a href="/Curso-matplotlib-08/#cor-marcadores">anteriormente</a>.
{: .text-justify}

**Exemplo:**

```python
explode = (0, 0.1, 0, 0, 0)
cores = ['g', 'gray', 'm', 'y', 'b']
plt.figure(figsize=(8,6))
plt.pie(quantidade_vendas, labels = sabor, autopct='%.1f%%', startangle=90, explode=explode, colors=cores)
plt.show()
```

*Figura 2* - Gráfico de pizza com cores alteradas.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-pizza/74/grafico-pizza-02.png" alt="gráfico de pizza desenhado com matplotlib com as cores alteradas" >
{: .text-center}

<br>

Caso o número de cores for menor do que o número de fatias, as cores serão repetidas (na sequência passada). Por exemplo:

```python
explode = (0, 0.1, 0, 0, 0)
cores = ['g', 'gray']
plt.figure(figsize=(8,6))
plt.pie(quantidade_vendas, labels = sabor, autopct='%.1f%%', startangle=90, explode=explode, colors=cores)
plt.show()
```

*Figura 3* - Gráfico de pizza com cores repetidas.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-pizza/74/grafico-pizza-03.png" alt="gráfico de pizza desenhado com matplotlib com as cores repetidas" >
{: .text-center}

<br>


<form id = "quiz" name = "quiz">

<p><strong>Qual é o parâmetro utilizado para alterar a cor das fatias da pizza?</strong></p>

<input type = "radio" id = "mc" name = "question1" value = "a"> colors
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "b"> color
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "c"> cor
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "d"> Colors
<p style="font-size: 50%"></p>
<p></p>
<input id = "button" type = "button" class="btn btn--info" value = "Enviar" onclick = "check();">
</form>

<div id = "after_submit">
<p style="font-size: 120%" id = "message"></p>
</div>


<br>

<p style="text-align: center">
  <a href="/Curso-matplotlib-73" class="btn btn--success">Anterior</a>
  <a href="/Curso-matplotlib-75" class="btn btn--success">Próximo</a>
</p>


<script>
function check(){
	var question1 = document.quiz.question1.value;
	var messages = [" 🎉 Correto! 🥳️ <br> ",
  " 😔 Incorreto! <br> O parâmetro correto é <code>colors</code>, com o <code>s</code> no final da palavra.",
  " 😔 Incorreto️ 😔! <br> O <code>plt.pie()</code> não tem o parâmetro <code>cor</code>.",
  " 😔 Incorreto! <br> O <code>plt.pie()</code> não tem o parâmetro <code>Colors</code>. O parâmetro correto é o parâmetro <code>colors</code>, iniciando com a letra <code>c</code> em minúsculo.",
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
