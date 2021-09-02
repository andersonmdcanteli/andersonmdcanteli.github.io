---
title: "Curso matplotlib - Gráfico de dispersão (editando os pontos do gráfico)"
data: 2021-07-17
tags: []
header:
  image: "/images/chess.jpg"
  image_description: "Chess pieces"
excerpt: "matplotlib"
locale: "pt-br"
---



<br>

O **matplotlib** permite a edição dos pontos, ou marcadores, de um gráfico de dispersão de forma bastante simples. Esta edição é feita através de alguns parâmetros que são adicionados em `plt.scatter()`. A edição dos marcadores permite uma melhor representação das informações contidas nos gráficos.
{: .text-justify}

Por exemplo, caso tenhamos dois grupos diferentes, podemos separa-los por cores, facilitando a sua interpretação. Com utilidade similar, também podemos utilizar diferentes marcadores. O tamanho dos marcadores também pode ser utilizado para representar o valor de uma variável que temos em um conjunto de dados (gráfico de bolhas).
{: .text-justify}

<h2><a style="color:black" id="cor-marcadores">Alterando a cor do marcador</a></h2>

<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/generico/banner.png" alt="banner provisório " >
{: .text-center}

Adicionar cores em um gráfico é uma das formas mais eficientes para expressar o que o gráfico deve representar.
{: .text-justify}

Para alterar a cor dos marcadores, devemos passar o parâmetro `color` ou apenas `c`, para o `plt.scatter()`. Este parâmetro deve receber o **nome da cor** em formato de `str`. Por padrão, a cor dos marcadores do gráfico de dispersão é <span style="color: #0000FF">azul</span>.
{: .text-justify}

Por exemplo, para deixar os pontos do gráfico preenchidos na cor preta, devemos utilizar:
{: .text-justify}

```python
plt.figure(figsize=(8,6))
plt.scatter(x=x, y=y, color="black")
plt.show()
```

*Figura 1* - Gráfico de dispersão com marcadores na cor preta.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/08/grafico-dispersao-marcador-preta.png" alt="gráfico de dispersão desenhado utilizando o **matplotlib** com os marcadores na cor preta" >
{: .text-center}

De forma análoga, mas utilizando a abreviação ```c = "black"```:

```python
plt.figure(figsize=(8,6))
plt.scatter(x=x, y=y, c="black")
plt.show()
```

*Figura 2* - Gráfico de dispersão com marcadores na cor preta utilizando o parâmetro `c`.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/08/grafico-dispersao-marcador-preta-2.png" alt="gráfico de dispersão desenhado utilizando o **matplotlib** com os marcadores na cor preta utilizando o parâmetro c ao invés do parâmetro color" >
{: .text-center}


<br>

É através deste parâmetro `c` ou `color` que passamos uma `str` que representa o **nome da cor** desejada para alterar a cor dos marcadores. Para as cores primárias (abaixo), temos opção de utilizar uma abreviação do nome da cor:
{: .text-justify}

<br>

- `"b"` ou `blue` (<span style="color: #0000FF">azul</span>);
- `"g"` ou `green` (<span style="color: #008000">verde</span>);
- `"r"` ou `red` (<span style="color: #FF0000">vermelho</span>);
- `"c"` ou `cyan` (<span style="color: #00FFFF">ciano</span>);
- `"m"` ou `magenta` (<span style="color: #FF00FF">magenta</span>);
- `"y"` ou `yellow` (<span style="color: #FFFF00">amarelo</span>);
- `"k"` ou `black` (<span style="color: #000000">preto</span>);
- `"w"` ou `white` (<span style="color: #FFFFFF">branco</span>).

Por exemplo, para deixar os marcadores com a cor <span style="color: #FF00FF">magenta</span>, basta passar a `str` `'m'` ou `'margenta'`:

```python
plt.figure(figsize=(8,6))
plt.scatter(x=x, y=y, c="m")
plt.show()
```

*Figura 3* - Gráfico de dispersão com marcadores na cor `'m'`.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/08/grafico-dispersao-marcador-magenta.png" alt="gráfico de dispersão desenhado utilizando o **matplotlib** com os marcadores na cor magenta utilizando o parâmetro c" >
{: .text-center}


Para as demais cores podemos utilizar o nome da cor, a representação hexadecimal ou valores de RGB. Uma excelente fonte de exemplo das cores disponíveis com seus respectivos nomes esta apresentado na figura abaixo:
{: .text-justify}


*Figura 4* - Lista de nomes de cores disponíveis para o **matplotlib**.
{: .text-center}
<img style="border: solid 1px black" src="https://matplotlib.org/stable/_images/sphx_glr_named_colors_003.png" alt="lista exemplificando os nomes das cores disponíveis com a respectiva cor ao lado para referência." >
{: .text-center}
Fonte - [documentação matplotlib](https://matplotlib.org/stable/gallery/color/named_colors.html).
{: .text-center}

Para imprimir todos os nomes disponíveis com seus respectivos valores hexadecimais, basta rodar o código abaixo.
{: .text-justify}

```python
import matplotlib
for name, hex in matplotlib.colors.cnames.items():
    print(name, hex)
```

<br>

Também podemos passar uma sequência (`list`, `tuple`, `ndarray`, etc) com diversas cores para alterar cada ponto do gráfico. Cada elemento dessa sequência deve conter uma `str` com o nome da cor desejada para cada ponto. É ***importante ressaltar*** que o tamanho desta sequência deve coincidir com o número de pontos do gráfico.
{: .text-justify}

Por exemplo, a lista `cores` tem, em cada elemento, uma `str` que representa uma cor:

```python
cores = ['k', 'k', 'b', 'b', 'y', 'y', 'm', 'r', 'r', 'g', 'g']
```

Podemos utilizar esta lista para alterar a cor de cada ponto, o que é feito atribuindo a lista `cores` para o parâmetro `c`:

```python
plt.figure(figsize=(8,6))
plt.scatter(x=x, y=y, c=cores)
plt.show()
```

*Figura 5* - Gráfico de dispersão com marcadores desenhados com diversas cores.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/08/grafico-dispersao-muticolorido.png" alt="gráfico de dispersão desenhado utilizando uma lista contendo diversas cores, o que resulta em um gráfico com cada ponto colorido com uma cor diferente" >
{: .text-center}


Observe que o tamanho da lista `cores` é o mesmo da lista `x`.

```python
len(cores) == len(x)
```
> True


<form id = "quiz" name = "quiz">

<p><strong>Qual é o parâmetro utilizado para alterar a cor dos marcadores ao gerar um elemento de plt.scatter()?</strong></p>

<input type = "radio" id = "mc" name = "question1" value = "a"> c
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "b"> cores
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "c"> cafézinho
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "d"> color
<p style="font-size: 50%"></p>
<p></p>
<input id = "button" type = "button" class="btn btn--info" value = "Enviar" onclick = "check();">
</form>

<div id = "after_submit">
<p style="font-size: 120%" id = "message"></p>
</div>

<br>

<p style="text-align: center">
  <a href="/Curso-matplotlib-07" class="btn btn--success">Anterior</a>
  <a href="/Curso-matplotlib-09" class="btn btn--success">Próximo</a>
</p>



<script>
function check(){
	var question1 = document.quiz.question1.value;
	var messages = ["🥳️ Correto! 🎉 <br> Também é possível utilizar o parâmetro <code>color</code>, mas a forma abreviada é mais eficiente!",
  "Incorreto! 😔 <br> O elemento <code>plt.scatter()</code> não tem o parâmetro <code>cores</code>. ",
  "😔 Incorreto!  <br> Apesar de que tomar um café é sempre uma boa ideia, não existe o parâmetro <code>cafézinho</code> em <code>plt.scatter()</code> e em nenhuma outra biblioteca do Python, pois acentos não são aceitos em nomes de variáveis/parâmetros/classes/funções, etc, sendo permitido apenas em <code>str</code>. Além disso, a palavra cafezinho não tem acento.",
  " 🎉 Correto! 🥳️ <br> Também é possível utilizar o parâmetro <code>c</code>, que é mais eficiente!",
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
