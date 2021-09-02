---
title: "Curso matplotlib - Elementos auxiliares (Flechas)"
data: 2021-08-01
tags: []
header:
  image: "/images/chess.jpg"
  image_description: "Chess pieces"
excerpt: "matplotlib"
locale: "pt-br"
---

<br>

Podemos utilizar o `plt.arrow()` para adicionar uma flecha utilizando o **matplotlib**. Este elemento necessita de pelo menos 4 parâmetros, sendo os dois primeiros (`x` e `y`) as coordenadas de `x` e `y` onde a flecha inicia, e os outros dois são as distâncias em `x` (`dx`) e `y` (`dy`) até o final da seta.
{: .text-justify}

Dessa forma, a flecha vai sair da coordenada `(x,y)` e irá até a coordenada `(x + dx, y + dy)`.
{: .text-justify}

**Exemplo:**

```python
plt.figure(figsize=(8,6))
plt.scatter(x,y)
plt.arrow(2.5, 1, 0.5, 0.5)
plt.show()
```

*Figura 1* - Gráfico de dispersão com flecha
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-elementos-auxiliares/42/grafico-elementos-auxiliares-01.png" alt="gráfico de dispersão genérico desenhado com o matplotlib, com flecha  " >
{: .text-center}

<br>

Observe que a flecha ficou pequena, o que acontece devido ao outros elementos do gráfico e aos valores padrão para as flechas, em geral, serem pequenos. Retirando os pontos e plotando o gráfico:
{: .text-justify}

```python
plt.arrow(2.5,1, 0.5,0.5)
plt.show()
```

*Figura 2* - Gráfico com flecha
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-elementos-auxiliares/42/grafico-elementos-auxiliares-02.png" alt="gráfico desenhado com o matplotlib com flecha  " >
{: .text-center}

<br>

Ainda temos uma flecha com a cabeça pequena, mas agora esta evidente que é uma flecha. Podemos alterar diversos parâmetros para melhorar esta flecha.
{: .text-justify}

<h2><a style="color:black" id="largura-corpo-flecha">Largura do corpo da flecha</a></h2>

O parâmetro `width` controla a largura do corpo da flecha (padrão é `0.001`).

**Exemplo:**

```python
plt.figure(figsize=(8,6))
plt.scatter(x,y)
plt.arrow(2.5,1, 0.5,0.5, width=0.01)
plt.show()
```

*Figura 3* - Gráfico de dispersão com flecha
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-elementos-auxiliares/42/grafico-elementos-auxiliares-03.png" alt="gráfico de dispersão genérico desenhado com o matplotlib, com flecha  " >
{: .text-center}

<br>

**Exemplo:**

```python
plt.figure(figsize=(8,6))
plt.scatter(x,y)
plt.arrow(2.5,1, 0.5,0.5, width=0.1)
plt.show()
```

*Figura 4* - Gráfico de dispersão com flecha
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-elementos-auxiliares/42/grafico-elementos-auxiliares-04.png" alt="gráfico de dispersão genérico desenhado com o matplotlib, com flecha  " >
{: .text-center}

<br>


Por padrão, o tamanho da flecha não inclui a ponta da flecha. Por isto que no gráfico acima, o intervalo de inicio e fim da flecha é maior do que o setado pelas coordenadas `(x, y)` e `(x+dx, y+dy)`.
{: .text-justify}

Para fazer com que o comprimento da flecha inclua a ponta, basta passar o parâmetro `length_includes_head` como `True`(padrão é `False`):
{: .text-justify}

**Exemplo:**

```python
plt.figure(figsize=(8,6))
plt.scatter(x,y)
plt.arrow(2.5,1, 0.5,0.5, width=0.1, length_includes_head=True)
plt.show()
```


*Figura 5* - Gráfico de dispersão com flecha
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-elementos-auxiliares/42/grafico-elementos-auxiliares-05.png" alt="gráfico de dispersão genérico desenhado com o matplotlib, com flecha  " >
{: .text-center}

<br>

<h2><a style="color:black" id="largura-ponto-flecha">Largura da ponta da flecha</a></h2>


Podemos controlar a largura da ponta da flecha através do parâmetro `head_width`. Idealmente, este parâmetro deve ser proporcional a outras partes da flecha. Como padrão, temos que `head_width = 3*width`.
{: .text-justify}

**Exemplo:**

```python
plt.figure(figsize=(8,6))
plt.scatter(x,y)
plt.arrow(2.5,1, 0.5,0.5, width=0.1, length_includes_head=True, head_width=3*0.1)
plt.show()
```

*Figura 6* - Gráfico de dispersão com flecha
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-elementos-auxiliares/42/grafico-elementos-auxiliares-06.png" alt="gráfico de dispersão genérico desenhado com o matplotlib, com flecha  " >
{: .text-center}

<br>

**Exemplo:**

```python
plt.figure(figsize=(8,6))
plt.scatter(x,y)
plt.arrow(2.5,1, 0.5,0.5, width=0.1, length_includes_head=True, head_width=2*0.1)
plt.show()
```

*Figura 7* - Gráfico de dispersão com flecha
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-elementos-auxiliares/42/grafico-elementos-auxiliares-07.png" alt="gráfico de dispersão genérico desenhado com o matplotlib, com flecha  " >
{: .text-center}

<br>

**Exemplo:**

```python
plt.figure(figsize=(8,6))
plt.scatter(x,y)
plt.arrow(2.5,1, 0.5,0.5, width=0.1, length_includes_head=True, head_width=1*0.1)
plt.show()
```

*Figura 8* - Gráfico de dispersão com flecha
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-elementos-auxiliares/42/grafico-elementos-auxiliares-08.png" alt="gráfico de dispersão genérico desenhado com o matplotlib, com flecha  " >
{: .text-center}

<br>


<h2><a style="color:black" id="comprimento-ponta-flecha">Comprimento da ponta da flecha</a></h2>


Também podemos controlar o comprimento da ponta da flecha, o que é feito através do parâmetro `head_length`. Idealmente, este parâmetro deve ser proporcional a alguma parte da flecha, geralmente a largura da flecha (o padrão é `1.5*head_width`).
{: .text-justify}

**Exemplo:**

```python
plt.figure(figsize=(8,6))
plt.scatter(x,y)
plt.arrow(2.5,1, 0.5,0.5, width=0.1, length_includes_head=True, head_length=0.5)
plt.show()
```

*Figura 9* - Gráfico de dispersão com flecha
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-elementos-auxiliares/42/grafico-elementos-auxiliares-09.png" alt="gráfico de dispersão genérico desenhado com o matplotlib, com flecha  " >
{: .text-center}

<br>

**Exemplo:**

```python
plt.figure(figsize=(8,6))
plt.scatter(x,y)
plt.arrow(2.5,1, 0.5,0.5, width=0.1, length_includes_head=True, head_length=0.1)
plt.show()
```

*Figura 10* - Gráfico de dispersão com flecha
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-elementos-auxiliares/42/grafico-elementos-auxiliares-10.png" alt="gráfico de dispersão genérico desenhado com o matplotlib, com flecha  " >
{: .text-center}

<br>

<h2><a style="color:black" id="forma-cabeça-flecha">Forma da cabeça da flecha</a></h2>

Podemos controlar a forma da ponta da flecha através do parâmetro `shape`. Temos 3 opções, sendo que o padrão `'full'` desenha uma ponta completa, `'right'` desenha apenas a parte à esquerda da ponta da flecha, e `'left'` desenha apenas a parte à direita da ponta da flecha.
{: .text-justify}

```python
plt.figure(figsize=(8,6))
plt.scatter(x,y)
plt.arrow(2.5,1, 0.5,0.5, width=0.1, length_includes_head=True, head_length=0.1, shape='right')
plt.show()
```

*Figura 11* - Gráfico de dispersão com flecha
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-elementos-auxiliares/42/grafico-elementos-auxiliares-11.png" alt="gráfico de dispersão genérico desenhado com o matplotlib, com flecha  " >
{: .text-center}

<br>

**Exemplo:**

```python
plt.figure(figsize=(8,6))
plt.scatter(x,y)
plt.arrow(2.5,1, 0.5,0.5, width=0.1, length_includes_head=True, head_length=0.1, shape='left')
plt.show()
```

*Figura 12* - Gráfico de dispersão com flecha
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-elementos-auxiliares/42/grafico-elementos-auxiliares-12.png" alt="gráfico de dispersão genérico desenhado com o matplotlib, com flecha  " >
{: .text-center}

<br>

Maiores informações na [documentação](https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.arrow.html#matplotlib.pyplot.arrow).

<br>

<p style="text-align: center">
  <a href="/Curso-matplotlib-41" class="btn btn--success">Anterior</a>
  <a href="/Curso-matplotlib-43" class="btn btn--success">Próximo</a>
</p>
