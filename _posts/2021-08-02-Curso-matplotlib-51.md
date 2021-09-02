---
title: "Curso matplotlib - Gráfico de barras verticais (rotação dos ticks do eixo)"
data: 2021-08-02
tags: []
header:
  image: "/images/chess.jpg"
  image_description: "Chess pieces"
excerpt: "matplotlib"
locale: "pt-br"
---

<br>

Em alguns casos, temos um descrição para um ponto que é muito longo e, por isso, ele ocupa mais espaço do que o esperado. Uma forma de contornar este problema, é rotacionando os nomes dos *ticks* eixo. Para fazer isto, podemos utilizar o método `plt.xticks()`, que é o elemento que controla as propriedades do eixo `x`, como o ângulo de rotação ([documentação](https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.xticks.html)).
{: .text-justify}

Para rotacionar os *ticks* no eixo `x`, basta passar o ângulo desejado através do parâmetro `rotation` em `plt.xticks()`. Por exemplo, para deixar o ângulo em 90 graus:
{: .text-justify}

```python
plt.figure(figsize=(8,6))
plt.bar(frutas, precos)
plt.xticks(rotation=90)
plt.show()
```


*Figura 1* - Gráfico de barras verticais os *ticks do eixo x rotacionados (90°).
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-barras-verticais/51/grafico-barras-verticais-01.png" alt="gráfico de barras verticais desenhado com o matplotlib." >
{: .text-center}

<br>

Para rotacionar os *ticks* em 45 graus:

```python
plt.figure(figsize=(8,6))
plt.bar(frutas, precos)
plt.xticks(rotation=45)
plt.show()
```

*Figura 2* - Gráfico de barras verticais os *ticks* do eixo x rotacionados (45°).
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-barras-verticais/51/grafico-barras-verticais-02.png" alt="gráfico de barras verticais desenhado com o matplotlib." >
{: .text-center}

<br>


<form id = "quiz" name = "quiz">

<p><strong>Qual é a utilidade de rotacionar os <i>ticks</i> dos eixos de um gráfico?</strong></p>

<input type = "radio" id = "mc" name = "question1" value = "a"> Melhorar a apresentação do gráfico
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "b"> Não tem nenhuma utilidade
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "c"> Melhorar a legibilidade do gráfico
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "d"> Evitar que nomes muito longos se sobreponham
<p style="font-size: 50%"></p>
<p></p>
<input id = "button" type = "button" class="btn btn--info" value = "Enviar" onclick = "check();">
</form>

<div id = "after_submit">
<p style="font-size: 120%" id = "message"></p>
</div>

<br>



<p style="text-align: center">
  <a href="/Curso-matplotlib-50" class="btn btn--success">Anterior</a>
  <a href="/Curso-matplotlib-52" class="btn btn--success">Próximo</a>
</p>

<script>
function check(){
	var question1 = document.quiz.question1.value;
	var messages = [" 🎉 Correto! 🥳️ <br> Rotacionar os <i>ticks</i> pode contribuir bastante para a melhora da apresentação do gráfico!",
  " 😔 Incorreto! 😔  <br> Rotacionar os <i>ticks</i> dos eixos pode ser muito útil!",
  "🎉 Correto! 🥳️ <br> Rotacionar os <i>ticks</i> pode melhorar a legibilidade do gráfico! ",
  " 🎉 Correto! 🥳️  <br> Rotacionar os <i>ticks</i> pode evitar a sobreposição de nomes muito longos!",
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
