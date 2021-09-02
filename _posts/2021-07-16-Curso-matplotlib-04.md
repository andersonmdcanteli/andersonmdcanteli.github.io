---
title: "Curso matplotlib - Gráfico de dispersão (Introdução)"
data: 2021-07-16
tags: []
header:
  image: "/images/chess.jpg"
  image_description: "Chess pieces"
excerpt: "matplotlib"
locale: "pt-br"
---

<br>

<img src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/anatomias/anatomia-scatter-plot.png" alt="anatomia do gráfico de dispersão " width=500>
{: .text-center}

<br>

Os gráficos de dispersão são uma forma de representar graficamente a associação entre pares de dados (`x` e `y`). O pareamento de `x` e `y` esta relacionado a diferentes características de um objeto.
{: .text-justify}

Para desenha-lo, utilizamos dados vinculados a uma observação. Por exemplo, a hora do dia e a temperatura registrada em uma hora específica. Um outro exemplo seria a relação entre o número de rotações de um ventilador dependendo da velocidade setada.
{: .text-justify}

Genericamente, temos uma variável `X` e uma variável `Y`, que tem o mesmo tamanho. Os dados de `X` geralmente estão relacionados a uma medida independente, enquanto que os dados de `Y` estão relacionados a uma medida dependente (de `X`).
{: .text-justify}

Por exemplo, o número de rotações do ventilador é dependente (variável `Y`) da velocidade escolhida (variável `X`).  A temperatura ambiente (variável `Y`) é dependente da hora (variável `X`) em que a medida foi feita.
{: .text-justify}

Mas também podemos relacionar variáveis que não apresentam essa relação direta. Por exemplo, a umidade relativa do ar e a temperatura ambiente. Embora relacionadas, não é possível ajustar uma para medir a outra.
{: .text-justify}

<br>

<h2><a style="color:black" id="">Índice</a></h2>

+ <a href="/Curso-matplotlib-05">Conjunto de dados</a>

+ <a href="/Curso-matplotlib-06">Criando gráfico de dispersão</a>

+ <a href="/Curso-matplotlib-07">Tamanho do gráfico</a>

+ <a href="/Curso-matplotlib-08">Edição dos marcadores</a>

  * <a href="/Curso-matplotlib-08#cor-marcadores">Cor dos marcadores</a>

  * <a href="/Curso-matplotlib-09">Tamanho dos marcadores</a>

  * <a href="/Curso-matplotlib-10">Editando dos marcadores</a>

    - <a href="/Curso-matplotlib-10#alterando-marcador">Formato do marcador</a>

    - <a href="/Curso-matplotlib-10#bordas-marcador">Bordas dos marcadores</a>

      + <a href="/Curso-matplotlib-10#espessura-linha">Espessura da bordas</a>

    - <a href="/Curso-matplotlib-10#cor-preenchimento">Cor do preenchimento</a>

+ <a href="/Curso-matplotlib-11">Elementos de texto</a>

  * <a href="/Curso-matplotlib-11#legendas">Legendas</a>

    - <a href="/Curso-matplotlib-11#posicao-legendas">Posição das legendas no gráfico</a>

    - <a href="/Curso-matplotlib-11#tamanho-legenda">Tamanho das legendas</a>

  * <a href="/Curso-matplotlib-11#titulo-eixo-x">Título do eixo x</a>

  * <a href="/Curso-matplotlib-11#titulo-eixo-y">Título do eixo y</a>

  * <a href="/Curso-matplotlib-11#titulo-grafico">Título do gráfico</a>

  * <a href="/Curso-matplotlib-12">Tipos de fontes</a>

    - <a href="/Curso-matplotlib-12#tamanho-fonte">Tamanho das fontes</a>

+ <a href="/Curso-matplotlib-13">Várias séries de dados</a>

  * <a href="/Curso-matplotlib-14">Edição</a>

+ <a href="/Curso-matplotlib-15">Exportando o gráfico</a>

  * <a href="/Curso-matplotlib-15#numero-dpis">Número de dpi's</a>

+ <a href="/Curso-matplotlib-16">Plano de fundo</a>

    * <a href="/Curso-matplotlib-16#preenchimento-bordas-externas">Preenchimento bordas externas</a>

    * <a href="/Curso-matplotlib-16#cor-background">Cor do background dos eixos (Axes)</a>

    * <a href="/Curso-matplotlib-16#transparencia">Adicionando transparência</a>


+ <a href="/Curso-matplotlib-17">Exercícios resolvidos</a>



<br>

<p style="text-align: center">
  <a href="/matplotlib-course" class="btn btn--info">Início</a>
  <a href="/Curso-matplotlib-05" class="btn btn--success">Próximo</a>
</p>
