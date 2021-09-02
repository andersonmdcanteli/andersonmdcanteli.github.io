---
title: "Curso matplotlib - Gráfico de dispersão (editando o tamanho do marcador)"
data: 2021-07-18
tags: []
header:
  image: "/images/chess.jpg"
  image_description: "Chess pieces"
excerpt: "matplotlib"
locale: "pt-br"
---

<br>

Existem basicamente dois motivos para alterar o tamanho padrão dos marcadores. O primeiro é por questões de design, de forma a deixar o marcador de um tamanho adequado para o leitor ter uma boa visualização do gráfico. O segundo é para destacar alguma informação a mais no gráfico. Por exemplo, caso tenha uma segunda variável dependente, é possível deixar o tamanho dos pontos relativo a esta outra variável, aumentando a quantidade de informações contidas no gráfico (gráfico de bolhas). Iremos abordar com detalhes este tipo de gráfico mais a frente.
{: .text-justify}

<h2><a style="color:black" id="">Alterando o tamanho do marcador</a></h2>

<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/generico/banner.png" alt="banner provisório " >
{: .text-center}


O parâmetro que deve ser passado para alterar o tamanho dos marcadores é o parâmetro `s`, que deve receber um número inteiro (`int`) ou decimal (`float`). O tamanho padrão dos marcadores `20`.
{: .text-justify}

Por exemplo, para deixar os macadores menores (do que o padrão), basta passar um número menor do que `20` através do parâmetro `s`:
{: .text-justify}

```python
plt.figure(figsize=(8,6))
plt.scatter(x,y, c='red', s = 10)
plt.show()
```


*Figura 1* - Gráfico de dispersão com o tamanho dos marcadores alterado.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/09/grafico-dispersao-tamanho-marcador-01.png" alt="gráfico de dispersão desenhado utilizando o **matplotlib** com os marcadores com tamanho menor do que o padrão" >
{: .text-center}

<br>

<hr style="height:4px;border:none;color:#333;background-color:#333;" />

<br>

Observe que na célula acima, os valores de `x` e `y` foram passados diretamante para o `plt.scatter()`. Antes, era feito desta forma:
{: .text-justify}

```python
plt.scatter(x=x, y=y)
```

E agora foi feito desta forma:

```python
plt.scatter(x, y)
```

Obtemos o mesmo gráfico, independentemente da forma utilizada. Mas observe que isto funciona pois estou passando os valores de `x` e `y` na ordem ***esperada*** pelo `plt.scatter()`. Caso fosse passado o `y` para primeiro parâmetro e o `x` como segundo parâmetro, desta forma:
{: .text-justify}

```python
plt.scatter(y, x)
```
Os valores de `y` seriam utilizados no eixo `x`, e os valores de `x` seriam utilizados no eixo `y`:
{: .text-justify}

*Figura 2* - Gráfico de dispersão invertido.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/09/grafico-dispersao-tamanho-marcador-01.png" alt="gráfico de dispersão desenhado utilizando o **matplotlib** com os valores de y no lugar eixo x, e os valores de x no eixo y." >
{: .text-center}


Observe a diferença entre a Figura 1 e a Figura 2.

Entretanto, a forma abaixo estaria correta, pois esta sendo efetivamente dito qual parâmetro esta sendo alterado, independentemente da ordem.
{: .text-justify}

```python
plt.scatter(y=y, x=x)
```

Este comportamento acontece pois os parâmetros podem ser passados para uma função na **ordem esperada** ou indicando **explicitament**e para qual parametro a variável esta sendo passada.
{: .text-justify}

<br>

<hr style="height:4px;border:none;color:#333;background-color:#333;" />

<br>

 Para deixar os marcadores maiores (do que o padrão), basta passar um número maior do que `20` para o parãmetro `s`:
{: .text-justify}

```python
plt.figure(figsize=(8,6))
plt.scatter(x,y, c='red', s = 100.1)
plt.show()
```

*Figura 3* - Gráfico de dispersão com o tamanho dos marcadores alterado.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/09/grafico-dispersao-tamanho-marcador-03.png" alt="gráfico de dispersão desenhado utilizando o **matplotlib** com os marcadores com tamanho maior do que o padrão" >
{: .text-center}

<br>

Também podemos passar uma sequência (`list`, `tuple`, `ndarray`, etc) para o parâmetro `s`, onde cada elemento deve ser um número correspondente ao tamanho do marcador. Esta sequência deve ter o *mesmo tamanho* que o número de pontos do gráfico.
{: .text-justify}

Por exemplo, a lista `tamanhos`, contém apenas valores númericos:

```python
tamanhos = [40, 40, 50, 50, 60, 10, 10, 100, 100, 150, 150]
```

Podemos utilizar esta lista (`tamanhos`) para alterar o tamanho de cada marcador, passando ela para o `s`:

```python
plt.figure(figsize=(8,6))
plt.scatter(x,y, c='red', s = tamanhos)
plt.show()
```

*Figura 4* - Gráfico de dispersão com o tamanho dos marcadores alterado utilizando uma lista.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/09/grafico-dispersao-tamanho-marcador-04.png" alt="gráfico de dispersão desenhado utilizando o **matplotlib** com os marcadores variando de tamanho dependendo do valor contido em uma lista" >
{: .text-center}

<br>

Observe que a lista ```tamanhos``` e ```x``` tem o mesmo número de elementos:

```python
len(tamanhos) == len(x)
```

> True

<br>

<form id = "quiz" name = "quiz">

<p><strong>Qual é o tipo de variável que deve ser passado através do parâmetro s para o <code>plt.scatter()</code> para alterar o tamanho do marcador?</strong></p>

<input type = "radio" id = "mc" name = "question1" value = "a"> int
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "b"> float
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "c"> string
<p style="font-size: 50%"></p>
<p></p>
<input id = "button" type = "button" class="btn btn--info" value = "Enviar" onclick = "check();">
</form>

<div id = "after_submit">
<p style="font-size: 120%" id = "message"></p>
</div>



<br>

<p style="text-align: center">
  <a href="/Curso-matplotlib-08" class="btn btn--success">Anterior</a>
  <a href="/Curso-matplotlib-10" class="btn btn--success">Próximo</a>
</p>



<script>
function check(){
	var question1 = document.quiz.question1.value;
	var messages = ["🥳️ Correto! 🎉 <br> Podemos passsar um número inteiro (<code>int</code>) ou um número decimal (<code>float</code>)",
  "🎉 Correto! 🥳️ <br> Podemos passsar número decimal (<code>float</code>) ou um número inteiro (<code>int</code>). ",
  "Incorreto! 😔  <br> Apenas números podem ser utilizados para alterar o tamanho dos marcadores ",
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
