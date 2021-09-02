---
title: "Gráfico de pizza (Preenchimento das fatias)"
data: 2021-08-08
tags: []
header:
  image: "/images/chess.jpg"
  image_description: "Chess pieces"
excerpt: "matplotlib"
locale: "pt-br"
---


<br>

<h2><a style="color:black" id="angulo-prenchimento">Ângulo inicial de preenchimento</a></h2>

Para alterar o ângulo em que as fatias começam a ser desenhadas, basta passar o valor do ângulo (`int` ou `float`) para o `plt.pie()` através do parâmetro `startangle` (valor padrão é `0` graus).
{: .text-justify}

Por exemplo, para iniciar o preenchimento das fatias a partir de 90°, basta:

```python
plt.figure(figsize=(8,8))
plt.pie(quantidade_vendas, labels = sabor, autopct='%.1f%%', startangle=90)
plt.show()
```

*Figura 1* - Gráfico de pizza com as fatias sendo preenchidas a partir do ângulo de 90°.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-pizza/72/grafico-pizza-01.png" alt="gráfico de pizza desenhado com matplotlib com as fatias sendo preenchidas a partir do ângulo de 90°" >
{: .text-center}

<br>

#### ATENÇÃO:

A não ser que você tenhas bons motivos, as fatias sempre devem iniciar o preenchimento com o ângulo de 90°.
{: .text-justify}

<h2><a style="color:black" id="direcao-preenchimento">Direção do preenchimento</a></h2>

Por padrão (`True`), o preenchimento é feito no sentido *anti-horário*. Para alterar para o sentido *horário*, basta passar um `bool` `False` para o `plt.pie()` através do parâmetro `counterclock`.
{: .text-justify}

**Exemplo:**

```python
plt.figure(figsize=(8,8))
plt.pie(quantidade_vendas, labels = sabor, autopct='%.1f%%', startangle=90, counterclock=False)
plt.show()
```

*Figura 2* - Gráfico de pizza com as fatias sendo preenchidas no sentido horário.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-pizza/72/grafico-pizza-02.png" alt="gráfico de pizza desenhado com matplotlib com as fatias sendo preenchidas no sentido horário" >
{: .text-center}

<br>


#### ATENÇÃO:

A não ser que você tenhas bons motivos, as fatias ***devem sempre*** ser preenchidas no sentido ***anti-horário***.
{: .text-justify}

<form id = "quiz" name = "quiz">

<p><i>As fatias das pizzas devem começar a ser preenchidas no ângulo de 90°, e o preenchimento deve acontecer no sentido anti-horarário</i>.</p>

<p style="font-size: 50%"></p>

<p><strong>A declaração acima é </strong></p>

<input type = "radio" id = "mc" name = "question1" value = "a"> Verdadeira
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "b"> Falsa
<p style="font-size: 50%"></p>

<p></p>
<input id = "button" type = "button" class="btn btn--info" value = "Enviar" onclick = "check();">
</form>

<div id = "after_submit">
<p style="font-size: 120%" id = "message"></p>
</div>



<br>


<p style="text-align: center">
  <a href="/Curso-matplotlib-71" class="btn btn--success">Anterior</a>
  <a href="/Curso-matplotlib-73" class="btn btn--success">Próximo</a>
</p>


<script>
function check(){
	var question1 = document.quiz.question1.value;
	var messages = [
  " 🎉 Correto! 🥳️ <br> ",
  " 😔 Incorreto! <br> A não ser que exista um bom motivo, esta é a forma recomendada de preencher as fatias da pizza",
  "☕️"];
	var score;

	if (question1 == "a") {
		score = 0;
	}	else if (question1 == "b") {
		score = 1;
  } else {
    score = 2;
  }

	document.getElementById("after_submit").style.visibility = "visible";
	document.getElementById("message").innerHTML = messages[score];

};

</script>
