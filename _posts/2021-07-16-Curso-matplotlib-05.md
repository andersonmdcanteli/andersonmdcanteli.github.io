---
title: "Curso matplotlib - Gráfico de dispersão (Conjunto de dados)"
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


<img style="float: center;" src="https://hypescience.com/wp-content/uploads/2010/07/cachorros.jpg" alt="Gráfico de dispersão" width="200">
{: .text-center}

<p style="text-align: center;" >Fonte: <a href="https://hypescience.com/como-criar-um-cachorro-grande-em-um-pequeno-apartamento/">www.hypescience.com</a></p>

<br>

Para exemplificação de como gerar gráficos de dispersão, será utilizado um conjunto de dados que relaciona a **altura** (em cm) com o **peso** (em kg) de diversas ***raças de cachorros***. Os valores utilizados são os *valores médios* dentro de cada raça.
{: .text-justify}

Os dados de **peso** foram atribuidos à variavel `x` utilizando uma `list`, e os dados da **altura** foram atribuidos à variável `y`, também utilizando uma `list`. As respectivas raças de cachorro foram amarzenadas na lista `raca_cachorro`.
{: .text-justify}

Os dados estão ***ordenados*** da raça mais leve para a mais pesada.

```python
x = [1.59, 4.53, 8.16, 10.2, 10.88, 22.68, 22.68, 30.62, 37.42, 45.36, 68.04] # peso em kilos

y = [19.05, 25.4, 26.67, 29.21, 36.83, 52.07, 54.61, 57.15, 60.96, 62.23, 67.31] # altura em em centímetros

raca_cachorro = ['Chihuahua', 'Poodle Toy', 'Pug', 'French Bulldog', 'Beagle', 'Chow Chow', 'Siberian Husky',
                 'Labrador Retriever', 'German Shepherd Dog', 'Rottweiler', 'Saint Bernard'] # nome da respectiva raça
```                 

Você encontra os dados originais [nesta página](https://www.dimensions.com/collection/dogs-dog-breeds).

<br>

<p style="text-align: center">
  <a href="/Curso-matplotlib-04" class="btn btn--success">Anterior</a>
  <a href="/Curso-matplotlib-06" class="btn btn--success">Próximo</a>
</p>
