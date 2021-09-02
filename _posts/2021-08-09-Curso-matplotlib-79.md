---
title: "Elementos auxiliares (Formas geométricas)"
data: 2021-08-09
tags: []
header:
  image: "/images/chess.jpg"
  image_description: "Chess pieces"
excerpt: "matplotlib"
locale: "pt-br"
---


<br>

Além das setas, elementos de texto e retas, também é possível inserir formas geométricas em um gráfico desenhado com o **matplotlib**, como retângulos, círculos, triângulos, etc. Estes elementos podem ser muito úteis para indicar uma região específica do gráfico, de forma a dar um maior destaque a uma região do gráfico.
{: .text-justify}

<h2><a style="color:black" id="forma-geometrica-conjunto-dados">Conjunto de dados</a></h2>

Para exemplificar como inserir formas geométricas, seguimos utilizando um conjunto de dados genérico, apenas para existir referência visual. Esta referência visual é novamente feita criando um gráfico de dispersão.
{: .text-justify}

```python
import matplotlib.pyplot as plt

x = [1,2,3,4]
y = [1,2,3,4]

plt.figure(figsize=(8,6))
plt.scatter(x, y)
plt.show()
```

*Figura 1* - Gráfico de dispersão.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-elementos-auxiliares-2/78/elementos-auxiliares-01.png" alt="gráfico de dispersão desenhado com matplotlib" >
{: .text-center}

<br>

Para inserir as figuras geométricas, é necessário utilizar a `class` `patches` do **matplotlib**. Para poder utilizar esta `class`, é necessário importa-la antes, o que geralmente é feito da seguinte forma:
{: .text-justify}

```python
import matplotlib.patches as patches
```

É através de `patches` que vamos inserir as formas geométricas, como o `Rectangle`, o `Circle`, a `Elipse` e o `Polygon`. Entretanto, é necessário *adicionar* a forma no gráfico, o que é feito de forma um pouco diferente do que vimos até agora.
{: .text-justify}

A inserção é feita através do `plt.gca().add_patch()`, onde passamos como parâmetro a forma desejada dentro de `.add_patch()`. Veremos detalhes para cada forma geométrica a seguir.
{: .text-justify}

<br>


<p style="text-align: center">
  <a href="/Curso-matplotlib-78" class="btn btn--success">Anterior</a>
  <a href="/Curso-matplotlib-80" class="btn btn--success">Próximo</a>
</p>
