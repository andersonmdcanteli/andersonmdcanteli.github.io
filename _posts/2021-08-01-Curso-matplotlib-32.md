---
title: "Curso matplotlib - Gráfico com barras de erros (elementos de texto)"
data: 2021-08-01
tags: []
header:
  image: "/images/chess.jpg"
  image_description: "Chess pieces"
excerpt: "matplotlib"
locale: "pt-br"
---

<br>

A adição de elementos de texto segue a mesma lógica que vimos até agora. Por exemplo:

```python
plt.figure(figsize=(8,6))
plt.errorbar(dias, media, yerr=desv_pad, ecolor='red', elinewidth=1, capsize=5, capthick=1,
             color='k', linestyle="none",)
plt.scatter(dias, media, label="Temperatura média")
plt.legend()
plt.xlabel("Dias")
plt.ylabel("Temperatura (°C)")
plt.show()
```

*Figura 1* - Gráfico de erros relacionando a temperatura média na cidade de Birigui-SP em três dias diferentes do ano de 2021.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-erros/32/grafico-erros-01.png" alt="gráfico de dispersão desenhado com o **matplotlib** relacionando o dia e a temperatura média do dia" >
{: .text-center}

<br>



<p style="text-align: center">
  <a href="/Curso-matplotlib-31" class="btn btn--success">Anterior</a>
  <a href="/Curso-matplotlib-33" class="btn btn--success">Próximo</a>
</p>
