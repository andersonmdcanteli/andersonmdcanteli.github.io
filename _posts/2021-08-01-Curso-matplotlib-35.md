---
title: "Curso matplotlib - Elementos auxiliares (Introdução)"
data: 2021-08-01
tags: []
header:
  image: "/images/chess.jpg"
  image_description: "Chess pieces"
excerpt: "matplotlib"
locale: "pt-br"
---

<br>

<img src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/anatomias/.png" alt="anatomia dos elementos auxiliares " width=500>
{: .text-center}

<br>

<br>

Até o momento, estudamos como desenhar os gráficos em si. Entretanto, em muitos casos apenas os pontos experimentais não são suficientes para compor o gráfico como um todo. Elementos de texto em alguns pontos específicos, setas, e retas são muito úteis em alguns casos. Vamos estudar alguns deles!
{: .text-justify}




<br>

<h2><a style="color:black" id="">Índice</a></h2>

+ <a href="/Curso-matplotlib-36">Conjunto de dados</a>

+ <a href="/Curso-matplotlib-37">Retas</a>

  * <a href="/Curso-matplotlib-37#reta-generica">Reta genérica</a>

  * <a href="/Curso-matplotlib-38">Reta vertical</a>

    - <a href="/Curso-matplotlib-38#plt-axvline">plt.axvline()</a>

    - <a href="/Curso-matplotlib-38#plt-vlines">plt.vlines()</a>

  * <a href="/Curso-matplotlib-39">Reta horizontal</a>

    - <a href="/Curso-matplotlib-39#plt-axhline">plt.axhline()</a>

    - <a href="/Curso-matplotlib-39#plt-hlines">plt.hlines()</a>

+ <a href="/Curso-matplotlib-40">Elemento de passo</a>

+ <a href="/Curso-matplotlib-41">Exercícios resolvidos</a>

+ <a href="/Curso-matplotlib-42">Flechas</a>

  - <a href="/Curso-matplotlib-42#largura-corpo-flecha">Largura do corpo da flecha</a>

  - <a href="/Curso-matplotlib-42#largura-ponto-flecha">Largura da ponta da flecha</a>

  - <a href="/Curso-matplotlib-42#comprimento-ponta-flecha">Comprimento da ponta da flecha</a>

  - <a href="/Curso-matplotlib-42#forma-cabeça-flecha">Forma da cabeça da flecha</a>

+ <a href="/Curso-matplotlib-43">Texto</a>

  - <a href="/Curso-matplotlib-43#formatacao">Formatação</a>

  - <a href="/Curso-matplotlib-43#negrito">Negrito</a>

  - <a href="/Curso-matplotlib-43#tamanho-fonte">Tamanho da fonte</a>

  - <a href="/Curso-matplotlib-43#familia-fonte">Família da fonte</a>

  - <a href="/Curso-matplotlib-43#rotacao">Rotação do texto</a>

  - <a href="/Curso-matplotlib-43#cor-texto">Cor do texto</a>

  - <a href="/Curso-matplotlib-43#cor-fundo">Cor de fundo</a>

  - <a href="/Curso-matplotlib-43#bordas">Bordas</a>

+ <a href="/Curso-matplotlib-44">Anotações</a>

  - <a href="/Curso-matplotlib-44#anotacoes-setas">Anotações com setas</a>

    * <a href="/Curso-matplotlib-44#espessura-ponta-seta">Espessura da ponta da seta</a>

    * <a href="/Curso-matplotlib-44#comprimento-ponta-seta">Comprimento da ponta da seta</a>

    * <a href="/Curso-matplotlib-44#espacamento-seta">Espaçamento entre o início e o fim da seta</a>

    * <a href="/Curso-matplotlib-44#outras-edicoes">Outras edições</a>

  - <a href="/Curso-matplotlib-44#estilos-pre-definidos">Estilos pré-definidos</a>

+ <a href="/Curso-matplotlib-45">Exercícios resolvidos</a>






<p style="text-align: center">
  <a href="/matplotlib-course" class="btn btn--info">Início</a>
  <a href="/Curso-matplotlib-36" class="btn btn--success">Próximo</a>
</p>
