---
title: "Curso matplotlib - Elementos gráficos"
data: 2021-07-14
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


Toda figura criada com o **matplotlib** terá uma série de elementos, que estão destacados na figura abaixo.

*Figura 1* - Elementos gráficos de uma figura do **matplotlib**.
{: .text-center}
<img style="border: solid 1px black" src="https://matplotlib.org/stable/_images/anatomy.png" alt="Gráfico desenhado utilizando o matplotlib que apresenta todos os elementos que uma figura do **matplotlib** contém" >
{: .text-center}

<p style="text-align: center;">Fonte: <a href="https://matplotlib.org/stable/tutorials/introductory/usage.html#sphx-glr-tutorials-introductory-usage-py">matplotlib.org</a></p>


<h2><a style="color:black" id="">Figure</a></h2>

O elemento `Figure` corresponde a figura como um todo. Ela controla todos os demais elementos, como os *Axes*, *Axis* e *Artists*. Entenda este elemento como sendo a tela (em branco) de uma pintura .
{: .text-justify}

<h2><a style="color:black" id="">Axes</a></h2>

O `Axes` corresponde a região da imagem com os dados preenchidos (a pintura). Cada figura pode conter diversos `Axes`. Cada `Axes` pode conter dois `Axis` (ou 3, no caso de um gráfico em 3 dimensões), que é o elemento que determina os limites dos dados do gráfico. O `Axes` é a entrada primária para utilizar a orientação a objetos, e por isso vamos utiliza-la pouco.
{: .text-justify}

<h2><a style="color:black" id="">Axis</a></h2>

Os ```Axis``` determinam os limites dos gráficos, os ticks e os tickslabels dos eixos.
{: .text-justify}


<h2><a style="color:black" id="">Artist</a></h2>

Um `Artist` é basicamente tudo que você vê em um gráfico (inclusive os `Axis`, `Axes` e `Figure`). Então os objetos de texto, linhas, coleções, etc, são todos da classe `Artist`, e quando a figura é renderizada, todos os artistas são desenhados no canvas.
{: .text-justify}


Como um exemplo genérico, observe a figura abaixo:

*Figura 2* - Exemplo genérico para os elementos de um figura.
{: .text-center}
<img style="border: solid 1px black" src="https://www.umsabadoqualquer.com/wp-content/uploads/2016/12/129.png" alt="A imagem mostra uma tirinha de carton da série cães e gatos do site umsabadoqualquer" >
{: .text-center}

<p style="text-align: center;">Fonte: <a href="https://www.umsabadoqualquer.com/caes-e-gatos-e-assim-que-eles-descobrem/">umsabadoqualquer.com</a></p>

No exemplo acima, temos os elementos do gráfico como o cão, o gato, textos, o bacon, etc (`Artist`), temos cada quadrinho (`Axes`), delimitados pelas linhas pretas (`Axis`) e o quadrinho completo (`Figure`).


<h2><a style="color:black" id="">Key-points</a></h2>

- `Figure` é a imagem final que contem 1 ou mais `Axes`;

- `Axes` representam um plot individual;

- Não confunda `Axes` com `Axis` (axis se refere aos eixos *x* e *y* (e *z*, se for um gráfico em 3D) do plot).


<h2><a style="color:black" id="">Referências</a></h2>

- [matplotlib](https://matplotlib.org/stable/index.html);


<h3><a style="color:black" id="">Links interessantes</a></h3>

- [Ciclo de vida de um plot](https://matplotlib.org/stable/tutorials/introductory/lifecycle.html#sphx-glr-tutorials-introductory-lifecycle-py)

- [matplotlib Usage Guide](https://matplotlib.org/stable/tutorials/introductory/usage.html#sphx-glr-tutorials-introductory-usage-py)

- [Pyplot tutorial](https://matplotlib.org/stable/tutorials/introductory/pyplot.html#sphx-glr-tutorials-introductory-pyplot-py)


<p style="text-align: center">
  <a href="/Curso-matplotlib-02" class="btn btn--success">Anterior</a>
  <a href="/Curso-matplotlib-04" class="btn btn--success">Próximo</a>
</p>
