---
title: "Curso matplotlib - Elementos auxiliares (elemento de passo)"
data: 2021-08-01
tags: []
header:
  image: "/images/chess.jpg"
  image_description: "Chess pieces"
excerpt: "matplotlib"
locale: "pt-br"
---

<br>

O elemento de passo, ou de "escada", é uma forma de desenhar linhas em "escadinha". São úteis para fazer gráficos de acumulação.
{: .text-justify}

Para adicionar uma linha na forma de escada, passamos duas sequências contendo os valores de `x` e `y` da escada através de ```plt.step()```.
{: .text-justify}

**Exemplo:**

```python
plt.figure(figsize=(8,6))
plt.scatter(x,y)
plt.step(x,y)
plt.show()
```

*Figura 1* - Gráfico de dispersão com reta em "escadinha".
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-elementos-auxiliares/40/grafico-elementos-auxiliares-01.png" alt="gráfico de dispersão genérico desenhado com o matplotlib, como reta em 'escadinha'  " >
{: .text-center}

<br>

As linhas são desenhadas utilizando o valor de `x` como referência, e temos 3 opções para a referência. Para alterar estas opções, basta passar o parâmetro `where` com uma das seguintes opções:
{: .text-justify}

- ```'pre'``` (padrão): a linha é desenhada primeiro no eixo `y`, e depois vai para a direita no eixo `x`.

**Exemplo:**

```python
plt.figure(figsize=(8,6))
plt.scatter(x,y)
plt.step(x,y, where='pre')
plt.show()
```

*Figura 2* - Gráfico de dispersão com reta em "escadinha" utilizando o `where='pre'`.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-elementos-auxiliares/40/grafico-elementos-auxiliares-02.png" alt="gráfico de dispersão genérico desenhado com o matplotlib, como reta em 'escadinha'  " >
{: .text-center}

<br>


- `'post'`:  a linha é desenhada primeiro no eixo `x`, e depois vai para a direção do eixo `y`.

**Exemplo:**

```python
plt.figure(figsize=(8,6))
plt.scatter(x,y)
plt.step(x,y, where='post')
plt.show()

```

*Figura 3* - Gráfico de dispersão com reta em "escadinha" utilizando o `where='post'`.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-elementos-auxiliares/40/grafico-elementos-auxiliares-03.png" alt="gráfico de dispersão genérico desenhado com o matplotlib, como reta em 'escadinha'  " >
{: .text-center}

<br>


- `'mid'`:  a linha é desenhada até a metade do eixo `x`, depois "sobe" até o valor de `y`, e então segue até a outra metade do eixo `x`.

```python
plt.figure(figsize=(8,6))
plt.scatter(x,y)
plt.step(x,y, where='mid')
plt.show()
```

*Figura 4* - Gráfico de dispersão com reta em "escadinha" utilizando o `where='mid'`.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-elementos-auxiliares/40/grafico-elementos-auxiliares-04.png" alt="gráfico de dispersão genérico desenhado com o matplotlib, como reta em 'escadinha'  " >
{: .text-center}

<br>


**ATENÇÃO**: observe que os pontos dos gráficos acima foram adicionados utilizando o `plt.scatter()`, e não são provenientes do `plt.step()`. Contudo, é possível inserir os pontos no gráfico, passando o parâmetro `marker` em `plt.step()`, seguindo a mesma lógica vista anteriormente.
{: .text-justify}

Por exemplo:

```python
plt.figure(figsize=(8,6))
plt.step(x,y, where='mid', marker="o")
plt.show()
```

*Figura 5* - Gráfico de passo com reta em "escadinha" utilizando o `where='mid'`.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-elementos-auxiliares/40/grafico-elementos-auxiliares-04.png" alt="gráfico de passo genérico desenhado com o matplotlib, como reta em 'escadinha'  " >
{: .text-center}

<br>

É possível editar as linhas e os marcadores do `plt.step()` de forma muito semelhante ao que vimos anteriormente. Maiores informações na [documentação](https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.step.html#matplotlib.pyplot.step).


<br>

<form id = "quiz" name = "quiz">

<p><strong>Qual é a função do parâmetro where quando utilizado em plt.step()?</strong></p>

<input type = "radio" id = "mc" name = "question1" value = "a"> O método <code>plt.step()</code> não tem um parâmetro chamado <code>where</code>.
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "b"> Determinar se o tamanho de cada escada é sempre igual.
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "c"> Determinar a forma como a "escada" será desenhada.
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "d"> Inserir marcadores no gráfico de passo.
<p style="font-size: 50%"></p>
<p></p>
<input id = "button" type = "button" class="btn btn--info" value = "Enviar" onclick = "check();">
</form>

<div id = "after_submit">
<p style="font-size: 120%" id = "message"></p>
</div>


<br>

<p style="text-align: center">
  <a href="/Curso-matplotlib-39" class="btn btn--success">Anterior</a>
  <a href="/Curso-matplotlib-41" class="btn btn--success">Próximo</a>
</p>



<script>
function check(){
	var question1 = document.quiz.question1.value;
	var messages = [" Incorreto! 😔 <br> O método <code>plt.step()</code> tem sim o parâmetro <code>where</code>.",
  " 😔 Incorreto! 😔  <br> O tamanho de cada escada é determinado pelos valores de <code>x</code> e <code>y</code>.",
  "🎉 Correto! 🥳️ <br> Esta é a função do parâmetro <code>where</code> ",
  " 😔 Incorreto! <br> O parâmetro utilizado para inserir marcadores no gráfico de passo é o parâmetro <code>marker</code>!",
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
