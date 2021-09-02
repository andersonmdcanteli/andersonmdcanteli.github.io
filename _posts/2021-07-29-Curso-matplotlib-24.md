---
title: "Curso matplotlib - Gráfico de linhas (Faixa dos eixos)"
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

É possível alterar os limites dos eixos `x` e `y` (alterar a faixa de plotagem).

- Para alterar o eixo `x`, passamos uma `tuple` com dois valores (valor inicial de `x`, valor final de `x`) para o `plt.xlim()`;
{: .text-justify}

- Para alterar o eixo `y`, passamos uma `tuple` com dois valores (valor inicial de `y`, valor final de `y`) para o `plt.ylim()`.
{: .text-justify}

Neste caso, temos no eixo `x` apenas `str` representando cada hora do dia. Como passamos uma `str` como valor de `x`, o **matplotlib** utiliza o índice de cada `str` como valores de `x`, e não o valor de cada `str` (pois a posição tem de ser numérica).
{: .text-justify}

Então se alterarmos o `xlim()` para 1 e 10, vamos cortar o primeiro elemento (`'00:00'`) e o último elemento (`'22:00'`), pois a lista `horario` tem 12 elementos, que variam entre a posição `0` e a posição `11`:
{: .text-justify}

**Exemplo:**

```python
plt.figure(figsize=(12,6))
plt.plot(horario, temperatura, c='red', linewidth=3.5, zorder=1, alpha=0.5, label='linha de conecção')
plt.scatter(horario, temperatura, marker='s', edgecolors='k', facecolors='g', s=250, linewidths=3.5,
          zorder=2, label='dados reais')
plt.legend(bbox_to_anchor=(1.22,1))
plt.xlabel("Horário", labelpad=15)
plt.ylabel("Temperatura (°C)", labelpad=15)
plt.title("Monitoramento da temperatura na cidade de Birigui-SP no dia 13/04/2021", pad=15)
plt.xlim(1,10)
plt.show()
```

*Figura 1* - Gráfico de dispersão com limites do eixo x alterados.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-linhas/24/grafico-dispersao-linhas-01.png" alt="gráfico de linhas desenhado com o **matplotlib** relacionando o horário e a temperatura ambiente" >
{: .text-center}

<br>


Mas se utilizamos um intervalo maior, entre -10 e 20 por exemplo:

```python
plt.figure(figsize=(12,6))
plt.plot(horario, temperatura, c='red', linewidth=3.5, zorder=1, alpha=0.5, label='linha de conecção')
plt.scatter(horario, temperatura, marker='s', edgecolors='k', facecolors='g', s=250, linewidths=3.5,
          zorder=2, label='dados reais')
plt.legend(bbox_to_anchor=(1.22,1))
plt.xlabel("Horário", labelpad=15)
plt.ylabel("Temperatura (°C)", labelpad=15)
plt.title("Monitoramento da temperatura na cidade de Birigui-SP no dia 13/04/2021", pad=15)
plt.xlim(-10,20)
plt.show()
```

*Figura 2* - Gráfico de dispersão com limites do eixo x alterados.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-linhas/24/grafico-dispersao-linhas-02.png" alt="gráfico de linhas desenhado com o **matplotlib** relacionando o horário e a temperatura ambiente" >
{: .text-center}

<br>


Já para o eixo `y`, temos valores numéricos na lista `temperatura` e podemos alterar os valores na unidade da temperatura mesmo, pois o eixo foi gerado com as dimensões contidas na lista `temperatura`, e não com o seu índice.
{: .text-justify}

Por exemplo, para alterar o intervalo para a temperatura entre 14 e 38 °C:
{: .text-justify}

```python
plt.figure(figsize=(12,6))
plt.plot(horario, temperatura, c='red', linewidth=3.5, zorder=1, alpha=0.5, label='linha de conecção')
plt.scatter(horario, temperatura, marker='s', edgecolors='k', facecolors='g', s=250, linewidths=3.5,
          zorder=2, label='dados reais')
plt.legend(bbox_to_anchor=(1.22,1))
plt.xlabel("Horário", labelpad=15)
plt.ylabel("Temperatura (°C)", labelpad=15)
plt.title("Monitoramento da temperatura na cidade de Birigui-SP no dia 13/04/2021", pad=15)
plt.ylim(14,38)
plt.show()
```


*Figura 3* - Gráfico de dispersão com limites do eixo x alterados.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-linhas/24/grafico-dispersao-linhas-03.png" alt="gráfico de linhas desenhado com o **matplotlib** relacionando o horário e a temperatura ambiente" >
{: .text-center}

<br>

<form id = "quiz" name = "quiz">

<p><strong>Qual método pode ser utilizado para controlar a faixa de plotagem do eixo <code>x</code>?</strong></p>

<input type = "radio" id = "mc" name = "question1" value = "a"> <code>plt.xlim()</code>
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "b"> <code>plt.xlabel()</code>
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "c"> <code>plt.ylim()</code>
<p style="font-size: 50%"></p>
<p></p>
<input id = "button" type = "button" class="btn btn--info" value = "Enviar" onclick = "check();">
</form>

<div id = "after_submit">
<p style="font-size: 120%" id = "message"></p>
</div>

<br>


<form id = "quiz" name = "quiz2">

<p><strong>Qual método pode ser utilizado para controlar a faixa de plotagem do eixo <code>y</code>?</strong></p>

<input type = "radio" id = "mc" name = "question1" value = "a"> <code>plt.ylim()</code>
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "b"> <code>plt.ylabel()</code>
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "c"> <code>plt.xlim()</code>
<p style="font-size: 50%"></p>
<p></p>
<input id = "button" type = "button" class="btn btn--info" value = "Enviar" onclick = "checkDois();">
</form>

<div id = "after_submit_dois">
<p style="font-size: 120%" id = "message_dois"></p>
</div>

<br>

<p style="text-align: center">
  <a href="/Curso-matplotlib-23" class="btn btn--success">Anterior</a>
  <a href="/Curso-matplotlib-25" class="btn btn--success">Próximo</a>
</p>



<script>
function check(){
	var question1 = document.quiz.question1.value;
	var messages = [" 🎉 Correto 🥳 !  <br> A função do <code>plt.xlim()</code> é controlar a faixa de plotagem do eixo x",
  " Incorreto! ️😔 <br> O <code>plt.xlabel()</code> é utilizado para adicionar título ao eixo x.",
  " 😔 Incorreto! ️  <br> O <code>plt.ylim()</code> é utilizado para controlar a faixo de plotagem do eixo y, não do eixo x",
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
	var messages = [" 🎉 Correto 🥳 !  <br> A função do <code>plt.ylim()</code> é controlar a faixa de plotagem do eixo y",
  " Incorreto! ️😔 <br> O <code>plt.ylabel()</code> é utilizado para adicionar título ao eixo y.",
  " 😔 Incorreto! ️  <br> O <code>plt.xlim()</code> é utilizado para controlar a faixo de plotagem do eixo x, não do eixo y",
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
