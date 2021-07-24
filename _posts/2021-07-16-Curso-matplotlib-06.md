---
title: "Curso matplotlib - Gráfico de dispersão (Criando o gráfico de dispersão)"
data: 2021-07-16
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


O método utilizado para desenhar um [gráfico de dispersão no matplotlib](https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.scatter.html) é o método `plt.scatter()`, que necessita de pelo menos dois parâmetros:
{: .text-justify}

- `x`: dados que serão utilizados no o eixo *x* (variável *independente*), que devem ser uma sequência (`list`, `tuple`, `ndarray`, etc);
- `y`: dados que serão utilizados no o eixo *y* (variável *dependente*), que devem ser uma sequência (`list`, `tuple`, `ndarray`, etc);

A estrutura mínima para desenhar um gráfico de dispersão é:

```python
plt.scatter(x,y)
plt.show()
```

Onde o `plt.scatter(x,y)` é o responsável por gerar o gráfico, enquanto que o `plt.show()` é o responsável por apresentar o gráfico. Dessa forma, basta atribuir os valores independentes para o `x` e os valores dependentes para o `y`. Então, ao passar rodar a célula com o código:
{: .text-justify}

```python
plt.scatter(x=x, y=y)
plt.show()
```

Obtemos o seguinte output:

*Figura 1* - Gráfico de dispersão simples desenhado com o **matplotlib**.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/06/grafico-dispersao-01.png" alt="gráfico de dispersão desenhado utilizando o **matplotlib** " >
{: .text-center}

Entretanto, o `plt.show()` não é necessário nos ***notebooks***, pois o gráfico sempre será impresso no output da célula. Então, se rodar apenas o código abaixo, o gráfico será impresso como na **Figura 2**.
{: .text-justify}

```python
plt.scatter(x=x, y=y)
```

*Figura 2* - Gráfico de dispersão simples desenhado com o **matplotlib**.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/06/grafico-dispersao-02.png" alt="gráfico de dispersão desenhado utilizando o **matplotlib** " >
{: .text-center}

Contudo, também será impresso no output a *representação do objeto* do gráfico criado (`<matplotlib.collections.PathCollection at 0x21f46f9d908>`), o que em muitas vezes não é interessante. Além disso, em diversas outras [IDE's (Ambiente Integral de Desenvolvimento)](https://en.wikipedia.org/wiki/Integrated_development_environment), como o [PyCharm](https://www.jetbrains.com/pycharm/) ou o [Atom](https://atom.io/), o gráfico não será apresentado. Por estes motivos, é recomendado sempre utilizar o `plt.show()`.
 {: .text-justify}

De qualquer forma, podemos editar este gráfico para que ele fique mais elegante e apresentável. Uma das principais edições que podemos fazer é alterar o tamanho do gráfico.
{: .text-justify}


<br>

<p style="text-align: center">
  <a href="/Curso-matplotlib-05" class="btn btn--success">Anterior</a>
  <a href="/Curso-matplotlib-07" class="btn btn--success">Próximo</a>
</p>
