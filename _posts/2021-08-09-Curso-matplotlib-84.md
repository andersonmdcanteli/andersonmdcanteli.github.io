---
title: "Elementos auxiliares (Fill between)"
data: 2021-08-09
tags: []
header:
  image: "/images/chess.jpg"
  image_description: "Chess pieces"
excerpt: "matplotlib"
locale: "pt-br"
---


<br>

O elemento do tipo *Fill between* preenche a área entre duas curvas horizontais. É um elemento muito útil para destacar diferenças entre duas condições, ou seja, dar ênfase a algum comportamento. Este elemento preenche com uma cor pré-definida tudo que estiver entre dois conjuntos de `y`.
{: .text-justify}

Dessa forma, é necessário ter 2 linhas, uma com (`x,y1`) e outra (`x,y2`).

<h2><a style="color:black" id="fill-conjunto-dados">Conjunto de dados</a></h2>

Iremos utilizar o conjunto de dados do clima utilizado na aula de <a href="/Curso-matplotlib-19/">gráfico de linhas</a>. Este conjunto de dados, tem a temperatura ambiente medida em dois dias diferentes (13/04/2021 e 29/04/2021) na cidade de Birigui-SP, em diversos horários. A ideia é utilizar o *fill between* para preencher a área entre os dois dias, para enfatizar a diferença.
{: .text-justify}

Para relembrar, estes são os dados:

```python
temperatura_13_04_2021 = [21, 19, 19, 18, 23, 27, 31, 33, 34, 28, 23, 26] # temperatura em °C
temperatura_29_04_2021 = [21, 19, 18, 15, 21, 26, 29, 30, 30, 24, 23, 21] # temperatura em °C
horario = ['00:00', '02:00', '04:00', '06:00', '08:00', '10:00', '12:00', '14:00', '16:00', '18:00', '20:00', '22:00']
```

E o gráfico (com poucas edições) é este:

```python
plt.figure(figsize=(12,6))
plt.plot(horario, temperatura_13_04_2021, c='k', marker="o", linewidth=1.5, label="13/04/2021")
plt.plot(horario, temperatura_29_04_2021, c='gray', marker="s", linewidth=1.5, label="29/04/2021")
plt.title("Monitoramento da temperatura na cidade de Birigui-SP em diferentes dias do mês de abril/2021")
plt.ylim(14,36)
plt.legend(loc=2)    
plt.show()
```

*Figura 1* - Gráfico de dispersão com linhas para o monitoramento da temperatura na cidade de Birigui-SP em dias diferentes.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-elementos-auxiliares-2/84/elementos-auxiliares-01.png" alt="Gráfico de dispersão com linhas desenhado com o matplotlib para o monitoramento da temperatura na cidade de Birigui-SP em dias diferentes" >
{: .text-center}

<br>

<h2><a style="color:black" id="fill-area-abaixo-curva">Preenchimento da área abaixo da curva</a></h2>

O elemento `fill_between()` requer pelo menos dois parâmetros, onde o primeiro (`x`) é uma sequência com os valores do eixo `x`, e o segundo (`y1`), que também é uma sequência (de mesmo tamanho que a sequência anterior), mas com os valores de `y`, e que define a primeira curva. Utilizando esta forma, a área será preenchida entre os valores passados para `y1` e a reta `y = 0`.
{: .text-justify}

Por exemplo, vamos preencher toda a área abaixo da curva obitida para os dados de temperatura medidos no dia 13/04/2021. Para isto, basta passar `x = horario` e `y1 = temperatura_13_04_2021`, da seguinte forma:
{: .text-justify}

```python
plt.figure(figsize=(12,6))
plt.plot(horario, temperatura_13_04_2021, c='k', marker="o", linewidth=1.5, label="13/04/2021")
plt.title("Monitoramento da temperatura na cidade de Birigui-SP em diferentes dias do mês de abril/2021")
plt.fill_between(x=horario, y1=temperatura_13_04_2021)
plt.legend(loc=2)    
plt.show()
```

*Figura 2* - Gráfico de dispersão com linhas para o monitoramento da temperatura na cidade de Birigui-SP em dias diferentes.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-elementos-auxiliares-2/84/elementos-auxiliares-02.png" alt="Gráfico de dispersão com linhas desenhado com o matplotlib para o monitoramento da temperatura na cidade de Birigui-SP em dias diferentes" >
{: .text-center}

<br>

<h2><a style="color:black" id="fill-area-entre-curvas">Preenchimento entre duas curvas</a></h2>

Também é possível passar um terceiro parâmetro (`y2`), que também deve ser uma sequência (uma sequência com o mesmo número de elementos que a sequência anterior ou um número inteiro) com os valores da segunda linha, sendo o padrão `y2 = 0` (que foi utilizado no tópico acima).
{: .text-justify}

Por exemplo, para preencher a área entre os dois dias monitorados, basta passar o primeiro dia para o parâmetro `y1`, e o segundo dia para o parâmetro `y2`, da seguinte forma:
{: .text-justify}

```python
plt.figure(figsize=(12,6))
plt.plot(horario, temperatura_13_04_2021, c='k', marker="o", linewidth=1.5, label="13/04/2021")
plt.title("Monitoramento da temperatura na cidade de Birigui-SP em diferentes dias do mês de abril/2021")
plt.fill_between(x=horario, y1=temperatura_13_04_2021, y2=temperatura_29_04_2021 )
plt.legend(loc=2)    
plt.show()
```

*Figura 3* - Gráfico de dispersão com linhas para o monitoramento da temperatura na cidade de Birigui-SP em dias diferentes.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-elementos-auxiliares-2/84/elementos-auxiliares-03.png" alt="Gráfico de dispersão com linhas desenhado com o matplotlib para o monitoramento da temperatura na cidade de Birigui-SP em dias diferentes" >
{: .text-center}

<br>

Observe que, por padrão, o `plt.fill_between()` não desenha linhas. As linhas desenhadas são provenientes do `plt.plot()`. Observe o resultado caso não seja utilizado o `plt.plot()`:
{: .text-justify}

```python
plt.figure(figsize=(12,6))
plt.title("Monitoramento da temperatura na cidade de Birigui-SP em diferentes dias do mês de abril/2021")
plt.fill_between(x=horario, y1=temperatura_13_04_2021, y2=temperatura_29_04_2021)
plt.show()
```

*Figura 4* - Gráfico de dispersão com linhas para o monitoramento da temperatura na cidade de Birigui-SP em dias diferentes.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-elementos-auxiliares-2/84/elementos-auxiliares-04.png" alt="Gráfico de dispersão com linhas desenhado com o matplotlib para o monitoramento da temperatura na cidade de Birigui-SP em dias diferentes" >
{: .text-center}

<br>

<h2><a style="color:black" id="">Edições</a></h2>

O `plt.fill_between()` aceita uma série de parâmetros para a sua edição, sendo possível alterar a cor de preenchimento (`color` ou `facecolor`), inserir linhas (`linestyle`, `linewidth`, `edgecolor`), inserir estilos de preenchimento (`hatch`), adicionar transparência (`alpha`), determinar a ordem de plotagem (`zorder`), inserir nome para legenda (`label`), entre outros, de forma similar ao que temos feito até aqui.
{: .text-justify}

Por exemplo:

```python
plt.figure(figsize=(12,6))
plt.title("Monitoramento da temperatura na cidade de Birigui-SP em diferentes dias do mês de abril/2021")
plt.fill_between(x=horario, y1=temperatura_13_04_2021, y2=temperatura_29_04_2021, edgecolor="k", facecolor="salmon", label="Dirferença de temperatura")
plt.legend(loc=2)
plt.show()
```
*Figura 5* - Gráfico de dispersão com linhas para o monitoramento da temperatura na cidade de Birigui-SP em dias diferentes.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-elementos-auxiliares-2/84/elementos-auxiliares-05.png" alt="Gráfico de dispersão com linhas desenhado com o matplotlib para o monitoramento da temperatura na cidade de Birigui-SP em dias diferentes" >
{: .text-center}

<br>

Outro exemplo:

```python
plt.figure(figsize=(12,6))
plt.title("Monitoramento da temperatura na cidade de Birigui-SP em diferentes dias do mês de abril/2021")
plt.fill_between(x=horario, y1=temperatura_13_04_2021, y2=temperatura_29_04_2021, edgecolor="k", facecolor="none", hatch = "//|", label="Dirferença de temperatura")
plt.legend(loc=2)
plt.show()
```

*Figura 6* - Gráfico de dispersão com linhas para o monitoramento da temperatura na cidade de Birigui-SP em dias diferentes.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-elementos-auxiliares-2/84/elementos-auxiliares-06.png" alt="Gráfico de dispersão com linhas desenhado com o matplotlib para o monitoramento da temperatura na cidade de Birigui-SP em dias diferentes" >
{: .text-center}

<br>


Você encontra maiores detalhes na [documentação](https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.fill_between.html).

<br>

<h2><a style="color:black" id="fill-area-entre-curvasx">Fill between x</a></h2>

Também temos a opção de utilizar o `fill_between()` entre duas curvas na direção do eixo `x`, ao invés da direção do eixo `y`. Para isto, utilizamos o `fill_betweenx()`, de forma muito similar ao `fill_between()`.
{: .text-justify}

A diferença é que precisamos passar os dados de `y` como primeiro parâmetro, e as curvas em `x` para os parâmetros `x1` e `x2`, sendo que o parâmetro `x2` é opcional (padrão `x2=0`).
{: .text-justify}

Para exemplificar, vamos inverter os dados de x e y de temperatura. Ou seja:

```python
plt.figure(figsize=(3,6))
plt.title("Monitoramento da temperatura na cidade de Birigui-SP \n em diferentes dias do mês de abril/2021")
plt.plot(temperatura_13_04_2021, horario, c='k', marker="o", linewidth=1.5, label="13/04/2021")
plt.plot(temperatura_29_04_2021, horario, c='gray', marker="s", linewidth=1.5, label="29/04/2021")
plt.legend(loc=4)
plt.xlabel("Temperatura ($°C$)")
plt.ylabel("Hora de monitoramento ($hora$)")
plt.show()
```

*Figura 7* - Gráfico de dispersão com linhas para o monitoramento da temperatura na cidade de Birigui-SP em dias diferentes - invertido.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-elementos-auxiliares-2/84/elementos-auxiliares-07.png" alt="Gráfico de dispersão com linhas desenhado com o matplotlib para o monitoramento da temperatura na cidade de Birigui-SP em dias diferentes" >
{: .text-center}

<br>

Para preencher entre os dados do dia 13/04/2021 e `x=0`, basta passar apenas os parâmetros `y` e `x1` em `plt.fill_betweenx()`:
{: .text-justify}


```python
plt.figure(figsize=(3,6))
plt.title("Monitoramento da temperatura na cidade de Birigui-SP \n em diferentes dias do mês de abril/2021")
plt.plot(temperatura_13_04_2021, horario, c='k', marker="o", linewidth=1.5, label="13/04/2021")
plt.fill_betweenx(y=horario, x1=temperatura_13_04_2021)
# plt.legend(loc=4)
plt.xlabel("Temperatura ($°C$)")
plt.ylabel("Hora de monitoramento ($hora$)")
plt.show()
```

*Figura 8* - Gráfico de dispersão com linhas para o monitoramento da temperatura na cidade de Birigui-SP em dias diferentes - invertido.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-elementos-auxiliares-2/84/elementos-auxiliares-08.png" alt="Gráfico de dispersão com linhas desenhado com o matplotlib para o monitoramento da temperatura na cidade de Birigui-SP em dias diferentes" >
{: .text-center}

<br>


De forma similar, para preencher entre os dados dos dois dias onde as temperaturas foram observadas (duas curvas):
{: .text-justify}

```python
plt.figure(figsize=(3,6))
plt.title("Monitoramento da temperatura na cidade de Birigui-SP \n em diferentes dias do mês de abril/2021")
plt.plot(temperatura_13_04_2021, horario, c='k', marker="o", linewidth=1.5, label="13/04/2021")
plt.fill_betweenx(y=horario, x1=temperatura_13_04_2021, x2=temperatura_29_04_2021)
plt.legend(loc=4)
plt.xlabel("Temperatura ($°C$)")
plt.ylabel("Hora de monitoramento ($hora$)")
plt.show()
```

*Figura 9* - Gráfico de dispersão com linhas para o monitoramento da temperatura na cidade de Birigui-SP em dias diferentes - invertido.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-elementos-auxiliares-2/84/elementos-auxiliares-09.png" alt="Gráfico de dispersão com linhas desenhado com o matplotlib para o monitoramento da temperatura na cidade de Birigui-SP em dias diferentes" >
{: .text-center}

<br>

Novamente, os pontos e as linhas são provenientes do `plt.plot()`. Caso ele seja removido, obtemos:

```python
plt.figure(figsize=(3,6))
plt.title("Monitoramento da temperatura na cidade de Birigui-SP \n em diferentes dias do mês de abril/2021")
plt.fill_betweenx(y=horario, x1=temperatura_13_04_2021, x2=temperatura_29_04_2021)
# plt.legend(loc=4)
plt.xlabel("Temperatura ($°C$)")
plt.ylabel("Hora de monitoramento ($hora$)")
plt.show()
```

*Figura 10* - Gráfico de dispersão com linhas para o monitoramento da temperatura na cidade de Birigui-SP em dias diferentes - invertido.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-elementos-auxiliares-2/84/elementos-auxiliares-10.png" alt="Gráfico de dispersão com linhas desenhado com o matplotlib para o monitoramento da temperatura na cidade de Birigui-SP em dias diferentes" >
{: .text-center}

<br>

Você encontra maiores detalhes na [documentação](https://matplotlib.org/stable/api/_as_gen/matplotlib.axes.Axes.fill_betweenx.html).

<br>

<form id = "quiz" name = "quiz">

<p><strong>Qual é a principal diferença entre o fill_between e o fill_betweenx?</strong></p>

<input type = "radio" id = "mc" name = "question1" value = "a"> O fill_betweenx preenche a área entre as curvas na direção do eixo x, enquanto que o fill_between preenche área entre as curvas na direção do eixo y.
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "b"> O fill_betweenx preenche a área entre as curvas na direção do eixo y, enquanto que o fill_between preenche área entre as curvas na direção do eixo x.
<p style="font-size: 50%"></p>
<p></p>
<input id = "button" type = "button" class="btn btn--info" value = "Enviar" onclick = "check();">
</form>

<div id = "after_submit">
<p style="font-size: 120%" id = "message"></p>
</div>

<br>

<p style="text-align: center">
  <a href="/Curso-matplotlib-83" class="btn btn--success">Anterior</a>
  <a href="/Curso-matplotlib-85" class="btn btn--success">Próximo</a>
</p>



<script>
function check(){
	var question1 = document.quiz.question1.value;
	var messages = [" 🎉 Correto! 🥳️ <br> ",
  " 😔 Incorreto! <br> O <code>fill_betweenx</code> preenche a área na direção do eixo <code>x</code>, enquanto que o <code>fill_between()</code> preenche a área na direção do eixo <code>y</code>, não o contrário!",
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
