---
title: "Curso matplotlib - Combinando gráfico de dispersão com gráfico de linhas"
data: 2021-07-29
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

Utilizar o `plt.plot()` para gerar gráfico de dispersão com linhas talvez não seja a melhor ideia, pois a *personalização* dos marcadores é mais ***simples*** quando utilizamos o `plt.scatter()`.
{: .text-justify}

A melhor forma de gerar um gráfico de dispersão com linhas é combinando dois elemento gráficos separadamente, sendo um o gráfico de linha (`plt.plot()`) e o outro o gráfico de dispersão (`plt.scatter()`), o que é feito da seguinte forma:
{: .text-justify}


```python
plt.figure(figsize=(12,6))
plt.plot(horario, temperatura, c='red', linewidth=3.5)
plt.scatter(horario, temperatura, marker='s', edgecolors='k', facecolors='g', s=250, linewidths=3.5)
plt.show()
```


*Figura 1* - Combinando gráfico de dispersão com gráfico de linhas.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-linhas/22/grafico-dispersao-linhas-01.png" alt="gráfico de linhas e pontos desenhado com o **matplotlib** relacionando o horário e a temperatura ambiente " >
{: .text-center}

<br>


<h2><a style="color:black" id="ordem-plotagem">Ordem de plotagem</a></h2>


No gráfico acima (Figura 1), observe que a linha foi desenhada em cima dos pontos, enquanto que no gráfico anterior, a linha estava desenhada por baixo. Por padrão, o `plt.plot()` aloca a linha por de baixo dos pontos.
{: .text-justify}

Quando adicionamos vários elementos gráficos, existe uma prioridade de qual ordem será utilizada para desenhar o gráfico. Entretanto, podemos **controlar** esta ordem de forma muito simples, através do parâmetro `zorder`.
{: .text-justify}

O parâmetro `zorder` deve receber um número (`int` ou `float`) que indica a ordem de plotagem do elemento. Elementos com maior valor de `zorder` são desenhados por cima dos demais. Por exemplo, caso queira deixar a linha por baixo dos marcadores, basta adicionar `zorder=-1` em `plt.plot()`:
{: .text-justify}

```python
plt.figure(figsize=(12,6))
plt.plot(horario, temperatura, c='red', linewidth=3.5, zorder=-1)
plt.scatter(horario, temperatura, marker='s', edgecolors='k', facecolors='g', s=250,
          linewidths=3.5)
plt.show()
```


*Figura 2* - Combinando gráfico de dispersão com gráfico de linhas.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-linhas/22/grafico-dispersao-linhas-02.png" alt="gráfico de linhas e pontos desenhado com o **matplotlib** relacionando o horário e a temperatura ambiente " >
{: .text-center}

<br>

Ou especificar a ordem em todos os elementos (recomendado):

```python
plt.figure(figsize=(12,6))
plt.plot(horario, temperatura, c='red', linewidth=3.5, zorder=1)
plt.scatter(horario, temperatura, marker='s', edgecolors='k', facecolors='g', s=250,
          linewidths=3.5, zorder=2)
plt.show()
```

*Figura 3* - Combinando gráfico de dispersão com gráfico de linhas.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-linhas/22/grafico-dispersao-linhas-03.png" alt="gráfico de linhas e pontos desenhado com o **matplotlib** relacionando o horário e a temperatura ambiente " >
{: .text-center}

<br>

<h2><a style="color:black" id="transparencia">Transparência</a></h2>

Também é possível adicionar transparência aos elementos gráficos, o que é feito passando um número (`float`) entre `0.0` (completamente transparente) e `1.0` (totalmente preenchido) através do parâmetro `alpha`.
{: .text-justify}

Por exemplo, para deixar os marcadores com metade da sua transparência, basta passar `alpha=0.5` em `plt.scatter()`:

```python
plt.figure(figsize=(12,6))
plt.plot(horario, temperatura, c='red', linewidth=3.5, zorder=1)
plt.scatter(horario, temperatura, marker='s', edgecolors='k', facecolors='g', s=250,
          linewidths=3.5, zorder=2, alpha=0.5)
plt.show()
```

*Figura 4* - Combinando gráfico de dispersão com gráfico de linhas.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-linhas/22/grafico-dispersao-linhas-04.png" alt="gráfico de linhas e pontos desenhado com o **matplotlib** relacionando o horário e a temperatura ambiente " >
{: .text-center}

<br>


Para deixar a linha transparente, basta passar `alpha=0.5` em `plt.plot()`:

```python
plt.figure(figsize=(12,6))
plt.plot(horario, temperatura, c='red', linewidth=3.5, zorder=1, alpha=0.5)
plt.scatter(horario, temperatura, marker='s', edgecolors='k', facecolors='g', s=250,
          linewidths=3.5, zorder=2)
plt.show()
```

*Figura 5* - Combinando gráfico de dispersão com gráfico de linhas.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-linhas/22/grafico-dispersao-linhas-05.png" alt="gráfico de linhas e pontos desenhado com o **matplotlib** relacionando o horário e a temperatura ambiente " >
{: .text-center}

<br>



<form id = "quiz" name = "quiz">

<p><strong>Qual é a função do parâmetro <code>zorder</code>?</strong></p>

<input type = "radio" id = "mc" name = "question1" value = "a"> Especificar a ordem de plotagem dos elementos gráficos.
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "b"> Adicionar transparência a uma elemento do <strong>matplotlib</strong>.
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "c"> Invocar o Zordon.
<p style="font-size: 50%"></p>
<p></p>
<input id = "button" type = "button" class="btn btn--info" value = "Enviar" onclick = "check();">
</form>

<div id = "after_submit">
<p style="font-size: 120%" id = "message"></p>
</div>

<br>


<form id = "quiz" name = "quiz2">

<p><strong>Qual é a função do parâmetro <code>alpha</code>?</strong></p>

<input type = "radio" id = "mc" name = "question1" value = "a"> Especificar a ordem de plotagem dos elementos gráficos.
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "b"> Adicionar transparência a uma elemento do <strong>matplotlib</strong>.
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "c"> Invocar o Alpha 5.
<p style="font-size: 50%"></p>
<p></p>
<input id = "button" type = "button" class="btn btn--info" value = "Enviar" onclick = "checkDois();">
</form>

<div id = "after_submit_dois">
<p style="font-size: 120%" id = "message_dois"></p>
</div>

<br>

<p style="text-align: center">
  <a href="/Curso-matplotlib-21" class="btn btn--success">Anterior</a>
  <a href="/Curso-matplotlib-23" class="btn btn--success">Próximo</a>
</p>




<script>
function check(){
	var question1 = document.quiz.question1.value;
	var messages = [" 🎉 Correto 🥳 !  <br> A função do parâmetro <code>zorder</code> é controlar a ordem de plotagem dos elementos gráficos",
  " Incorreto! ️😔 <br> Para controlar a transparência dos elementos gráficos é utilizado o parâmetro <code>alpha</code> e não o parâmetro <code>zorder</code>",
  " 😔 Incorreto! ️  <br> O <a href='https://powerrangers.fandom.com/wiki/Zordon'>Zordon</a> é um personagem fictício da franquia Power Rangers, e não tem nenhuma relação com os parâmetros do <strong>matplotlib</strong>",
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
	var question1 = document.quiz2.question1.value;
	var messages = [" 😔 Incorreto !  <br> A função do parâmetro <code>alpha</code> é controlar a transparência dos elementos gráficos, e não a ordem de plotagem. O parâmetro utilizado para controlar a ordem de plotagem é o parâmetro <code>zorder</code>.",
  " 🎉 Correto 🥳 ! <br> O parâmetro  <code>alpha</code> é utilizado para controlar a transparência dos elementos gráficos!",
  " 😔 Incorreto! ️  <br> O <a href='https://powerrangers.fandom.com/wiki/Alpha_5'>Alpha 5</a> é um personagem fictício da franquia Power Rangers, e não tem nenhuma relação com os parâmetros do <strong>matplotlib</strong>! ",
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

	document.getElementById("after_submit_dois").style.visibility = "visible";
	document.getElementById("message_dois").innerHTML = messages[score];

};

</script>
