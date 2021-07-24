---
title: "Curso matplotlib - Várias séries"
data: 2021-07-19
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


Em muitos casos vamos ter dois ou mais conjuntos de dados para serem plotados no gráfico, ou seja, várias séries de `x` e `y`. No exemplo que esta sendo utilizado, com dados relacionando peso e altura dos cachorros, temos várias raças, e seria importante diferenciar as raças no gráfico.
{: .text-justify}

Para adicionar mais de uma série em um gráfico de dispersão, basta adicionar um novo elemento de ```plt.scatter()``` com a nova série.
{: .text-justify}

Por exemplo, o gráfico de dispersão que relaciona peso e altura apenas para a raça `'Chihuahua'` (posição 0) é:
{: .text-justify}

```python
plt.figure(figsize=(8,6))
plt.scatter(x[0], y[0], label=raca_cachorro[0])
plt.legend()
plt.show()
```


*Figura 1* - Gráfico de dispersão para a raça Chihuahua.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/13/grafico-dispersao-series-01.png" alt="gráfico de dispersão desenhado utilizando o **matplotlib** para a raça Chihuahua" >
{: .text-center}

<br>


Já para a raça `'Poodle Toy'` (posição 1):

```python
plt.figure(figsize=(8,6))
plt.scatter(x[1], y[1], label=raca_cachorro[1])
plt.legend()
plt.show()
```

*Figura 2* - Gráfico de dispersão para a raça Poodle Toy.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/13/grafico-dispersao-series-03.png" alt="gráfico de dispersão desenhado utilizando o **matplotlib** para a raça Poodle Toy" >
{: .text-center}

<br>


Para juntar estes dois gráficos (como séries diferentes), combinamos dois elementos de `plt.scatter()`, um após o outro:
{: .text-justify}

```python
plt.figure(figsize=(8,6))
plt.scatter(x[0], y[0], label=raca_cachorro[0])
plt.scatter(x[1], y[1], label=raca_cachorro[1])
plt.legend()
plt.show()
```

*Figura 3* - Gráfico de dispersão para a raça Chihuahua e Poodle Toy.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/13/grafico-dispersao-series-03.png" alt="gráfico de dispersão desenhado utilizando o **matplotlib** para a raça Chihuahua e Poodle Toy" >
{: .text-center}

<br>


Observe que o **matplotlib** irá automaticamente diferenciar a cor do marcador das diferentes séries de dados. É possível adicionar quantas séries quanto desejarmos:
{: .text-justify}

```python
plt.figure(figsize=(8,6))
plt.scatter(x[0], y[0], label=raca_cachorro[0])
plt.scatter(x[1], y[1], label=raca_cachorro[1])
plt.scatter(x[2], y[2], label=raca_cachorro[2])
plt.scatter(x[3], y[3], label=raca_cachorro[3])
plt.scatter(x[4], y[4], label=raca_cachorro[4])
plt.scatter(x[5], y[5], label=raca_cachorro[5])
plt.scatter(x[6], y[6], label=raca_cachorro[6])
plt.scatter(x[7], y[7], label=raca_cachorro[7])
plt.scatter(x[8], y[8], label=raca_cachorro[8])
plt.scatter(x[9], y[9], label=raca_cachorro[9])
plt.scatter(x[10], y[10], label=raca_cachorro[10])
plt.legend()
plt.show()
```

*Figura 4* - Gráfico de dispersão para todas as raças de cachorro avaliadas.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/13/grafico-dispersao-series-04.png" alt="gráfico de dispersão desenhado utilizando o **matplotlib** para todas as raças de cachorro avaliadas" >
{: .text-center}

<br>

<form id = "quiz" name = "quiz">

<p><strong>Como adicionar diversos elementos de dispersão no matplotlib?</strong></p>

<input type = "radio" id = "mc" name = "question1" value = "a"> Adicionando vários elementos de <code>plt.scatter()</code> antes de apresentar o gráfico
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "b"> Criando várias sequências de criação de gráficos (criar canvas, adicionar elemento, apresentar o gráfico)
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "c"> Passando várias séries de dados através do parâmetro y em <code>plt.scatter()</code>.
<p style="font-size: 50%"></p>
<p></p>
<input id = "button" type = "button" class="btn btn--info" value = "Enviar" onclick = "check();">
</form>

<div id = "after_submit">
<p style="font-size: 120%" id = "message"></p>
</div>


<h1><a style="color:black" id="">Desafio 1</a></h1>

Crie o mesmo gráfico da Figura 4, mas utilizando um loop `for` para adicionar as raças de cachorro no gráfico. São necessárias apenas 5 linhas de código.
{: .text-justify}

Você pode acessar o notebook básico [clicando aqui](https://github.com/andersonmdcanteli/matplotlib-course/blob/main/curso/grafico-dispersao/desafio-1/Desafio-1.ipynb) (mas tente criar um novo notebook do zero, e implementar todos os dados por conta própria).
{: .text-justify}

O notebook com a resolução do desafio pode ser acessado [clicando aqui](https://github.com/andersonmdcanteli/matplotlib-course/blob/main/curso/grafico-dispersao/desafio-1/Desafio-1-Resolucao.ipynb). O vídeo da resolução do desafio 1 pode ser acessado [neste link](https://youtu.be/PziPMMthKY4).
{: .text-justify}


<p style="text-align: center">
  <a href="/Curso-matplotlib-12" class="btn btn--success">Anterior</a>
  <a href="/Curso-matplotlib-14" class="btn btn--success">Próximo</a>
</p>



<script>
function check(){
	var question1 = document.quiz.question1.value;
	var messages = [" 🎉 Correto! 🥳️  <br>  Os elementos devem ser adicionados antes do <code>plt.show()</code>",
  " Incorreto! 😔  <br> Desta forma, a cada sequência um novo gráfico será desenhado!.",
  " 😔 Incorreto!  <br> Passar diversas séries para o parâmetro <code>y</code> irá levantar um erro!",
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
