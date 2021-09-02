---
title: "Curso matplotlib - Elementos auxiliares (Texto)"
data: 2021-08-01
tags: []
header:
  image: "/images/chess.jpg"
  image_description: "Chess pieces"
excerpt: "matplotlib"
locale: "pt-br"
---

<br>

Para adicionar um texto no gráfico do **matplotlib** podemos utilizar o ```plt.text()```. Este método recebe três parâmetros, que são as coordenadas de x (```x```) e y (```y```), e o texto que será desenhado no texto (`s`).
{: .text-justify}

**Exemplo:**

```python
plt.figure(figsize=(8,6))
plt.scatter(x,y)
plt.text(2.5,2,"Meu texto")
plt.show()
```

*Figura 1* - Gráfico de dispersão com texto inserido
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-elementos-auxiliares/43/grafico-elementos-auxiliares-01.png" alt="gráfico de dispersão genérico desenhado com o **matplotlib**, com texto inserido " >
{: .text-center}

<br>


<h2><a style="color:black" id="formatacao">Formatação</a></h2>


Podemos editar de forma simples o texto inserido. Para alterar o estilo do texto, passamos o parâmetro `style` (ou `fontstyle`) como:
{: .text-justify}

- `'italic'` (para deixar o texto em itálico);

```python
plt.figure(figsize=(8,6))
plt.scatter(x,y)
plt.text(2.5,2,"Meu texto", style='italic')
plt.show()
```

*Figura 2* - Gráfico de dispersão com texto inserido em itálico
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-elementos-auxiliares/43/grafico-elementos-auxiliares-02.png" alt="gráfico de dispersão genérico desenhado com o matplotlib, com texto inserido em itálico" >
{: .text-center}

<br>


- `'oblique'` (para deixar o texto obliquo);

```python
plt.figure(figsize=(8,6))
plt.scatter(x,y)
plt.text(2.5,2,"Meu texto", fontstyle='oblique')
plt.show()
```

*Figura 3* - Gráfico de dispersão com texto inserido obliquo
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-elementos-auxiliares/43/grafico-elementos-auxiliares-03.png" alt="gráfico de dispersão genérico desenhado com o matplotlib, com texto inserido obliquo" >
{: .text-center}

<br>

- `'normal'` (para deixar o texto normal, que é o padrão);


<h3><a style="color:black" id="negrito">Negrito</a></h3>

Para deixar o texto em negrito, utilizamos o parâmetro `fontweight` (ou `weight`) com `str` de referência (`'ultralight'`, `'light'`, `'normal'`, `'regular'`, `'book'`, `'medium'`, `'roman'`, `'semibold'`, `'demibold'`, `'demi'`, `'bold'`, `'heavy'`, `'extra bold'`, `'black'`).
{: .text-justify}

Visualmente, as opções são renderizadas desta forma:

```python
plt.figure(figsize=(8,6))
plt.scatter(x,y)
plt.text(1.0,3.75,"ultralight", fontweight='ultralight')
plt.text(1.0,3.5,"light", fontweight='light')
plt.text(1.0,3.25,"normal", fontweight='normal')
plt.text(1.0,3.0,"regular", fontweight='regular')
plt.text(1.0,2.75,"book", fontweight='book')
plt.text(1.0,2.5,"medium", fontweight='medium')
plt.text(1.0,2.25,"roman", fontweight='roman')
plt.text(1.0,2.0,"semibold", fontweight='semibold')
plt.text(1.0,1.75,"demibold", fontweight='demibold')
plt.text(1.0,1.5,"demi", fontweight='demi')
plt.text(1.0,1.25,"bold", fontweight='bold')
plt.text(2.0,3.25,"heavy", fontweight='heavy')
plt.text(2.0,3.0,"extra bold", fontweight='extra bold')
plt.text(2.0,2.75,"black", fontweight='black')
plt.show()
```

*Figura 4* - Gráfico de dispersão com texto formatado com diferentes pesos
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-elementos-auxiliares/43/grafico-elementos-auxiliares-04.png" alt="gráfico de dispersão genérico desenhado com o matplotlib, com texto formatado com diferentes pesos" >
{: .text-center}

<br>



<h2><a style="color:black" id="tamanho-fonte">Tamanho da fonte</a></h2>

Para alterar o tamanho da fonte, passamos um número (`int` ou `float`) ou uma `str` de referência (`'xx-small`', `'x-small'`, `'small'`, `'medium'`, `'large'`, `'x-large'`, `'xx-large'`) através do parâmetro `fontsize` ou `size`:
{: .text-justify}

Visualmente, as opções são renderizadas desta forma:

```python
plt.figure(figsize=(8,6))
plt.scatter(x,y)
plt.text(1.0,3.75,"xx-small", fontsize='xx-small')
plt.text(1.0,3.5,"x-small", fontsize='x-small')
plt.text(1.0,3.25,"small", fontsize='small')
plt.text(1.0,3.0,"medium", fontsize='medium')
plt.text(1.0,2.75,"large", fontsize='large')
plt.text(1.0,2.5,"x-large", fontsize='x-large')
plt.text(1.0,2.25,"xx-large", fontsize='xx-large')
plt.show()
```

*Figura 5* - Gráfico de dispersão com texto formatado com diferentes tamanhos de fontes
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-elementos-auxiliares/43/grafico-elementos-auxiliares-05.png" alt="gráfico de dispersão genérico desenhado com o matplotlib, com texto formatado com diferentes tamanho de fonte" >
{: .text-center}

<br>


<h2><a style="color:black" id="familia-fonte">Família da fonte</a></h2>


Para alterar a fonte utilizada para desenhar o texto, basta passar o nome da fonte desejada através do parâmetro `fontfamily` (ou `family`):
{: .text-justify}

Por exemplo, para alterar o tipo de família para <span style="font-family: Arial">Arial</span>:

```python
plt.figure(figsize=(8,6))
plt.scatter(x,y)
plt.text(2.5,2,"Meu texto", fontsize=16, fontfamily='Arial')
plt.show()
```

*Figura 6* - Gráfico de dispersão com texto formatado com a fonte <span style="font-family: Arial">Arial</span>.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-elementos-auxiliares/43/grafico-elementos-auxiliares-06.png" alt="gráfico de dispersão genérico desenhado com o matplotlib, com texto na fonte Arial" >
{: .text-center}

<br>

As fontes disponíveis são as mesmas vistas <a href="/Curso-matplotlib-12/">anteriormente</a>.

<h3><a style="color:black" id="rotacao">Rotação do texto</a></h3>

Podemos rotacionar o texto utilizando o parâmetro `rotation`, passando um número, que representa o ângulo de rotação, ou uma das opções:
{: .text-justify}

* `'vertical'` (para alinhar verticalmente ao eixo `x`);

* `'horizontal'` (para alinhar horizontalmente ao eixo `x`).
{: .text-justify}

**Exemplo:**

```python
plt.figure(figsize=(8,6))
plt.scatter(x,y)
plt.text(2.75,2.2,"Quarenta e cinco", size='xx-large', rotation=45)
plt.text(2.5,2.2,"vertical", size='xx-large', rotation='vertical')
plt.text(2.5,2,"horizontal", size='xx-large', rotation='horizontal')
plt.show()
```

*Figura 7* - Gráfico de dispersão com texto rotacionado
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-elementos-auxiliares/43/grafico-elementos-auxiliares-07.png" alt="gráfico de dispersão genérico desenhado com o matplotlib, com texto rotacionado" >
{: .text-center}

<br>

<h3><a style="color:black" id="cor-texto">Cor do texto</a></h3>

Para alterar a cor do texto, basta passar o parâmetro `color` (ou `c`) com o nome da cor desejada (`str`). As cores disponíveis são as mesmas vistas <a href="/Curso-matplotlib-08#cor-marcadores">anteriormente</a>.
{: .text-justify}

Por exemplo, para deixar o texto na cor verde:

```python
plt.figure(figsize=(8,6))
plt.scatter(x,y)
plt.text(2.5,2,"Meu texto", size='xx-large', c='g')
plt.show()
```

*Figura 8* - Gráfico de dispersão com texto na cor verde
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-elementos-auxiliares/43/grafico-elementos-auxiliares-08.png" alt="gráfico de dispersão genérico desenhado com o matplotlib, com texto na cor verde" >
{: .text-center}

<br>

<h3><a style="color:black" id="cor-fundo">Cor de fundo</a></h3>

Para alterar a cor de fundo do elemento de texto, basta passar o nome da cor (`str`) para o parâmetro `backgroundcolor`. As cores disponíveis são as mesmas vistas <a href="/Curso-matplotlib-08#cor-marcadores">anteriormente</a>.
{: .text-justify}

Por exemplo, para deixar a cor de fundo preta:

```python
plt.figure(figsize=(8,6))
plt.scatter(x,y)
plt.text(2.5,2,"Meu texto", size='xx-large', c='w', backgroundcolor='k')
plt.show()
```

*Figura 9* - Gráfico de dispersão com a cor de fundo do texto na cor preta.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-elementos-auxiliares/43/grafico-elementos-auxiliares-09.png" alt="gráfico de dispersão genérico desenhado com o matplotlib, com a cor de fundo do texto na cor preta." >
{: .text-center}

<br>

<h2><a style="color:black" id="bordas">Bordas</a></h2>


Para adicionar bordas ao elemento de texto, precisamos passar o parâmetro `bbox` com alguns parâmetros (através de um `dict`), pois este parâmetro vai criar uma caixa por cima do texto.
{: .text-justify}

- Para deixar esta caixa com a cor de preenchimento vazia, passamos o `facecolor='none'`;

- Para deixar esta caixa com a borda preta (ou a cor preferida), passamos o `edgecolor='k'`;

Por exemplo:

```python
plt.figure(figsize=(8,6))
plt.scatter(x,y)
plt.text(2.5,2,"Meu texto", size='xx-large', bbox={'facecolor': 'none', 'edgecolor': 'k'})
plt.show()
```

*Figura 10* - Gráfico de dispersão com texto com bordas.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-elementos-auxiliares/43/grafico-elementos-auxiliares-10.png" alt="gráfico de dispersão genérico desenhado com o matplotlib, com texto com bordas" >
{: .text-center}

<br>

Podemos deixar esta caixa com cantos arredondados e espaçamento, passando para o parâmetro `boxstyle` o `round` para deixar os cantos arredondados, e o `pad` para adicionar espaçamento:
{: .text-justify}

**Exemplo:**

```python
plt.figure(figsize=(8,6))
plt.scatter(x,y)
plt.text(2.5,2,"Meu texto", size='xx-large', bbox={'facecolor': 'none', 'edgecolor': 'k', 'boxstyle': 'round, pad=1'})
plt.show()
```

*Figura 11* - Gráfico de dispersão com texto com bordas arredondadas.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-elementos-auxiliares/43/grafico-elementos-auxiliares-11.png" alt="gráfico de dispersão genérico desenhado com o matplotlib, com texto com bordas arredondadas" >
{: .text-center}

<br>

Você encontra mais detalhes e muita fonte de inspiração na [documentação](https://matplotlib.org/stable/gallery/shapes_and_collections/fancybox_demo.html).

<br>

<form id = "quiz" name = "quiz">

<p><strong>Qual é a função do parâmetro rotation em plt.text()?</strong></p>

<input type = "radio" id = "mc" name = "question1" value = "a"> Rotacionar o texto
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "b"> Aumentar o tamanho da fonte do texto
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "c"> Alterar a fonte do texto
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "d"> O <code>plt.text()</code> não tem nenhum parâmetro <code>rotation</code>.
<p style="font-size: 50%"></p>
<p></p>
<input id = "button" type = "button" class="btn btn--info" value = "Enviar" onclick = "check();">
</form>

<div id = "after_submit">
<p style="font-size: 120%" id = "message"></p>
</div>

<br>

<p style="text-align: center">
  <a href="/Curso-matplotlib-42" class="btn btn--success">Anterior</a>
  <a href="/Curso-matplotlib-44" class="btn btn--success">Próximo</a>
</p>

<script>
function check(){
	var question1 = document.quiz.question1.value;
	var messages = [" 🎉 Correto! 🥳️ <br> Esta [e a função do parâmetro <code>rotation</code>",
  " 😔 Incorreto! 😔  <br> O parâmetro utilizado para alterar o tamanho da fonte é o parâmetro <code>size</code> ou o parâmetro <code>fontsize</code>.",
  " Incorreto! 😔 <br> O parâmetro utilizado para alterar o tipo de fonte é o <code>fontfamily</code>. ",
  " 😔 Incorreto! <br> O <code>plt.text()</code> tem como opção o parâmetro <code>rotation</code>, e sua função é rotacionar o texto.",
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
