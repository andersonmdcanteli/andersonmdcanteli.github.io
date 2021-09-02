---
title: "Elementos auxiliares (Retângulo)"
data: 2021-08-09
tags: []
header:
  image: "/images/chess.jpg"
  image_description: "Chess pieces"
excerpt: "matplotlib"
locale: "pt-br"
---


<br>

O `patch` disponível para inserir um retângulo é o `Rectangle`. Este elemento requer pelo menos três parâmetros:

- `xy`: uma `tuple` com as coordenadas (`int` ou `float`) de `x` e `y` onde o retângulo irá *iniciar*;

- `width`: um número (`int` ou `float`) com a espessura desejada para o retângulo (posição final no eixo `x`);

- `height`: um número (`int` ou `float`) com a altura desejada para o retângulo (posição final no eixo `y`);

Por exemplo, para inserir um retângulo iniciando em `x = 1.5` e `y = 1.5`, com `width = 2` e `height = 1`:
{: .text-justify}

```python
plt.figure(figsize=(8,6))
plt.scatter(x,y)
plt.gca().add_patch(patches.Rectangle(xy=(1.5, 1.5), width=2, height=1))
plt.show()
```

*Figura 1* - Gráfico de dispersão com um retângulo inserido.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-elementos-auxiliares-2/80/elementos-auxiliares-01.png" alt="gráfico de dispersão desenhado com matplotlib com um retângulo inserido" >
{: .text-center}

<br>

Também é possível rotacionar o retângulo em torno do ponto inicial (`xy`), o que é feito passando o ângulo desejado (`int` ou `float`) para o parâmetro `angle` (padrão é `0`). Por exemplo, para rotacionar o retângulo em 45°, basta passar `angle = 45`:
{: .text-justify}

```python
plt.figure(figsize=(8,6))
plt.scatter(x,y)
plt.gca().add_patch(patches.Rectangle(xy=(1.5, 1.5), width=2, height=1, angle=45))
plt.show()
```

*Figura 2* - Gráfico de dispersão com um retângulo rotacionado em 45°.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-elementos-auxiliares-2/80/elementos-auxiliares-02.png" alt="gráfico de dispersão desenhado com matplotlib com um retângulo rotacionado em 45°" >
{: .text-center}

<br>

Observe que a origem do `Rectangle` se manteve inalterada (`xy=(1.5, 1.5)`), e agora a linha da base do `Rectangle` está inclinada em `45°`.
{: .text-justify}

<h2><a style="color:black" id="">Edições</a></h2>

O `patches.Rectangle` aceita uma série de parâmetros para a sua edição, sendo possível alterar a cor de preenchimento (`color` ou `facecolor`), remover o preenchimento (`fill`), inserir linhas (`linestyle`, `linewidth`, `edgecolor`), inserir estilos de preenchimento (`hatch`), adicionar transparência (`alpha`), determinar a ordem de plotagem (`zorder`), inserir nome para legenda (`label`), entre outros, de forma similar ao que temos visto.

Você encontra maiores detalhes na [documentação](https://matplotlib.org/stable/api/_as_gen/matplotlib.patches.Rectangle.html#matplotlib.patches.Rectangle).

<br>

<form id = "quiz" name = "quiz">

<p><strong>Qual a função do parâmetro width em patches.Rectangle?</strong></p>

<input type = "radio" id = "mc" name = "question1" value = "a"> Determinar o comprimento da base do retângulo
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "b"> Determinar o comprimento da altura do retângulo
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "c"> Determinar o ponto inicial do retângulo
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "d"> Determinar a espessura das linhas do retângulo
<p style="font-size: 50%"></p>
<p></p>
<input id = "button" type = "button" class="btn btn--info" value = "Enviar" onclick = "check();">
</form>

<div id = "after_submit">
<p style="font-size: 120%" id = "message"></p>
</div>

<br>

<p style="text-align: center">
  <a href="/Curso-matplotlib-79" class="btn btn--success">Anterior</a>
  <a href="/Curso-matplotlib-81" class="btn btn--success">Próximo</a>
</p>


<script>
function check(){
	var question1 = document.quiz.question1.value;
	var messages = [" 🎉 Correto! 🥳️ ",
  " 😔 Incorreto! <br> A função do parâmetro <code>width</code> é determinar o comprimento da base do retângulo. Para determinar o comprimento da altura do retângulo, deve ser utilizado o parâmetro <code>height</code>.",
  " Incorreto!️ 😔  <br> O ponto inicial do retângulo é determinado pelo parâmetro <code>xy</code>. A função do parâmetro <code>width</code> é determinar o comprimento da base do retângulo.",
  " 😔 Incorreto! 😔 <br> Para determinar a espessura das linhas do retângulo, devemos passar o parâmetro <code>linewidth</code>. ",
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
