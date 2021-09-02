---
title: "Gráfico de pizza (Porcentagem de cada fatia como label)"
data: 2021-08-08
tags: []
header:
  image: "/images/chess.jpg"
  image_description: "Chess pieces"
excerpt: "matplotlib"
locale: "pt-br"
---


<br>

Uma informação extremamente relevante para um gráfico de pizza, é a quantidade que cada fatia ocupa do total da pizza. Apesar de visualmente ser possível estimar este valor, efetivamente inseri-lo é a melhor forma de passar esta informação ao leitor.
{: .text-justify}

Para adicionar a porcentagem que cada fatia ocupa na pizza, basta passar uma `str` formatada através do parâmetro `autopct`. Uma forma bem simples de passar essa `str` é:
{: .text-justify}

`'%.Yf%%'`
{: .text-center}

onde o `Y` corresponde ao número de casas decimais, e o `f` é um parâmetro de formatação. Para inserir a porcentagem com apenas 1 casa decimal, basta substituir o `Y` pelo número `1`, ou seja, `'%.1f%%'`. Por exemplo:
{: .text-justify}

```python
plt.figure(figsize=(8,8))
plt.pie(quantidade_vendas, labels = sabor, autopct='%.1f%%')
plt.show()
```

*Figura 1* - Gráfico de pizza com a porcentagem que cada fatia ocupa escrita na respectiva fatia.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-pizza/71/grafico-pizza-01.png" alt="gráfico de pizza desenhado com matplotlib com a porcentagem que cada fatia ocupa na respectiva fatia." >
{: .text-center}

<br>

Já para deixar com 4 casas decimais, basta substituir o `Y` pelo número `4`, ou seja, `'%.4f%%'`. Por exemplo:
{: .text-justify}

```python
plt.figure(figsize=(8,8))
plt.pie(quantidade_vendas, labels = sabor, autopct='%.4f%%')
plt.show()
```

*Figura 2* - Gráfico de pizza com a porcentagem que cada fatia ocupa escrita na respectiva fatia.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-pizza/71/grafico-pizza-02.png" alt="gráfico de pizza desenhado com matplotlib com a porcentagem que cada fatia ocupa na respectiva fatia." >
{: .text-center}

<br>


<h2><a style="color:black" id="distancia-centro-porcentagem">Distância entre o centro da pizza e a porcentagem de cada fatia</a></h2>

Caso o parâmetro `autopct` tenha sido passado, podemos controlar a distância entre o centro da pizza e a porcentagem inserida, de forma similar a distância entre o centro da pizza e os labels. Basta passar um número (`int` ou `float`) para o `plt.pie()` através do `pctdistance` (o valor padrão é  `0.6`).
{: .text-justify}

Por exemplo, para deixar estas porcentagens fora da pizza, basta passar um valor para o `pctdistance` maior do que o raio.

```python
plt.figure(figsize=(8,8))
plt.pie(quantidade_vendas, autopct='%.1f%%', pctdistance=1.1) # labels removidos para evitar sobreposição
plt.show()
```

*Figura 3* - Gráfico de pizza com a porcentagem que cada fatia ocupa escrita na respectiva fatia.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-pizza/71/grafico-pizza-03.png" alt="gráfico de pizza desenhado com matplotlib com a porcentagem que cada fatia ocupa na respectiva fatia." >
{: .text-center}

<br>


<form id = "quiz" name = "quiz">

<p><strong>Qual a função do parâmetro autopct?</strong></p>

<input type = "radio" id = "mc" name = "question1" value = "a"> Não tem nenhum função no plt.pie()
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "b"> Controla o ângulo em que a porcentagem da pizza é inserida
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "c"> Inserir a porcentagem que cada fatia da pizza ocupa
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "d"> Controla a distância entre o centro da pizza e onde a porcentagem que cada pizza ocupa é inserida
<p style="font-size: 50%"></p>
<p></p>
<input id = "button" type = "button" class="btn btn--info" value = "Enviar" onclick = "check();">
</form>

<div id = "after_submit">
<p style="font-size: 120%" id = "message"></p>
</div>



<br>



<p style="text-align: center">
  <a href="/Curso-matplotlib-70" class="btn btn--success">Anterior</a>
  <a href="/Curso-matplotlib-72" class="btn btn--success">Próximo</a>
</p>



<script>
function check(){
	var question1 = document.quiz.question1.value;
	var messages = [" Incorreto! 😔 <br> O parâmetro <code>autopct</code> tem a função de inserir a porcentagem que cada pizza ocupa no gráfico",
  " 😔 Incorreto! <br> O parâmetro <code>autopct</code> tem a função de inserir a porcentagem que cada pizza ocupa no gráfico",
  " 🎉 Correto! 🥳️ <br> Esta é a função do parâmetro <code>autopct</code>.",
  " 😔 Incorreto! <br> O parâmetro <code>autopct</code> tem a função de inserir a porcentagem que cada pizza ocupa no gráfico. O parâmetro que controla esta distância é o <code>pctdistance</code>!",
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
