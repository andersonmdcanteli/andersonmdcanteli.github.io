---
title: "Dashboards com Plotly Express - Parte 1"
data: 2021-02-12
tags: [dashboard, python, plotly, dash, amazônia, plotly express, pantanal, queimadas, bioma, INPE]
header:
  image: "/images/chess.jpg"
  image_description: "Chess pieces"
excerpt: "Comparando todos os estados do Brasil"
locale: "pt-br"
---

Olá 😀!

Nesse artigo/tutorial vou seguir com a criação de dashboards (utilizando plotly express e Dash), mas ao invés de utilizar o <code>go.Scatter()</code> <a href="/Dashboards-Parte-1" target="_blank">como fiz anteriormente</a>, eu vou utilizar o <code>plotly.express()</code>, que é uma forma mais simples de trabalhar com o Plotly (como o Seaborn é para o matplotlib). Ao invés de utilizar os <a href="/Dashboards-Parte-1" target="_blank">dados das queimadas nos Biomas</a>, eu vou utilizar dados por estado apenas por questão de trabalhar com dados diferentes e aprender com eles (dados diferentes, novas perspectivas, novos problemas para serem resolvidos 🙃).
{: .text-justify}

Este novo dashboard vai ter gráficos de dispersão, gráficos de barra, mapas e tabelas, não nesta ordem. A versão final ficou como na figura abaixo:
{: .text-justify}

*Figura 1* - Dashboard finalizado.
{: .text-center}

<img src="{{ site.url }}{{ site.baseurl }}/images/dashboards-plotly-express/parte-1/dashboard-finalizado.png" alt="captura de tela do dashboard finalizado para os dados de queimadas nos estados brasileiros." >
{: .text-center}

Este artigo foi separado em algumas partes para facilitar a organização das ideias. Os principais tópicos abordados são:
{: .text-justify}

* <a>Parte 1;</a>
  + <a href="#introducao">Introdução;</a>
  + <a href="#versao-python">Ambiente de trabalho;</a>
  + <a href="#coletando-dados">Aquisição de dados;</a>
  + <a href="#dados-estado">Visualização dos dados divididos por estado para todo o Brasil;</a>
    - <a href="#graficos-mapas">Mapas com os dados de queimadas por ano;</a>
    - <a href="#tabela-mapas">Tabela com os dados ordenados;</a>
  + <a href="#adicionando-elementos">Adicionando os elementos ao Dashboard;</a>
    - <a href="#elemento-titulo-geral">Título geral;</a>
    - <a href="#elemento-titulo-mapa-brasil">Primeiro sub título;</a>
    - <a href="#elemento-dropdown">Dropdown;</a>
    - <a href="#elemento-texto-popover">Texto fixo e Popover;</a>
    - <a href="#elemento-mapa">Mapa e tabela;</a>
    - <a href="#elemento-modal">Modal;</a>
  + <a href="#script-finalizado">Script finalizado;</a>




* <a href="/Dashboards-com-Plotly-Express-Parte-2">Parte 2;</a>
  + <a href="/Dashboards-com-Plotly-Express-Parte-2#introducao">Introdução;</a>
  + <a href="/Dashboards-com-Plotly-Express-Parte-2#grafico-plotly">Gráficos e tabelas com plotly express;</a>
    - <a href="/Dashboards-com-Plotly-Express-Parte-2#grafico-barras-regioes-estado">Gráfico de barras para comparar os estados dentro da sua região;<a>
    - <a href="/Dashboards-com-Plotly-Express-Parte-2#grafico-barras-regioes">Gráfico de barras para cada região;</a>
    - <a href="/Dashboards-com-Plotly-Express-Parte-2#tabela-barras-regioes">Tabela para comparar os dados médios da Região;</a>

  + <a href="/Dashboards-com-Plotly-Express-Parte-2#layout">Layout;</a>
    - <a href="/Dashboards-com-Plotly-Express-Parte-2#elemento-titulo">Título;</a>
    - <a href="/Dashboards-com-Plotly-Express-Parte-2#elemento-texto-popover">Texto simples e Popover;</a>
    - <a href="/Dashboards-com-Plotly-Express-Parte-2#elemento-dropdown">Dropdown;</a>
    - <a href="/Dashboards-com-Plotly-Express-Parte-2#elemento-grafico-agrupado">Gráfico de barras agrupado;</a>
    - <a href="/Dashboards-com-Plotly-Express-Parte-2#elemento-grafico-tabela">Gráfico de barras e tabela;</a>
  + <a href="/Dashboards-com-Plotly-Express-Parte-2#script-finalizado">Script finalizado;</a>

* <a href="/Dashboards-com-Plotly-Express-Parte-3">Parte 3;</a>
  + <a href="/Dashboards-com-Plotly-Express-Parte-3#introducao">Introdução;</a>
    - <a href="/Dashboards-com-Plotly-Express-Parte-3#grafico-dispersao">Gráfico de dispersão com linhas para comparar os meses;</a>
    - <a href="/Dashboards-com-Plotly-Express-Parte-3#grafico-barras-estados">Gráfico de barras para comparar os anos;</a>

  + <a href="/Dashboards-com-Plotly-Express-Parte-3#layout">Layout;</a>
    - <a href="/Dashboards-com-Plotly-Express-Parte-3#elemento-titulo">Título;</a>
    - <a href="/Dashboards-com-Plotly-Express-Parte-3#elemento-texto-popover">Texto simples e Popover;</a>
    - <a href="/Dashboards-com-Plotly-Express-Parte-3#elemento-dropdown">Dropdown;</a>
    - <a href="/Dashboards-com-Plotly-Express-Parte-3#elemento-grafico-dispersao-linhas">Gráfico de dispersão com linhas;</a>
    - <a href="/Dashboards-com-Plotly-Express-Parte-3#elemento-grafico-barras">Gráfico de barras;</a>
  + <a href="/Dashboards-com-Plotly-Express-Parte-3#script-finalizado">Script finalizado;</a>

* <a href="/Dashboards-com-Plotly-Express-Parte-4">Parte 4;</a>

<h2><a style="color:black" id="introducao">Introdução</a></h2>

Especificamente neste post, eu irei desenvolver um mapa do Brasil com dados de queimadas divididos por estados e uma tabela com os valores ordenados do total de queimadas por estado.
{: .text-justify}

No Dashboard será incluído estes dois elementos, além de título dinâmico, Dropdown, texto estático, modal e Popover. A versão final ficou assim:
{: .text-justify}

*Figura 2* - Estado final do Dashboard desenvolvido neste post.
{: .text-center}

<img src="{{ site.url }}{{ site.baseurl }}/images/dashboards-plotly-express/parte-1/print-17.png" alt="Captura de tela do dashboard com o mapa e a tabela para o ano de 2016.">
{: .text-center}

<!-- Versão do Python -->
<h2><a style="color:black" id="versao-python">Versão do Python e bibliotecas</a></h2>

Para desenvolver este artigo eu utilizei a distribuição Anaconda do Python (3.7.3). Também utilizei a IDE Jupyter notebook (para desenvolver os códigos) e o Atom (para fazer o deploy ao final do desenvolvimento). As principais bibliotecas utilizadas foram:
{: .text-justify}

 ✔ Pandas, versão = 0.24.2 (para gerenciar os dados) -> pip install pandas==0.24.2;

 ✔ NumPy, versão = 1.16.4 (vai que precisa) -> pip install numpy==1.16.4;

 ✔ json, versão = 2.0.9 (para carregar dados de geo localização) -> instala junto com o Python;

 ✔ Plotly, versão = 4.14.3 (para gerar gráficos interativos) -> pip install plotly==4.14.3;

 ✔ Dash, versão = 1.19.0 (para gerar Dashboards interativos) -> pip install dash==1.19.0;

 ✔ Dash Bootstrap Components, versão = 0.11.3 (para utilizar BOOTSTRAP) -> pip install dash-bootstrap-components==0.11.3.    




 <!-- Coletando dados -->
 <h2><a style="color:black" id="coletando-dados">Aquisição de dados</a></h2>

Os dados foram coletados no site do <a href="http://queimadas.dgi.inpe.br/queimadas/portal-static/estatisticas_estados/" target="_blank">INPE</a>, tendo sido obtido os dados de focos de queimadas separados por <em>estados</em> brasileiros, no dia 30/01/2021.
{: .text-justify}

É importante fazer algumas alterações nos dados (praticamente as mesmas que foram feitas para o <a href="/Dashboards-Parte-1#coletando-dados">conjunto de dados dos biomas</a>):
* Adicionar nome para a primeira coluna;
* Adicionar uma nova coluna para o nome do Estado e da Região;
* Remover as linhas com valores máximos, mínimos e médios;
* Substituir o "-" por um "0";
* Transformar os valores do data frame de <code>string</code> para <code>int</code>;
* Salvar os dados em um novo arquivo (<a href = "/assets/files/dashboards/historico_estados_queimadas.csv" download="historico_bioma_completo.csv">baixe ele aqui</a>).

Após ter feito todas estas alterações no arquivo de dados, podemos efetivamente começar. E começamos pelo começo, importando as bibliotecas necessárias:
{: .text-justify}

```python
import dash
import dash_core_components as dcc
import dash_html_components as html
from dash.dependencies import Input, Output, State
import dash_bootstrap_components as dbc
import pandas as pd
import numpy as np
import plotly.offline as pyo
import plotly.express as px
import json
import dash_table
from dash_table.Format import Format, Group, Scheme, Symbol
```

Então importamos os dados e visualizamos as primeiras linhas para poder entender como os dados estão dispostos:
{: .text-justify}

```python
df = pd.read_csv('historico_estados_queimadas.csv', encoding='latin-1')
df.head()
```

*Figura 3* - Estrutura dos dados dispostos no DataFrame de queimadas por estado.
{: .text-center}

<img src="{{ site.url }}{{ site.baseurl }}/images/dashboards-plotly-express/parte-1/print-01.PNG" alt="captura de tela do DataFrame com os dados de queimadas por estado." >
{: .text-center}

Temos diversas colunas para os dados, que estão divididos em dados de queimadas por mês (colunas 'Janeiro', 'Fevereiro', ..., 'Dezembro'), e também temos uma coluna com o total no ano (coluna 'Total'). Ainda temos colunas com o nome do estado (coluna 'UF') e uma coluna para o nome de cada região ('Regiao'). Cada linha representa um ano da série de dados.
{: .text-justify}

Com este conjunto de dados temos diversas possibilidades para análise gráfica. Podemos visualizar o Brasil como um todo, por estado ou por região. E ainda podemos separar por Ano ou por mês. Vou fazer todas estas variações. Para organizar melhor, eu vou começar com formas de comparação macro (todos os estados, parte 1), depois visualizar dados entre as regiões (todos os estados de cada região, parte 2), e por fim por uma visualização por estado (micro, parte 3).
{: .text-justify}


<!-- Visualização dos dos dados por estado -->
<h2><a style="color:black" id="dados-estado">Visualização dos dados divididos por estado para todo o Brasil.</a></h2>

Uma das melhores formas de apresentar dados que são separados por *divisas* são os *mapas*. Mapas apresentam uma grande facilidade na interpretação, pois podem ser pintados com cores que representem alguma informação importe que se deseja apresentar. Entretanto, valores numéricos também são importantes pois trazem a informação precisa, e não apenas visual. Por isso, vou combinar a apresentação dos dados do Brasil como um todo com uma mapa e com uma tabela.
{: .text-justify}

<h3><a style="color:black" id="graficos-mapas">Mapas para o número de focos de queimadas por estado no Brasil</a></h3>

A ideia aqui é gerar uma mapa onde a área de cada estado é preenchida com uma cor de acordo com o total de focos de queimadas identificados por ano, e que uma animação seja gerada com o mapa, passando os dados através dos anos.
{: .text-justify}


Para gerar mapas com o plotly podemos utilizar o ploty express (<code>px.choropleth_mapbox()</code>), mas é necessário passar o parâmetro <code>geojson</code>, que, dentre os parâmetros desse elemento, é o menos usual aqui. Este parâmetro deve receber um arquivo ".geojson" que é um tipo de arquivo designado para representar componentes geográficos (os limites geográficos dos mapas). Para o <code>px.choropleth_mapbox()</code> é necessário que o arquivo ".geojson" seja uma coleção de recursos de polígono, com IDs, que são referências dos locais. Isso pode soar complicado, mas não é tanto assim.
{: .text-justify}

Então vamos começar pelo mais dificil, que é a obtenção dos limites dos estados brasileiros em um arquivo ".geojson". Podemos obter este
<a href="https://raw.githubusercontent.com/codeforamerica/click_that_hood/master/public/data/brazil-states.geojson" target="_blank">arquivo aqui</a> (muito obrigado pela informação <a href="https://medium.com/python-in-plain-english/how-to-create-a-interative-map-using-plotly-express-geojson-to-brazil-in-python-fb5527ae38fc" target="_blank">Nayane Maia</a>) para delimitar os estados. Você pode fazer o
<a href="/assets/files/dashboards/estados_brasil.geojson" download="estados_brasil.geojson">download dele clicando aqui</a>.
{: .text-justify}

Para carregar o arquivo utilizamos a sintaxe normal, mas utilizamos a biblioteca json para importar o arquivo.
{: .text-justify}

```python
with open('estados_brasil.geojson') as data: # carregando o arquivo ".geojson"
    limites_brasil = json.load(data)
```

Para utilizar este arquivo no plotly express, é necessário que o arquivo ".geojson" tenha IDs para cada localidade (estado), e este arquivo não contém os IDs. Mas para adiciona-los, é bem simples: basta criar uma nova chave para o dicionário chamada 'id' (o arquivo ".geojson" tem formato de dicionário), e alocar o ID nessa chave. Mas é necessário que esse ID esteja dentro do dicionário 'features' que está dentro do dicionário ".geojson". O ID tem que corresponder a uma identificação do DataFrame que contém os dados, e o mais fácil é correlacionar com o nome do estado (coluna 'UF'). Como este arquivo ".geojson" tem o nome de cada estado no dicionário 'properties' (que está dentro de 'features'), podemos fazer da seguinte forma:
{: .text-justify}

```python
for feature in limites_brasil ['features']: # adicionado o ID aos dados
    feature['id'] = feature['properties']['name']
```

Agora basta desenhar o gráfico. Inicialmente, criamos uma figura do tipo <code>px.choropleth_mapbox()</code> e passamos alguns parâmetros para esta figura. O primeiro parâmetro é o DataFrame que contém os dados, que neste caso é o DataFrame completo (<code>df</code>).
{: .text-justify}

```python
# criando o mapa
fig = px.choropleth_mapbox(
                            df, # primeiro parâmetro é o dataframe com os dados
)
```

Depois passamos o <code>locations</code> que deve receber a coluna do DataFrame que contém os IDs; neste caso a coluna "UF".
{: .text-justify}

```python
fig = px.choropleth_mapbox(
                            ...
                            locations = 'UF', # coluna do DF que referencia as IDs do mapa
)
```

Em seguida passamos o arquivo ".geojson" (limites_brasil) através do parâmetro <code>geojson</code>.
{: .text-justify}

```python
fig = px.choropleth_mapbox(
                            ...
                            geojson = limites_brasil, # arquivo com os limites dos estados
)
```

Depois precisamos setar a coluna que contém os valores que serão utilizados para gerar a palheta de cor, que neste caso é a coluna "Total", e que deve ser passado através do parâmetro <code>color</code>.
{: .text-justify}

```python
fig = px.choropleth_mapbox(
                            ...
                            color = 'Total', # indicando qual coluna será utilizada para pintar os estados
)
```

Depois podemos alterar o estilo do mapa através do parâmetro <code>mapbox_style</code>. O Plotly tem alguns estilos bastante interesantes, mas o que eu mais gostei para este mapa foi o "carto-positron".
{: .text-justify}

```python
fig = px.choropleth_mapbox(
                            ...
                            mapbox_style = "carto-positron", # estilo do mapa
)
```
Depois podemos setar a posição central onde o mapa será apresentado através do parâmetro <code>center</code>. Esse parâmetro recebe um dicionário com duas chaves, uma para a longitude ("lon") e outro para a latitude ("lat"). O centro do Brasil é próximo a lat: -14 e lon: -55.
{: .text-justify}

```python
fig = px.choropleth_mapbox(
                            ...
                            center = {'lon':-55, 'lat':-14}, # definindo a posição inicial do mapa
)
```

Podemos ainda definir o zoom inicial do mapa, através do parâmetro <code>zoom</code>. O zoom deve ser um número inteiro entre 0 e 20 (8 é o padrão). Eu achei um zoom igual a 3 agradável.
{: .text-justify}

```python
fig = px.choropleth_mapbox(
                            ...
                            zoom = 3, # definindo o zoom do mapa (número inteiro entre 0 e 20)
)
```

Podemos setar uma opacidade para o gráfico, de forma que background apareça. Entretanto, este é um parâmetro que deve ser utilizado com *cautela* quando a **cor tem significado**. Por enquanto vou utilizar <code>opacity=0.5</code>, mas provavelmente vou remover futuramente.
{: .text-justify}

```python
fig = px.choropleth_mapbox(
                            ...
                            opacity = 0.5, # definindo uma opacidade para a cor do mapa
)
```

E com estes parâmetros setados já podemos gerar o mapa:
```python
pyo.offline.plot(fig, filename = "mapa-01.html") # criando o arquivo html
```

*Figura 4* - Mapa de focos de queimadas por ano nos diferentes estados brasileiros.
{: .text-center}

<img src="{{ site.url }}{{ site.baseurl }}/images/dashboards-plotly-express/parte-1/print-02.PNG" alt="print do mapa gerado para o total de focos de queimadas no Brasil." >
{: .text-center}

Você pode ver o <a href="/images/dashboards-plotly-express/parte-1/mapa-01.html" target="_blank">mapa interativo
clicando aqui</a>.
{: .text-justify}

O código está assim:
```python
fig = px.choropleth_mapbox(
    df, # data frame com os dados
    locations = "UF", # coluna com o ID, neste caso, o
    geojson = limites_brasil, # arquivo com os limites do mapa
    color = "Total", # coluna do data frame para os valores reais
    mapbox_style = "carto-positron", # define o estilo do mapa
    center={"lat":-14, "lon": -55}, # define a posição do mapa que será gerado
    zoom = 3, # zoom inicial
    opacity = 0.5, # adiciona opacidade para que apareça o fundo
)
pyo.offline.plot(fig, filename = "mapa-01.html")
```

Mas ainda podemos melhorada este mapa. Primeiro eu vou dar nome para o hover passando a coluna 'UF' para o parâmetro <code>hover_name</code>, mas vou remover essa informação do texto que aparece no hover para não ficar repetido, o que é feito passando o nome da coluna que se deseja remover como False através de um dicionário para o parâmetro <code>hover_data</code>.
{: .text-justify}

```python
fig = px.choropleth_mapbox(
                            ...
                            hover_name = "UF", # nome do hover
                            hover_data = {'UF': False}, # removendo o UF para não ficar repetido
)
```

Outra coisa que não me agradou neste mapa foi a palheta de cores. Para este caso, eu vou optar por uma palheta de cor linear (uma única cor), pois eu quero que a intensidade da cor indique o maior número de focos identificados. Para alterar a palheta, podemos utilizar o parâmetro <code>color_continuous_scale</code>, passando o nome de uma palheta de cores do próprio Plotly. Temos diversas opções no plotly express, que podem ser obtidas de <code>px.colors.named_colorscales()</code>. Eu gostei da palheta do cor <code>'reds'</code>, que é uma palheta que sai do branco e vai para o vermelho escuro. A escolha pelo do vermelho aqui é devido as queimadas serem, na maioria das vezes, algo negativo, e a cor vermelha geralmente é atribuída a coisas negativas.
{: .text-justify}

```python
fig = px.choropleth_mapbox(
                            ...
                            color_continuous_scale = 'reds', # muda a escala de cor
)
```

 Um outro ponto importante aqui é definir os valores mínimos e máximos para as cores. Isto é importante para a animação. A animação nada mais é do que uma série de mapas, variando o Ano (neste caso específico). Como cada ano tem um limite máximo diferente dos demais (variação no número de focos de queimadas a cada ano), a escala muda todo gráfico. Mas se for setado um valor mínimo e um máximo para todos os Anos, esta escala vai se manter igual em todos os frames da animação, mantendo o padrão. Para fazer isto, basta passar uma lista com dois elementos (onde o primeiro elemento é o valor mínimo, e o segundo é o valor máximo), através do parâmetro <code>range_color</code>. Como valor mínimo vou passar 0 (nenhum foco de queimada), e como valor máximo vou passar o maior valor total de focos de queimadas do DataFrame (<code>df['Total'].max()</code>)
{: .text-justify}

```python
fig = px.choropleth_mapbox(
                            ...
                            range_color = [0, df['Total'].max()], # limites do eixo Y
)
```

Um outra coisa que não ficou interessante foi o espaçamento das margens do gráfico. Para controlar o tamanho das margens, basta aplicar o método <code>update_layout()</code> à instância de <code>fig</code>, e passar o tamanho das margens em um dicionário para o parâmetro <code>margin</code>. Eu vou remover o tamanho de todas as margens, imitando o método <code>tight_layout</code> do matplotlib.
{: .text-justify}

```python
fig.update_layout(margin={"r":0,"t":0,"l":0,"b":0})
```

Com  estas alterações, o mapa fica desta forma:
{: .text-justify}

*Figura 5* - Mapa de focos de queimadas por ano no Brasil editado.
{: .text-center}

<img src="{{ site.url }}{{ site.baseurl }}/images/dashboards-plotly-express/parte-1/print-03.png" alt="print do mapa gerado para o total de focos de queimadas no Brasil editado." >
{: .text-center}

Você pode ver o <a href="/images/dashboards-plotly-express/parte-1/mapa-02.html" target="_blank">mapa interativo
clicando aqui</a>.
{: .text-justify}

O código esta assim:

```python
# criando o mapa
fig = px.choropleth_mapbox(
                            df, # primeiro parâmetro é o dataframe com os dados
                            locations = 'UF', # coluna do DF que referencia as IDs do mapa
                            geojson = limites_brasil, # arquivo com os limites dos estados
                            color = 'Total', # indicando qual coluna será utilizada para pintar os estados
                            mapbox_style = "carto-positron", # estilo do mapa
                            center = {'lon':-55, 'lat':-14}, # definindo a posição inicial do mapa
                            zoom = 3, # definindo o zoom do mapa (número inteiro entre 0 e 20)
                            opacity = 0.5, # definindo uma opacidade para a cor do mapa
                            hover_name = "UF", # nome do hover
                            hover_data = {'UF': False}, # removendo o UF para não ficar repetido
                            color_continuous_scale = 'reds', # muda a escala de cor
                            range_color = [0, df['Total'].max()], # limites do eixo Y
)
fig.update_layout(margin={"r":0,"t":0,"l":0,"b":0})
pyo.offline.plot(fig, filename = "mapa-02.html") # criando o arquivo html
```

Mas aqui entra o problema com o parâmetro <code>opacity</code>. Como as cores dos gráficos estão com opacidade, a cor que enxergamos em cada estado acaba não correspondendo com a barra de legenda. Repare a diferença na imagem abaixo:
{: .text-justify}

*Figura 6* - Comparativo entre o mapa desenhado com opacidade de 0.5 com opacidade de 1.0.
{: .text-center}

<img src="{{ site.url }}{{ site.baseurl }}/images/dashboards-plotly-express/parte-1/print-04.png" alt="No gráfico à esquerda o mapa com opacidade de 0.5 apresenta cor muito menos intensa do que o mesmo mapa com opacidade de 1.0." >
{: .text-center}

Dessa forma fica evidente que, neste caso, utilizar o valor de opacidade prejudica a interpretação dos mapas, e por isso vou utilizar <code>opacity=1.0</code>. Podemos seguir então.
{: .text-justify}

Da forma como o mapa está, ele apresenta apenas os dados do ano de 2020, e essa informação nem esta aparecendo no gráfico. Uma forma de contornar isto é gerar uma animação ao gráfico. Essa animação funciona como um vídeo, onde você aperta o play e o gráfico atualiza passando os anos. Entretanto, o arquivo final gerado é muito pesado, e por isso, ele não será adicionado no Dashboard final. Mas ainda assim é interessante gerar essa animação, pois é uma opção bem interessante para uma aplicação que não necessite de banda larga (aplicação offline).
{: .text-justify}

Parar gerar uma animação, basta adicionar o parâmetro <code>animation_frame</code>, que vai gerar uma animação ao gráfico pra gente. Para gerar os frames, passamos a coluna que desejamos variar na animação (que neste caso é a coluna 'Ano') através do parâmetro <code>animation_frame</code>.

```python
fig = px.choropleth_mapbox(
                            ...
                            animation_frame = "Ano",
)
```

O arquivo final gerado é um arquivo ".html" igual aos demais gráficos gerados. Entretanto, o tamanho desse arquivo acaba ficando muito grande, pois temos muita informação na animação. Por exemplo, o arquivo gerado para esta animação é de pouco mais de 54 MB (e por isso eu não coloquei ele aqui), enquanto que o mapa gerado para a Figura 4 (por exemplo) tem 5.5 MB aproximadamente. Muitos navegadores não vão conseguir renderizar a animação de forma correta (o meu inclusive) por causa do tamanho do arquivo, então esta função pode acabar atrapalhando mais do que ajudando.
{: .text-justify}

Mas para que você possa ver como que fica a animação, eu criei um ".gif" com os frames gerados (baixei o mapa de cada frame e utilizei o Google fotos para gerar o gif.
{: .text-justify}


*Gif 1* - Gif animado do Mapa de queimadas por ano no Brasil (1998-2020).
{: .text-center}

<img src="{{ site.url }}{{ site.baseurl }}/images/dashboards-plotly-express/parte-1/animacao_final.gif" alt="gif da animação gerada para o mapa de focos de queimadas totais nos diferentes estados brasileiros ao longo da série histórica entre 1998 e 2020." >
{: .text-center}

O código esta dessa forma:

```python
# criando o mapa
fig = px.choropleth_mapbox(
                            df, # primeiro parâmetro é o dataframe com os dados
                            locations = 'UF', # coluna do DF que referencia as IDs do mapa
                            geojson = limites_brasil, # arquivo com os limites dos estados
                            color = 'Total', # indicando qual coluna será utilizada para pintar os estados
                            mapbox_style = "carto-positron", # estilo do mapa
                            center = {'lon':-55, 'lat':-14}, # definindo a posição inicial do mapa
                            zoom = 3, # definindo o zoom do mapa (número inteiro entre 0 e 20)
                            opacity = 1.0, # definindo uma opacidade para a cor do mapa
                            hover_name = "UF", # nome do hover
                            hover_data = {'UF': False}, # removendo o UF para não ficar repetido
                            color_continuous_scale = 'reds', # muda a escala de cor
                            range_color = [0, df['Total'].max()], # limites do eixo Y
                            animation_frame = "Ano",
)
fig.update_layout(margin={"r":0,"t":0,"l":0,"b":0})
pyo.offline.plot(fig, filename = "mapa-03.html") # criando o arquivo html
```

Eu tentei utilizar esta animação no Dashbard, mas tive alguns problemas. Além da demora em carregar a aplicação, em diversas ocasiões o valor do hover não correspondia ao valor correto, mas não pelos dados estarem errados, mas pela lentidão na atualização do Dashboard. Então eu escolhi remover completamente a animação do Dashboard, e deixar a mudança dos anos para o usuário através de um dropdown, o que será feito em breve.
{: .text-justify}

<!-- Tabela para o mapa -->
<h3><a style="color:black" id="tabela-mapas">Tabela com os dados ordenados</a></h3>

Juntamente com o mapa, é interessante apresentar os numeros do total de queimadas para uma melhor visualização do todo, pois em alguns mapas ficou difícil de verificar diferenças entre alguns estados, pois as cores estavam semelhantes, ou pois os estados estavam distantes uns dos outros (Pernambuco e Paraná por exemplo).
{: .text-justify}

A ideia é criar uma tabela com os dados ordenados do estado com maior número total de focos para o estado com menor número total de focos. Então esta tabela deve ter uma coluna para a ordem ("Rank"), uma para o total de focos no ano ('Total'), outra para o nome do estado ("UF") e uma para a região ("Regiao"). Observe que estou utilizando Região sem o ~, pois está assim no DataFrame, mas poderia ser alterado para deixar a grafia correta.
{: .text-justify}

Então precisamos montar o DataFrame com as colunas citadas. Como é o usuário que vai ficar responsável por alterar o ano (através de um dropdown), podemos criar um novo DataFrame filtrado com os dados apenas de um único ano:
{: .text-justify}

```python
# Tabela para acompanhar o mapa do brasil
selected_year = 1998 # fixando um ano para filtrar (vai ser alterado mais tarde pelo usuário através de um dropdown)
df_ano = df[df['Ano'] == selected_year] # filtrando o dataframe inicial para apenas o ano selecionado
df_ano.head()
```

*Figura 7* - DataFrame filtrado para o ano de 1998.
{: .text-center}

<img src="{{ site.url }}{{ site.baseurl }}/images/dashboards-plotly-express/parte-1/print-05.png" alt="print do output gerado ao solicitar para apresentar as primeiras linhas do DataFrame filtrado para o ano de 1998." >
{: .text-center}

Acontece que este DataFrame tem muita informação que não será utilizada. Então eu vou remover as colunas com dados de focos de queimadas para cada mês e também a coluna "Ano", pois já sabemos qual ano estamos avaliando (variável <code>selected_year</code>).
{: .text-justify}

```python
df_ano = df_ano.drop(['Janeiro', 'Fevereiro', 'Março', 'Abril', 'Maio', 'Junho', 'Julho', 'Agosto', 'Setembro', 'Outubro', 'Novembro', 'Dezembro', 'Ano'], axis=1) # removendo colunas que não seráo utilizadas
```

Essa tabela deve conter os dados de forma decrescente (do maior para o menor), então é necessário ordenar o DataFrame de acordo com a coluna 'Total'. Fazer isto com um DataFrame é extremamente simples, pois temos o método <code>sort_values()</code>:
{: .text-justify}

```python
df_ano.sort_values(by='Total', inplace=True, ascending=False) # ordenando os dados do maior para o menor baseado na coluna 'Total'
```

*Figura 8* - DataFrame alterado para o ano de 1998.
{: .text-center}

<img src="{{ site.url }}{{ site.baseurl }}/images/dashboards-plotly-express/parte-1/print-06.png" alt="print do output gerado ao solicitar para apresentar as primeiras linhas do DataFrame filtrado para o ano de 1998 após remoção de colunas e ordenação." >
{: .text-center}

É importante adicionar uma coluna nesta tabela para que seja indicado que os dados estão ordenados (ou rankeados). Poderíamos fazer isto de muitas formas, eu vou utilizar o índice do DataFrame. Mas para utiliza-lo, primeiro tenho de reseta-lo:
{: .text-justify}

```python
df_ano.reset_index(inplace=True, drop=True) # resetando o indice, mas sem que uma nova coluna seja adicionada ao dataframe
```
Depois vou criar um nova coluna 'Rank' utilizando o próprio índice que foi resetado:
{: .text-justify}

```python
df_ano['Rank'] = df_ano.index # criando uma nova coluna chamada 'Rank' com o indice
```
Então vou somar 1 a cada elemento dessa nova coluna para que o Rank varie entre 1 e 27 ao invés de 0 e 26:
{: .text-justify}

```python
df_ano['Rank'] = df_ano['Rank'] + 1 # somando 1 a cada elemento da coluna Rank para que ela inicie em 1
```

*Figura 9* - DataFrame alterado para o ano de 1998.
{: .text-center}

<img src="{{ site.url }}{{ site.baseurl }}/images/dashboards-plotly-express/parte-1/print-07.png" alt="print do output gerado ao solicitar para apresentar as primeiras linhas do DataFrame filtrado para o ano de 1998 após remoção de colunas e ordenação." >
{: .text-center}

Agora repare que a ordem das colunas é "Total",	"UF",	"Regiao" e	"Rank", o que não é o ideal. Eu quero que a tabela esteja nesta ordem: 'Rank', 'Total', 'UF' e 'Regiao'. Alterar a ordem das colunas em um DataFrame é muito simples:
{: .text-justify}

```python
df_ano = df_ano[['Rank', 'Total', 'UF', 'Regiao']] # rearranjando as posições das colunas
```

*Figura 10* - DataFrame alterado para o ano de 1998.
{: .text-center}

<img src="{{ site.url }}{{ site.baseurl }}/images/dashboards-plotly-express/parte-1/print-08.png" alt="print do output gerado ao solicitar para apresentar as primeiras linhas do DataFrame filtrado para o ano de 1998 após remoção de colunas, ordenação e mudança na ordem das colunas." >
{: .text-center}

Mas até aqui, estávamos apenas ajustando o DataFrame para criar uma tabela no plotly; agora falta cria-la!!
{: .text-justify}

Criar tabelas no plotly utilizando um DataFrame é muito simples. Entretanto, temos de utilizar a estrutura tipo <code>go.Figure()</code>, passando um elemento de <code>go.Table()</code> através do parâmetro <code>data</code>. No parâmetro <code>data</code> passamos dois parâmetros, um para o cabeçalho e outro para o corpo da tabela.
{: .text-justify}

```python
fig = go.Figure(data=[go.Table(
    header=dict(),
    cells=dict())
])
```

O parâmetro <code>header</code> seta o nome das colunas através de um dicionário. Como os dados estão em um DataFrame, e temos apenas os dados que serão utilizados, podemos passar o nome de cada coluna no cabeçalho assim:
{: .text-justify}

```python
header=dict(values=list(df_ano.columns),),
```

Já o parâmetro <code>cells</code> define os dados que vão estar no corpo da tabela, e é necessário passar um dicionário com os dados para este parâmetro. Podemos fazer da seguinte forma:
{: .text-justify}

```python
cells=dict(values=[df_ano.Rank, df_ano.Total, df_ano.UF, df_ano.Regiao],))
```

Uma vez setado os valores do cabeçalho e do corpo da tabela, basta criar o arquivo da mesma forma que fazemos anteriormente:

```python
pyo.offline.plot(fig, filename = "tabela-01.html") # criando o arquivo html
```

*Figura 11* - Tabela para os dados de focos de queimadas identificados nos estados durante o ano de 1998.
{: .text-center}

<img src="{{ site.url }}{{ site.baseurl }}/images/dashboards-plotly-express/parte-1/print-09.png" alt="print da tabela gerada para os dados de focos de queimadas em 1998.">
{: .text-center}

Você pode ver o <a href="/images/dashboards-plotly-express/parte-1/tabela-01.html" target="_blank">a tabela gerada
clicando aqui</a>.
{: .text-justify}

O código ficou desta forma:

```python
# Criando a figura da tabela (sim, figura da tabela)
fig = go.Figure(data=[go.Table(
    header=dict(values=list(df_ano.columns),), # dados do cabeçalho
    cells=dict(values=[df_ano.Rank, df_ano.Total, df_ano.UF, df_ano.Regiao],)) # dados do corpo da tabela
])
pyo.offline.plot(fig, filename = "tabela-01.html") # criando o arquivo html
```

É bem possível (e até tranquilo) alterar a cor, tamanho das colunas, fonte, posição do texto dentro das colunas, etc. Mas para gerar o Dashboard eu vou criar a tabela de uma outra forma, então deixamos estas edições para daqui a pouco.
{: .text-justify}




<!-- criando o layout do dashboard -->
<h2><a style="color:black" id="adicionando-elementos">Adicionando os elementos ao Dashboard</a></h2>

O Layout é essencial para desenhar um bom Dashboard. Ele deve ser bonito, responsivo e auxiliar o usuário a focar no que realmente importa. Eu confesso definir o *design* do Layout é um tanto complicado para mim (eu não sei nem combinar roupas direito rsrs). Mas ter uma boa base de layout já ajuda e muito em gerar um design agradável.
{: .text-justify}

O Dash tem componentes que auxiliam na construção do Layout do dashboard, que são baseados no sistema de grid do Bootstrap. Esse sistema tem doze colunas e cinco níveis responsivos que auxiliam o posicionamento dos elementos na tela, inclusive se adaptando a telas de tamanhos diferentes. Cada elemento do dashboard pode ocupar até 12 colunas, e podemos especificar quantas colunas o elemento deve ocupar, se o elemento deve ocupar todas as colunas, como as colunas que sobram vão se comportar, etc.
{: .text-justify}

Existem três componentes de Layout no dash-bootstrap-components: o <code>Container</code>, o <code>Row</code> e o <code>Col</code>. O <code>Container</code> basicamente centraliza o conteúdo da aplicação, e fornece um espaçamento horizontal. Entretanto, os exemplos da documentação não utilizam o <code>Container</code> (utilizam uma <code>Div</code>), então não parece ser algo essencial, e por não ter exemplos diretos na documentação eu vou utilizar as <code>Div</code> mesmo.
{: .text-justify}

O componente <code>Row</code> é um agregador de <code>Col</code>. Basicamente, você seta uma linha, e dentro da linha você seta as colunas. E dentro das colunas que são adicionados os elementos gráficos, tabelas, texto, etc.
{: .text-justify}

Então, os elementos ficam dentro das <code>Col</code>, que fica dentro da <code>Row</code>, que fica dentro do <code>Container</code> (ou uma <code>Div</code>). Todos estes elementos já tem algum estilo aplicado (padrão), mas é simples altera-lo.
{: .text-justify}

Voltemos a aplicação em si. A ideia é que a aplicação tenha um título, depois um aviso para o usuário selecionar um ano e um popover com informações textuais extras (lado a lado), depois um dropdown onde o usuário pode trocar o ano, e por último o mapa e a tabela, lado a lado. Como vamos ter mais de um conjunto de informações (Brasil, Região, Estado), a ideia é ter uma estrutura similar a citada acima para cada um destes conjuntos. Então cada conjunto deste deve estar dentro de uma Div (eu vou utilizar Div ao invés de um Container mesmo), e estas Divs dentro de uma Div geral.
{: .text-justify}

A estrutura básica então fica assim:
{: .text-justify}

```python
app = dash.Dash() # Criando a instancia da aplicação

app.layout = html.Div([ # Div geral
                    html.Div(), # Div para o Titulo Geral
                    html.Div(), # Div para os dados do Brasil (mapa)
                    html.Div(), # Div para os dados separados por Região
                    html.Div(), # Div para os dados separados por estado
                    html.Div(), # Div para um footer
])

# Rodando a aplicação através de um servidor
if __name__ == '__main__':
    app.run_server(debug = True, use_reloader = False)
```







<h3><a style="color:black" id="elemento-titulo-geral">Título geral</a></h3>

Vou começar criando apenas o título geral para a aplicação. O titulo vai ser composto de uma única linha com apenas uma coluna, que deve estar centralizada. Então o texto do título deve estar dentro de uma <code>Col</code>, que por sua vez deve estar dentro de uma <code>Row</code>, que deve estar dentro da <code>Div</code> do título, que esta dentro da <code>Div</code> geral:
{: .text-justify}

```python
app = dash.Dash() # Criando a instancia da aplicação

app.layout = html.Div([ # Div geral
                    html.Div(# Div para o Titulo Geral
                        dbc.Row( # Linha
                            dbc.Col( # Coluna
                                # Aqui é o elemento de texto
                            )
                        )
                    ),
])
# Rodando a aplicação através de um servidor
if __name__ == '__main__':
    app.run_server(debug = True, use_reloader = False)
```

Como elemento de texto, eu vou utilizar um título <code>H3</code> para não ficar muito grande.


*Figura 12* - Dasboard com titulo geral simples.
{: .text-center}

<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/dashboards-plotly-express/parte-1/print-10.png" alt="print do Dashboard com o título geral.">
{: .text-center}

Mas como você (talvez) possa perceber, nem o sistema de grid nem os componentes do Bootstrap foram aplicados ao título. Para que eles sejam aplicados é preciso dizer para a aplicação que estes estilos devem ser utilizados. Para fazer isto, devemos passar o tema do Bootstrap (<code>dbc.themes.BOOTSTRAP</code>) e o tema do sistema de grid (<code>dbc.themes.GRID</code>) em uma lista através do parâmetro <code>external_stylesheets</code> para a aplicação:

```python
app = dash.Dash() # Criando a instancia da aplicação
app = dash.Dash(external_stylesheets=[dbc.themes.BOOTSTRAP, dbc.themes.GRID]) # Criando a instancia da aplicação
...
```

*Figura 13* - Dasboard com titulo geral simples aplicado estilos.
{: .text-center}

<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/dashboards-plotly-express/parte-1/print-11.png" alt="print do Dashboard com o título geral.">
{: .text-center}

Repare que o tamanho do texto foi alterado, bem como a fonte utilizada (o que vem do Bootstrap). Mas o titulo deve estar centralizado, e para fazer isto, basta adicionar um estilo para o elemento <code>dbc.Col</code> para que ele fique centralizado. Também vou alterar a cor do texto, para o azul:
{: .text-justify}

```python
...
                            dbc.Col( # Coluna
                                html.H3("Histórico de queimadas no Brasil entre 1998 e 2020.") # Aqui é o elemento de texto
                            ), style = {'textAlign': 'center', 'color': 'blue'} # deixando o conteúdo da coluna centralizado
...
```

Mas eu não quero que o título fique grudado no topo da tela. Por isso, vou adicionar um espaçamento acima e abaixo do título, e este estilo deve ser aplicado na <code>dbc.Row</code>:
{: .text-justify}

```python
...
                        dbc.Row( # Linha
                            dbc.Col( # Coluna
                                html.H3("Histórico de queimadas no Brasil entre 1998 e 2020.") # Aqui é o elemento de texto
                            ), style = {'textAlign': 'center', 'color': 'blue'} # deixando o conteúdo da coluna centralizado
                        ), style = {'paddingTop': "20px", 'paddingBottom': "20px"} # adicionado espaçamento para a linha
...
```
*Figura 14* - Dasboard com titulo geral simples com os temas aplicados.
{: .text-center}

<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/dashboards-plotly-express/parte-1/print-12.png" alt="print do Dashboard com o título geral após a aplicação dos estilos de grid e Bootstrap.">
{: .text-center}

Agora vamos adicionar os elementos relacionados ao dados do Brasil. Nesta Div vamos ter um titulo (uma linha, uma coluna), um texto e um popover (uma linha, duas colunas), um dropdown (uma linha, uma coluna), o mapa do Brasil e a tabela (uma linha, duas colunas).
{: .text-justify}

Então vamos ter a seguinte estrutura:

```python
app = dash.Dash(external_stylesheets=[dbc.themes.BOOTSTRAP, dbc.themes.GRID]) # Criando a instancia da aplicação
app.layout = html.Div([ # Div geral
                    html.Div(),# Div para o Titulo Geral
                    html.Div( # Div para os dados do Brasil (mapa)
                        [
                            dbc.Row(), # Titulo
                            dbc.Row(), # Texto + Popover
                            dbc.Row(), # Dropdown
                            dbc.Row(), # Mapa + tabela                            
                        ]
                    ),
])
# Rodando a aplicação através de um servidor
if __name__ == '__main__':
    app.run_server(debug = True, use_reloader = False)
```

Como temos vários elementos nesta <code>Div</code>, eles devem estar dentro de uma lista na ordem que serão renderizados.
{: .text-justify}

<h3><a style="color:black" id="elemento-titulo-mapa-brasil">Primeiro sub título</a></h3>

Vou começar com o título desta <code>Div</code>. Este título deve informar ao usuário de qual ano os dados apresentados se referem: "Total de focos de queimadas identificados por estado no ano de " concatenado com o Ano selecionado pelo usuário. Para atualizar o ano toda vez que o usuário alterar o Dropdown é necessário utilizar uma função com um <code>callback</code>. Mas antes disso, vou apenas criar o texto sem referência nenhuma.
{: .text-justify}

Este título vai estar dentro de um <code>dbc.Col()</code> e vai ser um <code>html.H3()</code> estilizado com o texto centralizado, e espaçamento em cima e embaixo:
{: .text-justify}

```python
app.layout = html.Div([ # Div geral
...
                    ),
                    html.Div( # Div para os dados do Brasil (mapa)
                        [
                            dbc.Row(# Titulo
                                dbc.Col(
                                    html.H3("Total de focos de queimadas identificados por estado no ano de XXXX"),
                                ), style = {'textAlign': 'center', 'paddingTop': '40px', 'paddingBottom': '40px'}
                            ),
                        ]
                    ),
])
```

*Figura 15* - Dasboard com titulo geral mais o titulo para a primeira Div.
{: .text-center}

<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/dashboards-plotly-express/parte-1/print-13.png" alt="print do Dashboard com o título geral e o título para a primeira Div.">
{: .text-center}

Agora precisamos importar os dados, pois vamos começar a inserir dados do DataFrame no Dashboard. A importação dos dados deve ser feita apenas uma vez (sempre que possível), logo no início do script, para que o sistema não fique lento e não gaste banda larga sem necessidade. Então vou carregar o DataFrame logo após as importações das bibliotecas.
{: .text-justify}

```python
df = pd.read_csv('historico_estados_queimadas.csv', encoding='latin-1') # carregando os dados
```

Agora criamos a função que vai ficar atualizando o valor baseado no Dropdown. Essa função deve receber o ano selecionado pelo usuário e retornar o texto concatenado com este ano.
{: .text-justify}

```python
# Função para atualizar o titulo da Div do Mapa + tabela
def update_mapa(selected_year):
    return "Total de focos de queimadas identificados por estado no ano de " + str(selected_year)
```

Mas para que a interação entre os componentes funcione, precisamos adicionar um <code>app.callback()</code> a esta função. Este callback vai ter dois parâmetros: um <code>Output()</code> (que deve ser importado) e que tem como primeiro parâmetro a ID do elemento de saída (neste caso, o ID de <code>html.H3</code> que acabamos de criar, mas que não tem ID ainda), e como segundo parâmetro temos de passar para qual parâmetro que o <code>return</code> vai ser utilizado (neste caso é o <code>children</code>, pois a função irá retornar o texto que será impresso na tela); e pelo menos um <code>Input()</code> (que deve estar em uma lista, e também precisa ser importado), que tem de ter pelo menos dois parâmetros, onde o primeiro é o ID do elemento que a informação irá vir (neste, o ID do dropdown que ainda não foi criado) e o segundo que é a informação que esta sendo passada pelo elemento (que neste caso vai ser o ano selecionado pelo usuário).
{: .text-justify}

Então adicionamos o callback na função, o que é feito através de um <code>decorator</code>:
{: .text-justify}


```python
# Função para atualizar o titulo da Div do Mapa + tabela
@app.callback(Output('title-year', 'children'),
             [Input('year-picker', 'value')])
def update_mapa(selected_year):
    return "Total de focos de queimadas identificados por estado no ano de " + str(selected_year)
```

Onde <code>'title-year'</code> é o ID do <code>html.H3()</code> (que ainda não setei) e <code>'year-picker'</code> é o ID do Dropdown que será criado daqui a pouco.
{: .text-justify}

Antes de seguir para a próxima linha, vou adicionar o ID para o titulo, bastando trocar o texto dentro de <code>html.H3()</code> pelo <code>id='title-year'</code>:

```python
app.layout = html.Div([ # Div geral
...
                    html.Div( # Div para os dados do Brasil (mapa)
                        [
                            dbc.Row(# Titulo
                                dbc.Col(
                                    html.H3(id="title-year"),
                                ), style = {'textAlign': 'center', 'paddingTop': '40px', 'paddingBottom': '40px'}
                            ),
                        ]
                    ),
])
```

Como não temos implementado o Dropdown ainda, não é possível gerar o dashboard no momento. Então antes de criar a linha com o texto e o popover, vou criar o dropdown.
{: .text-justify}










<h3><a style="color:black" id="elemento-dropdown">Dropdown</a></h3>

Na linha do dropdown temos apenas este elemento, então temos uma única coluna nessa linha. O elemento do dropdown é um <code>dcc.Dropdown()</code>, que deve ter: um <code>id</code> para poder se acessado; um valor inicial, que deve ser passado através do parâmetro <code>value</code>; e uma lista com um dicionário contendo todas as opções que irão aparecer quando o usuário clicar no elemento, o que é feito através do parâmetro <code>options</code> (que vamos criar daqui a pouco). Temos outros parâmetros que podem ser passados, mas vou utilizar apenas dois: o parâmetro <code>clearable=False</code>, que vai impedir do usuário deixar a opção do dropdown vazia (o que poderia ser um problema no futuro); e o parâmetro <code>style</code> que determina alguns estilos para o dropdown. Eu vou apenas alterar o tamanho do dropdown, de forma que ele ocupe metade do tamanho disponível (<code>style = {'width': '50%'}</code>)
{: .text-justify}

Vou definir um estilo para a coluna onde o dropdown foi inserido, para que ela tenha um pequeno espaçamento acima, abaixo e a esquerda.
{: .text-justify}

```python
app.layout = html.Div([ # Div geral
...
#                             dbc.Row(), # Texto + popover
                            dbc.Row(# Dropdown
                                dbc.Col(
                                        dcc.Dropdown(id = 'year-picker', # id do dropdown
                                                     value = 2020, # seta o valor inicial,
                                                     options = year_options, # as opções que vão aparecer no dropdown
                                                     clearable = False, # permite remover o valor (acho importante manter false para evitar problemas)
                                                     style = {'width': '50%'} # especifica que a largura do dropdown
                                                     ),
                                    ), style = {'paddingTop': "5px",'paddingLeft': '10%', 'paddingBottom': '10px'}                                    
                                )
                            ),
                        ]
                    ),
])
```

Agora precisamos de uma lista <code>year_options</code> para que o usuário possa trocar de ano. Essa lista deve ser um dicionário com duas chaves, uma de nome <code>label</code>, que é o que será apresentado para o usuário e deve ser uma string, e outra de nome <code>value</code>, que é o valor que será utilizado pelo script. Eu vou utilizar o ano como <code>label</code> e como <code>value</code>, obtendo ele através de um loop for:
{: .text-justify}

```python
# criando as opções que serão apresentadas para o usuário trocar de ano no mapa do Brasil
year_options = []
for ano in df['Ano'].unique():
    year_options.append({'label':str(ano), 'value':ano})
```

*Figura 16* - Dasboard com titulo geral mais o titulo para a primeira Div e o dropdown.
{: .text-center}

<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/dashboards-plotly-express/parte-1/print-14.png" alt="print do Dashboard com o título geral e o título para a primeira Div e o dropdown.">
{: .text-center}









<h3><a style="color:black" id="elemento-texto-popover">Texto fixo e Popover</a></h3>

Agora vou adicionar o texto fixo e o popover. Como são dois elementos em uma única linha, precisamos passar dois elementos de colunas (<code>dbc.Col()</code>) para o a linha (<code>dbc.Row()</code>), mas eles tem de estar dentro de uma lista.
{: .text-justify}

```python
app.layout = html.Div([ # Div geral
                    html.Div(),# Div para o Titulo Geral
                    html.Div( # Div para os dados do Brasil (mapa)
                        [
                            dbc.Row(), # Titulo
                            dbc.Row(# Texto + Popover
                                [
                                    dbc.Col(), # Texto
                                    dbc.Col(), # Popover
                                ]
                            ),
                            dbc.Row(), # Dropdown
                            dbc.Row(), # Mapa + tabela                            
                        ]
                    ),
])
```

O texto vai dizer apenas "Escolha um Ano", e ele tem de ficar logo acima do dropdown. Como é apenas um texto fixo (que não vai mudar com alguma interação do usuário com o dashboard), este elemento não irá precisar de um ID e uma função para ser atualizado. Então um simples <code>html.Label()</code> já é o suficiente.
{: .text-justify}

Mas como temos dois elementos dentro desta linha, precisamos informar quantas colunas cada um dos elementos devem preencher, o que é feito através do parâmetro <code>width</code>. A soma do <code>width</code> de todos os elementos de uma linha não pode ultrapassar 12 (pois é o tamanho máximo de colunas do bootstrap). Também podemos passar o parâmetro <code>align</code> para especificar a posição onde o elemento deve ser apresentado dentro do tamanho das colunas indicadas no <code>width</code>. Estas escolhas são puramente por estilo, e certamente eu preciso melhorar o posicionamento e estilização, mas por enquanto esta satisfatório.
{: .text-justify}

```python
app.layout = html.Div([ # Div geral
...
                            dbc.Row(
                                [
                                    dbc.Col( # texto
                                        html.Label("Escolha um ano"), # texto que será impresso
                                        width = 3, # número de colunas que o texto irá preencher
                                        align = 'left', # posição do elemento dentro do número de colunas setado por width
                                        style = {'diplay': 'inline-block'}, # apenas estilo
                                    ),
                                    dbc.Col( # Popover

                                    ),
                                ]
                            ),
])
...
```

Já o popover é um pouco mais complicado. Este elemento nada mais é do que um botão que, ao clicarmos nele, um texto popa do botão com algumas informações extras. Este elemento pode ser extremamente útil em alguns casos onde existem informações importantes para o usuário, mas que não precisam ficar poluindo o dashboard o tempo todo.
{: .text-justify}

Por exemplo, uma informação interessante para esta parte do dashboard seria um resumo dos principais acontecimentos relacionados as queimadas no Brasil no respectivo ano. Esta seria uma informação importante, mas que se adicionada como texto fixo, acabaria poluindo o dashboard, distraindo o usuário das informações visuais.
{: .text-justify}

Infelizmente, eu não encontrei relatórios gerais de cada ano relacionados as queimadas para adicionar informações concretas. Mas, eu fiz de uma forma que, caso as encontre, fique bem simples de adicionar. Eu criei um novo arquivo ".csv" com um texto genérico para ser adicionado ao popover. Mas este arquivo ".csv " não foi pensado para ser um arquivo separado por vírgulas, mas separado por um ponto e vírgula ";". Esta escolha foi feita para ficar mais simples de utilizar tags de html no popover, de forma a aplicar estilo ao texto do elemento (centralizar, colocar palavras em negrito/itálico/sublinhado, etc).
{: .text-justify}

Este novo DataFrame contém duas colunas: a coluna "Ano" que é o respectivo ano (e é utilizada para filtrar o texto), e a coluna "Texto", que contém o texto que que irá popar quando o botão for clicado. Como neste caso eu não encontrei um resumo de cada ano, o texto é simples e não tem nenhuma marcação html, mas nos outros popovers eu vou adicionar as marcações. E quando (se) eu encontrar estas informações, basta eu alterar o arquivo ".csv".
{: .text-justify}

*Figura 17* - Arquivo csv contendo o texto que irá "popar" quando o usuário clicar no botão do popover.
{: .text-center}

<img src="{{ site.url }}{{ site.baseurl }}/images/dashboards-plotly-express/parte-1/print-15.png" alt="print do arquivo csv contendo dados textuais sobre as queimadas no Brasil em cada ano da série histórica.">
{: .text-center}

Você pode fazer o <a href="/assets/files/dashboards/info-anos.csv" download="info-anos.csv">download desse arquivo clicando aqui</a>.
{: .text-justify}

Para fazer o carregamento deste arquivo com o Pandas é necessário adicionar o parâmetro <code>sep=";"</code>, pois as diferentes colunas são interpretadas como um ponto e vírugla (";").
{: .text-justify}

```python
df_texto_ano = pd.read_csv('info-anos.csv', encoding='latin-1', sep=";") # carregando os dados do popover do mapa
```

Agora que temos o texto que será impresso no popover, vamos criar o popover. Neste caso eu vou seguir estritamente a documentação do dash. O popover é um conjunto de dois elementos: um elemento <code>dbc.Button()</code>, e um elemento <code>dbc.Popover()</code> que devem estar em uma <code>Div()</code>. Estes elementos se comunicam utilizando a ID do <code>dbc.Button()</code> com o <code>target</code> do <code>dbc.Popover()</code>.
{: .text-justify}

Já o <code>dbc.Popover()</code> por si só, é composto de outros dois elementos: o <code>dbc.PopoverHeader()</code>, que é o cabeçalho do popover, e o <code>dbc.PopoverBody()</code>, que é o corpo do popover. No cabeçalho eu irei adicionar o "Ano" e no corpo eu irei adicionar o "Texto". Mas como eu quero que o texto do corpo tenha estilos de markdown, eu vou adicionar um elemento <code>dcc.Markdown()</code> dentro do <code>dbc.PopoverBody()</code>.
{: .text-justify}

```python
app.layout = html.Div([ # Div geral
                    html.Div(),# Div para o Titulo Geral
                    html.Div( # Div para os dados do Brasil (mapa)
                        [
                            dbc.Row(), # Titulo
                            dbc.Row(# Texto + Popover
                                [
                                    dbc.Col(), # Texto
                                    dbc.Col(
                                        html.Div(
                                            [
                                                dbc.Button(), # botão do popover
                                                dbc.Popover( # o popover
                                                    [
                                                        dbc.PopoverHeader(), # O cabeçalho do popover
                                                        dbc.PopoverBody( # o corpo do popover
                                                            dcc.Markdown() # O markdown para facilitar o html
                                                        )
                                                    ]
                                                )
                                            ]
                                        )
                                    ),
                                ]
                            ),
                            dbc.Row(), # Dropdown
                            dbc.Row(), # Mapa + tabela                            
                        ]
                    ),
])
```

Vamos adicionar primeiro o botão. Eu adicionei alguns parâmetros ao botão para melhorar a aparência dele e não são essenciais. Mas o parâmetro <code>id</code> é fundamental, pois é através dele que o popover será acionado.
{: .text-justify}

```python
app.layout = html.Div([ # Div geral
...
                                    dbc.Col( # popover
                                        html.Div(
                                            [
                                                dbc.Button( # botão que compoe o popover
                                                    "+ info", # Texto do botão
                                                    outline = True, # Adiciona contorno ao botão para melhorar o stylo
                                                    id = "popovertarget-mapa", # id do botão
                                                    style= {'fontFamily': 'Garamond', }, # alterando a fonte do botão
                                                    className="mr-2", # alterando o tipo do botão com uma classe do bootstrap
                                                    color="success", # alterando a cor do botão
                                                    size="sm", # alterando o tamanho do botão para pequeno
                                                ),
                                                dbc.Popover(),
                                            ]
                                            )
                                          )
...
])
```

Agora vamos ao popover em si. Como vimos, temos dois elementos. O primeiro é o <code>dbc.PopoverHeader()</code> que é o título do popover. Como eu quero que esse título seja o nome do ano, e o ano varia de acordo com o valor setado no dropdown, ele necessita de uma função. Então, esse elemento precisa apenas de uma <code>id</code>. Poderia adicionar estilos ao título, mas não tem necessidade.
{: .text-justify}

O segundo elemento é o <code>dbc.PopoverBody()</code>, que vai ser um elemento de <code>dcc.Markdown()</code>, que vai conter o conteúdo contido no DataFrame <code>df_texto_ano['Texto']</code>. Como o conteúdo depende do ano setado no dropdown, este elemento também precisa de uma função. Então este elemento também precisa de um <code>id</code>. Eu vou adicionar um estilo para este elemento, de forma que o texto fique justificado.
{: .text-justify}

Em alguns casos a quantidade de texto que deve aparecer no popover pode ser grande de mais, e acabar não aparecendo, ou apresentar alguma distorção. Para evitar isso, eu vou adicionar ao elemento <code>dbc.PopoverBody()</code> uma barra de rolagem e um tamanho máximo, o que feito através do parâmetro <code>style</code>. Entretanto, a posição do popover aberto pode se alterar dependendo da posição da tela do usuário. É um ponto para ficar atento no final do desenvovimento do aplicativo para fazer ajustes.
{: .text-justify}

```python
app.layout = html.Div([ # Div geral
...
                                    dbc.Col( # popover
                                        html.Div(
                                            [
                                                dbc.Button( # botão que compoe o popover
                                                    "+ info", # Texto do botão
                                                    outline = True, # Adiciona contorno ao botão para melhorar o stylo
                                                    id = "popovertarget-mapa", # id do botão
                                                    style= {'fontFamily': 'Garamond', }, # alterando a fonte do botão
                                                    className="mr-2", # alterando o tipo do botão com uma classe do bootstrap
                                                    color="success", # alterando a cor do botão
                                                    size="sm", # alterando o tamanho do botão para pequeno
                                                ),
                                                dbc.Popover( # popover em si
                                                    [
                                                        dbc.PopoverHeader(id='popover-header-mapa'), # id do cabeçalho do popover
                                                        dbc.PopoverBody( # O corpo do popover
                                                            dcc.Markdown( # elemento para rodar tags markdown
                                                                    id='popover-body-mapa', # id do corpo do popover
                                                                    style={'textAlign': 'justify',} # deixando o texto do corpo justificado
                                                                ),
                                                                style= {'overflow': 'auto', # adicionado barra de rolagem ao corpo do popover
                                                                        'max-height': '500px'} # colocando um tamanho máximo para a caixa do popover
                                                            ),
                                                    ],
                                                ),
                                            ]
                                        )
                                    ),
...
])
```

Agora é importante adicionar alguns parâmetros o <code>dbc.Popover()</code>. Precisamos dar um <code>id</code> para ele, que vai ser utilizado para definir o estado do popver (aparecendo ou não aparecendo). Também é necessário adicionar o parâmetro <code>target</code>, que deve receber a <code>id</code> do botão do popover ("popovertarget-mapa"). Um outro parâmetro interessante é o <code>placement</code> que indica em qual posição o popover deve "popar". E também é importante setar o parâmetro <code>is_open</code> como <code>False</code> para que o estado inicial do popover seja escondido, afinal de contas, eu quero que o popover apareça apenas quando o usuário clicar no botão.
{: .text-justify}


```python
app.layout = html.Div([ # Div geral
...
                                    dbc.Col( # popover
                                        html.Div(
                                            [
                                                dbc.Button( # botão que compoe o popover
                                                    "+ info", # Texto do botão
                                                    outline = True, # Adiciona contorno ao botão para melhorar o stylo
                                                    id = "popovertarget-mapa", # id do botão
                                                    style= {'fontFamily': 'Garamond', }, # alterando a fonte do botão
                                                    className="mr-2", # alterando o tipo do botão com uma classe do bootstrap
                                                    color="success", # alterando a cor do botão
                                                    size="sm", # alterando o tamanho do botão para pequeno
                                                ),
                                                dbc.Popover( # popover em si
                                                    [
                                                        dbc.PopoverHeader(id='popover-header-mapa'), # id do cabeçalho do popover
                                                        dbc.PopoverBody( # O corpo do popover
                                                            dcc.Markdown( # elemento para rodar tags markdown
                                                                    id='popover-body-mapa', # id do corpo do popover
                                                                    style={'textAlign': 'justify',} # deixando o texto do corpo justificado
                                                                ),
                                                                style= {'overflow': 'auto', # adicionado barra de rolagem ao corpo do popover
                                                                        'max-height': '500px'} # colocando um tamanho máximo para a caixa do popover
                                                            ),
                                                    ],
                                                    id ='popover-mapa', # setando a id
                                                    target = "popovertarget-mapa", # setando o botão de target
                                                    placement='bottom-end', # definindo a posição que o popver deve abrir na tela em relação ao botão
                                                    is_open = False, # definindo que o estado inicial do popover é fechado
                                                ),
                                            ]
                                        )
                                    ),
...
])
```

Agora precisamos apenas adicionar as funções com os callbacks. A função para o conteúdo do popover é parecida com a função para atualizar o nome do titulo da Div do mapa e da tabela. A função tem de receber o ano selecionado no dropdown, e retornar o texto escrito no DataFrame <code>df_texto_ano</code> filtrado com o ano selecionado (<code>selected_year</code>).  Como callback, a função deve receber como input o valor setado no dropdown, que tem <code>id='year-picker'</code>, e ter como output o <code>id</code> do corpo do popover, que é <code>id='popover-body-mapa'</code>.
{: .text-justify}

```python
# Conteudo do corpo para o popover do mapa
@app.callback(Output('popover-body-mapa', 'children'),
             [Input('year-picker', 'value')])
def update_pop_over_body_mapa(selected_year):
    return df_texto_ano[df_texto_ano['Ano'] == selected_year]['Texto']
```

De forma semelhante, temos a função para o cabeçalho. A função deve receber o ano selecionado, e retornar o própio ano como uma string. Como Input, tem de receber o valor setado no dropdown com <code>id='year-picker'</code>, e tem de enviar o texto para o cabeçalho do popover com <code>id='popover-header-mapa'</code>.
{: .text-justify}
```python
# Header para o popover do mapa
@app.callback(Output('popover-header-mapa', 'children'),
             [Input('year-picker', 'value')])
def update_pop_over_header_mapa(selected_year):
    return "Brasil em " + str(selected_year)
```

E agora falta apenas a função que define a ação que acontece ao clicar no botão, que é o de abrir e fechar o popover. Essa função recebe o número de clicks (<code>n_clicks</code> e o <code>is_open</code>, e alterna entre False e True baseado no número de cliques no botão. Como input, temos o número de clicks do botão com <code>id='popovertarget-mapa'</code>. Como output, temos o <code>True or False</code> baseado no número de clicks (para o parâmetro <code>is_open</code>) para o popover com <code>id='popover-mapa'</code>. E, neste caso, precisamos adicionar o <code>State()</code>, pois queremos que o popover seja acionado/desligado apenas quando o botão é clicado (não é exatamente assim, é mais ligado ao fato de acessar o valor atual do parâmetro... reescrever o texto no futuro).
{: .text-justify}

```python
# Alterando o estado do popover, de False para True, de True para false ao clicar
@app.callback(Output("popover-mapa", "is_open"),
            [Input('popovertarget-mapa',"n_clicks")],
            [State("popover-mapa", "is_open")])
def toggle_popover_mapa(n, is_open):
    if n:
        return not is_open
    return is_open
```

E por fim falta adicionar o tamanho e o alinhamento do popover na linha. Eu vou deixar 2 colunas para o popover, pois o botão é pequeno. Vou alinha-lo à direita. E vou aproveitar e adicionar um espaçamento lateral para a linha, e setar o parâmetro <code>justify='between'</code>, que faz com que as colunas que sobram (12 - 3 - 2 = 7 colunas sobrando) fiquem entre as duas colunas.
{: .text-justify}


*Figura 18* - Captura de tela do dashboard com o popover.
{: .text-center}

<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/dashboards-plotly-express/parte-1/print-16.png" alt="Captura de tela do dashboard com o popover.">
{: .text-center}

O script está assim no momento:

```python
df = pd.read_csv('historico_estados_queimadas.csv', encoding='latin-1') # carregando os dados
df_texto_ano = pd.read_csv('info-anos.csv', encoding='latin-1', sep=";") # carregando os dados do popover do mapa
# criando as opções que serão apresentadas para o usuario trocar de ano no mapa do Brasil
year_options = []
for ano in df['Ano'].unique():
    year_options.append({'label':str(ano), 'value':ano})


app = dash.Dash(external_stylesheets=[dbc.themes.BOOTSTRAP, dbc.themes.GRID]) # Criando a instancia da aplicação

app.layout = html.Div([ # Div geral
                    html.Div(# Div para o Titulo Geral
                        dbc.Row( # Linha
                            dbc.Col( # Coluna
                                html.H3("Histórico de queimadas no Brasil entre 1998 e 2020.") # Aqui é o elemento de texto
                            ), style = {'textAlign': 'center', 'color': 'blue'} # deixando o conteúdo da coluna centralizado
                        ), style = {'paddingTop': "20px", 'paddingBottom': "20px"} # adicionado espaçamento para a linha
                    ),
                    html.Div( # Div para os dados do Brasil (mapa)
                        [
                            dbc.Row(# Titulo
                                dbc.Col(
                                    html.H3(id="title-year"),
                                ), style = {'textAlign': 'center', 'paddingTop': '40px', 'paddingBottom': '40px'}
                            ),
                            dbc.Row(
                                [
                                    dbc.Col( # texto
                                        html.Label("Escolha um ano"), # texto que será impresso
                                        width = 3, # número de colunas que o texto irá preencher
                                        align = 'left', # posição do elemento dentro do número de colunas setado por width
                                        style = {'diplay': 'inline-block'}, # apenas estilo
                                    ),
                                    dbc.Col( # popover
                                        html.Div(
                                            [
                                                dbc.Button( # botão que compoe o popover
                                                    "+ info", # Texto do botão
                                                    outline = True, # Adiciona contorno ao botão para melhorar o stylo
                                                    id = "popovertarget-mapa", # id do botão
                                                    style= {'fontFamily': 'Garamond', }, # alterando a fonte do botão
                                                    className="mr-2", # alterando o tipo do botão com uma classe do bootstrap
                                                    color="success", # alterando a cor do botão
                                                    size="sm", # alterando o tamanho do botão para pequeno
                                                ),
                                                dbc.Popover( # popover em si
                                                    [
                                                        dbc.PopoverHeader(id='popover-header-mapa'), # id do cabeçalho do popover
                                                        dbc.PopoverBody( # O corpo do popover
                                                            dcc.Markdown( # elemento para rodar tags markdown
                                                                    id='popover-body-mapa', # id do corpo do popover
                                                                    style={'textAlign': 'justify',} # deixando o texto do corpo justificado
                                                                ),
                                                                style= {'overflow': 'auto', # adicionado barra de rolagem ao corpo do popover
                                                                        'max-height': '500px'} # colocando um tamanho máximo para a caixa do popover
                                                            ),
                                                    ],
                                                    id ='popover-mapa', # setando a id
                                                    target = "popovertarget-mapa", # setando o botão de target
                                                    placement='bottom-end', # definindo a posição que o popver deve abrir na tela em relação ao botão
                                                    is_open = False, # definindo que o estado inicial do popover é fechado
                                                ),
                                            ]
                                        ),
                                        width = 2, # setando o numero de colunas que o elemento de ocupar
                                        align = 'right', # setando a posição que o elemento deve ficar
                                    ),
                                ], style = {'paddingLeft': '12%', 'paddingRight': '5%'}, # adicionando um espaçamento lateral
                                   justify='between', # definindo que as colunas que "sobram" devem ficar entre as colunas setadas
                            ),
                            dbc.Row(# Dropdown
                                dbc.Col(
                                        dcc.Dropdown(id = 'year-picker', # id do dropdown
                                                     value = 2020, # seta o valor inicial,
                                                     options = year_options, # as opções que vão aparecer no dropdown
                                                     clearable = False, # permite remover o valor (acho importante manter false para evitar problemas)
                                                     style = {'width': '50%'} # especifica que a largura do dropdown
                                                     ),
                                    ), style = {'paddingTop': "5px",'paddingLeft': '10%', 'paddingBottom': '10px'}                                    
                                ),

                        ]
                    ),
])


# Alterando o estado do popover, de False para True, de True para false ao clicar
@app.callback(Output("popover-mapa", "is_open"),
            [Input('popovertarget-mapa',"n_clicks")],
            [State("popover-mapa", "is_open")])
def toggle_popover_mapa(n, is_open):
    if n:
        return not is_open
    return is_open

# Header para o popover do mapa
@app.callback(Output('popover-header-mapa', 'children'),
             [Input('year-picker', 'value')])
def update_pop_over_header_mapa(selected_year):
    return "Brasil em " + str(selected_year)

# Conteudo do corpo para o popover do mapa
@app.callback(Output('popover-body-mapa', 'children'),
             [Input('year-picker', 'value')])
def update_pop_over_body_mapa(selected_year):
    return df_texto_ano[df_texto_ano['Ano'] == selected_year]['Texto']

# Função para atualizar o titulo da Div do Mapa + tabela
@app.callback(Output('title-year', 'children'),
             [Input('year-picker', 'value')])
def update_mapa(selected_year):
    return "Total de focos de queimadas identificados por estado no ano de " + str(selected_year)

# Rodando a aplicação através de um servidor
if __name__ == '__main__':
    app.run_server(debug = True, use_reloader = False)
```

Agora falta adicionar os elementos gráficos na última linha dessa parte. A estrutura de colunas e linhas segue o mesmo padrão que o anterior que tinha um texto e o popover, a diferença é que utilizo um elemento de gráfico para o mapa, e uma div para a tabela:
{: .text-justify}

```python
app.layout = html.Div([ # Div geral
                    html.Div(),# Div para o Titulo Geral
                    html.Div( # Div para os dados do Brasil (mapa)
                        [
                            dbc.Row(), # Titulo
                            dbc.Row(# Texto + Popover
                                [
                                    dbc.Col(), # Texto
                                    dbc.Col(
                                        html.Div(
                                            [
                                                dbc.Button(), # botão do popover
                                                dbc.Popover( # o popover
                                                    [
                                                        dbc.PopoverHeader(), # O cabeçalho do popover
                                                        dbc.PopoverBody( # o corpo do popover
                                                            dcc.Markdown() # O markdown para facilitar o html
                                                        )
                                                    ]
                                                )
                                            ]
                                        )
                                    ),
                                ]
                            ),
                            dbc.Row(), # Dropdown
                            dbc.Row(# Mapa + tabela                            
                                [
                                    dbc.Col(
                                        dcc.Graph() # mapa
                                    ),
                                    dbc.Col(
                                        html.Div() # tabela
                                    ),
                                ]
                            ),
                        ]
                    ),
])
```












<h3><a style="color:black" id="elemento-mapa">Mapa e tabela</a></h3>

Vou começar pelo mapa do Brasil. No Layout é necessário apenas passar uma <code>id</code> para o gráfico, pois como ele vai ser atualizado todo vez que o usuário trocar o ano selecionado, o mapa em si tem de estar na saída de uma função que recebe a mudança no dropdown. Mas como temos dois elementos na mesma linha, é precisamos setar a quantidade de colunas que o elemento irá ocupar (<code>width</code>). Após alguns testes, achei que 7 era uma quantidade ok. Também vou deixar o gráfico centralizado, passando o parâmetro <code>align</code> como <code>'center'</code>. E vou adicionar uma pequena borda no mapa através do parâmetro <code>style</code>.
{: .text-justify}

Para a tabela temos a mesma estrutura, com a diferença que o elemento da tabela é um <code>html.Div()</code>, e a tabela vai expandir em 5 colunas (12-7=5).
{: .text-justify}

```python
app.layout = html.Div([ # Div geral
...
                            dbc.Row( # mapa + tabela
                                [
                                    dbc.Col( # mapa
                                        dcc.Graph(id = 'map-brazil'), # id do mapa
                                        width = 7, # numero de colunas que o mapa irá ocupar
                                        align = 'center', # posição do elemento dentro das colunas
                                        style = {'display': 'inline-block', 'paddingLeft': '2%', 'paddingRight': '2%'} # adicionando um espaçamento para não ficar tudo grudado
                                    ),
                                    dbc.Col( # Tabela
                                        html.Div(id = 'mapa-data-table'), # id da tabela do mapa
                                        width = 5, # número de colunas que a tabela irá ocupar
                                        align = 'center', # centralizando a tabela dentro das colunas
                                        style = {'display': 'inline-block', 'paddingLeft': '2%', 'paddingRight': '2%'} # adicionando um espaçamento para não ficar tudo grudado
                                    ),

                        ]
                    ),
])
```

Agora vamos as funções com os callbacks, começando pelo mapa. A função vai receber o ano selecionado (que vem no input do dropdown com <code>id='year-picker'</code>), vai filtrar o DataFrame <code>df</code> para um novo DataFrame <code>df_ano</code>, e esse DataFrame será utilizado para gerar o mapa exatamente como fizemos no inicio desse post. A função vai retornar a figura criada, que vai ser enviada para o elemento gráfico com <code>id='map-brazil'</code>. As diferenças entre o que fizemos no inicio e agora, são que ao invés de utilizar <code>df</code> utilizei o <code>df_ano</code> (mas apenas no primeiro argumento, pois o <code>range_color</code> deve manter o range completo de dados, e não o filtrado), e removi o <code>hover_data</code>, pois não faz mais sentido ter ele aqui (pois os dados estão filtrados para um único ano).
{: .text-justify}

```python
# Função para atualizar o mapa quando o usuario alterar o dropdown
@app.callback(Output('map-brazil','figure'),
             [Input('year-picker','value')])
def update_map_brazil(selected_year):

    df_ano = df[df['Ano'] == selected_year] # novo df com os dados de apenas 1 estado por vez
    # criando o mapa
    fig = px.choropleth_mapbox(
                                df_ano, # primeiro parâmetro é o dataframe com os dados
                                locations = 'UF', # coluna do DF que referencia as IDs do mapa
                                geojson = limites_brasil, # arquivo com os limites dos estados
                                color = 'Total', # indicando qual coluna será utilizada para pintar os estados
                                mapbox_style = "carto-positron", # estilo do mapa
                                center = {'lon':-55, 'lat':-14}, # definindo a posição inicial do mapa
                                zoom = 3, # definindo o zoom do mapa (número inteiro entre 0 e 20)
                                opacity = 1.0, # definindo uma opacidade para a cor do mapa
                                hover_name = "UF", # nome do hover
                                color_continuous_scale = 'reds', # muda a escala de cor
                                range_color = [0, df['Total'].max()], # limites do eixo Y

    )
    fig.update_layout(margin={"r":0,"t":0,"l":0,"b":0})

    return fig
```

E não podemos esquecer que temos de carregar o arquivo de geo-localização, o que fazemos logo no início do script.
{: .text-justify}

```python
# Carregando os dados de geolocalização
with open('estados_brasil.geojson') as response: # carregando o arquivo ".geojson"
    limites_brasil = json.load(response)
for feature in limites_brasil ['features']: # adicionado o ID aos dados
    feature['id'] = feature['properties']['name']
```

Agora vamos para a tabela. A função para atualizar a tabela deve receber como input o valor setado no dropdown com <code>id='year-picker'</code>, filtrar e adaptar o DataFrame exatamente como fizemos anteriormente, e retornar a tabela para o elemento com <code>id='mapa-data-table'</code>. Mas aqui eu não vou retornar uma figura, mas uma <code>dash_table.DataTable()</code>, e a sintaxe é um pouco diferente do que fizemos.
{: .text-justify}

Eu vou seguir aqui como esta na documentação. Basicamente, o <code>dash_table.DataTable()</code> trabalha com dicionários para as colunas e para os dados, mas de forma separada. Cada coluna deve ter um <code>id</code>, pois é possível utilizar callbacks para alterar os valores dentro das colunas e células. Os dados também devem estar em um dicionário, o que pode ser facilmente feito quando temos um DataFrame, utilizando o método <code>to_dict('records')</code> dos DataFrames.
{: .text-justify}

A vantagem do <code>dash_table.DataTable()</code> é que é bem simples de estilizar partes da tabela, setando o posicionamento do cabeçalho (<code>style_header={'textAlign': 'center'},</code>) das células (<code>style_cell={'textAlign': 'center', 'font-size': '14px'}</code>), entre outras opções.
{: .text-justify}

```python
# Função para atualizar a tabela do mapda quando o usuário alterar o dropdown
@app.callback(Output('mapa-data-table', 'children'),
            [Input('year-picker', 'value')])
def update_table_map(selected_year):
    df_ano = df[df['Ano'] == selected_year] # filtrando o data frame com o selected_year
    df_ano = df_ano.drop(['Janeiro', 'Fevereiro', 'Março', 'Abril', 'Maio', 'Junho', 'Julho', 'Agosto', 'Setembro', 'Outubro', 'Novembro',
                'Dezembro', 'Ano'], axis=1) # removendo as colunas que não são utilizadas
    df_ano.sort_values(by='Total', inplace=True, ascending=False) # ordenando os dados
    df_ano.reset_index(inplace=True, drop=True) # resetando o indice
    df_ano['Rank'] = df_ano.index # criando uma nova coluna com o indice
    df_ano['Rank'] = df_ano['Rank'] + 1 # somando 1 a nova coluna para que o rank varie entre 1 e 27 ao invés de 0 e 26
    df_ano = df_ano[['Rank', 'Total', 'UF', 'Regiao']] # reordenando a posição das colunas

    return [
            dash_table.DataTable(
                columns=[{"name": i, "id": i} for i in df_ano.columns], # passando o nome das colunas com um id
                data=df_ano.to_dict('records'), # passando os dados
                fixed_rows={'headers': True}, # fixando o cabeçalho para que a barra de rolamento não esconda o cabeçalho
                style_table={'height': '400px', 'overflowY': 'auto'}, # adicionando uma barra de rolamento, e fixando o tamanho da tabela em 400px
                style_header={'textAlign': 'center'}, # centralizando o texto do cabeçalho
                style_cell={'textAlign': 'center', 'font-size': '14px'}, # centralizando o texto das céluas e alterando o tamanho da fonte
                style_as_list_view=True, # deixa a tabela sem bordas entre as colunas
                style_data_conditional=[ # este parametro altera a cor da célula quando o usuário clica na célula
                                        {
                                            "if": {"state": "selected"},
                                            "backgroundColor": "rgba(205, 205, 205, 0.3)",
                                            "border": "inherit !important",
                                        }
                                        ],
                                )
                ]
```

*Figura 19* - Captura de tela do dashboard com mapa e tabela.
{: .text-center}

<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/dashboards-plotly-express/parte-1/print-17.png" alt="Captura de tela do dashboard com o mapa e a tabela para o ano de 2016.">
{: .text-center}


Mas você vai reparar que o mapa demora para renderizar, o que provavelmente é devido ao tamanho do mapa que é criado toda vez que o usuário troca de ano. Isto pode ser um problema para um usuário desavisado, e então é importante avisa-lo.
{: .text-justify}









<h3><a style="color:black" id="elemento-modal">Modal</a></h3>

Para avisar o usuário que o mapa pode demorar a ser carregado, eu vou utilizar um elemento <code>dbc.Modal()</code>. O Modal tem uma função semelhante à função de 'alert' do JavaScrip, só que é mais simples de estilizar (pelo menos eu acho 🙃).
{: .text-justify}

O Modal é composto de três partes: o cabeçalho (<code>dbc.ModalHeader()</code>), que geralmente é apenas um título; o corpo (<code>dbc.ModalBody()</code>), que é onde o texto efetivamente é adicionado; e o footer (<code>dbc.ModalFooter()</code>) onde geralmente temos um botão para interagir o modal. Como eu quero que ele apareça logo quando o usuário abra o dashboard, eu vou colocar os elementos do modal em um <code>html.Div()</code> como primeira Div do layout.
{: .text-justify}

```python
app.layout = html.Div([ # Div geral
                    html.Div(# Div para o modal
                        dbc.Modal( # elemento modal
                            [
                                dbc.ModalHeader(), # cabeçalho do modal
                                dbc.ModalBody(), # corpo do modal
                                dbc.ModalFooter() # toter do modal
                            ]
                        ),
                    ),
                    html.Div(),# Div para o Titulo Geral
                    html.Div( # Div para os dados do Brasil (mapa)
                        [
                            dbc.Row(), # Titulo
                            dbc.Row(# Texto + Popover
                                [
                                    dbc.Col(), # Texto
                                    dbc.Col(
                                        html.Div(
                                            [
                                                dbc.Button(), # botão do popover
                                                dbc.Popover( # o popover
                                                    [
                                                        dbc.PopoverHeader(), # O cabeçalho do popover
                                                        dbc.PopoverBody( # o corpo do popover
                                                            dcc.Markdown() # O markdown para facilitar o html
                                                        )
                                                    ]
                                                )
                                            ]
                                        )
                                    ),
                                ]
                            ),
                            dbc.Row(), # Dropdown
                            dbc.Row(# Mapa + tabela                            
                                [
                                    dbc.Col(
                                        dcc.Graph() # mapa
                                    ),
                                    dbc.Col(
                                        html.Div() # tabela
                                    ),
                                ]
                            ),
                        ]
                    ),
])
```

No cabeçalho do Modal eu vou adicionar apenas um texto de 'Aviso!', e estilizar com a cor vermelha para chamar um pouco a atenção. O corpo do Modal vai ser um conjunto de elementos html. Primeiro um <code>html.Label()</code> com a parte principal do aviso. Depois uma quebra de linha (<code>html.Br()</code>). Depois mais duas linhas, pedindo desculpas e um emoticon (por razões óbvias).
{: .text-justify}

E por último temos o footer, que vai ter apenas um botão para fechar o modal. É muito importante adicionar o <code>id</code> ao botão, pois ele será utilizado para fechar o modal.
{: .text-justify}


```python
app.layout = html.Div([ # Div geral
                    html.Div(# div para o modal
                        dbc.Modal( # add o modal
                            [
                                dbc.ModalHeader("Aviso!", # add o texto do cabeçalho do modal
                                               style = {'color': 'red'}), # alterando a cor to texto do cabeçalho do modal
                                dbc.ModalBody( # adicionando o corpo do modal, que é um conjunto de elementos html
                                    [
                                        # add texto
                                        html.Label("O mapa do Brasil pode demorar alguns segundos a mais para atualizar do que os demais gráficos em alguns navegadores."),
                                        html.Br(), # adcionando um linha em branco
                                        html.Label("Pedimos desculpas pelo incoveniente"), # adicionando mais texto
                                        html.Label("\U0001F605") # adicionando um emoticon
                                    ]
                                ),
                                dbc.ModalFooter( # add o footer
                                    dbc.Button( # add um botão para fechar o modal
                                        "Ok!", # texto do botão
                                        id = 'close-sm', # id do botão
                                        className = "ml-auto", # dando uma classe de botão para o botão
                                    )
                                ),
                            ],
                            id = 'modal', # add uma ID ao modal
                            is_open = True, # definindo que o modal vai estar aberto quando o usuario abrir o dashboard
                            centered = True, # definindo que o modal vai estar centralizado
                            style = {'textAlign': 'center'} # centralizando o texto do modal
                        )
                    ),
                    ...
])
```

Agora falta apenas a função para fechar o Modal quando o usuário clicar em "Ok!" (botão com <code>id='close-sm'</code>). A função vai ter como input número de clicks no botão com <code>id='close-sm'</code>, e vai retornar o parâmetro <code>is_open</code> para o modal (<code>id='modal'</code>). Esse parâmetro esta como <code>True</code> no inicio, e quando u usuário clicar um vez no botão, ele irá se tornar <code>False</code>, e o modal irá fechar. Essa função também precisa do <code>State()</code>, que recebe os mesmos parâmetros que o output.

```python
# Função para fechar o modal
@app.callback(Output('modal', 'is_open'),
              [Input('close-sm', 'n_clicks')],
              [State('modal', 'is_open')])
def close_modal(n, is_open):
    if n:
        return not is_open
    return is_open
```

*Figura 20* - Captura de tela do dashboard com o modal aplicado.
{: .text-center}

<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/dashboards-plotly-express/parte-1/print-18.png" alt="Captura de tela do dashboard com o modal aplicado.">
{: .text-center}

Repare que o modal fica destacado, e é adicionando um fundo cinza. E para obter este estilo, não precisei alterar nada do estilo do modal.
{: .text-justify}

E assim, esta primeira parte do Dashboard está pronta. Na <a href="/Dashboards-com-Plotly-Express-Parte-2">Parte 2</a>) eu irei criar e adicionar outros gráficos e tabelas, mas agora focando os dados nas regiões brasileiras. Mas como o grosso do trabalho foi feito nesta parte, as próximas serão muito mais rápidas. Vejo você lá 😀
{: .text-justify}






<h2><a style="color:black" id="script-finalizado">Script finalizado</a></h2>

O código completo ficou assim:

```python
import dash
import dash_core_components as dcc
import dash_html_components as html
from dash.dependencies import Input, Output, State
import dash_bootstrap_components as dbc
import pandas as pd
import numpy as np
import plotly.express as px
import json
import dash_table
import plotly.offline as pyo
from dash_table.Format import Format, Group, Scheme, Symbol
import plotly.graph_objects as go

df = pd.read_csv('historico_estados_queimadas.csv', encoding='latin-1') # carregando os dados
df_texto_ano = pd.read_csv('info-anos.csv', encoding='latin-1', sep=";") # carregando os dados do popover do mapa

# Carregando os dados de geolocalização
with open('estados_brasil.geojson') as response: # carregando o arquivo ".geojson"
    limites_brasil = json.load(response)
for feature in limites_brasil ['features']: # adicionado o ID aos dados
    feature['id'] = feature['properties']['name']


# criando as opções que serão apresentadas para o usuario trocar de ano no mapa do Brasil
year_options = []
for ano in df['Ano'].unique():
    year_options.append({'label':str(ano), 'value':ano})


app = dash.Dash(external_stylesheets=[dbc.themes.BOOTSTRAP, dbc.themes.GRID]) # Criando a instancia da aplicação

app.layout = html.Div([ # Div geral
                    html.Div(# div para o modal
                        dbc.Modal( # add o modal
                            [
                                dbc.ModalHeader("Aviso!", # add o texto do cabeçalho do modal
                                               style = {'color': 'red'}), # alterando a cor to texto do cabeçalho do modal
                                dbc.ModalBody( # adicionando o corpo do modal, que é um conjunto de elementos html
                                    [
                                        # add texto
                                        html.Label("O mapa do Brasil pode demorar alguns segundos a mais para atualizar do que os demais gráficos em alguns navegadores."),
                                        html.Br(), # adcionando um linha em branco
                                        html.Label("Pedimos desculpas pelo incoveniente"), # adicionando mais texto
                                        html.Label("\U0001F605") # adicionando um emoticon
                                    ]
                                ),
                                dbc.ModalFooter( # add o footer
                                    dbc.Button( # add um botão para fechar o modal
                                        "Ok!", # texto do botão
                                        id = 'close-sm', # id do botão
                                        className = "ml-auto", # dando uma classe de botão para o botão
                                    )
                                ),
                            ],
                            id = 'modal', # add uma ID ao modal
                            is_open = True, # definindo que o modal vai estar aberto quando o usuario abrir o dashboard
                            centered = True, # definindo que o modal vai estar centralizado
                            style = {'textAlign': 'center'} # centralizando o texto do modal
                        )
                    ),
                    html.Div(# Div para o Titulo Geral
                        dbc.Row( # Linha
                            dbc.Col( # Coluna
                                html.H3("Histórico de queimadas no Brasil entre 1998 e 2020.") # Aqui é o elemento de texto
                            ), style = {'textAlign': 'center', 'color': 'blue'} # deixando o conteúdo da coluna centralizado
                        ), style = {'paddingTop': "20px", 'paddingBottom': "20px"} # adicionado espaçamento para a linha
                    ),
                    html.Div( # Div para os dados do Brasil (mapa)
                        [
                            dbc.Row(# Titulo
                                dbc.Col(
                                    html.H3(id="title-year"),
                                ), style = {'textAlign': 'center', 'paddingTop': '40px', 'paddingBottom': '40px'}
                            ),
                            dbc.Row(
                                [
                                    dbc.Col( # texto
                                        html.Label("Escolha um ano"), # texto que será impresso
                                        width = 3, # número de colunas que o texto irá preencher
                                        align = 'left', # posição do elemento dentro do número de colunas setado por width
                                        style = {'diplay': 'inline-block'}, # apenas estilo
                                    ),
                                    dbc.Col( # popover
                                        html.Div(
                                            [
                                                dbc.Button( # botão que compoe o popover
                                                    "+ info", # Texto do botão
                                                    outline = True, # Adiciona contorno ao botão para melhorar o stylo
                                                    id = "popovertarget-mapa", # id do botão
                                                    style= {'fontFamily': 'Garamond', }, # alterando a fonte do botão
                                                    className="mr-2", # alterando o tipo do botão com uma classe do bootstrap
                                                    color="success", # alterando a cor do botão
                                                    size="sm", # alterando o tamanho do botão para pequeno
                                                ),
                                                dbc.Popover( # popover em si
                                                    [
                                                        dbc.PopoverHeader(id='popover-header-mapa'), # id do cabeçalho do popover
                                                        dbc.PopoverBody( # O corpo do popover
                                                            dcc.Markdown( # elemento para rodar tags markdown
                                                                    id='popover-body-mapa', # id do corpo do popover
                                                                    style={'textAlign': 'justify',} # deixando o texto do corpo justificado
                                                                ),
                                                                style= {'overflow': 'auto', # adicionado barra de rolagem ao corpo do popover
                                                                        'max-height': '500px'} # colocando um tamanho máximo para a caixa do popover
                                                            ),
                                                    ],
                                                    id ='popover-mapa', # setando a id
                                                    target = "popovertarget-mapa", # setando o botão de target
                                                    placement='bottom-end', # definindo a posição que o popver deve abrir na tela em relação ao botão
                                                    is_open = False, # definindo que o estado inicial do popover é fechado
                                                ),
                                            ]
                                        ),
                                        width = 2, # setando o numero de colunas que o elemento de ocupar
                                        align = 'right', # setando a posição que o elemento deve ficar
                                    ),
                                ], style = {'paddingLeft': '12%', 'paddingRight': '5%'}, # adicionando um espaçamento lateral
                                   justify='between', # definindo que as colunas que "sobram" devem ficar entre as colunas setadas
                            ),
                            dbc.Row(# Dropdown
                                dbc.Col(
                                        dcc.Dropdown(id = 'year-picker', # id do dropdown
                                                     value = 2020, # seta o valor inicial,
                                                     options = year_options, # as opções que vão aparecer no dropdown
                                                     clearable = False, # permite remover o valor (acho importante manter false para evitar problemas)
                                                     style = {'width': '50%'} # especifica que a largura do dropdown
                                                     ),
                                    ), style = {'paddingTop': "5px",'paddingLeft': '10%', 'paddingBottom': '10px'}                                    
                                ),
                            dbc.Row( # mapa + tabela
                                [
                                    dbc.Col( # mapa
                                        dcc.Graph(id = 'map-brazil'), # id do mapa
                                        width = 7, # numero de colunas que o mapa irá ocupar
                                        align = 'center', # posição do elemento dentro das colunas
                                        style = {'display': 'inline-block', 'paddingLeft': '2%', 'paddingRight': '2%'} # adicionando um espaçamento para não ficar tudo grudado
                                    ),
                                    dbc.Col( # Tabela
                                        html.Div(id = 'mapa-data-table'), # id da tabela do mapa
                                        width = 5, # número de colunas que a tabela irá ocupar
                                        align = 'center', # centralizando a tabela dentro das colunas
                                        style = {'display': 'inline-block', 'paddingLeft': '2%', 'paddingRight': '2%'} # adicionando um espaçamento para não ficar tudo grudado
                                    ),
                                ]
                            ),

                        ]
                    ),
])


# Função para fechar o modal
@app.callback(Output('modal', 'is_open'),
              [Input('close-sm', 'n_clicks')],
              [State('modal', 'is_open')])
def close_modal(n, is_open):
    if n:
        return not is_open
    return is_open


# Função para atualizar a tabela do mapda quando o usuário alterar o dropdown
@app.callback(Output('mapa-data-table', 'children'),
            [Input('year-picker', 'value')])
def update_table_map(selected_year):
    df_ano = df[df['Ano'] == selected_year] # filtrando o data frame com o selected_year
    df_ano = df_ano.drop(['Janeiro', 'Fevereiro', 'Março', 'Abril', 'Maio', 'Junho', 'Julho', 'Agosto', 'Setembro', 'Outubro', 'Novembro',
                'Dezembro', 'Ano'], axis=1) # removendo as colunas que não são utilizadas
    df_ano.sort_values(by='Total', inplace=True, ascending=False) # ordenando os dados
    df_ano.reset_index(inplace=True, drop=True) # resetando o indice
    df_ano['Rank'] = df_ano.index # criando uma nova coluna com o indice
    df_ano['Rank'] = df_ano['Rank'] + 1 # somando 1 a nova coluna para que o rank varie entre 1 e 27 ao invés de 0 e 26
    df_ano = df_ano[['Rank', 'Total', 'UF', 'Regiao']] # reordenando a posição das colunas

    return [
            dash_table.DataTable(
                columns=[{"name": i, "id": i} for i in df_ano.columns], # passando o nome das colunas com um id
                data=df_ano.to_dict('records'), # passando os dados
                fixed_rows={'headers': True}, # fixando o cabeçalho para que a barra de rolamento não esconda o cabeçalho
                style_table={'height': '400px', 'overflowY': 'auto'}, # adicionando uma barra de rolamento, e fixando o tamanho da tabela em 400px
                style_header={'textAlign': 'center'}, # centralizando o texto do cabeçalho
                style_cell={'textAlign': 'center', 'font-size': '14px'}, # centralizando o texto das céluas e alterando o tamanho da fonte
                style_as_list_view=True, # deixa a tabela sem bordas entre as colunas
                style_data_conditional=[ # este parametro altera a cor da célula quando o usuário clica na célula
                                        {
                                            "if": {"state": "selected"},
                                            "backgroundColor": "rgba(205, 205, 205, 0.3)",
                                            "border": "inherit !important",
                                        }
                                        ],
                                )
                ]


# Função para atualizar o mapa quando o usuario alterar o dropdown
@app.callback(Output('map-brazil','figure'),
             [Input('year-picker','value')])
def update_map_brazil(selected_year):

    df_ano = df[df['Ano'] == selected_year] # novo df com os dados de apenas 1 estado por vez
    # criando o mapa
    fig = px.choropleth_mapbox(
                                df_ano, # primeiro parâmetro é o dataframe com os dados
                                locations = 'UF', # coluna do DF que referencia as IDs do mapa
                                geojson = limites_brasil, # arquivo com os limites dos estados
                                color = 'Total', # indicando qual coluna será utilizada para pintar os estados
                                mapbox_style = "carto-positron", # estilo do mapa
                                center = {'lon':-55, 'lat':-14}, # definindo a posição inicial do mapa
                                zoom = 3, # definindo o zoom do mapa (número inteiro entre 0 e 20)
                                opacity = 1.0, # definindo uma opacidade para a cor do mapa
                                hover_name = "UF", # nome do hover
                                color_continuous_scale = 'reds', # muda a escala de cor
                                range_color = [0, df['Total'].max()], # limites do eixo Y

    )
    fig.update_layout(margin={"r":0,"t":0,"l":0,"b":0})

    return fig


# Alterando o estado do popover, de False para True, de True para false ao clicar
@app.callback(Output("popover-mapa", "is_open"),
            [Input('popovertarget-mapa',"n_clicks")],
            [State("popover-mapa", "is_open")])
def toggle_popover_mapa(n, is_open):
    if n:
        return not is_open
    return is_open

# Header para o popover do mapa
@app.callback(Output('popover-header-mapa', 'children'),
             [Input('year-picker', 'value')])
def update_pop_over_header_mapa(selected_year):
    return "Brasil em " + str(selected_year)

# Conteudo do corpo para o popover do mapa
@app.callback(Output('popover-body-mapa', 'children'),
             [Input('year-picker', 'value')])
def update_pop_over_body_mapa(selected_year):
    return df_texto_ano[df_texto_ano['Ano'] == selected_year]['Texto']

# Função para atualizar o titulo da Div do Mapa + tabela
@app.callback(Output('title-year', 'children'),
             [Input('year-picker', 'value')])
def update_mapa(selected_year):
    return "Total de focos de queimadas identificados por estado no ano de " + str(selected_year)

# Rodando a aplicação através de um servidor
if __name__ == '__main__':
    app.run_server(debug = True, use_reloader = False)
```
