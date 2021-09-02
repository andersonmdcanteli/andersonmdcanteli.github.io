---
title: "Boxplot "
data: 2021-08-13
tags: []
header:
  image: "/images/chess.jpg"
  image_description: "Chess pieces"
excerpt: "matplotlib"
locale: "pt-br"
---


<br>

O Boxplot é uma forma gráfica de representar a mediana e os quartis de um conjunto de dados, sendo muito interessante para verificar se existem dados discrepantes, verificar a tendência dos dados à normalidade e simetria, além de comparar diferentes conjuntos dados.
{: .text-justify}

Ele é composto pela mediana (geralmente através de um único ponto no centro ou uma linha), um retângulo (caixa) que representa a distância interquartílica, e linhas de intervalo entre \\(Q_{1}-1,5DI\\) e \\(Q_{3}+1,5DI\\). Este intervalo compreende uma região que abrange 99,3% dos dados de uma distribuição Normal.
{: .text-justify}

Diversos autores atribuem a pontos que estão fora do intervalo \\(Q_{1}-1,5DI\\) e \\(Q_{3} + 1,5DI\\), como sendo considerados *outliers*. Entretanto, a presença destes dados pode ser um indicativo de que o conjunto de dados não segue uma distribuição Normal, que a distribuição não é centrada na média ou ainda que o tamanho amostral é pequeno.
{: .text-justify}

Para desenhar um boxplot utilizando o **matplotlib** basta passar uma sequência (`list`, `tuple`, etc) para o `plt.boxplot()`.
{: .text-justify}

Por exemplo, para o conjunto de dados referente a altura de crianças com 11 anos:
{: .text-justify}

```python
plt.figure(figsize=(8,6))
plt.boxplot(altura_11_anos)
plt.show()
```

*Figura 1* - Gráfico de boxplot para a altura das crianças de 11 anos.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/boxplot/89/boxplot-01.png" alt="gráfico tipo boxplot desenhado com matplotlib" >
{: .text-center}

<br>


Também é possível desenhar em um mesmo gráfico um série de boxplots de vários vários conjuntos de dados. Para isto, basta passar uma sequência de sequências (uma `list` contendo `lists` internas por exemplo). Para desenhar o boxplot comparando os dados da altura de crianças com 11 e 12 anos, basta os dois conjuntos dentro de uma `list`:
{: .text-justify}


```python
plt.figure(figsize=(8,6))
plt.boxplot([altura_11_anos, altura_12_anos])
plt.show()
```

*Figura 2* - Gráfico de boxplot para a altura das crianças de 11 e 12 anos.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/boxplot/89/boxplot-02.png" alt="gráfico tipo boxplot desenhado com matplotlib" >
{: .text-center}

Você encontra mais informações na [documentação](https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.boxplot.html).

<br>

<form id = "quiz" name = "quiz">

<p><strong>Como são representados os possíveis outliers em um boxplot?</strong></p>

<input type = "radio" id = "mc" name = "question1" value = "a"> Através de uma linha
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "b"> Através de um ponto
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "c"> Através de uma seta
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "d"> Outliers não são identificados nos boxplots
<p style="font-size: 50%"></p>
<p></p>
<input id = "button" type = "button" class="btn btn--info" value = "Enviar" onclick = "check();">
</form>

<div id = "after_submit">
<p style="font-size: 120%" id = "message"></p>
</div>

<br>


<p style="text-align: center">
  <a href="/Curso-matplotlib-88" class="btn btn--success">Anterior</a>
  <a href="/Curso-matplotlib-90" class="btn btn--success">Próximo</a>
</p>




<script>
function check(){
	var question1 = document.quiz.question1.value;
	var messages = [" Incorreto! 😔 <br> A linha inserida indica a posição da mediana. ",
  " 🎉 Correto! 🥳️ ! <br> ",
  "  Incorreto! 😔 <br> Por padrão, nenhuma seta é inserida nos boxplots.",
  " 😔 Incorreto! 😔 <br> Os outilers podem ser identificados nos boxplots!",
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
