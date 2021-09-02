---
title: "Curso matplotlib - Gráfico de barras horizontais (Conjunto de dados)"
data: 2021-08-02
tags: []
header:
  image: "/images/chess.jpg"
  image_description: "Chess pieces"
excerpt: "matplotlib"
locale: "pt-br"
---

<img style="float: center;" src="https://super.abril.com.br/wp-content/uploads/2019/03/site_feira.png" alt="Gráfico de dispersão" width="600">
{: .text-center}

<p style="text-align: center;" >Fonte: <a href="https://super.abril.com.br/mundo-estranho/por-que-os-dias-da-semana-tem-feira-no-nome/">www.super.abril.com.br</a></p>

<br>

Desenhar gráficos de barras horizontais utilizando o **matplotlib** é muito semelhante ao gráfico de barras verticais. Por este motivo, vamos seguir utilizando o conjunto de dados do preço de frutas utilizados anteriormente.
{: .text-justify}

```python
frutas = ['Banana Caturra', 'Laranja Pêra', 'Limão Tahiti', 'Maçã Gala', 'Mamão Formosa']
precos = [1.77, 2.49, 2.29, 3.98, 2.98]
```

Neste caso, utilizamos o `plt.barh()`, passando pelo menos dois parâmetros. O primeiro parâmetro deve receber os valores do eixo `y` (através do parâmetro `y`), e o segundo parâmetro deve receber os valores de `x` (através do parâmetro `width`).
{: .text-justify}

**Exemplo:**

```python
plt.figure(figsize=(8,6))
plt.barh(frutas, precos)
plt.show()
```

*Figura 1* - Gráfico de barras horizontais.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-barras-horizontais/56/grafico-barras-horizontais-01.png" alt="gráfico de barras horizontais desenhado com o matplotlib." >
{: .text-center}

<br>

Você encontra maiores detalhes na [documentação](https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.barh.html#matplotlib.pyplot.barh).
{: .text-justify}



<p style="text-align: center">
  <a href="/Curso-matplotlib-55" class="btn btn--success">Anterior</a>
  <a href="/Curso-matplotlib-57" class="btn btn--success">Próximo</a>
</p>
