---
title: "Curso matplotlib - Elementos de texto"
data: 2021-07-18
tags: []
header:
  image: "/images/chess.jpg"
  image_description: "Chess pieces"
excerpt: "matplotlib"
locale: "pt-br"
---

<br>

Os elementos de texto (legendas e títulos) são muito importantes para um gráfico, pois é através deles que dizemos ao leitor o que cada elemento gráfico representa.
{: .text-justify}

<h2><a style="color:black" id="">Legendas</a></h2>

<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/generico/banner.png" alt="banner provisório " >
{: .text-center}

As legendas são caixas de texto que explicam os elementos dos gráficos. Inserir uma legenda no gráfico criado com o **matplotlib** é muito simples, bastando passar o nome desejado para o parâmetro `label` em `plt.scatter()`. Também precisamos adicionar o `plt.legend()`, que irá efetivamente criar a legenda e adicionar ela a figura criada. Este último parâmetro deve estar posicionado após o `plt.scatter()` e antes de `plt.show()`.
{: .text-justify}


Então, precisamos da seguinte estrutura:

```python
plt.figure()
plt.scatter(label="Nome da legenda")
plt.legend()
plt.show()
```

Por exemplo, caso for adicionado apenas o parâmetro `label` em `plt.scatter()`:

```python
plt.figure(figsize=(8,6))
plt.scatter(x,y, s = 100.1, marker = "D", edgecolors = 'k', facecolors='none',
            label="Raças de cachorros")
plt.show()
```

*Figura 1* - Gráfico de dispersão com legenda não inserida.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/11/grafico-dispersao-legenda-01.png" alt="gráfico de dispersão desenhado utilizando o **matplotlib** com a legenda não inserida" >
{: .text-center}

<br>

obtemos o gráfico sem as legendas. Mas ao adicionar o `plt.legend()` após o `plt.scatter()`, obtemos as legendas corretamente:
{: .text-justify}

```python
plt.figure(figsize=(8,6))
plt.scatter(x,y, s = 100.1, marker = "D", edgecolors = 'k', facecolors='none',
            label="Raças de cachorros")
plt.legend()
plt.show()
```

*Figura 2* - Gráfico de dispersão com legenda.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/11/grafico-dispersao-legenda-02.png" alt="gráfico de dispersão desenhado utilizando o **matplotlib** com legenda" >
{: .text-center}

<br>


Observe que, se o `plt.legend()` estiver antes de `plt.scatter()`, a legenda não será inserida e um aviso será apresentado:
{: .text-justify}

> No handles with labels found to put in legend.

Devemos inserir a legendas apenas ***após*** a criação dos elementos anteriores, como a figura (`plt.figure()`) e o elemento de dispersão (`plt.scatter()`). O `plt.legend()` deve ser adicionado ***antes*** do gráfico ser apresentado (`plt.show()`).
{: .text-justify}


<h2><a style="color:black" id="">Posição das Legendas no gráfico</a></h2>

Podemos especificar o local em que a legenda será inserida no gráfico, o que é feito passando a **posição** desejada através do parâmetro `loc` em `plt.legend()`. Esta posição pode ser definida através de uma `str` ou através de um número `int` que se refere a posição desejada.
{: .text-justify}

Temos 10 posições disponíveis, sendo que a `loc='best'` é a posição padrão:
{: .text-justify}

- `'best`', que corresponde ao código `0`, e a legenda é posicionada na melhor posição definida por um algoritmo (valor padrão);
- `'upper right'`, que corresponde ao código `1`, e a legenda é posicionada no canto superior direito;
- `'upper left'`, que corresponde ao código `2`, e a legenda é posicionada no canto superior esquerdo;
- `'lower left'`, que corresponde ao código `3`, e a legenda é posicionada no canto inferior esquerdo;
- `'lower right'`, que corresponde ao código `4`, e a legenda é posicionada no canto inferior direito;
- `'right'`, que corresponde ao código `5`, e a legenda é posicionada no canto direito;
- `'center left'`, que corresponde ao código `6`, e a legenda é posicionada no centro a esquerda;
- `'center right'`, que corresponde ao código `7`, e a legenda é posicionada no centro a direita;
- `'lower center'`, que corresponde ao código `8`, e a legenda é posicionada no centro inferior;
- `'upper center'`, que corresponde ao código `9`, e a legenda é posicionada no centro superior;
- `'center'`, que corresponde ao código `10`, e a legenda é posicionada no centro do gráfico;

<br>

Visualmente:

<img style="float: center;" src="https://raw.githubusercontent.com/andersonmdcanteli/matplotlib-course/main/auxiliary-scripts/matplotlib-all-legend-positions/legend-positions.png" alt="Gráfico apresentando as posiçoespadrão disponíveis para alocar a legenda" width="800">


O notebook utilizado para desenhar a imagem acima pode ser acessado [clicando aqui](https://github.com/andersonmdcanteli/matplotlib-course/blob/main/auxiliary-scripts/matplotlib-all-legend-positions/matplotlib-legend-positions.ipynb).

Por exemplo, para deixar a legenda no centro do gráfico, podemos utilizar `loc='center'`:

```python
plt.figure(figsize=(8,6))
plt.scatter(x,y, s = 100.1, marker = "D", edgecolors = 'k', facecolors='none',
            label="Raças de cachorros")
plt.legend(loc = 'center')
plt.show()
```

*Figura 3* - Gráfico de dispersão com a legenda posicionada no centro do gráfico.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/11/grafico-dispersao-legenda-03.png" alt="gráfico de dispersão desenhado utilizando o **matplotlib** com a legenda posicionada no centro da imagem" >
{: .text-center}

<br>


Também temos a possibilidade de **especificar a posição** da legenda de forma ***arbitrária***, o que é feito passando uma `tuple` com a posição desejada para `x` e `y`para o parâmetro `bbox_to_anchor` em `plt.legend()`.
{: .text-justify}

```python
plt.legend(bbox_to_anchor=(x,y))
```

Por exemplo, para adicionar a legenda em `x = 0` e `y = 0`:

```python
plt.figure(figsize=(8,6))
plt.scatter(x,y, s = 100.1, marker = "D", edgecolors = 'k', facecolors='none',
            label="Raças de cachorros")
plt.legend(bbox_to_anchor=(0,0))
plt.show()
```

*Figura 4* - Gráfico de dispersão com a legenda posicionada em `x = 0` e `y = 0`.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/11/grafico-dispersao-legenda-04.png" alt="gráfico de dispersão desenhado utilizando o **matplotlib** com a legenda posicionada na origem do gráfico" >
{: .text-center}

<br>


Para alocar a legenda **fora** do gráfico, basta passar valores maiores de 1 para `x` e/ou `y`. Por exemplo, para deixar a legenda no canto superior direito, mas fora do gráfico, podemos deixar `x = 1.02` e `y = 1`:
{: .text-justify}

```python
plt.figure(figsize=(8,6))
plt.scatter(x,y, s = 100.1, marker = "D", edgecolors = 'k', facecolors='none',
            label="Raças de cachorros")
plt.legend(bbox_to_anchor=(1.02,1))
plt.show()
```

*Figura 5* - Gráfico de dispersão com a legenda posicionada em `x = 1.02` e `y = 1`.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/11/grafico-dispersao-legenda-05.png" alt="gráfico de dispersão desenhado utilizando o **matplotlib** com a legenda posicionada fora do gráfico" >
{: .text-center}

<br>

Você encontra mais detalhes sobre o posicionamento das legendas [na documentação](https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.legend.html).



<h2><a style="color:black" id="">Tamanho da fonte da legenda no gráfico</a></h2>


<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/generico/banner.png" alt="banner provisório " >
{: .text-center}


É possível alterar o tamanho da fonte da legenda diretamente em `plt.legend()`. Basta passar um número (`int` ou `float`) para o `plt.legend()` através do parâmetro `fontsize`:

```python
plt.figure(figsize=(8,6))
plt.scatter(x,y, s = 100.1, marker = "D", edgecolors = 'k', facecolors='none',
            label="Raças de cachorros")
plt.legend(bbox_to_anchor=(1.02,1), fontsize=20)
plt.show()
```

*Figura 6* - Gráfico de dispersão com a legenda com tamanho de fonte aumentado.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/11/grafico-dispersao-legenda-06.png" alt="gráfico de dispersão desenhado utilizando o **matplotlib** com o tamanho da fonte da legenda aumentada " >
{: .text-center}

<br>


<form id = "quiz" name = "quiz">

<p><strong>Como adicionar legenda em um gráfico de dispersão no matplotlib?</strong></p>

<input type = "radio" id = "mc" name = "question1" value = "a"> Imprimindo o gráfico e escrevendo com uma caneta
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "b"> Adicionando o <code>plt.legend()</code> após a <code>adição do plt.scatter()</code>
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "c"> Passando o parâmetro <code>label</code> em <code>plt.scatter()</code> com o nome que será utilizado na legenda.
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "d"> Combinando as respostas b e c
<p style="font-size: 50%"></p>
<p></p>
<input id = "button" type = "button" class="btn btn--info" value = "Enviar" onclick = "check();">
</form>

<div id = "after_submit">
<p style="font-size: 120%" id = "message"></p>
</div>


<h2><a style="color:black" id="">Título ao eixo x</a></h2>


<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/generico/banner.png" alt="banner provisório " >
{: .text-center}


Para adicionar um título ao eixo `x`, utilizamos o `plt.xlabel()`, passando como uma `str` o texto que será adicionado ao título do eixo `x`. O `plt.xlabel()` **precisa** estar posicionado **antes** de `plt.show()`:
{: .text-justify}

```python
plt.figure()

...

plt.xlabel()
plt.show()
```

Por exemplo:


```python
plt.figure(figsize=(8,6))
plt.scatter(x,y, s = 100.1, marker = "D", edgecolors = 'k', facecolors='none',
            label="Raças de cachorros")
plt.legend()
plt.xlabel("Peso (kg)")
plt.show()
```

*Figura 7* - Gráfico de dispersão título no eixo `x`.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/11/grafico-dispersao-legenda-07.png" alt="gráfico de dispersão desenhado utilizando o **matplotlib** com título no eixo x" >
{: .text-center}

<br>


É possível alterar o espaçamento entre o eixo `x` e o nome do eixo x, passando um número (que pode ser um `float` ou `int`) através do parâmetro `labelpad`. O valor padrão é `4.0`. Por exemplo:
{: .text-justify}

```python
plt.figure(figsize=(8,6))
plt.scatter(x,y, s = 100.1, marker = "D", edgecolors = 'k', facecolors='none',
            label="Raças de cachorros")
plt.legend()
plt.xlabel("Peso (kg)", labelpad=20.0)
plt.show()
```

*Figura 8* - Gráfico de dispersão com título no eixo `x` com espaçamento.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/11/grafico-dispersao-legenda-08.png" alt="gráfico de dispersão desenhado utilizando o **matplotlib** com título no eixo x com espaçamento" >
{: .text-center}

<br>

É possível alterar a **posição** do título do eixo x através do parâmetro `loc`. Temos três opções:

- `'center'` (padrão): posiciona o título no centro do eixo `x`;
- `'right'`: posiciona o título à direita do eixo `x`;
- `'left'`: posiciona o título à esquerda do eixo `x`;

Por exemplo, para deixar o título do eixo `x` no canto direito basta passar `loc="right"`:

```python
plt.figure(figsize=(8,6))
plt.scatter(x,y, s = 100.1, marker = "D", edgecolors = 'k', facecolors='none',
            label="Raças de cachorros")
plt.legend()
plt.xlabel("Peso (kg)", labelpad=20, loc="right")
plt.show()
```

*Figura 9* - Gráfico de dispersão com título no eixo `x` no canto direito e com espaçamento .
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/11/grafico-dispersao-legenda-09.png" alt="gráfico de dispersão desenhado utilizando o **matplotlib** com título no eixo x no canto direito e com espaçamento" >
{: .text-center}

<br>

Você encontra mais informações na [Documentação](https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.xlabel.html).

<h2><a style="color:black" id="">Título ao eixo y</a></h2>


<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/generico/banner.png" alt="banner provisório " >
{: .text-center}


Para adicionar um título ao eixo `y`, utilizamos o `plt.ylabel()`, passando como uma `str` o texto que será adicionado ao título do eixo `y`. Assim como o `plt.xlabel()`, o `plt.ylabel()` precisa esta posicionado antes de `plt.show()`.
{: .text-justify}

```python
plt.figure()

...

plt.ylabel()
plt.show()
```

Por exemplo:

```python
plt.figure(figsize=(8,6))
plt.scatter(x,y, s = 100.1, marker = "D", edgecolors = 'k', facecolors='none',
            label="Raças de cachorros")
plt.legend()
plt.xlabel("Peso (kg)")
plt.ylabel("Altura (cm)")
plt.show()
```

*Figura 10* - Gráfico de dispersão título no eixo `y`.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/11/grafico-dispersao-legenda-10.png" alt="gráfico de dispersão desenhado utilizando o **matplotlib** com título no eixo y" >
{: .text-center}

<br>

Também é possível alterar o espaçamento entre o eixo `y` e o titulo do eixo `y`, passando um número (`float` ou `int`) através do parâmetro `labelpad`. O valor padrão é `4.0`. Por exemplo:
{: .text-justify}

```python
plt.figure(figsize=(8,6))
plt.scatter(x,y, s = 100.1, marker = "D", edgecolors = 'k', facecolors='none',
            label="Raças de cachorros")
plt.legend()
plt.xlabel("Peso (kg)")
plt.ylabel("Altura (cm)", labelpad=25)
plt.show()
```

*Figura 11* - Gráfico de dispersão título no eixo `y` com espaçamento.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/11/grafico-dispersao-legenda-11.png" alt="gráfico de dispersão desenhado utilizando o **matplotlib** com título no eixo y com espaçamento" >
{: .text-center}

<br>

Também é possível alterar a **posição** do título do eixo `y` através do parâmetro `loc`. Temos três opções:
{: .text-justify}

- `'center'` (padrão): posiciona o título no centro do eixo `y`;
- `'bottom'`: posiciona o título na base do eixo `y`;
- `'top'`: posiciona o título no topo do eixo `y`;

Por exemplo, para deixar o título do eixo `y` no topo, basta utilizar `loc = "top"`:

```python
plt.figure(figsize=(8,6))
plt.scatter(x,y, s = 100.1, marker = "D", edgecolors = 'k', facecolors='none',
            label="Raças de cachorros")
plt.legend()
plt.xlabel("Peso (kg)")
plt.ylabel("Altura (cm)", labelpad=25, loc='top')
plt.show()
```

*Figura 12* - Gráfico de dispersão título no eixo `y` com espaçamento e no topo do gráfico.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/11/grafico-dispersao-legenda-12.png" alt="gráfico de dispersão desenhado utilizando o **matplotlib** com título no eixo y com espaçamento e no topo do gráfico" >
{: .text-center}

<br>

Mais informações sobre o `plt.ylabel()` podem ser encontradas na [Documentação](https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.ylabel.html).


<h2><a style="color:black" id="">Título no gráfico</a></h2>

<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/generico/banner.png" alt="banner provisório " >
{: .text-center}

Para adicionar um título ao gráfico utilizamos o `plt.title()`, passando como uma `str` o nome para o título. O `plt.title()` **precisa** esta posicionado **antes** de `plt.show()`.
{: .text-justify}

```python
plt.figure()

...

plt.title()
plt.show()
```

Por exemplo:

```python
plt.figure(figsize=(8,6))
plt.scatter(x,y, s = 100.1, marker = "D", edgecolors = 'k', facecolors='none',
            label="Raças de cachorros")
plt.legend()
plt.xlabel("Peso (kg)")
plt.ylabel("Altura (cm)")
plt.title("Relação entre peso e altura de diversas raças de cachorro")
plt.show()
```

*Figura 13* - Gráfico de dispersão com título.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/11/grafico-dispersao-legenda-13.png" alt="gráfico de dispersão desenhado utilizando o **matplotlib** com título " >
{: .text-center}

<br>


É possível alterar o espaçamento entre o título do gráfico e o topo do gráfico, passando um número (`float` ou `int`) através do parâmetro `labelpad`. O valor padrão é `6.0`. Por exemplo:
{: .text-justify}

```python
plt.figure(figsize=(8,6))
plt.scatter(x,y, s = 100.1, marker = "D", edgecolors = 'k', facecolors='none',
            label="Raças de cachorros")
plt.legend()
plt.xlabel("Peso (kg)")
plt.ylabel("Altura (cm)")
plt.title("Relação entre peso e altura de diversas raças de cachorro", pad=40)
plt.show()
```

*Figura 14* - Gráfico de dispersão com título com espaçamento.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/11/grafico-dispersao-legenda-14.png" alt="gráfico de dispersão desenhado utilizando o **matplotlib** com título com espaçamento" >
{: .text-center}

<br>

Também é possível alterar a posição do título do gráfico através do parâmetro ```loc```. Temos três opções:

- `'center'` (padrão): posiciona o título no centro (em relação ao eixo x);
- `'right'`: posiciona o título à direita (em relação ao eixo x);
- `'left'`: posiciona o título à esquerda (em relação ao eixo x);

Por exemplo, para deixar o título do gráfico justificado à direita:


```python
plt.figure(figsize=(8,6))
plt.scatter(x,y, s = 100.1, marker = "D", edgecolors = 'k', facecolors='none',
            label="Raças de cachorros")
plt.legend()
plt.xlabel("Peso (kg)")
plt.ylabel("Altura (cm)")
plt.title("Relação entre peso e altura de diversas raças de cachorro", pad=40, loc='right')
plt.show()
```

*Figura 15* - Gráfico de dispersão com título com espaçamento e justificado à direita.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/11/grafico-dispersao-legenda-15.png" alt="gráfico de dispersão desenhado utilizando o **matplotlib** com título com espaçamento e justificado à direita" >
{: .text-center}

<br>


Você encontra mais informações sobre o `plt.title()` na [Documentação](https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.title.html).


<form id = "quiz" name = "quiz2">

<p><strong>Como adicionar espaçamento entre o título do gráfico e o gráfico?</strong></p>

<input type = "radio" id = "mc" name = "question1" value = "a"> Passando o parâmetro <code>pad</code> em  <code>plt.xlabel()</code>
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "b"> Passando o parâmetro <code>labelpad</code> em <code>plt.title()</code>
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "c"> Passando o parâmetro <code>pad</code> em <code>plt.title()</code>
<p style="font-size: 50%"></p>
<p></p>
<input id = "button" type = "button" class="btn btn--info" value = "Enviar" onclick = "checkDois();">
</form>

<div id = "after_submit_dois">
<p style="font-size: 120%" id = "message_dois"></p>
</div>


<br>

<p style="text-align: center">
  <a href="/Curso-matplotlib-10" class="btn btn--success">Anterior</a>
  <a href="/Curso-matplotlib-12" class="btn btn--success">Próximo</a>
</p>


<script>
function check(){
	var question1 = document.quiz.question1.value;
	var messages = [" 😔️  Incorreto! <br> Apesar de de que imprimir o gráfico e adicionar a legenda manualmente seja plausível, a pergunta quer saber como adicionar a legenda utilizando o matplotlib.",
  "Incorreto! 😔  <br> Adicionar o <code>plt.legend()</code> apenas irá criar um elemento de legenda. É necessário adicionar o nome (<code>label</code>) para cada elemento do gráfico.",
  "Incorreto! 😔  <br> Apenas adicionar o <code>label</code> em <code>plt.scatter()</code> não irá criar um elemento de legenda.",
  "🎉 Correto! 🥳️ <br> A legenda somente será adicionada ao gráfico caso o parâmetro <code>label</code> seja passado em <code>plt.scatter()</code> e o <code>plt.legend()</code> for adicionado após o <code>plt.scatter()</code>.",
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


<script>
function checkDois(){
	var question1 = document.quiz2.question1.value;
	var messages = [" 😔️  Incorreto! <br> O parâmetro <code>pad</code> esta correto, mas ele deve ser passado em <code>plt.title()</code> ao invés de <code>plt.xlabel()</code>",
  "Incorreto! 😔  <br> O parâmetro <code>labelpad</code> adiciona espaçamento ao título dos eixos, e não aos título do gráfico.",
  "🎉 Correto! 🥳️ <br> Esta é a forma correta de adicionar espaçamento ao título de um gráfico no matplotlib.",
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

	document.getElementById("after_submit_dois").style.visibility = "visible";
	document.getElementById("message_dois").innerHTML = messages[score];

};

</script>
