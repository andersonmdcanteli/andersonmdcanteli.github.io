---
title: "Curso matplotlib - Gráfico de dispersão (alterando os marcadores)"
data: 2021-07-18
tags: []
header:
  image: "/images/chess.jpg"
  image_description: "Chess pieces"
excerpt: "matplotlib"
locale: "pt-br"
---

<br>

Os marcadores tem uma grande importância no entendimento dos gráficos. Dependendo do tipo de dado, é preferivel utilizar algum tipo de marcador, que talvez não seja adequado para outros tipos de dados. Além disso, utilizar marcadores diferentes é uma das melhores formas de diferenciar séries diferentes em um mesmo gráfico.
{: .text-justify}

<h2><a style="color:black" id="alterando-marcador">Alterando o tipo do marcador</a></h2>

<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/generico/banner.png" alt="banner provisório " >
{: .text-center}


Para alterar o tipo do marcador utilizamos o parâmetro `marker`, que deve receber uma `str` contendo o símbolo desejado ou um número inteiro (`int`) da lista de referências de marcadores.
{: .text-justify}

Os marcadores mais utilizados são:

- `"."` (ponto);
- `"o"` (circulo);
- `"v"` (triângulo para cima);
- `"s"` (quadrado);
- `"\* "` (estrela);
- `"D"` (diamante);
- `"+"` (mais);

Na Figura abaixo você pode visualizar todos os marcadores disponíveis:


<img style="float: center;" src="https://raw.githubusercontent.com/andersonmdcanteli/matplotlib-course/main/auxiliary-scripts/matplotlib-all-markers/matplotlib_markers.png" alt="Gráfico de dispersão mostrando os diferentes marcadores" width="800">
{: .text-center}


O script utilizado para desenhar o gráfico acima pode ser acessado [neste link](https://github.com/andersonmdcanteli/matplotlib-course/blob/main/auxiliary-scripts/matplotlib-all-markers/matplotlib-all-markers.ipynb).

Você encontra maiores informações na [documentação](https://matplotlib.org/stable/api/markers_api.html).


Por exemplo, para deixar os marcadores em formato de diamante:

```python
plt.figure(figsize=(8,6))
plt.scatter(x,y, c='red', s = 100.1, marker = "D")
plt.show()
```

*Figura 1* - Gráfico de dispersão com o marcador em formato de diamante.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/10/grafico-dispersao-tipo-marcador-01.png" alt="gráfico de dispersão desenhado utilizando o **matplotlib** com os marcadores com estilo de diamante" >
{: .text-center}

<br>

Veremos como deixar os marcadores com símbolos diferentes mais a frente.

<br>

<form id = "quiz" name = "quiz">

<p><strong>O que é um marker?</strong></p>

<input type = "radio" id = "mc" name = "question1" value = "a"> Uma empresa
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "b"> Parâmetro utilizado para alterar o simbolo do marcador em um gráfico do matplotlib
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "c"> Parâmetro utilizado para alterar o tamanho do marcador em um gráfico do matplotlib
<p style="font-size: 50%"></p>
<p></p>
<input id = "button" type = "button" class="btn btn--info" value = "Enviar" onclick = "check();">
</form>

<div id = "after_submit">
<p style="font-size: 120%" id = "message"></p>
</div>



<h2><a style="color:black" id="bordas-marcador">Alterando a cor da linha do marcador (bordas do marcador)</a></h2>

<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/generico/banner.png" alt="banner provisório " >
{: .text-center}


Também é possível alterar a cor das linhas (bordas) dos marcadores de forma bem simples, bastando passar o nome da cor desejada (como uma `str`) através do parâmetro `edgecolors`. As cores seguem o mesmo padrão apresentado no item <a href="/Curso-matplotlib-08/#cor-marcadores">alterando a cor do marcador</a>.
{: .text-justify}

Por exemplo, para deixar a borda na cor preta:
{: .text-justify}

```python
plt.figure(figsize=(8,6))
plt.scatter(x,y, c='red', s = 100.1, marker = "D", edgecolors = 'k')
plt.show()
```

*Figura 2* - Gráfico de dispersão com marcadores com bordas na cor preta.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/10/grafico-dispersao-tipo-marcador-02.png" alt="gráfico de dispersão desenhado utilizando o **matplotlib** com os marcadores com estilo de diamante com bordas na cor preta" >
{: .text-center}

<br>

Também podemos passar uma sequência de elementos (`list`, `tuple`, `ndarray`, etc) com os nomes das cores para alterar a cor da borda de cada ponto do gráfico.
{: .text-justify}

Utilizando a lista `cores` criada anteriormente:

```python
plt.figure(figsize=(8,6))
plt.scatter(x,y, c='red', s = 100.1, marker = "D", edgecolors = cores)
plt.show()
```

*Figura 3* - Gráfico de dispersão com marcadores com bordas com diversas cores.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/10/grafico-dispersao-tipo-marcador-03.png" alt="gráfico de dispersão desenhado utilizando o **matplotlib** com os marcadores com estilo de diamante com bordas com cores diferentes" >
{: .text-center}

<br>


<form id = "quiz2" name = "quiz2">

<p><strong>Qual linha de comando alteraria a cor da borda de um marcador para a cor verde?</strong></p>

<input type = "radio" id = "mc" name = "question1" value = "a"> <code>plt.scatter(x, y, s='g')</code>
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "b"> <code>plt.scatter(x, y, edge_colors='g')</code>
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "c"> <code>plt.scatter(x, y, edgecolors='g')</code>
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "d"> <code>plt.scatter(x, y, edgecolors='g)</code>
<p style="font-size: 50%"></p>
<p></p>
<input id = "button" type = "button" class="btn btn--info" value = "Enviar" onclick = "checkDois();">
</form>

<div id = "after_submit_dois">
<p style="font-size: 120%" id = "message_dois"></p>
</div>

<br>


<h2><a style="color:black" id="espessura-linha">Alterando a espessura da linha do marcador (espessura da borda)</a></h2>

<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/generico/banner.png" alt="banner provisório " >
{: .text-center}


Também é possível alterar a espessura da borda dos marcadores, o que é feito passando um número inteiro (`int`) ou decimal (`float`) através do parâmetro `linewidths`.
{: .text-justify}

```python
plt.figure(figsize=(8,6))
plt.scatter(x,y, c='red', s = 100.1, marker = "D", edgecolors = cores, linewidths=2.5)
plt.show()
```

*Figura 4* - Gráfico de dispersão com marcadores com bordas com diversas cores com a borda mais espessa.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/10/grafico-dispersao-tipo-marcador-04.png" alt="gráfico de dispersão desenhado utilizando o **matplotlib** com os marcadores com estilo de diamante com bordas com cores diferentes e bordas espessas" >
{: .text-center}

<br>

Também podemos passar uma sequência (`list`, `tuple`, etc) com diversos valores para a espessura das bordas. Por exemplo, podemos utilizar a `list`:
{: .text-justify}

```python
espessura_marcador = [1, 1.2, 1.4, 1.6, 1.8, 2, 2.2, 2.4, 2.6, 2.8, 3.0]
```

que contém apenas valores numéricos e o mesmo tamanho de `x` para alterar a espessura da borda de cada marcador indivualmente:
{: .text-justify}

```python
plt.figure(figsize=(8,6))
plt.scatter(x,y, c='red', s = 100.1, marker = "D", edgecolors = cores, linewidths=espessura_marcador)
plt.show()
```

*Figura 5* - Gráfico de dispersão com marcadores com bordas com diversas cores com a borda com espessura variada.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/10/grafico-dispersao-tipo-marcador-05.png" alt="gráfico de dispersão desenhado utilizando o **matplotlib** com os marcadores com estilo de diamante com bordas com cores diferentes e bordas com espessura variada" >
{: .text-center}

<br>


<form id = "quiz" name = "quiz3">

<p><strong>Qual a função do parâmetro linewidths quando passado para o <code>plt.scatter()</code>?</strong></p>

<input type = "radio" id = "mc" name = "question1" value = "a"> Adicionar uma linha entre os pontos
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "b"> Alterar a cor da borda dos marcadores
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "c"> Alterar a espessura da borda dos marcadores
<p style="font-size: 50%"></p>
<p></p>
<input id = "button" type = "button" class="btn btn--info" value = "Enviar" onclick = "checkTres();">
</form>

<div id = "after_submit_tres">
<p style="font-size: 120%" id = "message_tres"></p>
</div>

<br>


<h2><a style="color:black" id="cor-preenchimento">Alterando a cor de preenchimento do marcador</a></h2>

<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/generico/banner.png" alt="banner provisório " >
{: .text-center}


É possível alterar a cor de dentro (interior) dos marcadores, o que é feito passando o nome da cor desejada através do parâmetro `facecolors`. As cores seguem o mesmo padrão apresentado no item <a href="/Curso-matplotlib-08/#cor-marcadores">alterando a cor do marcador</a>.
{: .text-justify}

Entretanto, não devemos passar o parâmetro `color`, pois ele tem prioridade mais elevada no código e irá sobrescrever as cores.
{: .text-justify}

Por exemplo, se adicionarmos o `facecolors='g'` no gráfico que estamos construindo, não teremos mudanças visuais no gráfico:
{: .text-justify}

```python
plt.figure(figsize=(8,6))
plt.scatter(x,y, c = 'red', s = 100.1, marker = "D", edgecolors = 'k', facecolors='g')
plt.show()
```

*Figura 6* - Gráfico de dispersão com marcadores com o parâmetro `color` tendo precedencia ao parâmetro `facecolors`.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/10/grafico-dispersao-tipo-marcador-06.png" alt="gráfico de dispersão desenhado utilizando o **matplotlib** sem influência do parâmetro facecolors devido ao parâmetro color" >
{: .text-center}

<br>

Como foi utilizado o parâmetro `facecolors='g'`, era ***esperado*** que as cores das faces ficassem verdes, o que não aconteceu. Mas ao remover parâmetro `c`, teremos o resultado desejado:
{: .text-justify}

```python
plt.figure(figsize=(8,6))
plt.scatter(x,y, s = 100.1, marker = "D", edgecolors = 'k', facecolors='g')
plt.show()
```

*Figura 7* - Gráfico de dispersão com marcadores na cor verde desenhado utilizando o parâmetro `facecolors`.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/10/grafico-dispersao-tipo-marcador-07.png" alt="gráfico de dispersão desenhado utilizando o **matplotlib** alterando a cor dos marcadores através do parametro facecolors " >
{: .text-center}

<br>

Também é possível passar uma sequência (`list`, `tuple`, `ndarray`, etc) com os nomes das cores para alterar a cor de preenchimento de cada marcador do gráfico individualmente. Utilizando a lista `cores` criada anteriormente, obtemos o seguinte gráfico:
{: .text-justify}

```python
plt.figure(figsize=(8,6))
plt.scatter(x,y, s = 100.1, marker = "D", edgecolors = 'k', facecolors=cores)
plt.show()
```

*Figura 8* - Gráfico de dispersão com marcadores com diversas cores.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/10/grafico-dispersao-tipo-marcador-08.png" alt="gráfico de dispersão desenhado utilizando o **matplotlib** alterando os marcadores com diversas cores " >
{: .text-center}

<br>

Também é possível remover a cor do marcador, de forma a deixar ele "aberto". Para fazer isto, basta  passar `facecolors = "none"` ou `facecolors = "None"`:

```python
plt.figure(figsize=(8,6))
plt.scatter(x,y, s = 100.1, marker = "D", edgecolors = 'k', facecolors='None')
plt.show()
```
*Figura 9* - Gráfico de dispersão com marcadores abertos.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/10/grafico-dispersao-tipo-marcador-09.png" alt="gráfico de dispersão desenhado utilizando o **matplotlib** com os marcadores abertos " >
{: .text-center}

<br>


<form id = "quiz" name = "quiz4">

<p><strong>Qual a forma de deixar o marcador aberto em <code>plt.scatter()</code>?</strong></p>

<input type = "radio" id = "mc" name = "question1" value = "a"> plt.scatter(x,y, facecolors='none')
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "b"> plt.scatter(x,y, facecolors='none', edgecolors='k')
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "c"> plt.scatter(x,y, facecolors='w', edgecolors='k')
<p style="font-size: 50%"></p>
<p></p>
<input id = "button" type = "button" class="btn btn--info" value = "Enviar" onclick = "checkQuatro();">
</form>

<div id = "after_submit_quatro">
<p style="font-size: 120%" id = "message_quatro"></p>
</div>

<br>


<br>

<p style="text-align: center">
  <a href="/Curso-matplotlib-09" class="btn btn--success">Anterior</a>
  <a href="/Curso-matplotlib-11" class="btn btn--success">Próximo</a>
</p>




<script>
function check(){
	var question1 = document.quiz.question1.value;
	var messages = [" 🥳️  Correto, mas fora de contexto 😔! <br> Existe pelo menos uma empresa com o nome Marker (Marker International), mas no contexto do matplotlib, <code>marker</code> é o parâmetro utilizado para alterar o marcador (ou símbolo) utilizado para os pontos de um gráfico.",
  "🎉 Correto! 🥳️ <br> É através do parâmetro <code>marker</code> que alteramos o tipo de marcador utilizado para desenhar os pontos de um gráfico. ",
  "Incorreto! 😔  <br> O parâmetro <code>marker</code> é utilizado para alterar o tipo do marcador. Para alterar o tamanho do marcador, utiliza-se o parâmetro <code>s</code>.",
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


<script>
function checkDois(){
	var question1 = document.quiz2.question1.value;
	var messages = [" Incorreto! 😔 <br> O parâmetro <code>s</code> altera o tamanho dos marcadores.",
  " Incorreto! 😔 <br>  O <code>plt.scatter()</code> não tem um parâmetro chamado <code>edge_colors</code>. ",
  " 🎉 Correto! 🥳️   <br> Esta é a forma correta de alterar a cor das 'bordas' de um marcador para a cor verde.",
  "😔 Incorreto! <br> Apesar do parâmetro utilizado estar correto, a aspa simples utilizada para passar o nome da cor não foi fechada, o que resultará em um erro.",
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

	document.getElementById("after_submit_dois").style.visibility = "visible";
	document.getElementById("message_dois").innerHTML = messages[score];

};

</script>



<script>
function checkTres(){
	var question1 = document.quiz3.question1.value;
	var messages = [" Incorreto! 😔 <br>  O <code>plt.scatter()</code> não tem um parâmetro para ligar os pontos do gráfico. Para isto, utilizamos o <code>plt.plot()</code>.",
  " 😔 Incorreto! <br>  O parâmetro utilizado para alterar a cor das bordas é o <code>edgecolors</code>. ",
  "🎉 Correto! 🥳️  <br> O parâmetro <code>linewidths</code> altera a espessura da borda dos marcadores!",
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

	document.getElementById("after_submit_tres").style.visibility = "visible";
	document.getElementById("message_tres").innerHTML = messages[score];

};

</script>


<script>
function checkQuatro(){
	var question1 = document.quiz4.question1.value;
	var messages = [" Incorreto! 😔 <br> Apesar de que passar <code>'none'</code> para o parâmetro <code>facecolors</code> irá efetivamente deixar o marcador aberto, ao não adicionar bordas no marcador, ele ficará todo transparente e não será possível identifica-lo gráfico.",
  " 🎉 Correto! 🥳️ <br>  Para deixar o marcador aberto precisamos adicionar uma cor à borda, e remover a cor da face do marcador.",
  " 😔 Incorreto! <br> Ao passar a string <code>'w'</code> para o parâmetro <code>facecolors</code>, a cor do marcador ficará branca, e não aberto.",
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

	document.getElementById("after_submit_quatro").style.visibility = "visible";
	document.getElementById("message_quatro").innerHTML = messages[score];

};

</script>
