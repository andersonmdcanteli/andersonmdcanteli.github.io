---
title: "Elementos auxiliares (Polígonos)"
data: 2021-08-09
tags: []
header:
  image: "/images/chess.jpg"
  image_description: "Chess pieces"
excerpt: "matplotlib"
locale: "pt-br"
---


<br>

O `patch` disponível para inserir polígonos é o `Polygon`. Este elemento requer apenas 1 parâmetro, que é o parâmetro `xy`, que recebe uma `list` de `list`, onde as `lists` internas devem conter as coordenadas `xy` para cada vértice do polígono (cada `list` interna deve conter dois elementos numéricos). O número de `list` internas irá determinar o número de vértices que o polígono terá.
{: .text-justify}

Por exemplo, a `list` `[[1,1]]` irá desenhar apenas 1 vértice (apenas 1 ponto).

Já a `list` `[[1,1], [2,2]]` irá desenhar dois vértices ligados, o primeiro na coordenada `xy=(1,1)`, e o segundo na coordenada `xy=(2,2)`, formando uma reta.
{: .text-justify}

Já a `list` `[[1,1], [2,2], [3,1]]` irá desenhar três vértices ligados, o primeiro na coordenada `xy=(1,1)`, o segundo na coordenada `xy=(2,2)`, e o terceiro na coordenada `xy=(3,1)`, formando um triângulo.
{: .text-justify}

Já a `list` `[[1,1], [2,2], [3,1], [2, 0.7]]` irá desenhar quatro vértices ligados, o primeiro na coordenada `xy=(1,1)`, o segundo na coordenada `xy=(2,2)`, o terceiro na coordenada `xy=(3,1)`, e o quarto na coordenada `xy=(2,0.7)`, formando uma figura geométrica de 4 lados.
{: .text-justify}

Por exemplo, para desenhar um triângulo, é necessário passar três `lists` internas:

```python
plt.figure(figsize=(8,6))
plt.scatter(x,y)
plt.gca().add_patch(patches.Polygon(xy=([[1,1], [2,2], [3,1]])))
plt.show()
```

*Figura 1* - Gráfico de dispersão com um triângulo inserido.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-elementos-auxiliares-2/81/elementos-auxiliares-01.png" alt="gráfico de dispersão desenhado com matplotlib com um triângulo inserido" >
{: .text-center}

<br>


Para desenhar um polígono de 4 lados, é necessário passar 4 `lists` internas:

```python
plt.figure(figsize=(8,6))
plt.scatter(x,y)
plt.gca().add_patch(patches.Polygon(xy=([[1,1], [2,2], [3,1], [2, 0.7]])))
plt.show()
```

*Figura 2* - Gráfico de dispersão com um polígono inserido.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-elementos-auxiliares-2/81/elementos-auxiliares-02.png" alt="gráfico de dispersão desenhado com matplotlib com um polígono inserido" >
{: .text-center}

<br>

O `patches.Polygon` também aceita o parâmetro `closed`, que recebe um `bool` onde `True` (padrão) indica que o polígono será fechado, e `False` indica que o polígono será aberto. Para exemplificar o comportamento, vou inserir cor para as bordas do polígono, e remover o seu preenchimento:
{: .text-justify}

```python
plt.figure(figsize=(8,6))
plt.scatter(x,y)
plt.gca().add_patch(patches.Polygon(xy=([[1,1], [2,2], [3,1], [2, 0.7]]), edgecolor='k', fill=False))
plt.show()
```

*Figura 3* - Gráfico de dispersão com um polígono inserido.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-elementos-auxiliares-2/81/elementos-auxiliares-03.png" alt="gráfico de dispersão desenhado com matplotlib com um polígono inserido" >
{: .text-center}

<br>

Observe que o polígono está fechado, ou seja, as arestas estão todas conectadas. Mas, caso passe o parâmetro `closed = False`, obtemos este outro comportamento:
{: .text-justify}

```python
plt.figure(figsize=(8,6))
plt.scatter(x,y)
plt.gca().add_patch(patches.Polygon(xy=([[1,1], [2,2], [3,1], [2, 0.7]]), edgecolor='k', fill=False, closed=False))
plt.show()
```

*Figura 4* - Gráfico de dispersão com um polígono inserido.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-elementos-auxiliares-2/81/elementos-auxiliares-04.png" alt="gráfico de dispersão desenhado com matplotlib com um polígono inserido" >
{: .text-center}

<br>

De qualquer forma, todas as arestas não precisam estar conectadas para que o polígono seja preenchido:

```python
plt.figure(figsize=(8,6))
plt.scatter(x,y)
plt.gca().add_patch(patches.Polygon(xy=([[1,1], [2,2], [3,1], [2, 0.7]]), edgecolor='k', fill=True, closed=False))
plt.show()
```

*Figura 5* - Gráfico de dispersão com um polígono inserido.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-elementos-auxiliares-2/81/elementos-auxiliares-05.png" alt="gráfico de dispersão desenhado com matplotlib com um polígono inserido" >
{: .text-center}

<br>

<h2><a style="color:black" id="">Edições</a></h2>

O `patches.Polygon` aceita uma série de parâmetros para a sua edição, sendo possível alterar a cor de preenchimento (`color` ou `facecolor`), remover o preenchimento (`fill`), inserir linhas (`linestyle`, `linewidth`, `edgecolor`), inserir estilos de preenchimento (`hatch`), adicionar transparência (`alpha`), determinar a ordem de plotagem (`zorder`), inserir nome para legenda (`label`), entre outros, de forma similar ao que vimos anteriormente.
{: .text-justify}

Você encontra maiores detalhes na [documentação](https://matplotlib.org/stable/api/_as_gen/matplotlib.patches.Polygon.html#matplotlib.patches.Polygon).
{: .text-justify}

<br>

<form id = "quiz" name = "quiz">

<p><strong>Quantos pontos são necessários para inserir um polígono de 8 lados?</strong></p>

<input type = "radio" id = "mc" name = "question1" value = "a"> 7
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "b"> 8
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "c"> 9
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "d"> 6
<p style="font-size: 50%"></p>
<p></p>
<input id = "button" type = "button" class="btn btn--info" value = "Enviar" onclick = "check();">
</form>

<div id = "after_submit">
<p style="font-size: 120%" id = "message"></p>
</div>

<br>

<p style="text-align: center">
  <a href="/Curso-matplotlib-80" class="btn btn--success">Anterior</a>
  <a href="/Curso-matplotlib-82" class="btn btn--success">Próximo</a>
</p>


<script>
function check(){
	var question1 = document.quiz.question1.value;
	var messages = [" Incorreto! 😔 <br> Com 7 pontos conseguimos desenhar um polígono com no máximo 7 lados",
  " 🎉 Correto! 🥳️ <br> Com 8 pontos é possível desenhar um polígono de 8 lados.",
  " 🎉 Correto! 🥳️ <br> Com 9 pontos também é possível desenhar um polígono de 8 lados, entretanto, pelo menos dois pontos devem ser iguais",
  " 😔 Incorreto! <br> Com 6 pontos é possível desenhar um polígono com no máximo 6 lados.",
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
