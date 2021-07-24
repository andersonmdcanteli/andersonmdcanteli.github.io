---
title: "Curso matplotlib - Exportando o gráfico"
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

Para exportar um gráfico desenhado com o **matplotlib** basta utilizar o `plt.savefig()`, que deve ter como argumento o nome do arquivo que será criado, que deve conter a extensão do arquivo desejada. O `plt.savefig()` deve ser adicionado logo acima de `plt.show()`, e após todos os demais elementos terem sido criados. Por exemplo:
{: .text-justify}

```python
plt.figure()
...
plt.savefig()
plt.show()
```

Podemos verificar quais tipos de extensões podem ser utilizadas, utilizando o seguinte comando:
{: .text-justify}

```python
plt.gcf().canvas.get_supported_filetypes()
```

Que irá retornar um `dict` contendo como `key` a extensão e como `value` o nome da respectiva `key`.
{: .text-justify}


<code>{'eps': 'Encapsulated Postscript',</code><br>
<code>'jpg': 'Joint Photographic Experts Group',</code><br>
<code>'jpeg': 'Joint Photographic Experts Group',</code><br>
<code>'pdf': 'Portable Document Format',</code><br>
<code>'pgf': 'PGF code for LaTeX',</code><br>
<code>'png': 'Portable Network Graphics',</code><br>
<code>'ps': 'Postscript',</code><br>
<code>'raw': 'Raw RGBA bitmap',</code><br>
<code>'rgba': 'Raw RGBA bitmap',</code><br>
<code>'svg': 'Scalable Vector Graphics',</code><br>
<code>'svgz': 'Scalable Vector Graphics',</code><br>
<code>'tif': 'Tagged Image File Format',</code><br>
<code>'tiff': 'Tagged Image File Format'}</code><br>


As opções podem variar de acordo com a versão do Python, versão do **matplotlib** e sistema operacional utilizado.
{: .text-justify}


Para criar um arquivo com o nome `"meu-grafico"` e com a extensão `".png"`, basta utilizar o `plt.savefig("meu-grafico.png")`. Por exemplo:
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
plt.savefig("meu-grafico.png")
plt.show()
```

*Figura 1* - Gráfico de dispersão exportando.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/15/meu-grafico.png" alt="gráfico de dispersão desenhado utilizando o **matplotlib**  ">
{: .text-center}

<br>

O arquivo será salvo no diretório onde o notebook esta armazenado. Para saber qual é o diretório em que o notebook está, podemos utilizar a biblioteca `os`, e utilizar o método `os.getcwd()`, que irá retornar o endereço local do arquivo do notebook.
{: .text-justify}

```python
import os
os.getcwd()
```

> 'C:\\Users\\###\\Graficos\\01 - Grafico de dispersao\\aula'


Em geral, arquivos com extensão `'.png'` não são muito adequados para publicações, pois eles não tem muita resolução. Dê preferência para arquivos `'.pdf'`, `'.eps'`, `'.tif'` ou `'.svg'`. Atente as instruções da revista para a extensão recomendada.
{: .text-justify}



<h2><a style="color:black" id="">Número de dpi's</a></h2>

Também podemos especificar a densidade de pixels (*dpi*) do gráfico, o que é feito passando um número (`float` ou `int`) através do parâmetro `dpi` em `plt.savefig()`. A quantidade de *dpis* padrão é de 100 dpis.
{: .text-justify}

Por exemplo, para alterar o número de dpis de 100 (padrão) para 300:

```python
plt.savefig("meu-grafico.png", dpi=300)
```

*Figura 2* - Gráfico de dispersão exportando com 300 dpis.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/15/meu-grafico-02.png" alt="gráfico de dispersão desenhado utilizando o **matplotlib**  ">
{: .text-center}

<br>


Quanto maior o número de dpi's, maior será a qualidade final do gráfico. Contudo, maior será o tamanho do arquivo gerado. O tamanho da Figura 1, desenhada com 100 dpis, é de 29 KB, enquanto que o tamanho da Figura 2, desenhada com 300 dpi's é de 176 KB. Atente para as recomendações da revista quanto ao número de dpi's.
{: .text-justify}



<br>

<p style="text-align: center">
  <a href="/Curso-matplotlib-14" class="btn btn--success">Anterior</a>
  <a href="/Curso-matplotlib-16" class="btn btn--success">Próximo</a>
</p>
