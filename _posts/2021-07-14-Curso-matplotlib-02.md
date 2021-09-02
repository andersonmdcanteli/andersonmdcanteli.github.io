---
title: "Curso matplotlib - Interfaces"
data: 2021-07-14
tags: []
header:
  image: "/images/chess.jpg"
  image_description: "Chess pieces"
excerpt: "matplotlib"
locale: "pt-br"
---

<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/generico/banner.png" alt="banner provisório " >
{: .text-center}


<br>

Temos dois métodos diferentes para desenhar gráficos utilizando o **matplotlib**: utilizando a orientação a objetos ou de forma direta. Mas para poder utilizar a biblioteca, é necessário importa-la antes:
{: .text-justify}

```python
import matplotlib.pyplot as plt
```

É dentro da classe `matplotlib.pyplot` que temos acesso a todas as funções para desenhar os mais diversos tipos de gráficos. Entretanto, como este termo é muito longo, é mais adequado dar um *alias* (apelido) à esta classe, que é o *alias* `plt`.
{: .text-justify}


<h2><a style="color:black">Forma direta (MATLAB style)</a></h2>

Esta forma utiliza as funções de forma bastante direta, criando e gerenciando as figuras e eixos de forma automática. Ela é inspirada no estilo de desenhar gráficos do MATLAB, que é uma outra linguagem de programação muito utilizada no meio cientifico.
{: .text-justify}

Exemplo:

```python
plt.plot([1,2,3,4,5],[1,2,3,5,7], label='Números primos') # criando o gráfico
plt.xlabel('x label') # adicionando nome no eixo x
plt.ylabel('y label') # adicionando nome no eixo y
plt.title('Meu título incrível') # adicionando titulo ao gráfico
plt.legend() # adicionando a legenda
plt.show() # apresentando o gráfico
```

*Figura 1* - Gráfico gerado com o estilo direto do **matplotlib**.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/01/matlab-style.png" alt="grafico de linhas desenhado utilizando o **matplotlib** com o estilo do MATLAB" >
{: .text-center}

<h2><a style="color:black">Orientação a objetos</a></h2>

A outra forma é através da orientação a objetos, que explicitamente cria figuras e eixos, sendo que os elementos gráficos são adicionados através da adição de métodos.
{: .text-justify}

Exemplo:

```python
fig, ax = plt.subplots()  # criando uma instância de figura e de eixo
ax.plot([1,2,3,4,5],[1,2,3,5,7], label='Números primos') # criando o gráfico
ax.set_xlabel('x label') # adicionando nome no eixo x
ax.set_ylabel('y label') # adicionando nome no eixo y
ax.set_title("Meu título incrível") # adicionando titulo ao gráfico
ax.legend() # adicionando a legenda
plt.show() # apresentando o gráfico
```

*Figura 2* - Gráfico gerado com a orientação a objetos do **matplotlib**.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/01/orientacao-objetos.png" alt="gráfico de linhas desenhado utilizando o **matplotlib** com o a orientação a objetos" >
{: .text-center}


Nós iremos utilizar o estilo direto de criar gráficos em toda a base do curso, de forma que você compreenda o funcionamento do **matplotlib**, pois esta é uma forma mais simples. Utilizar a orientação a objetos é mais eficiente, entretanto, requer maior conhecimento em Python, e por isso, vamos utilizar esta forma mais a frente do curso.
{: .text-justify}


<br>

<p style="text-align: center">
  <a href="/Curso-matplotlib-01" class="btn btn--success">Anterior</a>
  <a href="/Curso-matplotlib-03" class="btn btn--success">Próximo</a>
</p>
