---
title: "Curso matplotlib - Elementos auxiliares (conjunto de dados)"
data: 2021-08-01
tags: []
header:
  image: "/images/chess.jpg"
  image_description: "Chess pieces"
excerpt: "matplotlib"
locale: "pt-br"
---

<br>

Nesta aula é utilizado um conjunto de dados genérico apenas para ter dados plotados no gráfico e assim, temos uma referência visual para os elementos que serão adicionados.
{: .text-justify}

```python
x = [1,2,3,4]
y = [1,2,3,4]
```

Para a referência visual, vamos desenhar um gráfico de dispersão com os dados de `x` e `y`.

```python
plt.figure(figsize=(8,6))
plt.scatter(x,y)
plt.show()
```


*Figura 1* - Gráfico de dispersão com dados genéricos.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-elementos-auxiliares/36/grafico-elementos-auxiliares-01.png" alt="gráfico de dispersão genérico desenhado com o **matplotlib** " >
{: .text-center}

<br>






<p style="text-align: center">
  <a href="/Curso-matplotlib-35" class="btn btn--success">Anterior</a>
  <a href="/Curso-matplotlib-37" class="btn btn--success">Próximo</a>
</p>
