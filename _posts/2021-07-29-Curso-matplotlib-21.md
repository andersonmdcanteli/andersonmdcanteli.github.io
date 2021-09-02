---
title: "Curso matplotlib - Gráfico de linhas (com pontos)"
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

Também podemos gerar um gráfico de linhas com pontos, onde os pontos especificados em (`x,y`) serão apresentados como um gráfico de dispersão juntamente com as linhas, de forma que os pontos consecutivos fiquem ligados por uma reta.
{: .text-justify}

Fazemos isto passando o tipo de marcador desejado através do parâmetro `marker`:
{: .text-justify}

```python
plt.figure(figsize=(12,6))
plt.plot(horario, temperatura, c='red', linewidth=3.5, marker = 'o')
plt.show()
```


*Figura 1* - Gráfico de linhas com pontos.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-linhas/21/grafico-linhas-01.png" alt="gráfico de linhas e pontos desenhado com o **matplotlib** relacionando o horário e a temperatura ambiente " >
{: .text-center}

<br>


<h3><a style="color:black" id="tipo-marcador">Tipo de marcadores</a></h3>

Para alterar o tipo de marcador, basta passar uma `str` com o símbolo desejado para o `plt.plot()`, através do parâmetro `marker`. Os símbolos disponíveis são os mesmos que foram detalhados <a href="/Curso-matplotlib-10#alterando-marcador">anteriormente</a>.
{: .text-justify}

**Exemplo:**

```python
plt.figure(figsize=(12,6))
plt.plot(horario, temperatura, c='red', linewidth=3.5, marker = 's')
plt.show()
```

*Figura 2* - Gráfico de linhas com pontos no estilo quadrado.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-linhas/21/grafico-linhas-02.png" alt="gráfico de linhas e pontos desenhado com o **matplotlib** relacionando o horário e a temperatura ambiente " >
{: .text-center}

<br>


<h3><a style="color:black" id="tamanho-marcador">Tamanho dos marcadores</a></h3>


Para alterar o tamanho de um marcador, basta passar um número (`int` ou `float`) para o `plt.plot()`, através do parâmetro `markersize`.
{: .text-justify}

**Exemplo:**

```python
plt.figure(figsize=(12,6))
plt.plot(horario, temperatura, c='red', linewidth=3.5, marker = 's', markersize = 16)
plt.show()
```

*Figura 3* - Gráfico de linhas com pontos no estilo quadrado.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-linhas/21/grafico-linhas-03.png" alt="gráfico de linhas e pontos desenhado com o **matplotlib** relacionando o horário e a temperatura ambiente " >
{: .text-center}

<br>

<h3><a style="color:black" id="cor-marcador">Cor dos marcadores</a></h3>

Para alterar a cor (de dentro) do marcador, passamos o nome da cor em uma `str` para o `plt.plot()` através do parâmetro `markerfacecolor`. As opções de cores disponíveis são as mesmas vistas <a href="/Curso-matplotlib-08#cor-marcadores">anteriormente</a>.
{: .text-justify}

**Exemplo:**

```python
plt.figure(figsize=(12,6))
plt.plot(horario, temperatura, c='red', linewidth=3.5, marker = 's', markersize = 16,
        markerfacecolor = 'g')
plt.show()
```

*Figura 4* - Gráfico de linhas com pontos com face na cor verde.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-linhas/21/grafico-linhas-04.png" alt="gráfico de linhas e pontos desenhado com o **matplotlib** relacionando o horário e a temperatura ambiente " >
{: .text-center}

<br>


<h3><a style="color:black" id="cor-marcador-borda">Cor da borda dos marcadores</a></h3>

Também podemos alterar a cor das bordas do marcador, passando uma `str` contendo o nome da cor desejada para o `plt.plot()` através do parâmetro `markeredgecolor`. As opções de cores disponíveis são as mesmas vistas <a href="/Curso-matplotlib-08#cor-marcadores">anteriormente</a>.
{: .text-justify}

**Exemplo:**

```python
plt.figure(figsize=(12,6))
plt.plot(horario, temperatura, c='red', linewidth=3.5, marker = 's', markersize = 16,
        markerfacecolor = 'g', markeredgecolor = 'k')
plt.show()
```

*Figura 5* - Gráfico de linhas com pontos com face na cor verde e bordas na cor preta.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-linhas/21/grafico-linhas-05.png" alt="gráfico de linhas e pontos desenhado com o **matplotlib** relacionando o horário e a temperatura ambiente " >
{: .text-center}

<br>


<h3><a style="color:black" id="espessura-borda-marcador">Espessura da borda dos marcadores</a></h3>

Ainda é possível alterar a espessura da borda dos marcadores, passando um número (`int` ou `float`) com o valor da espessura desejada para o `plt.plot()` através do parâmetro `markeredgewidth`.
{: .text-justify}

**Exemplo:**

```python
plt.figure(figsize=(12,6))
plt.plot(horario, temperatura, c='red', linewidth=3.5, marker = 's', markersize = 16,
        markerfacecolor = 'g', markeredgecolor = 'k', markeredgewidth=3.5)
plt.show()
```

*Figura 6* - Gráfico de linhas com pontos com face na cor verde e bordas espessas na cor preta.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-linhas/21/grafico-linhas-06.png" alt="gráfico de linhas e pontos desenhado com o **matplotlib** relacionando o horário e a temperatura ambiente " >
{: .text-center}

<br>


<form id = "quiz" name = "quiz">

<p><strong>Qual opções abaixo irá adicionar marcadores em um gráfico desenhado utilizando o <code>plt.plot()</code>?</strong></p>

<input type = "radio" id = "mc" name = "question1" value = "a"> Parâmetro <code> marcador = "o"</code>
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "b"> Parâmetro <code> marker = o </code>
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "c"> Parâmetro <code> marker = "o"</code>
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "d"> Parâmetro <code> marker = "s"</code>
<p style="font-size: 50%"></p>
<p></p>
<input id = "button" type = "button" class="btn btn--info" value = "Enviar" onclick = "check();">
</form>

<div id = "after_submit">
<p style="font-size: 120%" id = "message"></p>
</div>


<br>

<form id = "quiz" name = "quiz2">

<p><strong>Qual das opções abaixo irá desenhar um gráfico com marcadores na cor preta? Considere que os métodos omitidos estão corretos</strong></p>

<input type = "radio" id = "mc" name = "question1" value = "a"> <code> plt.plot(horario, temperatura, c='green',  marker = 's', markerfacecolor = 'k', markeredgecolor = 'k')</code>
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "b"> <code> plt.plot(horario, temperatura, c='k', marker="s")</code>
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "c"> <code> plt.plot(horario, temperatura, c='k',  marker = 's', markerfacecolor = 'm', markeredgecolor = 'k')</code>
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "d"> <code> plt.plot(horario, temperatura, c='k',  marker = 's', markerfacecolor = 'black', markeredgecolor = 'k')</code>
<p style="font-size: 50%"></p>
<p></p>
<input id = "button" type = "button" class="btn btn--info" value = "Enviar" onclick = "checkDois();">
</form>

<div id = "after_submit_dois">
<p style="font-size: 120%" id = "message_dois"></p>
</div>


<br>

<p style="text-align: center">
  <a href="/Curso-matplotlib-20" class="btn btn--success">Anterior</a>
  <a href="/Curso-matplotlib-22" class="btn btn--success">Próximo</a>
</p>



<script>
function check(){
	var question1 = document.quiz.question1.value;
	var messages = [" 😔 Incorreto! ️ <br> O método <code>plt.plot()</code> não tem um parâmetro chamado <code>marcador</code>",
  " Incorreto! ️😔 <br> O nome do parâmetro está correto, entretanto, como o símbolo não foi passado como uma <code>str</code>, um erro será levantado!",
  "🥳️  Correto 🎉!  <br> Passando a <code>str</code> <code>'o'</code> para o parâmetro <code>marker</code>, será adicionado marcadores com formato circular no gráfico!  ",
  "🎉 Correto 🥳 !  <br> Passando a <code>str</code> <code>'s'</code> para o parâmetro <code>marker</code>, será adicionado marcadores com formato quadrado no gráfico!  ",  
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




<script>
function checkDois(){
	var question1 = document.quiz2.question1.value;
	var messages = [" 🎉 Correto 🥳 ! <br> Desta forma, a cor dos marcadores será preta; entretanto, a cor da linha será verde",
  " 🎉️  Correto 🥳 !  <br> Passando estes parâmetros, não apenas os marcadores ficaram na cor preta, mas a linha também ficará na cor preta!",
  " Incorreto! ️😔!  <br> Passando estes parâmetros, as linhas ficarão com a cor preta, as bordas dos marcadores ficaram na cor preta, mas a cor da face dos marcadores ficará na cor magenta",
  "🎉 Correto 🥳 !  <br> Passando estes parâmetros, não apenas os marcadores ficaram na cor preta, mas a linha também ficará na cor preta! Observe que <code>'black'</code> é igual a <code>'k'</code>! ",  
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

	document.getElementById("after_submit_dois").style.visibility = "visible";
	document.getElementById("message_dois").innerHTML = messages[score];

};

</script>
