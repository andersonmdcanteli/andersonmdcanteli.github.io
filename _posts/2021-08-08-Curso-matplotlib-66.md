---
title: "Legendas (Espaçamentos)"
data: 2021-08-08
tags: []
header:
  image: "/images/chess.jpg"
  image_description: "Chess pieces"
excerpt: "matplotlib"
locale: "pt-br"
---

<br>

<h2><a style="color:black" id="espacamento-label-borda">Espaçamento dos labels em relação as borda</a></h2>

Para alterar o espaço entre a legenda e a sua borda, basta alterar o valor do parâmetro `borderpad`, passando um número (`float` ou `int`), sendo que o valor padrão é `0.4`.
{: .text-justify}

```python
plt.figure(figsize=(8,6))
plt.scatter(cachorro_peso, cachorro_altura, label="Cachorros")
plt.scatter(gatos_peso, gatos_altura, label="Gatos")
plt.plot(pinguins_peso, pinguins_altura, marker="o", c="g", label="Pinguins")
plt.xlabel("Peso (kg)")
plt.ylabel("Altura (cm)")
plt.title("Relação entre peso e altura de diferentes animais")
plt.ylim([0,125])
leg = plt.legend(ncol=2, title="Animais", title_fontsize='xx-large', borderpad=2)
leg._legend_box.align = "left"
plt.show()
```

*Figura 1* - Caixa da legenda com espaçamento dos labels em relação as bordas.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/legendas/66/legendas-01.png" alt="gráfico de dispersão combinado com gráfico de linhas desenhado com matplotlib, caixa da legenda com espaçamento em relação as bordas" >
{: .text-center}

<br>

<h2><a style="color:black" id="espacamento-marcador-label">Espaçamento entre o marcador e o label da legenda</a></h2>

Para alterar o espaço entre o marcador e o label da sua respectiva legenda, basta alterar o valor do parâmetro `handletextpad`, passando um número (`float` ou `int`), onde o padrão é `0.8`.
{: .text-justify}

```python
plt.figure(figsize=(8,6))
plt.scatter(cachorro_peso, cachorro_altura, label="Cachorros")
plt.scatter(gatos_peso, gatos_altura, label="Gatos")
plt.plot(pinguins_peso, pinguins_altura, marker="o", c="g", label="Pinguins")
plt.xlabel("Peso (kg)")
plt.ylabel("Altura (cm)")
plt.title("Relação entre peso e altura de diferentes animais")
plt.ylim([0,125])
leg = plt.legend(ncol=2, title="Animais", title_fontsize='xx-large', borderpad=2, labelspacing=2, handletextpad=5)
leg._legend_box.align = "left"
plt.show()
```

*Figura 2* - Caixa da legenda com espaçamento dos labels em relação aos marcadores.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/legendas/66/legendas-02.png" alt="gráfico de dispersão combinado com gráfico de linhas desenhado com matplotlib, caixa da legenda com espaçamento em relação aos marcadores" >
{: .text-center}

<br>

<h2><a style="color:black" id="espamento-entre-colunas">Espaço entre as colunas da legenda</a></h2>

Para alterar o espaço entre duas colunas na legenda, basta alterar o valor do parâmetro `columnspacing`, passando um número (`float` ou `int`), onde o padrão é `2.0`.
{: .text-justify}

```python
plt.figure(figsize=(8,6))
plt.scatter(cachorro_peso, cachorro_altura, label="Cachorros")
plt.scatter(gatos_peso, gatos_altura, label="Gatos")
plt.plot(pinguins_peso, pinguins_altura, marker="o", c="g", label="Pinguins")
plt.xlabel("Peso (kg)")
plt.ylabel("Altura (cm)")
plt.title("Relação entre peso e altura de diferentes animais")
plt.ylim([0,125])
leg = plt.legend(ncol=2, title="Animais", title_fontsize='xx-large', columnspacing=5)
leg._legend_box.align = "left"
plt.show()
```

*Figura 3* - Caixa da legenda com espaçamento entre as colunas da legenda.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/legendas/66/legendas-03.png" alt="gráfico de dispersão combinado com gráfico de linhas desenhado com matplotlib, caixa da legenda com espaçamento entre as colunas da legenda" >
{: .text-center}

<br>


<h2><a style="color:black" id="espacamento-legenda-eixo">Espaçamento entre a legenda e o eixo do gráfico</a></h2>

Para alterar o espaço entre a legenda e o eixo do gráfico, basta alterar o valor do parâmetro `borderaxespad`, passando um número (`float` ou `int`), onde o valor padrão é `0.5`.
{: .text-justify}

```python
plt.figure(figsize=(8,6))
plt.scatter(cachorro_peso, cachorro_altura, label="Cachorros")
plt.scatter(gatos_peso, gatos_altura, label="Gatos")
plt.plot(pinguins_peso, pinguins_altura, marker="o", c="g", label="Pinguins")
plt.xlabel("Peso (kg)")
plt.ylabel("Altura (cm)")
plt.title("Relação entre peso e altura de diferentes animais")
plt.ylim([0,125])
leg = plt.legend(ncol=2, title="Animais", title_fontsize='xx-large', borderaxespad=2)
leg._legend_box.align = "left"
plt.show()
```


*Figura 4* - Caixa da legenda com espaçamento entre a legenda e o eixo do gráfico.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/legendas/66/legendas-04.png" alt="gráfico de dispersão combinado com gráfico de linhas desenhado com matplotlib, caixa da legenda com espaçamento entre a legenda e o eixo do gráfico" >
{: .text-center}

<br>



<p style="text-align: center">
  <a href="/Curso-matplotlib-65" class="btn btn--success">Anterior</a>
  <a href="/Curso-matplotlib-67" class="btn btn--success">Próximo</a>
</p>
