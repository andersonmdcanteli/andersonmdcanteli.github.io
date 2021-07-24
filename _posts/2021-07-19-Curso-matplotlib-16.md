---
title: "Curso matplotlib - Plano de fundo"
data: 2021-07-19
tags: []
header:
  image: "/images/chess.jpg"
  image_description: "Chess pieces"
excerpt: "matplotlib"
locale: "pt-br"
---


<br>

Uma propriedade muito importante em um gráfico é o seu background. Por padrão, o background dos gráficos do **matplotlib** é branco.
{: .text-justify}

*Gif 1* - Gráfico de dispersão exportando com a borda transparente.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/16/gif-borda-transparente-01.gif" alt="gráfico de dispersão desenhado utilizando o **matplotlib**  com a borda externa transparente">
{: .text-center}

<br>

Mas em alguns casos, especialmente para apresentações, é interessante que o fundo do gráfico tenha alguma cor, ou até mesmo que seja transparente.
{: .text-justify}

<h2><a style="color:black" id="">Preenchimento bordas externas</a></h2>

<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/generico/banner.png" alt="banner provisório " >
{: .text-center}

Por padrão, a borda externa do gráfico (tudo aquilo que fica *fora* dos limites do eixo do gráfico) é transparente. Para alterar esta cor, basta passar a cor desejada para o parâmetro `facecolor` em `plt.figure()`:
{: .text-justify}

Por exemplo, para alterar a cor das bordas do gráfico para azul, podemos fazer da seguinte forma:
{: .text-justify}

```python
plt.figure(figsize=(8,6), facecolor='yellow')
plt.scatter(x[0], y[0], label=raca_cachorro[0], edgecolor='k', facecolor='none', marker='o', s = marker_size)
plt.scatter(x[1], y[1], label=raca_cachorro[1], edgecolor='k', facecolor='none', marker='s', s = marker_size)
plt.scatter(x[2], y[2], label=raca_cachorro[2], edgecolor='k', facecolor='none', marker='p', s = marker_size)
plt.scatter(x[3], y[3], label=raca_cachorro[3], edgecolor='k', facecolor='none', marker='*', s = marker_size)
plt.scatter(x[4], y[4], label=raca_cachorro[4], edgecolor='k', facecolor='none', marker='v', s = marker_size)
plt.scatter(x[5], y[5], label=raca_cachorro[5], edgecolor='k', facecolor='none', marker='^', s = marker_size)
plt.scatter(x[6], y[6], label=raca_cachorro[6], edgecolor='k', facecolor='none', marker='<', s = marker_size)
plt.scatter(x[7], y[7], label=raca_cachorro[7], edgecolor='k', facecolor='none', marker='>', s = marker_size)
plt.scatter(x[8], y[8], label=raca_cachorro[8], edgecolor='k', facecolor='k', marker='x', s = marker_size)
plt.scatter(x[9], y[9], label=raca_cachorro[9], edgecolor='k', facecolor='none', marker='D', s = marker_size)
plt.scatter(x[10], y[10], label=raca_cachorro[10], edgecolor='k', facecolor='none', marker='H', s = marker_size)
plt.legend(fontsize=12)
plt.xlabel("Peso (kg)", labelpad=15)
plt.ylabel("Altura (cm)", labelpad=15)
plt.title("Relação entre peso e altura de diversas raças de cachorros", pad=15)
plt.show()
```



*Figura 1* - Gráfico de dispersão exportando com borda externa amarela.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/16/grafico-background-01.png" alt="gráfico de dispersão desenhado utilizando o **matplotlib**  com a borda externa amarela">
{: .text-center}

<br>


Em alguns casos pode acontecer do gráfico exportado "corte" alguma parte do gráfico. Um exemplo bem comum ocorre caso a posição das legendas seja alterada para fora do gráfico:
{: .text-justify}

```python
plt.figure(figsize=(8,6), facecolor='yellow')
plt.scatter(x[0], y[0], label=raca_cachorro[0], edgecolor='k', facecolor='none', marker='o', s = marker_size)
plt.scatter(x[1], y[1], label=raca_cachorro[1], edgecolor='k', facecolor='none', marker='s', s = marker_size)
plt.scatter(x[2], y[2], label=raca_cachorro[2], edgecolor='k', facecolor='none', marker='p', s = marker_size)
plt.scatter(x[3], y[3], label=raca_cachorro[3], edgecolor='k', facecolor='none', marker='*', s = marker_size)
plt.scatter(x[4], y[4], label=raca_cachorro[4], edgecolor='k', facecolor='none', marker='v', s = marker_size)
plt.scatter(x[5], y[5], label=raca_cachorro[5], edgecolor='k', facecolor='none', marker='^', s = marker_size)
plt.scatter(x[6], y[6], label=raca_cachorro[6], edgecolor='k', facecolor='none', marker='<', s = marker_size)
plt.scatter(x[7], y[7], label=raca_cachorro[7], edgecolor='k', facecolor='none', marker='>', s = marker_size)
plt.scatter(x[8], y[8], label=raca_cachorro[8], edgecolor='k', facecolor='k', marker='x', s = marker_size)
plt.scatter(x[9], y[9], label=raca_cachorro[9], edgecolor='k', facecolor='none', marker='D', s = marker_size)
plt.scatter(x[10], y[10], label=raca_cachorro[10], edgecolor='k', facecolor='none', marker='H', s = marker_size)
plt.legend(fontsize=12, bbox_to_anchor=(1.,1.))
plt.xlabel("Peso (kg)", labelpad=15)
plt.ylabel("Altura (cm)", labelpad=15)
plt.title("Relação entre peso e altura de diversas raças de cachorros", pad=15)
plt.show()
```

*Figura 2* - Gráfico de dispersão exportando com as legendas cortadas.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/16/grafico-background-02.png" alt="gráfico de dispersão desenhado utilizando o **matplotlib**  com as legendas cortadas">
{: .text-center}

<br>

Para evitar que isto aconteça, podemos passar o parâmetro `bbox_inches='tight'` em `plt.savefig()`. Por exemplo:

```python
plt.savefig("meu-grafico-01.png", dpi=100, bbox_inches='tight')
```

*Figura 3* - Gráfico de dispersão exportando com as legendas corretas.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/16/meu-grafico-01.png" alt="gráfico de dispersão desenhado utilizando o **matplotlib**  exportado com as legendas corretas ">
{: .text-center}

<br>


O `bbox_inches='tight'` é muito útil para remover espaços vazios do gráfico, sendo possível obter um gráfico maior ocupando o mesmo tamanho da figura. Observe que o output gerado é semelhante ao output gerado antes de utilizar o `bbox_inches='tight'` em `plt.savefig()`, mas não é igual. Observe que o espaço entre os títulos (tanto dos eixos, como do titulo) está mais próximo do limite do gráfico. O gráfico ficou "ajustado".
{: .text-justify}

Voltando a legenda para a posição `best` e com o  ```bbox_inches='tight'```, obtemos:


*Figura 4* - Gráfico de dispersão exportando com borda externa amarela.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/16/grafico-background-03.png" alt="gráfico de dispersão desenhado utilizando o **matplotlib**  com a borda externa amarela">
{: .text-center}

<br>


<h2><a style="color:black" id="">Cor do backgound dos eixos (`Axes`)</a></h2>

<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/generico/banner.png" alt="banner provisório " >
{: .text-center}

Para alterar a cor do fundo dos eixos é necessário **acessar** os eixos (`Axes`) previamente. Para fazer isto, utilizamos o `plt.gca()`. Contudo, é necessário atribuir os eixos a uma variável, que geralmente recebe o nome de `ax` para representar os eixos:
{: .text-justify}

```python
ax = plt.gca()
```

Esta método permite a edição de diversas outras propriedades dos eixos do gráfico, sendo uma delas o backgound dos eixos, o que é feito aplicando o método `ax.set_facecolor()`. Este método recebe como parâmetro o nome da cor que o background do gráfico terá. Por exemplo, para alterar a cor do backgound do gráfico para amarelo:
{: .text-justify}

```python
ax.set_facecolor('yellow')
```

O método `set_facecolor()` deve ser aplicado antes de `plt.show()` e antes de `plt.savefig()` para que a cor do background seja efetivamente alterada.
{: .text-justify}

```python
plt.figure(figsize=(8,6))
plt.scatter(x[0], y[0], label=raca_cachorro[0], edgecolor='k', facecolor='none', marker='o', s = marker_size)
plt.scatter(x[1], y[1], label=raca_cachorro[1], edgecolor='k', facecolor='none', marker='s', s = marker_size)
plt.scatter(x[2], y[2], label=raca_cachorro[2], edgecolor='k', facecolor='none', marker='p', s = marker_size)
plt.scatter(x[3], y[3], label=raca_cachorro[3], edgecolor='k', facecolor='none', marker='*', s = marker_size)
plt.scatter(x[4], y[4], label=raca_cachorro[4], edgecolor='k', facecolor='none', marker='v', s = marker_size)
plt.scatter(x[5], y[5], label=raca_cachorro[5], edgecolor='k', facecolor='none', marker='^', s = marker_size)
plt.scatter(x[6], y[6], label=raca_cachorro[6], edgecolor='k', facecolor='none', marker='<', s = marker_size)
plt.scatter(x[7], y[7], label=raca_cachorro[7], edgecolor='k', facecolor='none', marker='>', s = marker_size)
plt.scatter(x[8], y[8], label=raca_cachorro[8], edgecolor='k', facecolor='k', marker='x', s = marker_size)
plt.scatter(x[9], y[9], label=raca_cachorro[9], edgecolor='k', facecolor='none', marker='D', s = marker_size)
plt.scatter(x[10], y[10], label=raca_cachorro[10], edgecolor='k', facecolor='none', marker='H', s = marker_size)
plt.legend(fontsize=12, bbox_to_anchor=(1.,1.))
plt.xlabel("Peso (kg)", labelpad=15)
plt.ylabel("Altura (cm)", labelpad=15)
plt.title("Relação entre peso e altura de diversas raças de cachorros", pad=15)
ax = plt.gca()
ax.set_facecolor('yellow')
plt.savefig("grafico-background-04.png", dpi=100)
plt.show()
```


*Figura 5* - Gráfico de dispersão exportando com o `Axes` na cor amarela.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/16/grafico-background-04.png" alt="gráfico de dispersão desenhado utilizando o **matplotlib**  com o Axes na cor amarela">
{: .text-center}

<br>


<h2><a style="color:black" id="">Adicionando transparência</a></h2>

<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/generico/banner.png" alt="banner provisório " >
{: .text-center}

Em alguns casos, especialmente em posters e banners, é interessante que o gráfico tenha transparência, de forma a facilitar a adição de outros elementos no banner/poster, evitando problemas de sobreposição.
{: .text-justify}

*Gif 2* - Gráfico de dispersão exportando com background transparente.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/16/gif-borda-transparente-03.gif" alt="gráfico de dispersão desenhado utilizando o **matplotlib**  com a background transparente">
{: .text-center}

<br>

Para exportar o gráfico com o background transparente, basta passar como `True` o parâmetro `transparent` em `plt.savefig()`.
{: .text-justify}

```python
plt.figure(figsize=(8,6))
plt.scatter(x[0], y[0], label=raca_cachorro[0], edgecolor='k', facecolor='none', marker='o', s = marker_size)
plt.scatter(x[1], y[1], label=raca_cachorro[1], edgecolor='k', facecolor='none', marker='s', s = marker_size)
plt.scatter(x[2], y[2], label=raca_cachorro[2], edgecolor='k', facecolor='none', marker='p', s = marker_size)
plt.scatter(x[3], y[3], label=raca_cachorro[3], edgecolor='k', facecolor='none', marker='*', s = marker_size)
plt.scatter(x[4], y[4], label=raca_cachorro[4], edgecolor='k', facecolor='none', marker='v', s = marker_size)
plt.scatter(x[5], y[5], label=raca_cachorro[5], edgecolor='k', facecolor='none', marker='^', s = marker_size)
plt.scatter(x[6], y[6], label=raca_cachorro[6], edgecolor='k', facecolor='none', marker='<', s = marker_size)
plt.scatter(x[7], y[7], label=raca_cachorro[7], edgecolor='k', facecolor='none', marker='>', s = marker_size)
plt.scatter(x[8], y[8], label=raca_cachorro[8], edgecolor='k', facecolor='k', marker='x', s = marker_size)
plt.scatter(x[9], y[9], label=raca_cachorro[9], edgecolor='k', facecolor='none', marker='D', s = marker_size)
plt.scatter(x[10], y[10], label=raca_cachorro[10], edgecolor='k', facecolor='none', marker='H', s = marker_size)
plt.legend(fontsize=12)
plt.xlabel("Peso (kg)", labelpad=15)
plt.ylabel("Altura (cm)", labelpad=15)
plt.title("Relação entre peso e altura de diversas raças de cachorros", pad=15)
plt.savefig("grafico-background-05.png", dpi=300, transparent='True')
plt.show()
```

*Gif 3* - Gráfico de dispersão exportando com background transparente.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/16/gif-borda-transparente-02.gif" alt="gráfico de dispersão desenhado utilizando o **matplotlib**  com a background transparente">
{: .text-center}

<br>

Mas observe que as legendas não ficaram completamente transparentes, pois por padrão elas não são completamente transparentes, e é necessário alterar essa transparência diretamente em `plt.legend()`, o que é feito passando um número `float` para  o parâmetro `framealpha`, sendo que `0.0` é completamente transparente, e `1.0` é completamente opaco.
{: .text-justify}

Dessa forma, para deixar a legenda transparente, basta:

```python
plt.legend(framealpha=0.0)
```

*Gif 4* - Gráfico de dispersão exportando com background transparente.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/16/gif-borda-transparente-03.gif" alt="gráfico de dispersão desenhado utilizando o **matplotlib**  com a background transparente">
{: .text-center}

<br>

<form id = "quiz" name = "quiz">

<p><strong>Como deixar o gráfico exportado fique com espaçamento justo?</strong></p>

<input type = "radio" id = "mc" name = "question1" value = "a"> Passar o parâmetro <code>tight = True</code> em <code>plt.scatter()</code>
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "b"> Passar o parâmetro <code>tight = True</code> em <code>plt.Figure()</code>
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "c"> Passar o parâmetro <code>bbox_inches = True</code> em <code>plt.savefig()</code>
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "d"> Passar o parâmetro <code>bbox_inches = 'tight'</code> em <code>plt.savefig()</code>
<p style="font-size: 50%"></p>
<p></p>
<input id = "button" type = "button" class="btn btn--info" value = "Enviar" onclick = "check();">
</form>

<div id = "after_submit">
<p style="font-size: 120%" id = "message"></p>
</div>


<br>

<p style="text-align: center">
  <a href="/Curso-matplotlib-15" class="btn btn--success">Anterior</a>
  <a href="/Curso-matplotlib-17" class="btn btn--success">Próximo</a>
</p>


<script>
function check(){
	var question1 = document.quiz.question1.value;
	var messages = ["  Incorreto 😔! <br> O <code>plt.scatter()</code> não tem o parâmetro <code>tight</code>!",
  " 😔 Incorreto ! <br>  O <code>plt.Figure()</code> não tem o parâmetro <code>tight</code>! ",
  " Incorreto! 😔  <br>  O parâmetro <code>bbox_inches</code> não aceita valores boleanos!",
  " 🎉 Correto! 🥳️ Esta é uma das formas de deixar o gráfico com espaçamento justo!",
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
