---
title: "Curso matplotlib - Várias séries (edição)"
data: 2021-07-19
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

Agora vamos utilizar os métodos de edição vistos para deixar o gráfico de forma apresentável.
{: .text-justify}

Em geral, gráficos **coloridos** são bons para *apresentações*, mas não para *artigos* (a inclusão de figuras coloridas geralmente esta atrelado ao pagamento de uma taxa elevada). Para alterar a cor dos marcadores para preta, fazemos como visto anteriormente:
{: .text-justify}

```python
plt.figure(figsize=(8,6))
plt.scatter(x[0], y[0], label=raca_cachorro[0], c='k')
plt.scatter(x[1], y[1], label=raca_cachorro[1], c='k')
plt.scatter(x[2], y[2], label=raca_cachorro[2], c='k')
plt.scatter(x[3], y[3], label=raca_cachorro[3], c='k')
plt.scatter(x[4], y[4], label=raca_cachorro[4], c='k')
plt.scatter(x[5], y[5], label=raca_cachorro[5], c='k')
plt.scatter(x[6], y[6], label=raca_cachorro[6], c='k')
plt.scatter(x[7], y[7], label=raca_cachorro[7], c='k')
plt.scatter(x[8], y[8], label=raca_cachorro[8], c='k')
plt.scatter(x[9], y[9], label=raca_cachorro[9], c='k')
plt.scatter(x[10], y[10], label=raca_cachorro[10], c='k')
plt.legend()
plt.show()
```


*Figura 1* - Gráfico de dispersão com os marcadores na cor preta.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/14/grafico-dispersao-series-edicao-01.png" alt="gráfico de dispersão desenhado utilizando o **matplotlib** com marcadores na cor preta" >
{: .text-center}

<br>


Entretanto, forma não é possível diferenciar as raças! Uma forma de diferenciar as diferentes séries é utilizar diferentes marcadores para cada série
{: .text-justify}


```python
plt.figure(figsize=(8,6))
plt.scatter(x[0], y[0], label=raca_cachorro[0], c='k', marker='o')
plt.scatter(x[1], y[1], label=raca_cachorro[1], c='k', marker='s')
plt.scatter(x[2], y[2], label=raca_cachorro[2], c='k', marker='p')
plt.scatter(x[3], y[3], label=raca_cachorro[3], c='k', marker='*')
plt.scatter(x[4], y[4], label=raca_cachorro[4], c='k', marker='v')
plt.scatter(x[5], y[5], label=raca_cachorro[5], c='k', marker='^')
plt.scatter(x[6], y[6], label=raca_cachorro[6], c='k', marker='<')
plt.scatter(x[7], y[7], label=raca_cachorro[7], c='k', marker='>')
plt.scatter(x[8], y[8], label=raca_cachorro[8], c='k', marker='x')
plt.scatter(x[9], y[9], label=raca_cachorro[9], c='k', marker='D')
plt.scatter(x[10], y[10], label=raca_cachorro[10], c='k', marker='H')
plt.legend()
plt.show()
```

*Figura 2* - Gráfico de dispersão com diversos marcadores na cor preta.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/14/grafico-dispersao-series-edicao-02.png" alt="gráfico de dispersão desenhado utilizando o **matplotlib** com diversos marcadores na cor preta" >
{: .text-center}

<br>


Contudo os marcadores ficaram pequenos. Como a mudança de tamanho é apenas para fins estéticos, é mais indicado que todos os marcadores tenham o mesmo tamanho. Então, vou criar uma variável chamada `marker_size` que vai receber o valor do tamanho dos marcadores, e vou passar esta variável para o parâmetro `s` em todos os elementos de dispersão.
{: .text-justify}

```python
marker_size = 80
```

Dessa forma, todas as séries terão marcador do mesmo tamanho, e caso deseje alterar o tamanho, não é necessário ficar alterando em todos os locais, bastando alterar o valor de `marker_size`.
{: .text-justify}

```python
plt.figure(figsize=(8,6))
plt.scatter(x[0], y[0], label=raca_cachorro[0], c='k', marker='o', s = marker_size)
plt.scatter(x[1], y[1], label=raca_cachorro[1], c='k', marker='s', s = marker_size)
plt.scatter(x[2], y[2], label=raca_cachorro[2], c='k', marker='p', s = marker_size)
plt.scatter(x[3], y[3], label=raca_cachorro[3], c='k', marker='*', s = marker_size)
plt.scatter(x[4], y[4], label=raca_cachorro[4], c='k', marker='v', s = marker_size)
plt.scatter(x[5], y[5], label=raca_cachorro[5], c='k', marker='^', s = marker_size)
plt.scatter(x[6], y[6], label=raca_cachorro[6], c='k', marker='<', s = marker_size)
plt.scatter(x[7], y[7], label=raca_cachorro[7], c='k', marker='>', s = marker_size)
plt.scatter(x[8], y[8], label=raca_cachorro[8], c='k', marker='x', s = marker_size)
plt.scatter(x[9], y[9], label=raca_cachorro[9], c='k', marker='D', s = marker_size)
plt.scatter(x[10], y[10], label=raca_cachorro[10], c='k', marker='H', s = marker_size)
plt.legend()
plt.show()
```


*Figura 3* - Gráfico de dispersão com diversos marcadores na cor preta.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/14/grafico-dispersao-series-edicao-04.png" alt="gráfico de dispersão desenhado utilizando o **matplotlib** com diversos marcadores na cor preta" >
{: .text-center}

<br>


Em diversos casos o uso de marcadores fechados não é uma boa ideia. Dados experimentais geralmente são apresentados abertos. Para deixar os marcadores abertos, basta trocar o parâmetro `c = 'k'` pelos parâmetros `edgecolor = 'k'` e `facecolor = 'none'`:
{: .text-justify}


```python
plt.figure(figsize=(8,6))
plt.scatter(x[0], y[0], label=raca_cachorro[0], edgecolor='k', facecolor='none', marker='o', s = marker_size)
plt.scatter(x[1], y[1], label=raca_cachorro[1], edgecolor='k', facecolor='none', marker='s', s = marker_size)
plt.scatter(x[2], y[2], label=raca_cachorro[2], edgecolor='k', facecolor='none', marker='p', s = marker_size)
plt.scatter(x[3], y[3], label=raca_cachorro[3], edgecolor='k', facecolor='none', marker='*', s = marker_size)
plt.scatter(x[4], y[4], label=raca_cachorro[4], edgecolor='k', facecolor='none', marker='v', s = marker_size)
plt.scatter(x[5], y[5], label=raca_cachorro[5], edgecolor='k', facecolor='none', marker='^', s = marker_size)
plt.scatter(x[6], y[6], label=raca_cachorro[6], edgecolor='k', facecolor='none', marker='<', s = marker_size)
plt.scatter(x[7], y[7], label=raca_cachorro[7], edgecolor='k', facecolor='none', marker='>', s = marker_size)
plt.scatter(x[8], y[8], label=raca_cachorro[8], edgecolor='k', facecolor='none', marker='x', s = marker_size)
plt.scatter(x[9], y[9], label=raca_cachorro[9], edgecolor='k', facecolor='none', marker='D', s = marker_size)
plt.scatter(x[10], y[10], label=raca_cachorro[10], edgecolor='k', facecolor='none', marker='H', s = marker_size)
plt.legend()
plt.show()
```

*Figura 4* - Gráfico de dispersão com diversos marcadores abertos.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/14/grafico-dispersao-series-edicao-03.png" alt="gráfico de dispersão desenhado utilizando o **matplotlib** com diversos marcadores abertos" >
{: .text-center}

<br>


Contudo, observe que o marcador da raça 'German Shepherd Dog' acabou desaparecendo, o que aconteceu pois o marcador utilizado é um `x`, e este marcador não tem `edgecolor`. Para resolver isto, basta passar a cor preta para o parâmetro `facecolor` ao invés de `"none"`:
{: .text-justify}

*Figura 5* - Gráfico de dispersão com diversos marcadores abertos.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/14/grafico-dispersao-series-edicao-05.png" alt="gráfico de dispersão desenhado utilizando o **matplotlib** com diversos marcadores abertos" >
{: .text-center}

<br>

Mas é essencial adicionar os elementos textuais no gráfico:

```python
plt.figure(figsize=(8,6))
plt.scatter(x[0], y[0], label=raca_cachorro[0], edgecolor='k', facecolor='none', marker='o', s = marker_size)
plt.scatter(x[1], y[1], label=raca_cachorro[1], edgecolor='k', facecolor='none', marker='s', s = marker_size)
plt.scatter(x[2], y[2], label=raca_cachorro[2], edgecolor='k', facecolor='none', marker='p', s = marker_size)
plt.scatter(x[3], y[3], label=raca_cachorro[3], edgecolor='k', facecolor='none', marker='*', s = marker_size)
plt.scatter(x[4], y[4], label=raca_cachorro[4], edgecolor='k', facecolor='none', marker='v', s = marker_size)
plt.scatter(x[5], y[5], label=raca_cachorro[5], edgecolor='k', facecolor='none', marker='^', s = marker_size)
plt.scatter(x[6], y[6], label=raca_cachorro[6], edgecolor='k', facecolor='none', marker='<', s = marker_size)
plt.scatter(x[7], y[7], label=raca_cachorro[7], edgecolor='k', facecolor='none', marker='>', s = marker_size)
plt.scatter(x[8], y[8], label=raca_cachorro[8], edgecolor='k', facecolor='k', marker='x', s = marker_size)
plt.scatter(x[9], y[9], label=raca_cachorro[9], edgecolor='k', facecolor='none', marker='D', s = marker_size)
plt.scatter(x[10], y[10], label=raca_cachorro[10], edgecolor='k', facecolor='none', marker='H', s = marker_size)
plt.legend()
plt.xlabel("Peso (kg)", labelpad=15)
plt.ylabel("Altura (cm)", labelpad=15)
plt.title("Relação entre peso e altura de diversas raças de cachorros", pad=15)
plt.show()
```

*Figura 6* - Gráfico de dispersão com diversos marcadores abertos e elementos textuais.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/14/grafico-dispersao-series-edicao-06.png" alt="gráfico de dispersão desenhado utilizando o **matplotlib** com diversos marcadores abertos e elementos textuais" >
{: .text-center}

<br>


 E por fim, vou alterar o tamanho das fontes para `14` e também a família das fontes para `'Arial'`, utilizando o `mpl.rc()`.

```python
mpl.rc('font', family = 'Arial', size = 14)
```

Entretanto, o tamanho da fonte na legenda acaba ficando maior do que o esperado, então vou reduzir o seu apenas o tamanho utilizando o parâmetro `fontsize` em  `plt.legend()`.
{: .text-justify}


```python
plt.figure(figsize=(8,6))
plt.scatter(x[0], y[0], label=raca_cachorro[0], edgecolor='k', facecolor='none', marker='o', s = marker_size)
plt.scatter(x[1], y[1], label=raca_cachorro[1], edgecolor='k', facecolor='none', marker='s', s = marker_size)
plt.scatter(x[2], y[2], label=raca_cachorro[2], edgecolor='k', facecolor='none', marker='p', s = marker_size)
plt.scatter(x[3], y[3], label=raca_cachorro[3], edgecolor='k', facecolor='none', marker='*', s = marker_size)
plt.scatter(x[4], y[4], label=raca_cachorro[4], edgecolor='k', facecolor='none', marker='v', s = marker_size)
plt.scatter(x[5], y[5], label=raca_cachorro[5], edgecolor='k', facecolor='none', marker='^', s = marker_size)
plt.scatter(x[6], y[6], label=raca_cachorro[6], edgecolor='k', facecolor='none', marker='<', s = marker_size)
plt.scatter(x[7], y[7], label=raca_cachorro[7], edgecolor='k', facecolor='none', marker='>', s = marker_size)
plt.scatter(x[8], y[8], label=raca_cachorro[8], edgecolor='k', facecolor='k', marker='x', s = marker_size)
plt.scatter(x[9], y[9], label=raca_cachorro[9], edgecolor='k', facecolor='none', marker='D', s = marker_size)
plt.scatter(x[10], y[10], label=raca_cachorro[10], edgecolor='k', facecolor='none', marker='H', s = marker_size)
plt.legend(fontsize=12)
plt.xlabel("Peso (kg)", labelpad=15)
plt.ylabel("Altura (cm)", labelpad=15)
plt.title("Relação entre peso e altura de diversas raças de cachorros", pad=15)
plt.show()
```

*Figura 7* - Gráfico de dispersão com diversos marcadores abertos e elementos textuais.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/14/grafico-dispersao-series-edicao-07.png" alt="gráfico de dispersão desenhado utilizando o **matplotlib** com diversos marcadores abertos e elementos textuais" >
{: .text-center}

<br>


E pronto, temos um gráfico de dispersão corretamente editado, e pronto para ser exportado.


<h1><a style="color:black" id="">Desafio 2</a></h1>

Obtenha o gráfico acima (Figura 7) com todas as edições aplicadas, mas utilizando um loop `for`.

O notebook base pode ser acessado [neste link](https://github.com/andersonmdcanteli/matplotlib-course/blob/main/curso/grafico-dispersao/desafio-2/Desafio-2.ipynb).

O notebook com a resolução pode ser acessado [neste outro link](https://github.com/andersonmdcanteli/matplotlib-course/blob/main/curso/grafico-dispersao/desafio-2/Desafio-2-final.ipynb). O vídeo com a resolução pode ser visto [clicando neste link](https://youtu.be/MImLX6iN5uA).


<br>

<p style="text-align: center">
  <a href="/Curso-matplotlib-13" class="btn btn--success">Anterior</a>
  <a href="/Curso-matplotlib-15" class="btn btn--success">Próximo</a>
</p>
