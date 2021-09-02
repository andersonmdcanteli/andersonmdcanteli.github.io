---
title: "Boxplot (edições gerais)"
data: 2021-08-13
tags: []
header:
  image: "/images/chess.jpg"
  image_description: "Chess pieces"
excerpt: "matplotlib"
locale: "pt-br"
---


<br>


<h2><a style="color:black" id="boxplot-posicao-caixa">Posições das caixas</a></h2>


Por padrão, os boxplots serão adicionados no eixo `x` com 1 unidade de distância entre si (`range(1, N+1)`, onde `N` é o número de conjuntos). Podemos alterar esta distância através do parâmetro `positions`, passando uma sequência (`list`, `tuple`, `ndarray`, etc) com as posições de desejadas.
{: .text-justify}

Por exemplo, para desenhar as caixas nas posições -1 e 1:

```python
plt.figure(figsize=(8,6))
plt.boxplot([altura_11_anos, altura_12_anos], positions=[-1,1])
plt.show()
```

*Figura 1* - Gráfico de boxplot para a altura das crianças de 11 e 12 anos - posição da caixa alterada.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/boxplot/90/boxplot-01.png" alt="gráfico tipo boxplot desenhado com matplotlib, com a posição da caixa alterada" >
{: .text-center}

<br>

Para deixar os boxplots mais próximos, basta passar valores mais próximos (`0` e `0.5` por exemplo):
{: .text-justify}

```python
plt.figure(figsize=(8,6))
plt.boxplot([altura_11_anos, altura_12_anos], positions=[0,0.5])
plt.show()
```

*Figura 2* - Gráfico de boxplot para a altura das crianças de 11 e 12 anos - posição da caixa alterada.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/boxplot/90/boxplot-02.png" alt="gráfico tipo boxplot desenhado com matplotlib, com a posição da caixa alterada" >
{: .text-center}

<br>

<h2><a style="color:black" id="boxplot-labels">Labels</a></h2>

Para dar um nome para cada boxplot, passamos uma sequência (`list`, `tuple`, `ndarray`, etc) para o parâmetro `labels`, onde cada elemento deve ser uma `str` com o nome de cada conjunto.
{: .text-justify}

Atente que os labels serão inseridos na posição de cada boxplot no eixo `x`, substituindo o número da posição do boxplot.
{: .text-justify}

Por exemplo:

```python
plt.figure(figsize=(8,6))
plt.boxplot([altura_11_anos, altura_12_anos], positions=[0,0.5], labels=["11 anos", "12 anos"])
plt.savefig("boxplot-03.png", dpi=100, bbox_inches='tight')
plt.show()
```

*Figura 3* - Gráfico de boxplot para a altura das crianças de 11 e 12 anos com labels.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/boxplot/90/boxplot-03.png" alt="gráfico tipo boxplot desenhado com matplotlib, com labels" >
{: .text-center}

<br>

ou ainda:

```python
nomes = ["11 anos", "12 anos"]
plt.figure(figsize=(8,6))
plt.boxplot([altura_11_anos, altura_12_anos], positions=[0,0.5], labels=nomes)
plt.show()
```

*Figura 4* - Gráfico de boxplot para a altura das crianças de 11 e 12 anos com labels.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/boxplot/90/boxplot-04.png" alt="gráfico tipo boxplot desenhado com matplotlib, com labels" >
{: .text-center}

<br>

<h2><a style="color:black" id="boxplot-simbolo-outliers">Símbolo dos outliers</a></h2>

Para alterar o tipo de símbolo utilizado para os outliers, basta passar a `str` correspondente ao símbolo desejado para o parâmetro `sym`. Os símbolos disponíveis são os mesmos vistos <a href="/Curso-matplotlib-08#cor-marcadores">anteriormente</a>.
{: .text-justify}

Por exemplo:

```python
plt.figure(figsize=(8,6))
plt.boxplot([altura_11_anos, altura_12_anos], positions=[0,0.5], labels=["11 anos", "12 anos"], sym="^")
plt.show()
```

*Figura 5* - Gráfico de boxplot para a altura das crianças de 11 e 12 anos com símbolo do outliers alterado.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/boxplot/90/boxplot-05.png" alt="gráfico tipo boxplot desenhado com matplotlib, com símbolo alterado" >
{: .text-center}

<br>

Para esconder este símbolo, basta passar uma `string` vazia. Entretanto, está não é uma prática recomendada, pois o outlier tem grande relevância na interpretação do boxplot.
{: .text-justify}

```python
plt.figure(figsize=(8,6))
plt.boxplot([altura_11_anos, altura_12_anos], positions=[0,0.5], labels=["11 anos", "12 anos"], sym="")
plt.show()
```

*Figura 6* - Gráfico de boxplot para a altura das crianças de 11 e 12 anos com outlier escondido.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/boxplot/90/boxplot-06.png" alt="gráfico tipo boxplot desenhado com matplotlib, com outlier escondido" >
{: .text-center}

<br>

Um outra forma de esconder os outliers é passando `False` para o parâmetro `showfliers` (padrão é `True`):
{: .text-justify}

Por exemplo:

```python
plt.figure(figsize=(8,6))
plt.boxplot([altura_11_anos, altura_12_anos], positions=[0,0.5], labels=["11 anos", "12 anos"], showfliers=False)
plt.show()
```

*Figura 7* - Gráfico de boxplot para a altura das crianças de 11 e 12 anos com outlier removido.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/boxplot/90/boxplot-07.png" alt="gráfico tipo boxplot desenhado com matplotlib, com outlier removido" >
{: .text-center}

<br>

<h2><a style="color:black" id="boxplot-espessura-caixas">Espessura das caixas</a></h2>

Para alterar a espessura dos boxplots, basta passar um número (`float` ou `int`) ou uma sequência (`list`, `tuple`, etc) através do parâmetro `widths` para o `plt.boxplot()`. O valor padrão é o menor valor entre `0.5` e `0.15` vezes a distância entre as posições mais extremas, ou seja, varia com o número de caixas inseridas.
{: .text-justify}

Por exemplo, para caixas com a mesma espessura:

```python
plt.figure(figsize=(8,6))
plt.boxplot([altura_11_anos, altura_12_anos], positions=[0,0.5], labels=["11 anos", "12 anos"], widths=0.4)
plt.show()
```

*Figura 8* - Gráfico de boxplot para a altura das crianças de 11 e 12 anos com espessura das caixas alterada.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/boxplot/90/boxplot-08.png" alt="gráfico tipo boxplot desenhado com matplotlib, com espessura das caixas alterada" >
{: .text-center}

<br>


Para personalizar a espessura de cada caixa, basta passar uma `list`:

```python
plt.figure(figsize=(8,6))
plt.boxplot([altura_11_anos, altura_12_anos], positions=[0,0.5], labels=["11 anos", "12 anos"], widths=[0.4, 0.1])
plt.show()
```

*Figura 9* - Gráfico de boxplot para a altura das crianças de 11 e 12 anos com espessura das caixas personalizada.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/boxplot/90/boxplot-09.png" alt="gráfico tipo boxplot desenhado com matplotlib, com espessura das caixas personalizada" >
{: .text-center}

<br>

Observe que este parâmetro altera ***todos*** os elementos do boxplot *proporcionalmente*.




<br>

<p style="text-align: center">
  <a href="/Curso-matplotlib-89" class="btn btn--success">Anterior</a>
  <a href="/Curso-matplotlib-91" class="btn btn--success">Próximo</a>
</p>
