---
title: "Elementos auxiliares (Grid)"
data: 2021-08-09
tags: []
header:
  image: "/images/chess.jpg"
  image_description: "Chess pieces"
excerpt: "matplotlib"
locale: "pt-br"
---


<br>

O grid é um elemento constituído por linhas verticais e horizontais, que são utilizados para guiar ou dar forma ao gráfico. Entretanto, o grid não faz parte da informação que se pretende passar em um gráfico, e certamente este não é um elemento adequado para publicações científicas, sendo considerado por muitos autores, como *lixo gráfico*.
{: .text-justify}

Contudo, ele pode ser muito útil na etapa de interpretação de resultados, e também em gráficos utilizados em apresentações, sendo utilizado para dar suporte para o leitor que tem pouco tempo para observar o gráfico. Atente que, em um artigo científico ou um pôster físico, o leitor tem boa uma quantidade de tempo para ler e compreender o gráfico, enquanto que em uma apresentação, este tempo é bastante escasso (dificilmente passando de 1 minuto) o que *talvez* justifique seu uso.
{: .text-justify}


<h2><a style="color:black" id="grid-conjunto-dados">Conjunto de dados</a></h2>

Para exemplificar como inserir o elemento de grid é utilizado um conjunto de dados genérico, apenas para existir referência visual. Esta referência visual é feita criando um gráfico de dispersão.
{: .text-justify}

```python
import matplotlib.pyplot as plt

x = [1,2,3,4]
y = [1,2,3,4]

plt.figure(figsize=(8,6))
plt.scatter(x, y)
plt.show()
```

*Figura 1* - Gráfico de dispersão.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-elementos-auxiliares-2/78/elementos-auxiliares-01.png" alt="gráfico de dispersão desenhado com matplotlib" >
{: .text-center}

<br>

Para inserir linhas de grid em um gráfico, utilizamos o método `plt.grid()`, que não demanda nenhum parâmetro. Por exemplo:
{: .text-justify}

```python
plt.figure(figsize=(8,6))
plt.scatter(x, y)
plt.grid()
plt.show()
```

*Figura 2* - Gráfico de dispersão com grid.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-elementos-auxiliares-2/78/elementos-auxiliares-02.png" alt="gráfico de dispersão desenhado com matplotlib com grid" >
{: .text-center}

<br>

Entretanto, é possível controlar todas as linhas do grid, o que é feito passando alguns parâmetros para o `plt.grid()`. Para controlar a inserção ou não do grid, podemos passar o parâmetro `b`, que recebe um valor `bool`, onde `True` (padrão) insere o grid, e `False` não insere o grid. Caso algum outro parâmetro seja passado, o grid sempre será inserido, com a exceção de quando for passado `b = False`.
{: .text-justify}

<h2><a style="color:black" id="grid-eixos">Eixos</a></h2>

É possível determinar em qual eixo o grid será desenhado, o que é feito através do parâmetro `axis`. Este parâmetro recebe uma `str` de referência, que pode ser:
{: .text-justify}

- `"x"`: grid inseridos apenas no eixo `x`;

- `"y"`: grid inseridos apenas no eixo `y`;

- `"both"`: grid inseridos em ambos os eixos (padrão);

Por exemplo:

```python
plt.figure(figsize=(8,6))
plt.scatter(x, y)
plt.grid(axis='x')
plt.show()
```

*Figura 3* - Gráfico de dispersão com grid apenas na vertical.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-elementos-auxiliares-2/78/elementos-auxiliares-03.png" alt="gráfico de dispersão desenhado com matplotlib com grid apenas na vertical" >
{: .text-center}

<br>

Outro exemplo:

```python
plt.figure(figsize=(8,6))
plt.scatter(x, y)
plt.grid(axis='y')
plt.show()
```

*Figura 4* - Gráfico de dispersão com grid apenas na horizontal.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-elementos-auxiliares-2/78/elementos-auxiliares-04.png" alt="gráfico de dispersão desenhado com matplotlib com grid apenas na horizontal" >
{: .text-center}

<br>


<h2><a style="color:black" id="grid-posicao">Posição</a></h2>

É possível determinar em qual posição o grid será inserido baseado nos *ticks* do gráfico. Para isto, é necessário passar a opção escolhida para o parâmetro `which`, que recebe um `str`de referência. Temos três opções:
{: .text-justify}

- `"major"`: insere linhas de grid apenas nos *ticks* principais (padrão);

- `"minor"`: insere linhas de grid apenas nos *ticks* secundários;

- `"both"`: insere linhas de grid em ambos os *ticks*;

Para inserir os `minor` *ticks* no gráfico, podemos utilizar o `plt.minorticks_on()`. Maiores detalhes na [documentação](https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.minorticks_on.html).
{: .text-justify}

Por exemplo, inserindo grids apenas na posição dos *ticks* secundários:

```python
plt.figure(figsize=(8,6))
plt.scatter(x, y)
plt.minorticks_on()
plt.grid(which='minor')
plt.show()
```

*Figura 5* - Gráfico de dispersão com grid baseado nos minor *tics*.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-elementos-auxiliares-2/78/elementos-auxiliares-05.png" alt="gráfico de dispersão desenhado com matplotlib com grid baseado nos minor *ticks" >
{: .text-center}

<br>


Caso queira inserir o grid em ambos os *ticks*, basta passar `which = "both"`:

```python
plt.figure(figsize=(8,6))
plt.scatter(x, y)
plt.minorticks_on()
plt.grid(which='both')
plt.show()
```

*Figura 6* - Gráfico de dispersão com grid baseado nos minor e major *tics*.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-elementos-auxiliares-2/78/elementos-auxiliares-06.png" alt="gráfico de dispersão desenhado com matplotlib com grid baseado nos minor e major *ticks" >
{: .text-center}

<br>

<h2><a style="color:black" id="grid-edicoes">Edições</a></h2>

O `plt.grid()` aceita uma série de parâmetros para a sua edição, sendo possível alterar a cor de preenchimento (`color` ou `facecolor`), remover o preenchimento (`fill`), inserir linhas (`linestyle`, `linewidth`, `edgecolor`), inserir estilos de preenchimento (`hatch`), adicionar transparência (`alpha`), determinar a ordem de plotagem (`zorder`), inserir nome para legenda (`label`), entre outros, de forma muito similar ao que vimos até o momento.
{: .text-justify}

Você encontra maiores detalhes na [documentação](https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.grid.html).
{: .text-justify}


<br>

<form id = "quiz" name = "quiz">

<p><strong>Quando devo utilizar grid?</strong></p>

<input type = "radio" id = "mc" name = "question1" value = "a"> Sempre
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "b"> Nunca
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "c"> Apenas no dia 29 de fevereiro
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "d"> Apenas quando necessário
<p style="font-size: 50%"></p>
<p></p>
<input id = "button" type = "button" class="btn btn--info" value = "Enviar" onclick = "check();">
</form>

<div id = "after_submit">
<p style="font-size: 120%" id = "message"></p>
</div>

<br>

<p style="text-align: center">
  <a href="/Curso-matplotlib-77" class="btn btn--success">Anterior</a>
  <a href="/Curso-matplotlib-79" class="btn btn--success">Próximo</a>
</p>


<script>
function check(){
	var question1 = document.quiz.question1.value;
	var messages = [" Incorreto! 😔 <br> O elemento de grid pode atrapalhar na visualização dos dados,e por este motivo seu uso geralmente não é recomendado",
  " 😔 Incorreto! <br> Apesar do grid atrapalhar na visualização dos dados, existem alguns momentos onde o seu uso é bem vindo, como durante a análise dos dados ou para auxiliar o leitor na visualização do gráfico, por exemplo",
  " 😔 Incorreto! 😔 <br> Você pode utilizar o elemento de grid em qualquer dia do ano, mas o utilize com parcimônia",
  " 🎉 Correto! 🥳️ <br> Utilize o grid apenas quando for necessário!",
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
