---
title: "Curso matplotlib - Gráfico de linhas (Anotações)"
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


Em alguns casos é interessante adicionar *elementos textuais* diretamente no gráfico para melhorar a sua apresentação. Uma informação importante que pode ser adicionada, é o valor de cada ponto.
{: .text-justify}

Neste caso, na forma como o gráfico está desenhado, o leitor tem apenas uma noção da variação da temperatura ao longo do dia, mas a visualização de cada temperatura não esta clara. Temos algumas opções para adicionar estas informações diretamente no gráfico; por enquanto, vamos ver o `plt.annotate()`. Através deste método podemos passar o valor contido no eixo `y` diretamente sob o ponto do gráfico.
{: .text-justify}

Este elemento, o `plt.annotate()`, precisa de pelo menos dois parâmetros: o `text`, que recebe o texto (`str`) que será anotado; e o `xy`, que recebe uma `tuple` contendo o par *xy* das *coordenadas do eixo*.
{: .text-justify}

Por exemplo, para adicionar a anotação `'minha anotação'` na posição `x = 05:00 horas` e `y = 30 °C`, é necessário passar o local correspondente às 05:00 (2.5) horas e a temperatura de 30 °C (30):
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
plt.annotate("minha anotação", xy=(2.5,30))
plt.show()
```

*Figura 1* - Gráfico de dispersão com limites com anotações.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-linhas/25/grafico-dispersao-linhas-01.png" alt="gráfico de linhas desenhado com o **matplotlib** relacionando o horário e a temperatura ambiente" >
{: .text-center}

<br>


De forma análoga, podemos anotar o valor do primeiro ponto do gráfico passando `text=str(temperatura[0])` e `xy=(0,temperatura[0])`:
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
plt.annotate(str(temperatura[0]), xy=(0,temperatura[0]))
plt.show()
```

*Figura 2* - Gráfico de dispersão com limites com anotações.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-linhas/25/grafico-dispersao-linhas-02.png" alt="gráfico de linhas desenhado com o **matplotlib** relacionando o horário e a temperatura ambiente" >
{: .text-center}

<br>

Observe que o valor inserido ficou escondido, pois é um número com apenas duas casas e o tamanho do marcador esta grande. Isso aconteceu pois foi passado para `xy` exatamente o centro do marcador, e texto e marcador acabaram se sobrepondo.
{: .text-justify}

Uma boa prática para evitar este problema, é passar uma posição um pouco deslocada para a anotação. Por exemplo, para deixar a anotação um pouco acima do marcador, podemos passar o valor de `y` um pouco maior do que o valor original:
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
plt.annotate(str(temperatura[0]), xy=(0,temperatura[0]+1))
plt.show()
```

*Figura 3* - Gráfico de dispersão com limites com anotações.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-linhas/25/grafico-dispersao-linhas-03.png" alt="gráfico de linhas desenhado com o **matplotlib** relacionando o horário e a temperatura ambiente" >
{: .text-center}

<br>


Para deixar o texto mais centralizado, basta passar um valor menor para o primeiro valor da `tuple`:

```python
plt.figure(figsize=(12,6))
plt.plot(horario, temperatura, c='red', linewidth=3.5, zorder=1, alpha=0.5, label='linha de conecção')
plt.scatter(horario, temperatura, marker='s', edgecolors='k', facecolors='g', s=250, linewidths=3.5, zorder=2,
           label='dados reais')
plt.legend(bbox_to_anchor=(1.22,1))
plt.xlabel("Horário", labelpad=15)
plt.ylabel("Temperatura (°C)", labelpad=15)
plt.title("Monitoramento da temperatura na cidade de Birigui-SP no dia 13/04/2021", pad=15)
plt.ylim(14,38)
plt.annotate(str(temperatura[0]), xy=(0 - 0.12,temperatura[0]+1))
plt.show()
```

*Figura 4* - Gráfico de dispersão com limites com anotações.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-linhas/25/grafico-dispersao-linhas-04.png" alt="gráfico de linhas desenhado com o **matplotlib** relacionando o horário e a temperatura ambiente" >
{: .text-center}

<br>


Para adicionar anotações em cada ponto é necessário adicionar diversos elementos de `plt.annotate()`, um para cada ponto. Uma boa prática é utilizar um loop `for` para adicionar uma anotação para cada ponto (mais eficiente):
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
for i in range(len(temperatura)):
    plt.annotate(str(temperatura[i]), xy=(i - 0.12,temperatura[i]+1))
plt.show()
```

*Figura 5* - Gráfico de dispersão com limites com anotações.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-linhas/25/grafico-dispersao-linhas-05.png" alt="gráfico de linhas desenhado com o **matplotlib** relacionando o horário e a temperatura ambiente" >
{: .text-center}

<br>


<form id = "quiz" name = "quiz">

<p><strong>Como determinar qual a posição do gráfico um texto será inserido ao utilizar o método <code>plt.annotate()</code>?</strong></p>

<input type = "radio" id = "mc" name = "question1" value = "a"> Passando uma lista com os valores de x e y para o parâmetro <code>xy</code>.
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "b"> Passando uma tuple com os valores de x e y para o parâmetro <code>yx</code>.
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "c"> Passando uma tuple com os valores de x e y para o parâmetro <code>xy</code>.
<p style="font-size: 50%"></p>
<p></p>
<input id = "button" type = "button" class="btn btn--info" value = "Enviar" onclick = "check();">
</form>

<div id = "after_submit">
<p style="font-size: 120%" id = "message"></p>
</div>

<br>



<p style="text-align: center">
  <a href="/Curso-matplotlib-24" class="btn btn--success">Anterior</a>
  <a href="/Curso-matplotlib-26" class="btn btn--success">Próximo</a>
</p>




<script>
function check(){
	var question1 = document.quiz.question1.value;
	var messages = ["😔 Incorreto! ️ <br> O parâmetro <code>xy</code> deve receber uma <code>tuple</code> e não uma <code>list</code>.",
  " Incorreto! ️😔 <br> O parâmetro <code>yx</code> não existe em <code>plt.annotate()</code>. O correto é utilizar o parâmetro <code>xy</code>",
  "  🎉 Correto 🥳 !  <br> É através do parâmetro <code>xy</code> que especifica-se qual a posição o texto será anotado no gráfico",
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
