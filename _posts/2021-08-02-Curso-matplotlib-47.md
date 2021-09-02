---
title: "Curso matplotlib - Gráfico de barras verticais (Conjunto de dados)"
data: 2021-08-02
tags: []
header:
  image: "/images/chess.jpg"
  image_description: "Chess pieces"
excerpt: "matplotlib"
locale: "pt-br"
---

<br>

Os dados de exemplo deste módulo, são dados de preço de frutas em um supermercado genérico.
{: .text-justify}

<img style="float: center;" src="https://super.abril.com.br/wp-content/uploads/2019/03/site_feira.png" alt="Gráfico de dispersão" width="600">
{: .text-center}

<p style="text-align: center;" >Fonte: <a href="https://super.abril.com.br/mundo-estranho/por-que-os-dias-da-semana-tem-feira-no-nome/">www.super.abril.com.br</a></p>


```python
frutas = ['Banana Caturra', 'Laranja Pêra', 'Limão Tahiti', 'Maçã Gala', 'Mamão Formosa']
precos = [1.77, 2.49, 2.29, 3.98, 2.98]
```

A `list` `frutas` armazena uma sequência de nomes de frutas, enquanto que a `list` `precos` armazena os respectivos preços das frutas.
{: .text-justify}

<h2><a style="color:black" id="">Desenhando gráfico de barras verticais</a></h2>

Para desenhar um gráfico de barras (verticais) com o **matplotlib**, utiliza-se o elemento `plt.bar()`.
{: .text-justify}

É necessário passar pelo menos dois parâmetros, sendo que o primeiro deve corresponder aos valores de `x`, que pode ser um número (`float` ou `int`) ou uma sequência (`list`, `tuple`, `ndarray`, etc) com vários elementos, que podem ser `float`, `int` ou `str`. O segundo parâmetro é o `height`, que são os valores de `y` e especificam a altura das barras (`float`, `int` ou um tipo de sequência).
{: .text-justify}

Por exemplo:
```python
plt.figure(figsize=(8,6))
plt.bar(frutas, precos)
plt.show()
```

*Figura 1* - Gráfico de barras verticais.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-barras-verticais/47/grafico-barras-verticais-01.png" alt="gráfico de barras verticais desenhado com o matplotlib." >
{: .text-center}

<br>

Você encontra maiores detalhes na [documentação](https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.bar.html).



<br>




<p style="text-align: center">
  <a href="/Curso-matplotlib-46" class="btn btn--success">Anterior</a>
  <a href="/Curso-matplotlib-48" class="btn btn--success">Próximo</a>
</p>
