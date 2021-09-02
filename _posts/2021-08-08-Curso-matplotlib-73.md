---
title: "Gráfico de pizza (tamanho e forma da pizza)"
data: 2021-08-08
tags: []
header:
  image: "/images/chess.jpg"
  image_description: "Chess pieces"
excerpt: "matplotlib"
locale: "pt-br"
---


<br>

<h2><a style="color:black" id="raio-pizza">Raio da pizza</a></h2>

Para alterar o tamanho do raio da pizza (o valor padrão é `1`), basta passar um número (`int` ou `float`) para o `plt.pie()` através do parâmetro `radius`.
{: .text-justify}

Por exemplo, para desenhar uma pizza pequena, basta passar um valor menor do que `1` para o parâmetro `radius`:
{: .text-justify}

```python
plt.figure(figsize=(8,8))
plt.pie(quantidade_vendas, labels = sabor, autopct='%.1f%%', startangle=90, radius=0.5)
plt.show()
```

*Figura 1* - Gráfico de pizza com raio reduzido.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-pizza/73/grafico-pizza-01.png" alt="gráfico de pizza desenhado com matplotlib com raio reduzido" >
{: .text-center}

<br>

Para desenhar uma pizza grande, basta passar um valor maior do que `1` para o parâmetro `radius`:
{: .text-justify}

```python
plt.figure(figsize=(8,8))
plt.pie(quantidade_vendas, labels = sabor, autopct='%.1f%%', startangle=90, radius=1.5)
plt.show()
```

*Figura 2* - Gráfico de pizza com raio aumentado.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-pizza/73/grafico-pizza-02.png" alt="gráfico de pizza desenhado com matplotlib com raio aumentado" >
{: .text-center}

<br>

<h2><a style="color:black" id="explode">Explode</a></h2>

Uma opção realmente *muito interessante* de estilização dos gráficos de pizza, é utilizar o parâmetro `explode`. Este parâmetro faz com que uma ou mais fatias fiquem para "fora" da pizza, de forma a dar um destaque maior para a fatia. Então, quando você quiser destacar uma informação, pode utilizar este parâmetro para "puxar" ele para fora do centro da pizza.
{: .text-justify}

Este parâmetro recebe uma `tuple` do mesmo tamanho de `x`, onde cada elemento dessa `tuple` deve ser número (`int` ou `float`).
{: .text-justify}

Por exemplo, utilizando a `tuple`:

```python
explode = (0, 0.1, 0, 0, 0)
```
apenas a segunda fatia ficará "puxada" para fora em `0.1`, sendo que as outras fatias ficaram na posição inicial normal:
{: .text-justify}

```python
explode = (0, 0.1, 0, 0, 0)
plt.figure(figsize=(8,8))
plt.pie(quantidade_vendas, labels = sabor, autopct='%.1f%%', startangle=90, explode=explode)
plt.show()
```

*Figura 3* - Gráfico de pizza desenhada utilizando o parâmetro `explode`.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-pizza/73/grafico-pizza-03.png" alt="gráfico de pizza desenhado com matplotlib utilizando o parâmetro explode" >
{: .text-center}

<br>

É possível deixar quantas fatias "puxadas" quanto você desejar, mas o ideal é destacar poucas fatias. Por exemplo:
{: .text-justify}

```python
explode = (0, 0.1, 0.5, 0.3, 0.2)
plt.figure(figsize=(8,8))
plt.pie(quantidade_vendas, labels = sabor, autopct='%.1f%%', startangle=90, explode=explode)
plt.show()
```

*Figura 4* - Gráfico de pizza desenhada utilizando o parâmetro `explode`.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-pizza/73/grafico-pizza-04.png" alt="gráfico de pizza desenhado com matplotlib utilizando o parâmetro explode" >
{: .text-center}

<br>


<form id = "quiz" name = "quiz">

<p><strong>Qual a função do parâmetro explode?</strong></p>

<input type = "radio" id = "mc" name = "question1" value = "a"> Queimar a pizza!
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "b"> Destacar uma fatia da pizza deixando ela mais brilhante
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "c"> Destacar uma ou mais fatias da pizza, "puxando" a(s) fatia(s) para "fora"
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "d"> Aumentar o tamanho da pizza
<p style="font-size: 50%"></p>
<p></p>
<input id = "button" type = "button" class="btn btn--info" value = "Enviar" onclick = "check();">
</form>

<div id = "after_submit">
<p style="font-size: 120%" id = "message"></p>
</div>


<br>

<p style="text-align: center">
  <a href="/Curso-matplotlib-72" class="btn btn--success">Anterior</a>
  <a href="/Curso-matplotlib-74" class="btn btn--success">Próximo</a>
</p>



<script>
function check(){
	var question1 = document.quiz.question1.value;
	var messages = [" Incorreto! 😔 <br> Além de não ser possível queimar um gráfico de pizza virtual, que tristeza seria queimar uma pizza 😭😭😭 ",
  " 😔 Incorreto! <br> O parâmetro <code>explode</code> é utilizado para destacar fatias da pizza, mas isto não é feito deixando as fatias brilhates.",
  " 🎉 Correto! 🥳️ <br> Esta é a função do parâmetro <code>explode</code>.",
  " 😔 Incorreto! <br> Para aumentar o tamanho da pizza utilizamos o parâmetro <code>radius</code>.",
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
