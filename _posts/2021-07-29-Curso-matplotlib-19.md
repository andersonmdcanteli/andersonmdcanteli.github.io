---
title: "Curso matplotlib - Gráfico de linhas (conjunto de dados)"
data: 2021-07-29
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

*Figura 1* - Conjunto de dados.
{: .text-center}
<img style="border: solid 1px black" src="/images/curso-matplotlib/generico/tempo.png" alt="imagem contendo os símbolos do tempo, sol nuvem, chuva, tempestade" width=600>
{: .text-center}
*Fonte* - [pinterest.com](https://br.pinterest.com/pin/329325791503174880/).
{: .text-center}


O conjunto de dados utilizado para demonstrar como desenhar gráficos de linhas foi obtido em *13/04/2021* em [climatempo.com.br/birigui](https://www.climatempo.com.br/previsao-do-tempo/15-dias/cidade/408/birigui-sp), e são os dados reais de temperatura (°C) ao longo do dia (horas) da cidade de Birigui-SP.
{: .text-justify}

```python
horario = ['00:00', '02:00', '04:00', '06:00', '08:00', '10:00', '12:00', '14:00', '16:00', '18:00', '20:00', '22:00']
temperatura = [21, 19, 19, 18, 23, 27, 31, 33, 34, 28, 23, 26]
```

<br>

* A variável `horario` armazena os horários no qual a medida foi realizada, onde cada horário esta armazenado como um `str`.
{: .text-justify}

* Já a variável `temperatura` armazena as respectivas temperaturas medidas, onde cada temperatura esta amarzenada como um número `int`.
{: .text-justify}


<br>

<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/generico/banner.png" alt="banner provisório " >
{: .text-center}

Desenhar um gráfico de linhas utilizando o **matplotlib** é muito semelhante ao gráfico de dispersão, bastando utilizar o `plt.plot()` ao invés de `plt.scatter()`:
{: .text-justify}

```python
plt.figure(figsize=(12,6))
plt.plot(horario,temperatura)
plt.show()
```

Observe que a variável `horario` foi alocada como valores do eixo `x`, enquanto que a variável `temperatura` foi alocada como valores do eixo `y`. O gráfico deve ser desenhado desta forma, pois a temperatura depende (variável dependente) do horário de medição (variável independente).
{: .text-justify}

Além disso, os dados ocorrem em uma sequência lógica. A primeira medida foi feita as `00:00` horas, a segunda medida foi feita as `02:00` horas, a terceira medida foi feita as `04:00` horas, e assim por diante. Dessa forma, os dados **são sequenciais**, e, por isto, a ligação entre os pontos com uma reta é adequada.
{: .text-justify}

*Figura 2* - Gráfico de linhas relacionando horário e temperatura ambiente na cidade de Birigui-SP em 13/04/2021.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-linhas/19/grafico-linhas-01.png" alt="gráfico de linhas desenhado com o **matplotlib** relacionando o horário e a temperatura ambiente" >
{: .text-center}

<br>



Você encontra a documentação completa para o `plt.plot()` [clicando aqui](https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.plot.html)
{: .text-justify}

<br>

<p style="text-align: center">
  <a href="/Curso-matplotlib-18" class="btn btn--success">Anterior</a>
  <a href="/Curso-matplotlib-20" class="btn btn--success">Próximo</a>
</p>
