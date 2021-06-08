---
title: "Dashboard de Normalidade"
data: 2021-06-07
tags: []
header:
  image: "/images/chess.jpg"
  image_description: "Chess pieces"
excerpt: "Normalidade"
locale: "pt-br"
---

Olá 😀!

Este artigo tem como objetivo descrever os métodos utilizados para desenvolver o ***Dashboard*** de avaliação da Normalidade de um conjunto de dados. Saber se um conjunto de dados segue, pelo menos aproximadamente, a distribuição Normal, impacta no tipo de estatísticas que podem ser aplicadas no conjunto de dados.
{: .text-justify}

<h2>Índice</h2>
- <a href="#introducao">Introdução;</a>

- <a href="#bibliotecas">Bibliotecas;</a>

- <a href="#conjunto-dados">Conjunto de dados base;</a>

- <a href="#grafico-dispersao">Gráfico de dispersão;</a>

- <a href="#tabela-estatisticas">Tabela de estatísticas básicas;</a>

- <a href="#histograma">Histograma;</a>

- <a href="#qq-plot">QQ-plot;</a>

- <a href="#tabela-normalidade">Tabela de Normalidade;</a>

  + <a href="#tabela-shapiro">Teste de Shapiro-Wilk;</a>

  + <a href="#tabela-kolmogorov-smirnov">Teste de Kolmogorov-Sminorv;</a>

  + <a href="#anderson-darling">Teste de Anderson-Darling;</a>

- <a href="#conclusao">Conclusão;</a>

O Dashboard finalizado tem esta aparência (estático):

*Figura 1* - Dashboard finalizado.
{: .text-center}

<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/dashboard-normalidade/print-dashboard.png" alt="captura de tela do Dashboard finalizado, contendo todos os gráficos e tabelas gerados." >
{: .text-center}

<h2><a style="color:black" id="introducao">Introdução</a></h2>

Este Dashbard foi desenvolvido para ser utilizado no <a href="https://colab.research.google.com/notebooks/intro.ipynb">google.colab</a>. Esta plataforma é um ambiente de Jupyter Notebooks gratuito que roda na nuvem e armazena seus notebooks no Google Drive. Dessa forma, é necessário ter uma conta no Google para poder utilizar este Dashboard.
{: .text-justify}

Para rodar o Dashboard, basta clicar <a href="https://colab.research.google.com/drive/19fduz4LufNndnYzKuHLIpZYP9pSlK4xY?usp=sharing">neste link</a> e seguir o passo a passo descrito.
{: .text-justify}

A partir da entrada de um conjunto de dados, é gerado **tabelas e gráficos interativos**, que *facilitam* a interpretação dos resultados. São gerados:
{: .text-justify}

- Gráfico de dispersão interativo;

- Tabela com as principais métricas de avaliação de uma amostra (média, mediana, desvio padrão, etc);

- Histograma de probabilidade interativo com a distribuição paramétrica (Normal) e distribuição não paramétrica;

- QQ-plot interativo;

- Tabela com os testes de Normalidade de Shapiro-Wilk, Anderson-Darling e Kolmogorov-Smirnov;

<!-- bibliotecas utilizadas -->
<h2><a style="color:black" id="bibliotecas">Bibliotecas utilizadas</a></h2>

Para rodar este Dashboard foram utilizadas as seguintes bibliotecas:
{: .text-justify}

 ✔ Pandas (para gerenciar os dados);

 ✔ NumPy (cálculos);

 ✔ SciPy (análise estatística);

 ✔ Plotly (para gerar gráficos interativos);

 ✔ Dash (para gerar Dashboards interativos);

 ✔ Dash Bootstrap Components (para utilizar BOOTSTRAP);

De qualquer forma, o script desenvolvido irá automaticamente baixar e instalar todas as bibliotecas necessárias, e você não precisa se preocupar com esta etapa.
{: .text-justify}

<!-- Conjunto de dados -->
<h2><a style="color:black" id="conjunto-dados">Conjunto de dados base</a></h2>

O conjunto de dados base (ou padrão) foi obtido no <a href="http://www.portalaction.com.br/inferencia/61-tecnica-grafica#Exemplo6.1.1">Portal Action</a>, onde podem ser facilmente validados quanto a todas as informações geradas nesse Dashboard.
{: .text-justify}

<!-- Grafico dispersao -->
<h2><a style="color:black" id="grafico-dispersao">Gráfico de dispersão</a></h2>

Para desenhar o gráfico de dispersão foi utilizado o ```plotly.express.scatter()```, com os valores fornecidos pelo usuário no *eixo y* e com a respectiva ordem numérica dos dados no *eixo x* (o primeiro elemento está na posição 0). Caso o usuário passe a unidade dos dados, ela será adiciona junto ao nome dos dados no título do *eixo y*.
{: .text-justify}

<!-- Tabela estatística -->
<h2><a style="color:black" id="tabela-estatisticas">Tabela de estatísticas básicas</a></h2>

Ao lado do gráfico de dispersão, uma tabela será desenhada contendo as principais métricas de avaliação de um conjunto de dados. São elas:

- Média: utilizando o método ```np.mean()```;

\\(\bar{x} = \frac{\sum_{i=1}^n x_{i} }{n}\\) &emsp; &emsp; &emsp; (1)
{: .text-center}

onde \\(x_{i}\\) é o valor de cada medida independente que foi obtida e (\\(n\\)) é o número total de observações.
{: .text-justify}

- Mediana: utilizando o método ```np.median()```

- Desvio padrão: utilizando o método ```np.std(ddof=1)```. O desvio padrão é calculado admitindo **dados amostrais**;

\\(s = \sqrt{\frac{\sum_{i=1}^n(x_{i}-\bar{x})^2 }{n-1} }\\) &emsp; &emsp; &emsp; (2)
{: .text-center}

- Variância: utilizando o método ```np.var(ddof=1)```. A variância é calculada admitindo **dados amostrais**;

\\(s^{2} = \frac{\sum_{i=1}^n(x_{i}-\bar{x})^2 }{n-1}\\) &emsp; &emsp; &emsp; (3)
{: .text-center}

- Coeficiente de variação: calculado utilizando a seguinte equação:

\\(CV(\%) = \frac{100\times s}{\bar{x}} \\) &emsp; &emsp; &emsp; (4)
{: .text-center}

- Contagem: número total de amostras presentes no conjunto de dados (número experimental);


O número de casas decimais apresentado depende no número de casas decimais do conjunto de dados original.

<!-- Histrograma -->
<h2><a style="color:black" id="histograma">Histograma</a></h2>
O histograma dos dados é desenhado utilizando o ```plotly.express.histogram()```, utilizando o número de colunas igual a 10 e com o parâmetro ```histnorm='probability density'```, o que gera o gráfico de densidade de probabilidade.
{: .text-justify}

Neste gráfico é adicionado os valores esperados para a distribuição Normal, que são obtidos utilizando ```stats.norm.pdf()``` com a média e o desvio padrão do conjunto de dados. A distribuição Normal esperada é plotada adicionando um traço de ```plotly.graph_objs.Scatter()``` na figura do histograma.
{: .text-justify}

Também é adicionado densidade não paramétrica para o conjunto de dados, sendo estimada utilizando o método ```stats.gaussian_kde()```. A densidade não paramétrica é adicionada através de um traço de ```plotly.graph_objs.Scatter()``` na figura do histograma.
{: .text-justify}

<!-- qq-plot -->
<h2><a style="color:black" id="qq-plot">QQ-plot</a></h2>
Os valores teóricos do qq-plot são calculados utilizando o método ```stats.probplot(dist="norm")```, sendo plotados no *eixo y*. No *eixo x*, são plotados os *valores originais ordenados de forma crescente*. O gráfico é desenhado utilizando o ```plotly.express.scatter()```.
{: .text-justify}

Para auxiliar na interpretação dos resultados, uma linha de regressão é adicionada no gráfico. A regressão linear é feita utilizando o ```scipy.stats.linregress()```. A linha obtida é adicionada no gráfico como um traço utilizando o ```plotly.graph_objs.Scatter()```.
{: .text-justify}

Também é adicionado o valor do coeficiente de Pearson no canto inferior direito do QQ-plot, através de uma anotação.
{: .text-justify}

<!-- normalidade -->
<h2><a style="color:black" id="tabela-normalidade">Tabela de Normalidade</a></h2>

Ao final do Dashboard é apresentada uma tabela com o resultado dos testes de Shapiro-Wilk, Anderson-Darling e Kolmogorov-Smirnov, com uma conclusão clara do resultado dos testes. Todos os testes são concluídos utilizando 5% de significância. Para selecionar várias células ao mesmo tempo, clique em cima de uma célula e selecione as linhas/colunas utilizando o teclado (Shift + setas). Após seleção, copie e cole utilizando Ctrl+C e Ctrl+V, respectivamente.
{: .text-justify}


<h3><a style="color:black" id="tabela-shapiro">Teste de Shapiro-Wilk</a></h3>
- Teste de Shapiro-Wilk:
Este teste é aplicado utilizando o ```scipy.stats.shapiro()```, retornando a estatística do teste, o valor tabelado, o p-valor e a conclusão baseada no valor de p. Mais detalhes sobre o teste de Shapiro-Wilk <a href="https://andersonmdcanteli.github.io/Shapiro-Wilk/">neste texto</a> ou <a href="https://www.youtube.com/watch?v=c8534_OfQPQ">neste vídeo</a>.
{: .text-justify}

<h3><a style="color:black" id="tabela-kolmogorov-smirnov">Teste de Kolmogorov-Sminorv</a></h3>
- Teste de Kolmogorov-Smirnov:
Este teste é aplicado utilizando o ```scipy.stats.kstest(cdf='norm')```, retornando a estatística do teste, o valor tabelado, o p-valor e a conclusão baseada no valor de p. Mais detalhes sobre o teste de Kolmogorov-Smirnov <a href="https://youtu.be/-rUm7Lx5VbE">neste vídeo</a>.
{: .text-justify}

<h3><a style="color:black" id="anderson-darling">Teste de Anderson-Darling</a></h3>
- Teste de Anderson-Darling:
Este teste é aplicado utilizando o ```scipy.stats.anderson('norm')```, retornando a estatística do teste, o valor tabelado, e a conclusão baseada no valor na comparação entre a estatística e o valor tabelado. Mais detalhes sobre o teste de Anderson-Darling <a href="https://youtu.be/S-xiUzOYKl0">aqui</a>.
{: .text-justify}

<h2><a style="color:black" id="conclusao">Conclusão</a></h2>

Verificar se um conjunto de dados segue a distribuição Normal nunca foi tão simples. Basta apenas entrar com os seus dados, e pronto. Várias formas de avaliar são apresentadas de forma simples e clara. Dashboards assim são muito promissores.

Dashboards interativos são uma ferramenta muito interessante para a visualização de dados, e ajuda muito na intepretação de resultados. Desenvolve-los não é tão difícil quanto parece quanto utilizamos o Plotlt e Dash. Entretanto, entregar eles para os usuários não é tão simples, pois requer um servidor on-line que requer investimento financeiro.

Contudo, utilizando o Google Colab esta barreira reduz, facilitando a entrega. Mas não se contrapartidas. Na fora utilizada aqui, o usuário ainda precisa ter contato com programação. Pouca coisa, mas precisa, o que é uma barreira. O ideal seria colocar o Dashboard on-line, mas falta investimento financeiro.
