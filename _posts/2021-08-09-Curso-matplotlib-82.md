---
title: "Elementos auxiliares (Círculo)"
data: 2021-08-09
tags: []
header:
  image: "/images/chess.jpg"
  image_description: "Chess pieces"
excerpt: "matplotlib"
locale: "pt-br"
---


<br>

O `patch` disponível para inserir círculos é o `Circle`. É necessário passar apenas o parâmetro `xy` para desenhar esta forma, que recebe uma `tuple` com dois números, que são as coordenadas do centro do círculo. Por exemplo, para inserir um círculo em `x = 2` e `y = 2`:
{: .text-justify}

```python
plt.figure(figsize=(8,6))
plt.scatter(x,y)
plt.gca().add_patch(patches.Circle(xy=(2,2)))
plt.show()
```

*Figura 1* - Gráfico de dispersão com um círculo inserido.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-elementos-auxiliares-2/82/elementos-auxiliares-01.png" alt="gráfico de dispersão desenhado com matplotlib com um círculo inserido" >
{: .text-center}

<br>

Observe que o círculo *não ficou perfeito*, o que ocorreu devido ao número de pixels utilizados em um eixo, comparado ao outro eixo. Neste exemplo, temos que os valores de `x` e `y` tem o mesmo *range*. Entretanto, a figura esta sendo criada mais larga (eixo `x`) do que alta (eixo `y`), e.g. `figsize=(8,6)`. Dessa forma, existe um incompatibilidade entre os pixels do eixo `x` e do eixo `y`, o que faz com que o círculo fique visualmente distorcido, e seja renderizado de forma ovalada.
{: .text-justify}

Para contornar este problema, temos algumas opções. A primeira delas, é utilizar uma figura de altura e largura iguais. Por exemplo:
{: .text-justify}

```python
plt.figure(figsize=(6,6))
plt.scatter(x,y)
plt.gca().add_patch(patches.Circle(xy=(2,2)))
plt.show()
```

*Figura 2* - Gráfico de dispersão com um círculo inserido.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-elementos-auxiliares-2/82/elementos-auxiliares-02.png" alt="gráfico de dispersão desenhado com matplotlib com um círculo inserido" >
{: .text-center}

<br>

Uma outra alternativa, é adicionar o método `plt.axis()` (que será estudado com mais detalhes um pouco a frente) e passar a `str` `"equal"` para este método, o que vai forçar a renderização de forma correta:
{: .text-justify}

```python
plt.figure(figsize=(8,6))
plt.scatter(x,y)
plt.gca().add_patch(patches.Circle(xy=(2,2)))
plt.axis("equal")
plt.show()
```

*Figura 3* - Gráfico de dispersão com um círculo inserido.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-elementos-auxiliares-2/82/elementos-auxiliares-03.png" alt="gráfico de dispersão desenhado com matplotlib com um círculo inserido" >
{: .text-center}

<br>

Mas observe que agora a faixa do eixo `x` é maior do que a faixa do eixo `y`, sendo este o resultado da aplicação do `plt.axis("equal")`.
{: .text-justify}

A outra opção é desenhar uma elipse com formato de círculo (veremos em seguida como fazer).
{: .text-justify}


<h2><a style="color:black" id="">Raio do círculo</a></h2>

Para determinar qual o raio o círculo terá, basta passar um número (`int` ou `float`) para o parâmetro `radius`. Por padrão, `radius=5`. Por exemplo, para desenhar um círculo de raio `1`:
{: .text-justify}

```python
plt.figure(figsize=(8,6))
plt.scatter(x,y)
plt.gca().add_patch(patches.Circle(xy=(2,2), radius=1))
plt.axis("equal")
plt.show()
```

*Figura 4* - Gráfico de dispersão com um círculo inserido com raio igual a 1.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-elementos-auxiliares-2/82/elementos-auxiliares-04.png" alt="gráfico de dispersão desenhado com matplotlib com um círculo inserido com raio igual a 1" >
{: .text-center}

<br>

<h2><a style="color:black" id="">Edições</a></h2>

O `patches.Circle` aceita uma série de parâmetros para a sua edição, sendo possível alterar a cor de preenchimento (`color` ou `facecolor`), remover o preenchimento (`fill`), inserir linhas (`linestyle`, `linewidth`, `edgecolor`), inserir estilos de preenchimento (`hatch`), adicionar transparência (`alpha`), determinar a ordem de plotagem (`zorder`), inserir nome para legenda (`label`), entre outros, de forma muito similar ao que temos feito até aqui.
{: .text-justify}

Você encontra maiores detalhes na [documentação](https://matplotlib.org/stable/api/_as_gen/matplotlib.patches.Circle.html#matplotlib.patches.Circle).

<br>

<form id = "quiz" name = "quiz">

<p><strong>Qual informação deve ser passada para o parâmetro xy?</strong></p>

<input type = "radio" id = "mc" name = "question1" value = "a"> raio do círculo e espessura da linha, respectivamente
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "b"> a posição de x e y do centro do círculo, respectivamente
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "c"> a posição y e x do centro do círculo, respectivamente
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "d"> os valores de espessura e largura do círculo, respectivamente
<p style="font-size: 50%"></p>
<p></p>
<input id = "button" type = "button" class="btn btn--info" value = "Enviar" onclick = "check();">
</form>

<div id = "after_submit">
<p style="font-size: 120%" id = "message"></p>
</div>

<br>

<p style="text-align: center">
  <a href="/Curso-matplotlib-81" class="btn btn--success">Anterior</a>
  <a href="/Curso-matplotlib-83" class="btn btn--success">Próximo</a>
</p>


<script>
function check(){
	var question1 = document.quiz.question1.value;
	var messages = [" Incorreto! 😔 <br> o raio do círculo é controlado através do parâmetro <code>radius</code>, enquanto que a espessura da linha é controlada através do parâmetro <code>linewidth</code>.",
  " 🎉 Correto! 🥳️ <br> ",
  " Incorreto! 😔  <br> O correto é passar a posição do eixo x primeiro, depois a posição do eixo y.",
  " 😔 Incorreto! <br> O elemento de círculo não tem parâmetros referentes a largura e a espessura do círculo.",
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
