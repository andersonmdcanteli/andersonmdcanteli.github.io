---
title: "Curso matplotlib - Gráfico de barras verticais (preenchimento das barras)"
data: 2021-08-02
tags: []
header:
  image: "/images/chess.jpg"
  image_description: "Chess pieces"
excerpt: "matplotlib"
locale: "pt-br"
---

<br>


Além de trocar as cores das barras, podemos adicionar preenchimento a elas (texturas), de forma a diferenciar as barras de uma forma mais visual. O uso de texturas é mais adequado do que cores para publicações, embora você deva ter a simplicidade sempre em mente.
{: .text-justify}

Mas antes de adicionar texturas, vamos deixar as barras sem preenchimento e aumentar o tamanho do gráfico:
{: .text-justify}

```python
plt.figure(figsize=(14,6))
plt.bar(x-2*width_bar, loja_1, label='Loja 1', width=width_bar, align='edge', color='none', edgecolor='k')
plt.bar(x-width_bar, loja_2, label='Loja 2', width=width_bar, align='edge', color='none', edgecolor='k')
plt.bar(x+width_bar, loja_3, label='Loja 3', width=-width_bar, align='edge', color='none', edgecolor='k')
plt.bar(x+2*width_bar, loja_4, label='Loja 4', width=-width_bar, align='edge', color='none', edgecolor='k')
plt.legend(prop={'size': 16})
plt.xticks(x, frutas)
plt.show()
```

*Figura 1* - Gráfico de barras verticais agrupado.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-barras-verticais/53/grafico-barras-verticais-01.png" alt="gráfico de barras verticais agrupado desenhado com o matplotlib." >
{: .text-center}

<br>

Para adicionar estas texturas (os *hatchs*) nas barras, precisamos passar e estilo desejado através do parâmetro ```hatch``` em ```plt.bar()```. Você encontra maiores informações na [documentação](https://matplotlib.org/stable/gallery/shapes_and_collections/hatch_style_reference.html?highlight=hatch%20style%20reference).
{: .text-justify}

As opções de *hatchs* são: `"/"`, `"\"`, `"|"` , `"-"`, `"+"`, `"x"`, `"o"`, `"O"`, `"."`, `"*"`.
{: .text-justify}


<img src="https://matplotlib.org/stable/_images/sphx_glr_hatch_style_reference_001.png" alt="Resultado de cada símbolo utilizado como hatch" width="800">
{: .text-center}

<p style="text-align: center;" >Fonte: <a href="https://matplotlib.org/devdocs/gallery/shapes_and_collections/hatch_style_reference.html">www.matplotlib.org</a></p>

<br>


Por exemplo:

```python
plt.figure(figsize=(14,6))
plt.bar(x-2*width_bar, loja_1, label='Loja 1', width=width_bar, align='edge', color='none', edgecolor='k', hatch='/')
plt.bar(x-width_bar, loja_2, label='Loja 2', width=width_bar, align='edge', color='none', edgecolor='k', hatch='X')
plt.bar(x+width_bar, loja_3, label='Loja 3', width=-width_bar, align='edge', color='none', edgecolor='k', hatch='O')
plt.bar(x+2*width_bar, loja_4, label='Loja 4', width=-width_bar, align='edge', color='none', edgecolor='k', hatch='*')
plt.legend(prop={'size': 16})
plt.xticks(x, frutas)
plt.show()
```

*Figura 2* - Gráfico de barras verticais com barras estilizadas.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-barras-verticais/53/grafico-barras-verticais-02.png" alt="gráfico de barras verticais agrupado desenhado com o matplotlib." >
{: .text-center}

<br>

Também é possível aumentar a densidade de símbolos dentro das barras repetindo o símbolo. Por exemplo: `'//'`, `'\\'`, `'||'`, `'--'`, `'++'`, `'xx'`, `'oo'`, `'OO'`, `'..'`, `'**'`.
{: .text-justify}

<img src="https://matplotlib.org/stable/_images/sphx_glr_hatch_style_reference_002.png" alt="Resultado de cada símbolo duplicado utilizado como hatch" width="800">
{: .text-center}

<p style="text-align: center;" >Fonte: <a href="https://matplotlib.org/devdocs/gallery/shapes_and_collections/hatch_style_reference.html">www.matplotlib.org</a></p>

<br>

**Exemplo:**

```python
plt.figure(figsize=(14,6))
plt.bar(x-2*width_bar, loja_1, label='Loja 1', width=width_bar, align='edge', color='none', edgecolor='k', hatch='//')
plt.bar(x-width_bar, loja_2, label='Loja 2', width=width_bar, align='edge', color='none', edgecolor='k', hatch='XX')
plt.bar(x+width_bar, loja_3, label='Loja 3', width=-width_bar, align='edge', color='none', edgecolor='k', hatch='OO')
plt.bar(x+2*width_bar, loja_4, label='Loja 4', width=-width_bar, align='edge', color='none', edgecolor='k', hatch='**')
plt.legend(prop={'size': 16})
plt.xticks(x, frutas)
plt.show()
```

*Figura 3* - Gráfico de barras verticais com barras estilizadas.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-barras-verticais/53/grafico-barras-verticais-03.png" alt="gráfico de barras verticais agrupado desenhado com o matplotlib." >
{: .text-center}

<br>


Ainda é possível combinar padrões, por exemplo: `'/o'`, `'\|'`, `'|*'`, `'-\\'`, `'+o'`, `'x*'`, `'o-'`, `'O|'`, `'O.'`, `'*-'`.
{: .text-justify}

<img src="https://matplotlib.org/stable/_images/sphx_glr_hatch_style_reference_003.png" alt="Resultado de cada combinações de símbolos utilizados como hatch" width="800">
{: .text-center}

<p style="text-align: center;" >Fonte: <a href="https://matplotlib.org/devdocs/gallery/shapes_and_collections/hatch_style_reference.html">www.matplotlib.org</a></p>

<br>

Por exemplo:

```python
plt.figure(figsize=(14,6))
plt.bar(x-2*width_bar, loja_1, label='Loja 1', width=width_bar, align='edge', color='none', edgecolor='k', hatch='/o')
plt.bar(x-width_bar, loja_2, label='Loja 2', width=width_bar, align='edge', color='none', edgecolor='k', hatch='X*')
plt.bar(x+width_bar, loja_3, label='Loja 3', width=-width_bar, align='edge', color='none', edgecolor='k', hatch='O|')
plt.bar(x+2*width_bar, loja_4, label='Loja 4', width=-width_bar, align='edge', color='none', edgecolor='k', hatch='*-')
plt.legend(prop={'size': 16})
plt.xticks(x, frutas)
plt.show()
```

*Figura 4* - Gráfico de barras verticais com barras estilizadas.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-barras-verticais/53/grafico-barras-verticais-04.png" alt="gráfico de barras verticais agrupado desenhado com o **matplotlib**." >
{: .text-center}

<br>

Com todas estas combinações, temos infinitas possibilidades para utilizar como texturas. Entretanto, a simplicidade é sempre recomendada, e então utilizar os símbolos simples como `'/'`, `'\'`, `'-'`, `'x'`, `'+'`, `'O'` é *geralmente* uma melhor escolha.
{: .text-justify}


<br>


<form id = "quiz" name = "quiz">

<p><strong>Qual é o parâmetro que deve ser passado em plt.bar() para alterar o estilo das barras?</strong></p>

<input type = "radio" id = "mc" name = "question1" value = "a"> <code>style</code>
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "b"> <code>hatch</code>
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "c"> <code>hath</code>
<p style="font-size: 50%"></p>
<p></p>
<input id = "button" type = "button" class="btn btn--info" value = "Enviar" onclick = "check();">
</form>

<div id = "after_submit">
<p style="font-size: 120%" id = "message"></p>
</div>

<br>

<p style="text-align: center">
  <a href="/Curso-matplotlib-52" class="btn btn--success">Anterior</a>
  <a href="/Curso-matplotlib-54" class="btn btn--success">Próximo</a>
</p>


<script>
function check(){
	var question1 = document.quiz.question1.value;
	var messages = [" Incorreto! 😔 <br> O <code>plt.bar()</code> não tem o parâmetro <code>style</code>!",
  " 🎉 Correto! 🥳️  <br> É o parâmetro <code>hatch</code> que é utilizado para alterar o estilo das barras!",
  " 😔 Incorreto! <br> O nome do parâmetro é <code>hatch</code>, e não <code>hath</code> (observe a falta da letra <code>c</code>)",
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
