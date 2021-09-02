---
title: "Gráfico de pizza (Conjunto de dados)"
data: 2021-08-08
tags: []
header:
  image: "/images/chess.jpg"
  image_description: "Chess pieces"
excerpt: "matplotlib"
locale: "pt-br"
---


<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/generico/homer.gif" alt="gráfico de dispersão desenhado utilizando o **matplotlib**  com a borda externa transparente">
{: .text-center}

<p style="text-align: center;" >Fonte: <a href="https://gifer.com/en/1I5n">gifer.com</a></p>

<br>

<h2><a style="color:black" id="">Conjunto de dados</a></h2>

O conjunto de dados utilizado para exemplificar a criação de gráficos de pizza, é um conjunto fictício do número de vendas de cinco tipos de pizza, em um único dia em uma pizzaria.
{: .text-justify}

```python
sabor = ['calabresa', 'frango com catupiry', 'quatro queijos', 'chocolate', 'vegetariana']
quantidade_vendas = [35, 41, 36, 15, 8]
```

Nesse conjunto de dados, temos a variável `sabor`, que é uma `list` que armazena os sabores das pizzas, e a variável `quantidade_vendas`, que armazena a quantidade de vendas de cada sabor em um dia.
{: .text-justify}

<h2><a style="color:black" id="">Gráfico de pizza</a></h2>

Para desenhar um gráfico de pizza, utilizamos o método `plt.pie()`, que precisa receber apenas um parâmetro com os dados numéricos, que é o parâmetro `x`. Neste caso, basta passar a variável `quantidade_vendas` como parâmetro para o `plt.pie()`:

```python
plt.figure(figsize=(8,8))
plt.pie(quantidade_vendas)
plt.show()
```

*Figura 1* - Gráfico de pizza para a quantidade de vendas de diversos tipos de sabores.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-pizza/69/grafico-pizza-01.png" alt="gráfico de pizza desenhado com matplotlib." >
{: .text-center}

<br>

Você encontra maiores detalhes na [documentação](https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.pie.html).


<p style="text-align: center">
  <a href="/Curso-matplotlib-68" class="btn btn--success">Anterior</a>
  <a href="/Curso-matplotlib-70" class="btn btn--success">Próximo</a>
</p>
