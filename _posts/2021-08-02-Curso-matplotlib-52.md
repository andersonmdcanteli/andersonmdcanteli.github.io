---
title: "Curso matplotlib - Gráfico de barras verticais (agrupado)"
data: 2021-08-02
tags: []
header:
  image: "/images/chess.jpg"
  image_description: "Chess pieces"
excerpt: "matplotlib"
locale: "pt-br"
---

<br>

Para gerar um gráfico de barras agrupado, é necessário gerar uma série de elementos de gráficos de barra com um mesmo valor de `x` (arbitrário). Mas os valores em `x` devem estar **espaçados** de acordo com a **largura da barra**.
{: .text-justify}

Para exemplificar este caso, seguimos utilizando um conjunto de dados de preço de frutas, mas agora temos o preço de cada uma das frutas em 4 lojas diferentes:
{: .text-justify}


```python
frutas = ['Banana Caturra', 'Laranja Pêra', 'Limão Tahiti', 'Maçã Gala', 'Mamão Formosa']
loja_1 = [1.77, 2.49, 2.29, 3.98, 2.98]
loja_2 = [0.99, 3.15, 4.71, 5.19, 4.49]
loja_3 = [3.68, 2.97, 2.58, 4.77, 6.25]
loja_4 = [2.49, 2.99, 2.79, 3.96, 4.99]
```

Para plotar o gráfico de forma mais simples, vamos criar um *numpy array* com valores igualmente espaçados (para facilitar), pois é mais simples manipular as posições das barras. Como no exemplo temos 5 produtos, vou criar um array com 5 elementos. Mas antes de criar este array, é preciso importar o ```numpy```:
{: .text-justify}

```python
import numpy as np
```

Agora criamos o array para manipular o eixo x:

```python
x = np.arange(5)
x
```

> array([0, 1, 2, 3, 4])


Também é importante criar um variável para especificar a largura da barra (neste caso, todas as barras terão a mesma largura):
{: .text-justify}

```python
width_bar = 0.3
```

Inicialmente, vamos plotar os dados da loja 1 (que corresponde aos dados que estamos utilizando até o momento):
{: .text-justify}

```python
plt.figure(figsize=(8,6))
plt.bar(x, loja_1, label='Loja 1', width=width_bar)
plt.legend()
plt.show()
```

*Figura 1* - Gráfico de barras verticais agrupado.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-barras-verticais/52/grafico-barras-verticais-01.png" alt="gráfico de barras verticais agrupado desenhado com o matplotlib." >
{: .text-center}

<br>

Agora vamos adicionar um novo elemento de ```plt.bar()``` para a loja 2:

```python
plt.figure(figsize=(8,6))
plt.bar(x, loja_1, label='Loja 1', width=width_bar)
plt.bar(x, loja_2, label='Loja 2', width=width_bar)
plt.legend()
plt.show()
```

*Figura 2* - Gráfico de barras verticais agrupado.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-barras-verticais/52/grafico-barras-verticais-02.png" alt="gráfico de barras verticais agrupado desenhado com o **matplotlib**." >
{: .text-center}

<br>


Observe que as barras foram sobrepostas, sendo que os dados da loja 2 estão por cima dos dados da loja 1. Isto aconteceu pois os valores de `x` são iguais para os dois conjuntos de dados.
{: .text-justify}

Para deixar as barras lado a lado, podemos reduzir a posição (em `x`) de um do conjunto de dados em exatamente a largura das barras, ou seja:
{: .text-justify}

```python
x - width_bar
```

> array([-0.3,  0.7,  1.7,  2.7,  3.7])

Dessa forma:

```python
plt.figure(figsize=(8,6))
plt.bar(x, loja_1, label='Loja 1', width=width_bar)
plt.bar(x-width_bar, loja_2, label='Loja 2', width=width_bar)
plt.legend()
plt.show()
```

*Figura 3* - Gráfico de barras verticais agrupado.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-barras-verticais/52/grafico-barras-verticais-03.png" alt="gráfico de barras verticais agrupado desenhado com o matplotlib." >
{: .text-center}

<br>


Observe que o *tick* acabou ficando no meio da barra da loja 1, e não no centro de cada grupo. Para resolver isto, no caso de termos apenas 2 elementos de gráfico de barras, passamos o parâmetro ```align='edge'``` para ambos os elementos:
{: .text-justify}

```python
plt.figure(figsize=(8,6))
plt.bar(x, loja_1, label='Loja 1', width=width_bar, align='edge')
plt.bar(x-width_bar, loja_2, label='Loja 2', width=width_bar, align='edge')
plt.legend()
plt.show()
```

*Figura 4* - Gráfico de barras verticais agrupado.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-barras-verticais/52/grafico-barras-verticais-04.png" alt="gráfico de barras verticais agrupado desenhado com o **matplotlib**." >
{: .text-center}

<br>


Seguindo a mesma lógica, podemos adicionar os dados da loja 3, somando ao array `x` a largura das barras:
{: .text-justify}


```python
plt.figure(figsize=(8,6))
plt.bar(x, loja_1, label='Loja 1', width=width_bar)
plt.bar(x-width_bar, loja_2, label='Loja 2', width=width_bar)
plt.bar(x+width_bar, loja_3, label='Loja 3', width=width_bar)
plt.legend()
plt.show()
```


*Figura 5* - Gráfico de barras verticais agrupado.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-barras-verticais/52/grafico-barras-verticais-05.png" alt="gráfico de barras verticais agrupado desenhado com o **matplotlib**." >
{: .text-center}

<br>


E para adicionar a quarta loja, seguimos a mesma lógica, utilizando uma maior distância para as barras mais externas:
{: .text-justify}

```python
plt.figure(figsize=(8,6))
plt.bar(x-2*width_bar, loja_1, label='Loja 1', width=width_bar, align='edge')
plt.bar(x-width_bar, loja_2, label='Loja 2', width=width_bar, align='edge')
plt.bar(x+width_bar, loja_3, label='Loja 3', width=-width_bar, align='edge')
plt.bar(x+2*width_bar, loja_4, label='Loja 4', width=-width_bar, align='edge')
plt.legend()
plt.show()
```

*Figura 6* - Gráfico de barras verticais agrupado.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-barras-verticais/52/grafico-barras-verticais-06.png" alt="gráfico de barras verticais agrupado desenhado com o matplotlib." >
{: .text-center}

<br>

Mas observe que as barras de cada produto se sobrepuseram, o que aconteceu pois a largura da barra esta grande em relação aos valores de `x`. Poderíamos contornar isto aumentando os valores no array `x` (e mais espaçados) ou reduzir a largura da barra.
{: .text-justify}

Ao reduzir a largura da barra para `0.1` por exemplo:

```python
width_bar = 0.1
plt.figure(figsize=(8,6))
plt.bar(x-2*width_bar, loja_1, label='Loja 1', width=width_bar, align='edge')
plt.bar(x-width_bar, loja_2, label='Loja 2', width=width_bar, align='edge')
plt.bar(x+width_bar, loja_3, label='Loja 3', width=-width_bar, align='edge')
plt.bar(x+2*width_bar, loja_4, label='Loja 4', width=-width_bar, align='edge')
plt.legend()
plt.show()
```

*Figura 7* - Gráfico de barras verticais agrupado.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-barras-verticais/52/grafico-barras-verticais-07.png" alt="gráfico de barras verticais agrupado desenhado com o matplotlib." >
{: .text-center}

<br>

Mas se aumentar o tamanho e espaçamento de `x`:

```python
x = np.arange(0,10,2)
x
```

> array([0, 2, 4, 6, 8])

E aumentar o tamanho da barra par 0.3, obtemos este gráfico:

```python
width_bar = 0.3
plt.figure(figsize=(8,6))
plt.bar(x-2*width_bar, loja_1, label='Loja 1', width=width_bar, align='edge')
plt.bar(x-width_bar, loja_2, label='Loja 2', width=width_bar, align='edge')
plt.bar(x+width_bar, loja_3, label='Loja 3', width=-width_bar, align='edge')
plt.bar(x+2*width_bar, loja_4, label='Loja 4', width=-width_bar, align='edge')
plt.legend()
plt.show()
```

*Figura 8* - Gráfico de barras verticais agrupado.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-barras-verticais/52/grafico-barras-verticais-08.png" alt="gráfico de barras verticais agrupado desenhado com o matplotlib." >
{: .text-center}

<br>

É possível substituir os números do eixo `x` pelo nome dos produtos que estão armazenados na variável ```frutas```, o que fazemos utilizando o ```plt.xticks()```. Neste caso, passamos como primeiro parâmetro os valores originais do eixo `x` (que é a variável `x` neste caso), e passamos como segundo parâmetro uma sequência com os valores que irão substituir os valores de `x`.
{: .text-justify}

```python
plt.figure(figsize=(8,6))
plt.bar(x-2*width_bar, loja_1, label='Loja 1', width=width_bar, align='edge')
plt.bar(x-width_bar, loja_2, label='Loja 2', width=width_bar, align='edge')
plt.bar(x+width_bar, loja_3, label='Loja 3', width=-width_bar, align='edge')
plt.bar(x+2*width_bar, loja_4, label='Loja 4', width=-width_bar, align='edge')
plt.legend()
plt.xticks(x, frutas)
plt.show()
```

*Figura 9* - Gráfico de barras verticais agrupado.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-barras-verticais/52/grafico-barras-verticais-09.png" alt="gráfico de barras verticais agrupado desenhado com o matplotlib." >
{: .text-center}

<br>


<form id = "quiz" name = "quiz">

<p><strong>Qual o fundamento da técnica utilizada para desenhar um gráfico de barras agrupado?</strong></p>

<input type = "radio" id = "mc" name = "question1" value = "a"> Utilizar o método <code>plt.bar_group()</code>
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "b"> Inserir vários elementos de <code>plt.bar()</code> com a espessura da barra de cada elemento com tamanho igual
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "c"> Inserir vários elementos de <code>plt.bar()</code> variando a posição inicial, de cada elemento, em relação a espessura da barra, que também tem de variar
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "d"> Inserir vários elementos de <code>plt.bar()</code> variando a posição inicial, de cada elemento, em relação a espessura da barra, que deve ser constante
<p style="font-size: 50%"></p>
<p></p>
<input id = "button" type = "button" class="btn btn--info" value = "Enviar" onclick = "check();">
</form>

<div id = "after_submit">
<p style="font-size: 120%" id = "message"></p>
</div>


<br>

<p style="text-align: center">
  <a href="/Curso-matplotlib-51" class="btn btn--success">Anterior</a>
  <a href="/Curso-matplotlib-53" class="btn btn--success">Próximo</a>
</p>


<script>
function check(){
	var question1 = document.quiz.question1.value;
	var messages = [" Incorreto! 😔 <br> Não existe o método <code>plt.bar_group()</code>!",
  " 😔 Incorreto! 😔  <br> Ao utilizar esta forma, as barras com mesmo valor de <code>x</code> serão sobrepostas.",
  " 🥳️ Correto 🎉! <br> É possível desenhar um gráfico de barras agrupado desta forma; entretanto, o fato da espessura das barras não ser constante irá trazer <i><strong>muitas dificuldades desnecessárias</i></strong> 😨 ",
  " 🎉 Correto! 🥳️ <br> Esta é uma descrição possível para a técnica utilizada de desenhar gráficos de barras agrupado!",
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
