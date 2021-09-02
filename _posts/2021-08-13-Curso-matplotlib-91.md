---
title: "Boxplot (Elementos do boxplot)"
data: 2021-08-13
tags: []
header:
  image: "/images/chess.jpg"
  image_description: "Chess pieces"
excerpt: "matplotlib"
locale: "pt-br"
---


<br>

Cada boxplot é formado por uma série de elementos, como os *whiskers*, o *box*, a *mediana*, os *outilers*, etc. Cada um deles pode ser editado individualmente através do parâmetro ***props*** de cada elemento.
{: .text-justify}


<h2><a style="color:black" id="boxplot-caps">Caps</a></h2>

Para alterar as propriedades dos caps, basta passar um `dict` para o parâmetro `capprops`, indicando a propriedade que deseja alterar (`key`) e o novo valor (`value`).
{: .text-justify}

Por exemplo, para alterar a cor dos caps, passamos a `key` como `color` e o `value` com o nome da cor desejada. As cores disponíveis são as mesmas vistas <a href="/Curso-matplotlib-08#cor-marcadores">anteriormente</a>.
{: .text-justify}

Por exemplo, para deixar o caps na cor <span style="color:magenta">magenta</span>:
{: .text-justify}

```python
plt.figure(figsize=(8,6))
plt.boxplot([altura_11_anos, altura_12_anos], positions=[0,0.5], labels=["11 anos", "12 anos"],
           capprops=dict(color='m'))
plt.show()
```

*Figura 1* - Gráfico de boxplot para a altura das crianças de 11 e 12 anos - caps na cor magenta.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/boxplot/91/boxplot-01.png" alt="gráfico tipo boxplot desenhado com matplotlib, caps na cor magenta" >
{: .text-center}

<br>

Para alterar o estilo do caps, passamos a `key` `linestyle` com o estilo de linha desejado como `value`. Os estilos disponíveis são os mesmos vistos <a href="/Curso-matplotlib-20#estilo-linha">anteriormente</a>.
{: .text-justify}

Por exemplo:


*Figura 2* - Gráfico de boxplot para a altura das crianças de 11 e 12 anos - caps tracejados.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/boxplot/91/boxplot-02.png" alt="gráfico tipo boxplot desenhado com matplotlib, caps tracejados" >
{: .text-center}

<br>


Para alterar a espessura do caps, passamos um número (`int` ou `float`) para a `key` `linewidth` com a espessura da linha desejada (`value`). Por exemplo:
{: .text-justify}

```python
plt.figure(figsize=(8,6))
plt.boxplot([altura_11_anos, altura_12_anos], positions=[0,0.5], labels=["11 anos", "12 anos"],
           capprops=dict(color='m', linestyle='--', linewidth=3))
plt.show()
```

*Figura 3* - Gráfico de boxplot para a altura das crianças de 11 e 12 anos - caps mais espessos.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/boxplot/91/boxplot-03.png" alt="gráfico tipo boxplot desenhado com matplotlib, caps mais espessos" >
{: .text-center}

<br>

<h2><a style="color:black" id="boxplot-box">Box</a></h2>

Para alterar as propriedades das caixas, basta passar um `dict` para o parâmetro `boxprops`, indicando a propriedade que deseja mudar (`key`) e o novo valor (`value`), de forma similar aos caps. Por exemplo:
{: .text-justify}

```python
plt.figure(figsize=(8,6))
plt.boxplot([altura_11_anos, altura_12_anos], positions=[0,0.5], labels=["11 anos", "12 anos"],
           boxprops=dict(color='m', linestyle='--', linewidth=3))
plt.show()
```

*Figura 4* - Gráfico de boxplot para a altura das crianças de 11 e 12 anos - caixa editada.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/boxplot/91/boxplot-04.png" alt="gráfico tipo boxplot desenhado com matplotlib, caixa editada" >
{: .text-center}

<br>

Contudo, para alterar a cor de preenchimento da caixa, também será necessário passar o parâmetro `patch_artist=True`.
{: .text-justify}

### Atenção

Isto vai alterar outros parâmetros, pois as caixas serão desenhadas com outro padrão.
{: .text-justify}

Por exemplo:

```python
plt.figure(figsize=(8,6))
plt.boxplot([altura_11_anos, altura_12_anos], positions=[0,0.5], labels=["11 anos", "12 anos"], patch_artist=True,
           boxprops=dict(color='m', linestyle='--', linewidth=3, facecolor='b'))
plt.show()
```

*Figura 5* - Gráfico de boxplot para a altura das crianças de 11 e 12 anos - caixa editada.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/boxplot/91/boxplot-05.png" alt="gráfico tipo boxplot desenhado com matplotlib, caixa editada" >
{: .text-center}

<br>


<h2><a style="color:black" id="boxplot-outros">Outros</a></h2>

Para alterar os outros elementos, como os whiskers, outliers, linha da mediana, e a média, utilize os seguintes parâmetros de forma similar ao feito anteriormente:
{: .text-justify}

- `whiskerprops`

- `flierprops`

- `medianprops`

- `meanprops`

<h2><a style="color:black" id="boxplot-media">Inserindo a média</a></h2>

Por padrão, o boxplot desenhado com o **matplotlib** apresenta a mediana como medida de tendência central, mas em alguns casos, é interessante adicionar a média aritmética. Para fazer isto, basta passar o parâmetro `showmeans` como `True` (o padrão é `False`, e por isso a média não é apresentada por padrão).
{: .text-justify}

Exemplo:

```python
plt.figure(figsize=(8,6))
plt.boxplot([altura_11_anos, altura_12_anos], positions=[0,0.5], labels=["11 anos", "12 anos"], showmeans=True, )
plt.show()
```

*Figura 6* - Gráfico de boxplot para a altura das crianças de 11 e 12 anos - média.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/boxplot/91/boxplot-06.png" alt="gráfico tipo boxplot desenhado com matplotlib, com o ponto da média inserido" >
{: .text-center}

<br>

Observe que a média é inserida como um ponto, e não como uma reta como a mediana.



<br>

<form id = "quiz" name = "quiz">

<p><strong>Qual é o parâmetro utilizado para alterar os whiskers, o box, a mediana, entre outros?</strong></p>

<input type = "radio" id = "mc" name = "question1" value = "a"> boxplot_props
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "b"> prop
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "c"> props
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "d"> props_boxplot
<p style="font-size: 50%"></p>
<p></p>
<input id = "button" type = "button" class="btn btn--info" value = "Enviar" onclick = "check();">
</form>

<div id = "after_submit">
<p style="font-size: 120%" id = "message"></p>
</div>

<br>


<h1><a style="color:black" id="boxplot-media">Desafio boxplot</a></h1>

Transforme o ponto desenhado para a média na Figura 6 em uma linha. Insira legendas para diferenciar a média da mediana.
{: .text-justify}

<br>

<p style="text-align: center">
  <a href="/Curso-matplotlib-90" class="btn btn--success">Anterior</a>
  <a href="/Curso-matplotlib-92" class="btn btn--success">Próximo</a>
</p>



<script>
function check(){
	var question1 = document.quiz.question1.value;
	var messages = [" Incorreto! 😔 <br> O <code>plt.boxplot()</code> não tem um parâmetro <code>boxplot_props</code>",
  " 😔 Incorreto! <br> O <code>plt.boxplot()</code> não tem um parâmetro <code>prop</code>",
  " 🎉 Correto! 🥳️ <br>",
  " 😔 Incorreto! <br>  O <code>plt.boxplot()</code> não tem um parâmetro <code>props_boxplot</code>",
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
