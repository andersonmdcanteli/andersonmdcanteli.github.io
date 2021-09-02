---
title: "Curso matplotlib - Elementos auxiliares (Anotações)"
data: 2021-08-01
tags: []
header:
  image: "/images/chess.jpg"
  image_description: "Chess pieces"
excerpt: "matplotlib"
locale: "pt-br"
---

<br>

O `plt.annotate()` já foi utilizado anteriormente, mas não foi estudado a fundo. Em geral, esta é a melhor forma de adicionar texto nos gráficos, ***especialmente se o este texto estiver relacionado a algum ponto do gráfico***.
{: .text-justify}

O elemento `plt.annotate()` recebe pelo menos dois parâmetros, sendo o primeiro parâmetro o `text`, que é o texto que será anotado (que deve ser uma `str`), e o segundo é o parâmetro `xy`, que é deve ser uma `tuple` de dois elementos (`int` ou `float`) com os valores de `x` e `y` referentes a posição onde o texto será anotado.
{: .text-justify}

**Por exemplo:**

```python
plt.figure(figsize=(8,6))
plt.scatter(x,y)
plt.annotate("minha anotação", (x[0], y[0]))
plt.show()
```

*Figura 1* - Gráfico de dispersão com texto inserido com o `plt.annotate()`.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-elementos-auxiliares/44/grafico-elementos-auxiliares-01.png" alt="gráfico de dispersão genérico desenhado com o matplotlib, com texto inserido com o plt.annotate()" >
{: .text-center}

<br>

Entretanto, o parâmetro `xy` define onde a anotação *inicia*. O parâmetro utilizado para definir onde o texto é realmente inserido é o parâmetro `xytext`, que também recebe uma `tuple` com as coordenadas `xy`.
{: .text-justify}

Por exemplo, passando o mesmo valor para `xy` e `xytext`, obtemos o mesmo resultado obtido anteriormente (Figura 1):
{: .text-justify}

```python
plt.figure(figsize=(8,6))
plt.scatter(x,y)
plt.annotate("minha anotação", (x[0], y[0]), xytext=(x[0],y[0]))
plt.show()
```

*Figura 2* - Gráfico de dispersão com texto inserido com o `plt.annotate()`.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-elementos-auxiliares/44/grafico-elementos-auxiliares-02.png" alt="gráfico de dispersão genérico desenhado com o matplotlib, com texto inserido com o plt.annotate()" >
{: .text-center}

<br>

Mas ao passar valores diferentes para ```xy``` e ```xytext```, obtemos um comportamento diferente:

```python
plt.figure(figsize=(8,6))
plt.scatter(x,y)
plt.annotate("minha anotação", (x[0], y[0]), xytext=(x[0] + 0.3,y[0] + 0.5))
plt.show()
```

*Figura 3* - Gráfico de dispersão com texto inserido com o `plt.annotate()`.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-elementos-auxiliares/44/grafico-elementos-auxiliares-03.png" alt="gráfico de dispersão genérico desenhado com o matplotlib, com texto inserido com o plt.annotate()" >
{: .text-center}

<br>


<h2><a style="color:black" id="anotacoes-setas">Annotações com setas</a></h2>


Este espaço "vazio" é importante para a adição de elementos entre os pontos definidos como `xy` e `xytext`. Por exemplo, podemos adicionar uma seta dentro de `plt.annotate()`, passando o parâmetro `arrowprops`.
{: .text-justify}

Este parâmetro recebe um `dict` com uma série de `keys` para inserir a seta. Para alterar a espessura dessa seta, passamos um número (`int` ou `float`) através da `key` `width`:
{: .text-justify}

```python
plt.figure(figsize=(8,6))
plt.scatter(x,y)
plt.annotate("minha anotação", (x[0], y[0]), xytext=(x[0] + 0.3,y[0] + 0.5),  
             arrowprops={'width': 2})
plt.show()
```

*Figura 4* - Gráfico de dispersão com texto com flecha inserido com o `plt.annotate()`.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-elementos-auxiliares/44/grafico-elementos-auxiliares-04.png" alt="gráfico de dispersão genérico desenhado com o matplotlib, com texto com flecha inserido com o plt.annotate()" >
{: .text-center}

<br>

<h3><a style="color:black" id="espessura-ponta-seta">Espessura da ponta da seta</a></h3>


Para alterar a espessura da cabeça da seta, passamos um número (`int` ou `float`) para a `key` `headwidth`:
{: .text-justify}

```python
plt.figure(figsize=(8,6))
plt.scatter(x,y)
plt.annotate("minha anotação", (x[0], y[0]), xytext=(x[0] + 0.3,y[0] + 0.5),  
             arrowprops={'width': 2, 'headwidth': 20})
plt.show()
```

*Figura 5* - Gráfico de dispersão com texto com flecha inserido com o `plt.annotate()`.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-elementos-auxiliares/44/grafico-elementos-auxiliares-05.png" alt="gráfico de dispersão genérico desenhado com o **matplotlib**, com texto com flecha inserido com o plt.annotate()" >
{: .text-center}

<br>

<h3><a style="color:black" id="comprimento-ponta-seta">Comprimento da ponta seta</a></h3>

Para alterar o comprimento da cabeça da seta, passamos um número (`int` ou `float`) para a `key` `headlength`:
{: .text-justify}

```python
plt.figure(figsize=(8,6))
plt.scatter(x,y)
plt.annotate("minha anotação", (x[0], y[0]), xytext=(x[0] + 0.3,y[0] + 0.5),  
             arrowprops={'width': 2, 'headwidth': 20, 'headlength': 20})
plt.show()
```

*Figura 6* - Gráfico de dispersão com texto com flecha inserido com o `plt.annotate()`.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-elementos-auxiliares/44/grafico-elementos-auxiliares-06.png" alt="gráfico de dispersão genérico desenhado com o matplotlib, com texto com flecha inserido com o plt.annotate()" >
{: .text-center}

<br>

<h3><a style="color:black" id="espacamento-seta">Espaçamento entre o início e fim da seta</a></h3>

Podemos ainda adicionar um espaçamento nos limites do elemento, de forma a evitar que a seta fique exatamente em cima do ponto. Fazemos isso passando um número (`int` ou `float`) para a `key` `shrink`:
{: .text-justify}

```python
plt.figure(figsize=(8,6))
plt.scatter(x,y)
plt.annotate("minha anotação", (x[0], y[0]), xytext=(x[0] + 0.3,y[0] + 0.5),  
             arrowprops={'width': 2, 'headwidth': 20, 'headlength': 20, 'shrink': 0.1,})
plt.show()
```

*Figura 7* - Gráfico de dispersão com texto com flecha inserido com o `plt.annotate()`.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-elementos-auxiliares/44/grafico-elementos-auxiliares-07.png" alt="gráfico de dispersão genérico desenhado com o **matplotlib**, com texto com flecha inserido com o plt.annotate()" >
{: .text-center}

<br>

<h3><a style="color:black" id="outras-edicoes">Outras edições</a></h3>

Para alterar a cor, espessura da linha, estilo de linha, etc, utilizamos os parâmetros normalmente que vimos anteriormente, como o `facecolor`, `linestyle`,`linewidth`, etc. Por exemplo:
{: .text-justify}

```python
plt.figure(figsize=(8,6))
plt.scatter(x,y)
plt.annotate("minha anotação", (x[0], y[0]), xytext=(x[0] + 2,y[0] + 1.5),  
             arrowprops={'width': 1, 'headwidth': 20, 'headlength': 20, 'shrink': 0.01,
                         'facecolor': 'k', 'linewidth': 2, 'linestyle': ':'})
plt.show()
```


*Figura 8* - Gráfico de dispersão com texto com flecha inserido com o `plt.annotate()`.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-elementos-auxiliares/44/grafico-elementos-auxiliares-08.png" alt="gráfico de dispersão genérico desenhado com o **matplotlib**, com texto com flecha inserido com o plt.annotate()" >
{: .text-center}

<br>


<h2><a style="color:black" id="estilos-pre-definidos">Estilos pré definidos</a></h2>

Temos a opção de passar a `key` `arrowstyle` que tem uma série de `values` pré-definidos com estilos. Entretanto, ao utilizar esta `key`, ***não*** podemos passar as `key` `widht`, `headwidht`, `headlength` e `shrink`.
{: .text-justify}

Por exemplo:

```python
plt.figure(figsize=(8,6))
plt.scatter(x,y)
plt.annotate("minha anotação", (x[0], y[0]), xytext=(x[0] + .3, y[0] + 0.5),  
             arrowprops={'arrowstyle': '-['})
plt.show()
```

*Figura 9* - Gráfico de dispersão com texto com flecha inserido com o `plt.annotate()`.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-elementos-auxiliares/44/grafico-elementos-auxiliares-09.png" alt="gráfico de dispersão genérico desenhado com o **matplotlib**, com texto com flecha inserido com o plt.annotate()" >
{: .text-center}

<br>


Todos os estilos disponíveis estão exemplificados na figura abaixo, sendo que o valor anotado é o nome do estilo que deve ser passado como `value` para a `key` `arrowstyle`.
{: .text-justify}

<img src="https://raw.githubusercontent.com/andersonmdcanteli/matplotlib-course/main/auxiliary-scripts/matplotlib-annotate-arrow-styles/arrow_styles.png" alt="estilos de flechas disponíveis em plt.annotate()" width=800>
{: .text-center}

<br>

[Click aqui](https://github.com/andersonmdcanteli/matplotlib-course/blob/main/auxiliary-scripts/matplotlib-annotate-arrow-styles/matplotlib-annotate-arrow-styles.ipynb) para acessar o notebook utilizado para desenhar a imagem acima.
{: .text-justify}


***Um detalhe importante*** ao utilizar a anotação com setas, é a **direção** das setas, especialmente quando queremos que a seta seja paralela aos eixos. Por exemplo:
{: .text-justify}

```python
plt.figure(figsize=(8,6))
plt.scatter(x,y)
plt.annotate("minha anotação", xy=(x[1], y[1]), xytext=(x[2] + .3, y[1]),  
             arrowprops={'arrowstyle': '->'})
plt.show()
```
*Figura 10* - Gráfico de dispersão com texto com flecha inserido com o `plt.annotate()`.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-elementos-auxiliares/44/grafico-elementos-auxiliares-10.png" alt="gráfico de dispersão genérico desenhado com o matplotlib, com texto com flecha inserido com o plt.annotate()" >
{: .text-center}

<br>

Observe que, apesar dos valores de `y` em `xy` e em `xytext` serem os mesmos (`y[1]`) a linha da seta não é paralela ao eixo `x`. Para confirmar isto, vou adicionar uma reta paralela ao eixo `x` em `y[1]`:
{: .text-justify}

```python
plt.figure(figsize=(8,6))
plt.scatter(x,y)
plt.annotate("minha anotação", xy=(x[1], y[1]), xytext=(x[2] + .3, y[1]),  
             arrowprops={'arrowstyle': '->'})
plt.axhline(y=y[1], xmin=0, xmax=1)
plt.show()
```

*Figura 11* - Gráfico de dispersão com texto com flecha inserido com o `plt.annotate()`.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-elementos-auxiliares/44/grafico-elementos-auxiliares-11.png" alt="gráfico de dispersão genérico desenhado com o matplotlib, com texto com flecha inserido com o plt.annotate()" >
{: .text-center}

<br>

Isto acontece pois a seta é direcionada ao ponto `xy` vinda do centro do texto. Como a base do texto é o ponto setado em `xytext`, temos esta pequena inclinação.
{: .text-justify}

Para contornar isto, basta passar o parâmetro `va` (de *vertical alignment*) em `plt.annotate()` como `center`:
{: .text-justify}

```python
plt.figure(figsize=(8,6))
plt.scatter(x,y)
plt.annotate("minha anotação", xy=(x[1], y[1]), xytext=(x[2] + .3, y[1]), va='center',
             arrowprops={'arrowstyle': '->'})
plt.axhline(y=y[1], xmin=0, xmax=1)
plt.show()
```

*Figura 12* - Gráfico de dispersão com texto com flecha inserido com o `plt.annotate()`.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-elementos-auxiliares/44/grafico-elementos-auxiliares-12.png" alt="gráfico de dispersão genérico desenhado com o **matplotlib**, com texto com flecha inserido com o plt.annotate()" >
{: .text-center}

<br>

Maiores detalhes sobre este "problema" nesta [thread no github](https://github.com/matplotlib/matplotlib/issues/9591/).

Mais detalhes na sobre o ```plt.annotate()```na [documentação](https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.annotate.html).

<form id = "quiz" name = "quiz">

<p><strong>Qual é a principal diferença os elementos plt.text() e o plt.annotate()?</strong></p>

<input type = "radio" id = "mc" name = "question1" value = "a"> O <code>plt.text()</code> é utilizado para inserir um texto genérico em uma posição arbitrária do gráfico, enquanto que o <code>plt.annotate()</code> é utilizado para inserir um texto em uma posição em relação a um ponto do gráfico.
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "b"> O <code>plt.annotate()</code> é utilizado para inserir apenas números, enquanto que o <code>plt.text()</code> é utilizado para inserir apenas texto.
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "c"> O <code>plt.annotate()</code> é utilizado para inserir um texto genérico em uma posição arbitrária do gráfico, enquanto que o <code>plt.text()</code> é utilizado para inserir um texto em uma posição em relação a um ponto do gráfico.
<p style="font-size: 50%"></p>
<p></p>
<input id = "button" type = "button" class="btn btn--info" value = "Enviar" onclick = "check();">
</form>

<div id = "after_submit">
<p style="font-size: 120%" id = "message"></p>
</div>


<br>

<p style="text-align: center">
  <a href="/Curso-matplotlib-43" class="btn btn--success">Anterior</a>
  <a href="/Curso-matplotlib-45" class="btn btn--success">Próximo</a>
</p>


<script>
function check(){
	var question1 = document.quiz.question1.value;
	var messages = [" 🥳️ Correto! 🎉  <br> Esta realmente é a principal diferença entre estes dois métodos",
  " 😔 Incorreto! <br> Tanto o <code>plt.text()</code> como o <code>plt.annotate()</code> inserem apenas texto. Para inserir um número, é necessário transformar este número em uma <code>str</code> antes.",
  " Incorreto! 😔 <br> O <code>plt.text</code> é utilizado para inserir um texto em uma posição arbitrária no gráfico, enquanto que o <code>plt.annotate()</code> é utilizado para inserir um texto em uma posição em relação a um ponto do gráfico.  ",

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
