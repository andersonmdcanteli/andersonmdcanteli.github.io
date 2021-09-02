---
title: "Elementos auxiliares (Elipse)"
data: 2021-08-09
tags: []
header:
  image: "/images/chess.jpg"
  image_description: "Chess pieces"
excerpt: "matplotlib"
locale: "pt-br"
---


<br>

Para desenhar uma elipse utilizando o **matplotlib**, podemos utilizar o `patch` `Ellipse`. Este `patch` precisa de pelo menos três parâmetros:
{: .text-justify}

- `xy`: uma `tuple` com dois números (`int` ou `float`) com as coordenadas do centro da elipse;

- `width`: um número (`int` ou `float`) com o comprimento da largura da elipse;

- `height`: um número (`int` ou `float`) com o comprimento da altura da elipse;

Por exemplo:

```python
plt.figure(figsize=(8,6))
plt.scatter(x,y)
plt.gca().add_patch(patches.Ellipse(xy=(2,2), width=1, height=2))
plt.show()
```

*Figura 1* - Gráfico de dispersão com uma elipse.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-elementos-auxiliares-2/83/elementos-auxiliares-01.png" alt="gráfico de dispersão desenhado com matplotlib com uma elipse" >
{: .text-center}

<br>

Observe que, mesmo se `width = height`, não teremos um círculo perfeito como deveria acontecer:

```python
plt.figure(figsize=(8,6))
plt.scatter(x,y)
plt.gca().add_patch(patches.Ellipse(xy=(2,2), width=1, height=1))
plt.show()
```

*Figura 2* - Gráfico de dispersão com uma elipse.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-elementos-auxiliares-2/83/elementos-auxiliares-02.png" alt="gráfico de dispersão desenhado com matplotlib com uma elipse" >
{: .text-center}

<br>

Isto novamente ocorre devido a proporção do eixo `x` em relação ao eixo `y`. Para desenhar um circulo perfeito com a elipse, temos as opções de utilizar eixos com o mesmo tamanho, utilizar o `plt.axis("equal")`, como vimos anteriormente, ou encontrar um valor de proporção para o circulo.
{: .text-justify}

Neste caso, temos que o eixo `x` tem `8` polegadas, e o eixo `y` tem `6` polegadas (`figsize=(8,6)`). Dessa forma, a relação `x/y` é `8/6 = 4/3`. Sendo assim, o eixo `x` é `4/3` mais longo que o eixo `y`. Então baseado nesta informação, podemos relativizar os valores de `widht` e `height`.
{: .text-justify}

Por exemplo, vamos desenhar um círculo com diâmetro de `1.0`, que seja proporcional ao tamanho do gráfico.
{: .text-justify}

Para isto, vou criar a variável `diametro`:

```python
diametro = 1
```

Como o gráfico tem proporção de `4(width)/3(height)`, e foi definido `diametro = 1`, precisamos definir em relação a qual eixo o diâmetro será efetivamente igual a `1`. Vamos supor que seja no eixo `x`, que é o `width`. Logo, o eixo `y`, que é o `height`, deve ser `4/3` o valor de diâmetro. Dessa forma, conseguimos desenhar um círculo com aparência perfeita:
{: .text-justify}

```python
plt.figure(figsize=(8,6))
plt.scatter(x,y)
plt.gca().add_patch(patches.Ellipse(xy=(2,2), width=diametro, height=diametro*4/3))
plt.show()
```

*Figura 3* - Gráfico de dispersão com um circulo feito com uma elipse.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-elementos-auxiliares-2/83/elementos-auxiliares-03.png" alt="gráfico de dispersão desenhado com matplotlib com um circulo feito com uma elipse." >
{: .text-center}

<br>

Observe que, efetivamente, o tamanho do círculo no eixo `x` é maior do que o tamanho do círculo no eixo `y`. Mas como o gráfico também tem esta característica (`figsize=(8,6)`), visualmente temos a impressão de um círculo perfeito.
{: .text-justify}

Para ficar mais óbvio, observe as linhas do grid:

```python
plt.figure(figsize=(8,6))
plt.scatter(x,y)
plt.gca().add_patch(patches.Ellipse(xy=(2,2), width=diametro, height=diametro*4/3))
plt.grid()
plt.show()
```

*Figura 4* - Gráfico de dispersão com um circulo feito com uma elipse.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-elementos-auxiliares-2/83/elementos-auxiliares-04.png" alt="gráfico de dispersão desenhado com matplotlib com um circulo feito com uma elipse." >
{: .text-center}

<br>

Caso queira desenhar um circulo com `height = 1`, basta apenas inverter a lógica:

```python
plt.figure(figsize=(8,6))
plt.scatter(x,y)
plt.gca().add_patch(patches.Ellipse(xy=(2,2), width=diametro*3/4, height=diametro))
plt.show()
```

*Figura 5* - Gráfico de dispersão com um circulo feito com uma elipse.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-elementos-auxiliares-2/83/elementos-auxiliares-05.png" alt="gráfico de dispersão desenhado com matplotlib com um circulo feito com uma elipse." >
{: .text-center}

<br>

Observe agora que, efetivamente, o tamanho do círculo no eixo `y` é maior do que o tamanho do círculo no eixo `x`. Mas como o gráfico também tem esta característica, visualmente temos a impressão de um círculo perfeito.
{: .text-justify}

Para ficar mais óbvio, conte as linhas do grid:

```python
plt.figure(figsize=(8,6))
plt.scatter(x,y)
plt.gca().add_patch(patches.Ellipse(xy=(2,2), width=diametro*3/4, height=diametro))
plt.grid()
plt.show()
```

*Figura 6* - Gráfico de dispersão com um circulo feito com uma elipse.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-elementos-auxiliares-2/83/elementos-auxiliares-06.png" alt="gráfico de dispersão desenhado com matplotlib com um circulo feito com uma elipse." >
{: .text-center}

<br>

<h2><a style="color:black" id="">Rotação</a></h2>

De forma análoga ao que vimos ao estudar a inserção do `Rectangle`, podemos rotacionar a elipse, passando o ângulo desejado ( `int` ou `float`) para o parâmetro `angle`. Por exemplo:
{: .text-justify}

```python
plt.figure(figsize=(8,6))
plt.scatter(x,y)
plt.gca().add_patch(patches.Ellipse(xy=(2,2), width=1, height=2, angle=45))
plt.show()
```

*Figura 7* - Gráfico de dispersão com um circulo feito com uma elipse.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-elementos-auxiliares-2/83/elementos-auxiliares-07.png" alt="gráfico de dispersão desenhado com matplotlib com um circulo feito com uma elipse." >
{: .text-center}

<br>

<h2><a style="color:black" id="">Edições</a></h2>

O `patches.Ellipse` aceita uma série de parâmetros para a sua edição, sendo possível alterar a cor de preenchimento (`color` ou `facecolor`), remover o preenchimento (`fill`), inserir linhas (`linestyle`, `linewidth`, `edgecolor`), inserir estilos de preenchimento (`hatch`), adicionar transparência (`alpha`), determinar a ordem de plotagem (`zorder`), inserir nome para legenda (`label`), entre outros, de forma análoga ao que temos feito.
{: .text-justify}

Você encontra maiores detalhes na [documentação](https://matplotlib.org/stable/api/_as_gen/matplotlib.patches.Ellipse.html#matplotlib.patches.Ellipse).
{: .text-justify}

<br>

<form id = "quiz" name = "quiz">

<p><strong>Qual a principal diferença entre os parâmetros utilizados para desenhar um Circle e uma Ellipse?</strong></p>

<input type = "radio" id = "mc" name = "question1" value = "a"> Não existe diferença
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "b"> Para desenhar o círculo, precisamos passar o seu raio, enquanto que para desenhar a elipse precisamos passar o comprimento da largura e da altura
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "c"> Para desenhar a elipse, precisamos passar o seu raio, enquanto que para desenhar o círculo precisamos passar o comprimento da largura e da altura
<p style="font-size: 50%"></p>
<p></p>
<input id = "button" type = "button" class="btn btn--info" value = "Enviar" onclick = "check();">
</form>

<div id = "after_submit">
<p style="font-size: 120%" id = "message"></p>
</div>

<br>

<p style="text-align: center">
  <a href="/Curso-matplotlib-82" class="btn btn--success">Anterior</a>
  <a href="/Curso-matplotlib-84" class="btn btn--success">Próximo</a>
</p>


<script>
function check(){
	var question1 = document.quiz.question1.value;
	var messages = [" Incorreto! 😔 <br> Para desenhar um círculo, é necessário passar o raio, enquanto que para desenhar a elipse é necessário passar o comprimento da altura e da largura",
  "  🎉 Correto! 🥳️! <br> ",
  " 😔 Incorreto! <br> A resposta esta invertida! Para desenhar um círculo, é necessário passar o raio, enquanto que para desenhar a elipse é necessário passar o comprimento da altura e da largura",
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
