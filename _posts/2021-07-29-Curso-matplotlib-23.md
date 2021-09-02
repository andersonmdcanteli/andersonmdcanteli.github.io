---
title: "Curso matplotlib - Combinando gráfico de dispersão com gráfico de linhas (Elementos de texto)"
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

Adicionar os elementos de texto (títulos, legendas, etc) segue a mesma lógica utilizada anteriormente.

**Exemplo:**

```python
plt.figure(figsize=(12,6))
plt.plot(horario, temperatura, c='red', linewidth=3.5, zorder=1, alpha=0.5, label='linha de conecção')
plt.scatter(horario, temperatura, marker='s', edgecolors='k', facecolors='g', s=250,
          linewidths=3.5, zorder=2,label='dados reais')
plt.legend(bbox_to_anchor=(1.22,1))
plt.xlabel("Horário", labelpad=15)
plt.ylabel("Temperatura (°C)", labelpad=15)
plt.title("Monitoramento da temperatura na cidade de Birigui-SP no dia 13/04/2021", pad=15)
plt.show()
```

*Figura 1* - Gráfico de dispersão com gráfico de linhas - elementos textuais.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-linhas/23/grafico-dispersao-linhas-01.png" alt="gráfico de linhas desenhado com o **matplotlib** relacionando o horário e a temperatura ambiente" >
{: .text-center}

<br>


<p style="text-align: center">
  <a href="/Curso-matplotlib-22" class="btn btn--success">Anterior</a>
  <a href="/Curso-matplotlib-24" class="btn btn--success">Próximo</a>
</p>
