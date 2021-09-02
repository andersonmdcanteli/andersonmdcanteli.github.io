---
title: "Legendas (Marcadores)"
data: 2021-08-08
tags: []
header:
  image: "/images/chess.jpg"
  image_description: "Chess pieces"
excerpt: "matplotlib"
locale: "pt-br"
---

<br>


<h2><a style="color:black" id="numero-colunas">Número de colunas</a></h2>

O número de colunas dentro da legenda pode ser controlado através do parâmetro `ncol`, que recebe um número (`int`) maior do que `0` (padrão é `1`). Por exemplo, para deixar a legenda com duas colunas, basta passar `ncol = 2`.
{: .text-justify}

```python
plt.figure(figsize=(8,6))
plt.scatter(cachorro_peso, cachorro_altura, label="Cachorros")
plt.scatter(gatos_peso, gatos_altura, label="Gatos")
plt.plot(pinguins_peso, pinguins_altura, marker="o", c="g", label="Pinguins")
plt.xlabel("Peso (kg)")
plt.ylabel("Altura (cm)")
plt.title("Relação entre peso e altura de diferentes animais")
plt.ylim([0,125])
plt.legend(ncol=2)
plt.show()
```

*Figura 1* - Legendas com o número de colunas alterado.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/legendas/63/legendas-01.png" alt="gráfico de dispersão combinado com gráfico de linhas desenhado com matplotlib, com o número de colunas alterado." >
{: .text-center}

<br>

Observe que se o valor passado para `ncol` for maior do que o número de `labels` inseridos, o número de colunas será igual a número total de `labels` inseridos.
{: .text-justify}

Por exemplo, caso `ncol=40`, obtemos apenas 3 colunas:

```python
plt.figure(figsize=(8,6))
plt.scatter(cachorro_peso, cachorro_altura, label="Cachorros")
plt.scatter(gatos_peso, gatos_altura, label="Gatos")
plt.plot(pinguins_peso, pinguins_altura, marker="o", c="g", label="Pinguins")
plt.xlabel("Peso (kg)")
plt.ylabel("Altura (cm)")
plt.title("Relação entre peso e altura de diferentes animais")
plt.ylim([0,125])
plt.legend(ncol=40)
plt.show()
```

*Figura 2* - Legendas com o número de colunas alterado.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/legendas/63/legendas-02.png" alt="gráfico de dispersão combinado com gráfico de linhas desenhado com matplotlib, com o número de colunas alterado." >
{: .text-center}

<br>


<h2><a style="color:black" id="numero-marcadores">Número de marcadores</a></h2>

É possível determinar o número de marcadores que são inseridos na legenda. O parâmetro que deve ser utilizado para realizar esta alteração, depende do tipo de método que foi utilizado para desenhar o gráfico.
{: .text-justify}

<h3><a style="color:black" id="plt-plot">plt.plot()</a></h3>

O número de marcadores dentro da legenda é controlado através do parâmetro `numpoints`, passando um `int` maior do que `0` (padrão é `1`).
{: .text-justify}

Por exemplo, para alterar o número de pontos para 3:
{: .text-justify}

```python
plt.figure(figsize=(8,6))
plt.scatter(cachorro_peso, cachorro_altura, label="Cachorros")
plt.scatter(gatos_peso, gatos_altura, label="Gatos")
plt.plot(pinguins_peso, pinguins_altura, marker="o", c="g", label="Pinguins")
plt.xlabel("Peso (kg)")
plt.ylabel("Altura (cm)")
plt.title("Relação entre peso e altura de diferentes animais")
plt.ylim([0,125])
plt.legend(ncol=2, numpoints=3)
plt.show()
```

*Figura 3* - Legendas com o número de marcadores alterado.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/legendas/63/legendas-03.png" alt="gráfico de dispersão combinado com gráfico de linhas desenhado com matplotlib, com o número de marcadores alterado." >
{: .text-center}

<br>

Observe que apenas a legenda referente aos Pinguins, que foi criada utilizando o `plt.plot()`, teve o número de pontos alterado para 3, enquanto que as demais seguem com apenas um marcador na legenda.
{: .text-justify}

<h3><a style="color:black" id="plt-scatter">plt.scatter()</a></h3>


O número de marcadores dentro da legenda é controlado através do parâmetro `scatterpoints`, passando um `int` maior do que `0` (padrão é `1`).
{: .text-justify}

```python
plt.figure(figsize=(8,6))
plt.scatter(cachorro_peso, cachorro_altura, label="Cachorros")
plt.scatter(gatos_peso, gatos_altura, label="Gatos")
plt.plot(pinguins_peso, pinguins_altura, marker="o", c="g", label="Pinguins")
plt.xlabel("Peso (kg)")
plt.ylabel("Altura (cm)")
plt.title("Relação entre peso e altura de diferentes animais")
plt.ylim([0,125])
plt.legend(ncol=2, scatterpoints=3)
plt.show()
```

*Figura 4* - Legendas com o número de marcadores alterado.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/legendas/63/legendas-04.png" alt="gráfico de dispersão combinado com gráfico de linhas desenhado com matplotlib, com o número de marcadores alterado." >
{: .text-center}

<br>

Observe que a legenda referente aos Gatos e aos Cachorros, que foi criada utilizando o `plt.scatter()`, teve o número de pontos alterado para 3.
{: .text-justify}

<h3><a style="color:black" id="plt-scatter-plot">plt.scatter() e plt.plot()</a></h3>

É possível utilizar o `scatterpoints`e o `numpoints` ao mesmo tempo, e com valores diferentes. Dessa forma, é possível alterar o número de marcadores dos elementos criados com o `plt.scatter()` e com o `plt.plot()`.
{: .text-justify}

```python
plt.figure(figsize=(8,6))
plt.scatter(cachorro_peso, cachorro_altura, label="Cachorros")
plt.scatter(gatos_peso, gatos_altura, label="Gatos")
plt.plot(pinguins_peso, pinguins_altura, marker="o", c="g", label="Pinguins")
plt.xlabel("Peso (kg)")
plt.ylabel("Altura (cm)")
plt.title("Relação entre peso e altura de diferentes animais")
plt.ylim([0,125])
plt.legend(ncol=2, scatterpoints=3, numpoints=2)
plt.show()
```

*Figura 5* - Legendas com o número de marcadores alterado.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/legendas/63/legendas-05.png" alt="gráfico de dispersão combinado com gráfico de linhas desenhado com matplotlib, com o número de marcadores alterado." >
{: .text-center}

<br>

<h2><a style="color:black" id="offset-marcadores">Offset dos marcadores</a></h2>

É possível controlar a distância vertical dos marcadores dentro da legenda, o que é feito através do parâmetro `scatteryoffsets`. Este parâmetro deve receber uma sequência (`list`, `tuple`, `ndarray`, etc) contendo números do tipo `float` com valores entre `0.0` e `1.0` (padrão é `[0.375, 0.5, 0.3125]`).
{: .text-justify}

Por exemplo, para deixar todos os marcadores na mesma altura, basta passar um único valor através de uma `list` (`[0.5]`).
{: .text-justify}

```python
plt.figure(figsize=(8,6))
plt.scatter(cachorro_peso, cachorro_altura, label="Cachorros")
plt.scatter(gatos_peso, gatos_altura, label="Gatos")
plt.plot(pinguins_peso, pinguins_altura, marker="o", c="g", label="Pinguins")
plt.xlabel("Peso (kg)")
plt.ylabel("Altura (cm)")
plt.title("Relação entre peso e altura de diferentes animais")
plt.ylim([0,125])
plt.legend(ncol=2, scatterpoints=3, numpoints=2, scatteryoffsets=[0.5])
plt.show()
```

*Figura 6* - Legendas com a posição dos marcadores alterada.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/legendas/63/legendas-06.png" alt="gráfico de dispersão combinado com gráfico de linhas desenhado com matplotlib, com a posição dos marcadores alterada." >
{: .text-center}

<br>

Para variar estas distâncias, basta passar valores distintos em cada elemento da `list` passada. Por exemplo:
{: .text-justify}

```python
plt.figure(figsize=(8,6))
plt.scatter(cachorro_peso, cachorro_altura, label="Cachorros")
plt.scatter(gatos_peso, gatos_altura, label="Gatos")
plt.plot(pinguins_peso, pinguins_altura, marker="o", c="g", label="Pinguins")
plt.xlabel("Peso (kg)")
plt.ylabel("Altura (cm)")
plt.title("Relação entre peso e altura de diferentes animais")
plt.ylim([0,125])
plt.legend(ncol=2, scatterpoints=3, numpoints=2, scatteryoffsets=[0.2, 0.5, 0.9])
plt.show()
```

*Figura 7* - Legendas com a posição dos marcadores alterada.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/legendas/63/legendas-07.png" alt="gráfico de dispersão combinado com gráfico de linhas desenhado com matplotlib, com a posição dos marcadores alterada." >
{: .text-center}

<br>


Observe que a legenda referente aos Gatos e aos Cachorros, que foi criada utilizando o `plt.scatter()`, teve a posição alterada, enquanto que a legenda referente aos Pinguins, que foi criada utilizando o `plt.plot()`, não teve mudança.
{: .text-justify}

<h2><a style="color:black" id="escala-marcadores">Escala dos marcadores</a></h2>

Podemos controlar a escala relativa dos marcadores dentro da legenda em relação ao tamanho original, o que é feito através do parâmetro `markerscale`. Este parâmetro que deve receber um número (`float` ou `int`), sendo que o valor padrão é `1.0`.
{: .text-justify}

```python
plt.figure(figsize=(8,6))
plt.scatter(cachorro_peso, cachorro_altura, label="Cachorros")
plt.scatter(gatos_peso, gatos_altura, label="Gatos")
plt.plot(pinguins_peso, pinguins_altura, marker="o", c="g", label="Pinguins")
plt.xlabel("Peso (kg)")
plt.ylabel("Altura (cm)")
plt.title("Relação entre peso e altura de diferentes animais")
plt.ylim([0,125])
plt.legend(ncol=2, markerscale=2.5)
plt.show()
```

*Figura 8* - Legendas com o tamanho dos marcadores alterada.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/legendas/63/legendas-08.png" alt="gráfico de dispersão combinado com gráfico de linhas desenhado com matplotlib, com o tamanho dos marcadores alterada." >
{: .text-center}

<br>

<h2><a style="color:black" id="posicao-marcadores-label">Posição dos marcadores em relação ao label</a></h2>

É possível alterar a posição em que o marcador é desenhado na legenda em relação ao `label`, o que é feito através do parâmetro `markerfirst`, que deve receber um valor `bool` (`True` (padrão) ou `False`).
{: .text-justify}

* Caso `markerfirst = True` (padrão) o marcador é desenhado à esquerda do texto da legenda;
* Caso `markerfirst = False` o marcador é desenhado à direita do texto da legenda;

Por exemplo, para deixar o marcador do lado esquerdo do label, basta passar `markerfirst = False`:
{: .text-justify}

```python
plt.figure(figsize=(8,6))
plt.scatter(cachorro_peso, cachorro_altura, label="Cachorros")
plt.scatter(gatos_peso, gatos_altura, label="Gatos")
plt.plot(pinguins_peso, pinguins_altura, marker="o", c="g", label="Pinguins")
plt.xlabel("Peso (kg)")
plt.ylabel("Altura (cm)")
plt.title("Relação entre peso e altura de diferentes animais")
plt.ylim([0,125])
plt.legend(ncol=2, markerfirst=False)
plt.show()
```

*Figura 9* - Legendas com a posição dos marcadores em relação aos labels alterada.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/legendas/63/legendas-09.png" alt="gráfico de dispersão combinado com gráfico de linhas desenhado com matplotlib, com a posição dos marcadores em relação aos labels alterada." >
{: .text-center}

<br>

<form id = "quiz" name = "quiz">

<p><strong>Qual parâmetro deve ser passado para aumentar o número de colunas das legendas para 2?</strong></p>

<input type = "radio" id = "mc" name = "question1" value = "a"> <code>num_cols=2</code>
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "b"> <code>ncol=2</code>
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "c"> <code>ncol="2"</code>
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "d"> <code>num_col=2</code>
<p style="font-size: 50%"></p>
<p></p>
<input id = "button" type = "button" class="btn btn--info" value = "Enviar" onclick = "check();">
</form>

<div id = "after_submit">
<p style="font-size: 120%" id = "message"></p>
</div>


<br>

<p style="text-align: center">
  <a href="/Curso-matplotlib-62" class="btn btn--success">Anterior</a>
  <a href="/Curso-matplotlib-64" class="btn btn--success">Próximo</a>
</p>




<script>
function check(){
	var question1 = document.quiz.question1.value;
	var messages = [" Incorreto! 😔 <br> Não temos um parâmetro <code>num_cols</code> em <code>plt.legend()</code>",
  " 🎉 Correto! 🥳️ <br> Devemos passar um número <code>int</code> para o <code>ncol</code> em <code>plt.legend()</code> para controlar o número de colunas das legendas.",
  " 😔 Incorreto 😔!  <br> O parâmetro <code>ncol</code> deve receber um número <code>int</code>, e não uma <code>str</code>.",
  " Incorreto! 😔 <br> Não temos um parâmetro <code>num_cols</code> em <code>plt.legend()</code>",
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
