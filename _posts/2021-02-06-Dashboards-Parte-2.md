---
title: "Dashboards com Python (Parte 2)"
data: 2021-02-06
tags: [dashboard, python, plotly, dash, matplotlib, amazônia, pantanal, queimadas, bioma, INPE]
header:
  image: "/images/chess.jpg"
  image_description: "Chess pieces"
excerpt: "Aprendendo a fazer Dashboards com Python!"
locale: "pt-br"
---

# Desenvolvendo gráficos com matplotlib, Plotly e Dash (Parte 2 de 3)!

Olá 😀!

Neste texto vou dar sequência a criação de Dashboards com Python, onde vou estudar como gerar gráficos com o Plotly. Na <a href="/Dashboards-Parte-1/">Parte 1</a> preparei os dados e criei os gráficos com o matplotlib. Já na <a href="/Dashboards-Parte-3/">Parte 3</a> criei os Dashboards.
{: .text-justify}

Você pode baixar o notebook construído até aqui <a href = "/assets/files/dashboards/queimadas-biomas-parte-1.ipynb" download="queimadas-biomas-parte-1.ipynb">neste link</a> e a planilha com os dados <a href = "/assets/files/dashboards/historico_bioma_completo.csv" download="historico_bioma_completo.csv">neste outro link</a>.
{: .text-justify}

* <a href="#introducao">Introdução</a>
* <a href="#graficos-plotly">Gráficos com Plotly;</a>
  + <a href="#graficos-dispersao">Gráfico de dispersão com linhas;</a>
  + <a href="#graficos-barras">Gráfico de barras;</a>
  + <a href="#graficos-pizza">Gráfico de pizza;</a>

<h2><a style="color:black" id="introducao">Introdução</a></h2>

Agora vamos utilizar o Plotly para gerar os gráficos. Através desta biblioteca, podemos gerar gráficos interativos onde é possível mostrar algumas informações ao passar o mouse em pontos no gráfico. A "desvantagem" é que os gráficos gerados são salvos em arquivos ".html".
{: .text-justify}

Para desenhar os gráficos e gerar os arquivos html, o Plotly combina script Python com marcações (tags) de HTML e estilo de CSS. Eu tenho conhecimento básico de HTML e CSS, e não tive dificuldade nenhuma em entender os passos. Caso você não saiba nada de HTML e CSS, talvez tenha alguma dificuldade, mas não desanime, pois não é nada complicado.
{: .text-justify}

De qualquer forma, os gráficos gerados com o Plotly são elegantes e não precisam de muita edição. Depois que você entende a sua sintaxe, a coisa fica bem dinâmica e relativamente simples.   
{: .text-justify}

<!-- Gráficos com Plotly -->
<h2><a style="color:black" id="graficos-plotly">Gráficos com Plotly</a></h2>

Para gerar gráficos com o Plotly precisamos montar duas estruturas: uma com os dados do gráfico, e outra com o estilo do gráfico. A estrutura dos dados geralmente é chamada de traço (<em>trace</em>), e corresponde ao conjunto de dados separados em listas (cada conjunto está em uma posição na lista). No gráfico de linhas, teremos um traço para o ano de 1998, um outro traço para o ano de 1999, outro para o de 2000 e assim por diante. Já o layout, é um conjunto de informações específicas para o design do gráfico (HTML e CSS). Depois basta combinar as duas estruturas em uma Figura do Plotly e pronto.
{: .text-justify}

Para começar, precisamos importar o Plotly:
{: .text-justify}


```python
import plotly.offline as pyo
import plotly.graph_objs as go
```
<br>

Então, **Vamos lá!**

<h3><a style="color:black" id="graficos-dispersao">Gráfico de dispersão com linhas</a></h3>

Vamos começar com o primeiro ano (1998, setando <code>i = 0</code>). Incialmente, criamos o traço para este conjunto de dados:
{: .text-justify}

```python
traco = [go.Scatter(
                    x = df_aux.columns.values[1:13], # os dados do eixo x
                    y = df_aux.loc[i][1:13] # acessando os dados dos meses (dados do eixo y),
                    mode = 'lines+markers' # define o tipo de gráfico, neste caso vai ter linhas e marcadores
)]
```

Depois criamos um layout simples para o traço:

```python
layout = go.Layout(
                   title = 'Número de focos de queimadas ao longo do ano'
)
```

Depois criamos uma instância de figura do Plotly, combinando o traço com o layout:
{: .text-justify}

```python
fig = go.Figure(data=tracos, layout=layout)
```

E por fim basta gerar o arquivo:

```python
pyo.plot(fig,filename = 'scatter-plot.html')
```

*Figura 1* - Gráfico de dispersão com linhas e pontos gerados com o Plotly.
{: .text-center}

<img src="{{ site.url }}{{ site.baseurl }}/images/dashboards/parte-2/plotly-1.png" alt="print do gráfico de linhas e pontos gerados com o Plotly" >
{: .text-center}


Você pode ver o <a href="/images/dashboards/parte-2/scatter-plot-1.html" target="_blank">gráfico interativo
clicando aqui</a>.
{: .text-justify}

Podemos editar um pouco mais este gráfico antes de gerar o gráfico com todos os anos. Adicionando o parâmetro <code>name</code> podemos dar um nome ao traço (legenda):
{: .text-justify}

```python
name = str(df_aux['Ano'][i]), # adiciono o nome do traço
```

Também podemos alterar o que é apresentado quando passamos o mouse sobre um ponto. Podemos alterar para qualquer coisa que quisermos, mas dependendo do que se deseja adicionar, pode ser bem complicado.
{: .text-justify}

```python
hovertemplate = df_aux.columns.values[1:13] + ' de ' + str(df_aux['Ano'][i]) + '<br>nº de focos: ' + [str(i) for i in list(df_aux.loc[i][1:13])],
```

Ainda alterando o hover, podemos mexer na sua aparência, passando o parâmetro hoverlabel para o layout:
{: .text-justify}

```python
showlegend=True, # garante que a legenda será mostrada
hovermode = "closest", # garante que o hover irá mostrar os dados do ponto mais próximo a seta do mouse
hoverlabel=dict(bgcolor="white", # altera a cor de fundo
                font_size=16, # altera o tamanho da fonte
                font_family="Roboto") # altera a fonte de texto
```

*Figura 2* - Gráfico de dispersão editado com linhas e pontos gerados com o Plotly.
{: .text-center}

<img src="{{ site.url }}{{ site.baseurl }}/images/dashboards/parte-2/plotly-2.png" alt="print do gráfico de linhas e pontos editado que foi gerado com o Plotly." >
{: .text-center}

Você pode ver o <a href="/images/dashboards/parte-2/scatter-plot-2.html" target="_blank">gráfico interativo
clicando aqui</a>.
{: .text-justify}

Agora falta apenas melhorar os eixos. Vou adicionar o nome ao eixo x e passar uma linha (y=0) preta
para demarcar o gráfico:
{: .text-justify}

```python
xaxis = dict(title = 'Meses', linecolor='rgba(0,0,0,1)'), # Nome do eixo x / adiciona uma linha preta em y=0
```

E vou fazer a mesma coisa para o eixo y:

```python
yaxis = dict(title = 'Número de focos de queimadas', linecolor='rgba(0,0,0,1)'), # Nome do eixo y / adiciona uma linha preta em x=0
```

*Figura 3* - Gráfico de dispersão editado com linhas e pontos gerados com o Plotly.
{: .text-center}

<img src="{{ site.url }}{{ site.baseurl }}/images/dashboards/parte-2/plotly-3.png" alt="print do gráfico de linhas e pontos editado que foi gerado com o Plotly." >
{: .text-center}

Você pode ver o <a href="/images/dashboards/parte-2/scatter-plot-3.html" target="_blank">gráfico interativo
clicando aqui</a>.
{: .text-justify}

Agora vamos adicionar os demais anos ao gráfico. Para isso, precisamos criar um traço para cada série de dados. A forma mais fácil de fazer isto é colocar a criação de traços dentro de um loop <code>for</code>, e *percorrer ao longo dos anos*. Então vou criar uma lista vazia chamada <code>tracos</code>, que a cada iteração receberá um novo traço. Depois é só passar esta lista para a Figura.
{: .text-justify}

```python
df_aux = df[df['Bioma'] == df['Bioma'].unique()[0]] # Dividindo o data frame para ter apenas os dados de 1 bioma
# criando os traços
tracos = []
for i in range(df_aux.shape[0]):
    tracos.append(go.Scatter(
                        x = df_aux.columns.values[1:13], # os dados do eixo x
                        y = df_aux.loc[i][1:13], # acessando os dados dos meses (dados do eixo y)
                        mode = 'lines+markers', # define o tipo de gráfico, neste caso vai ter linhas e marcadores
                        name = str(df_aux['Ano'][i]), # adiciono o nome do traço
                        hovertemplate = df_aux.columns.values[1:13] + ' de ' + str(df_aux['Ano'][i]) + '<br>nº de focos: '
                        + [str(i) for i in list(df_aux.loc[i][1:13])] , # alterando o template do hover
    ))
# criando o layout
layout = go.Layout(
                   title = 'Número de focos de queimadas ao longo do ano no bioma: ' + df['Bioma'].unique()[0],
                   showlegend=True, # garante que a legenda será mostrada
                   hovermode = "closest", # garante que o hover irá mostrar os dados do ponto mais próximo a seta do mouse
                   hoverlabel=dict(bgcolor="white", # altera a cor de fundo
                                    font_size=16, # altera o tamanho da fonte
                                    font_family="Roboto"), # altera a fonte de texto
                   xaxis = dict(title = 'Meses', linecolor='rgba(0,0,0,1)'), # Nome do eixo x / adiciona uma linha preta em y=0
                   yaxis = dict(title = 'Número de focos de queimadas', linecolor='rgba(0,0,0,1)'),
)
# Criando a figura
fig = go.Figure(data=tracos, layout=layout)
pyo.plot(fig,filename = 'scatter-plot.html') # gerando o arquivo
```

*Figura 4* - Gráfico de dispersão editado com linhas e pontos gerados com o Plotly para o total de focos de queimadas no bioma Amazônia ao longo de todo o período avaliado.
{: .text-center}

<img src="{{ site.url }}{{ site.baseurl }}/images/dashboards/parte-2/plotly-4.PNG" alt="print do gráfico de linhas e pontos para todos os anos do periodo avaliado que foi gerado com o Plotly." >
{: .text-center}

Você pode ver o <a href="/images/dashboards/parte-2/scatter-plot-4.html" target="_blank">gráfico interativo
clicando aqui</a>.
{: .text-justify}

Agora falta criar o mesmo gráfico para os outros biomas, o que pode ser feito com um novo for loop (como foi feito anteriormente), ou apenas alterando a primeira linha para o bioma desejado.
{: .text-justify}

<h3><a style="color:black" id="graficos-barras">Gráfico de barras</a></h3>

Agora vamos gerar o gráfico de barras para o total de focos de queimadas registrado ao longo do período. Vou seguir com a mesma estratégia de fazer para o primeiro ano, e depois expandir para os outros anos.
{: .text-justify}

A estrutura é exatamente a mesma: criamos o traço com os dados para o gráfico (agora o gráfico de barras), e criamos o layout. Depois juntamos em uma figura, e geramos o arquivo .html.
{: .text-justify}

```python
df_aux = df[df['Bioma'] == df['Bioma'].unique()[0]] # Dividindo o data frame para ter apenas os dados de 1 bioma
traco = [go.Bar(
                x = df_aux['Ano'], # os dados do eixo x
                y = df_aux['Total'])] # acessando os dados dos anos (dados do eixo y)

layout = go.Layout(
                  title = 'Total de focos de queimadas ao longo de todo o período avaliado no bioma: ' +
                  df['Bioma'].unique()[0], # adicionando um titulo
                    )
# Criando a figura
fig = go.Figure(data = traco, layout = layout)
pyo.plot(fig, filename = 'bar-plot.html')# gerando o arquivo
```

*Figura 5* - Gráfico de barras gerado com o Plotly.
{: .text-center}

<img src="{{ site.url }}{{ site.baseurl }}/images/dashboards/parte-2/plotly-5.PNG" alt="print do gráfico de barras que foi gerado com o Plotly." >
{: .text-center}

Você pode ver o <a href="/images/dashboards/parte-2/bar-plot.html" target="_blank">gráfico interativo
clicando aqui</a>.
{: .text-justify}

Agora falta adicionar detalhes. A única coisa diferente que vou fazer é especificar os labels do eixo x, para que seja apresentado o ano abaixo de cada barra no eixo x, e também vou remover o formato dos ticks no eixo y para que apareça o número inteiro.
{: .text-justify}

```python
df_aux = df[df['Bioma'] == df['Bioma'].unique()[0]] # Dividindo o data frame para ter apenas os dados de 1 bioma
traco = [go.Bar(
                x = df_aux['Ano'], # os dados do eixo x
                y = df_aux['Total'],
                name = df['Bioma'].unique()[0],
                hovertemplate = ['Total de focos de queimadas: ' + i for i in [str(i) for i in (df_aux['Total'])]],
)] # acessando os dados dos anos (dados do eixo y)

layout = go.Layout(
                  title = 'Total de focos de queimadas ao longo de todo o período avaliado no bioma: ' +
                  df['Bioma'].unique()[0], # adicionando um titulo
                  xaxis = dict(title = 'Anos', linecolor='rgba(0,0,0,1)', tickmode = 'array', tickvals = df_aux['Ano'], ticktext = df_aux['Ano']), # adicionando nome eo eixo x, barra (y=0) na cor preta, e fixando o ano abaixo de todas as barras
                  yaxis = dict(title = 'Total de queimadas por ano', linecolor='rgba(0,0,0,1)', tickformat=False), # adicionando nome no eixo y, passando uma linha preta em x = 0, e removendo a formatação padrão dos ticks, para que não apareça o K
                  showlegend=True, # adicionando a legenda
                  hoverlabel=dict(bgcolor="white", # alterando a cor de fundo do hover
                                    font_size=16, # alterando o tamanho da letra no hover
                                    font_family="Roboto") # alterando a fonte do hover

                    )
# Criando a figura
fig = go.Figure(data = traco, layout = layout)
pyo.plot(fig, filename = 'bar-plot.html')# gerando o arquivo
```

*Figura 6* - Gráfico de barras gerado com o Plotly para o total de focos de queimadas identificados no bioma Amazônia em todo o período avaliado.
{: .text-center}

<img src="{{ site.url }}{{ site.baseurl }}/images/dashboards/parte-2/plotly-6.png" alt="print do gráfico de barras editado que foi gerado com o Plotly." >
{: .text-center}

Você pode ver o <a href="/images/dashboards/parte-2/bar-plot-1.html" target="_blank">gráfico interativo
clicando aqui</a>.
{: .text-justify}

<h3><a style="color:black" id="graficos-pizza">Gráfico de pizza</a></h3>

Agora vamos ao gráfico de pizza. É muito semelhante ao que fizemos até agora, mas vamos precisar explicitar os valores de y através do parâmetro <code>values</code>, e os valores de x através do parâmetro <code>labels</code>. Mas a estrutura permanece a mesma.
{: .text-justify}


```python
df_aux = df[df['Bioma'] == df['Bioma'].unique()[0]] # Dividindo o data frame para ter apenas os dados de 1 bioma
traco = [go.Pie(
                labels = df_aux['Ano'], # adicionando os labels das fatias de pizza
                values = df_aux['Total'], # adicionando o tamanho das fatais de pizza

)]

layout = go.Layout(
                    title_text='Total de focos de queimadas ao longo de todo o período avaliado no bioma: ' +
                    df['Bioma'].unique()[0], # adicionando um titulo
                  )
# Criando a figura
fig = go.Figure(data = traco, layout = layout)
pyo.plot(fig, filename = 'pie-plot.html')# gerando o arquivo
```

*Figura 7* - Gráfico de pizza obtido com o Plotly para o total de focos de queimadas no bioma Amazônia ao longo de todo o período avaliado.
{: .text-center}

<img src="{{ site.url }}{{ site.baseurl }}/images/dashboards/parte-2/plotly-7.PNG" alt="print do gráfico de pizza que foi gerado com o Plotly." >
{: .text-center}

Você pode ver o <a href="/images/dashboards/parte-2/pie-plot.html" target="_blank">gráfico interativo
clicando aqui</a>.
{: .text-justify}

Observe que por padrão o gráfico já esta na ordem da maior fatia para a menor fatia. Entretanto, ele começa no ângulo diferente (confesso que não identifiquei qual ângulo exato... esta próximo a 45°, mas não tenho certeza...). Para alterar a posição de inicio das fatias, basta passar o parâmetro <code>rotation</code> com o valor do ângulo que deseja utilizar. Entretanto, este parâmetro não me pareceu estar consolidado, pois ao trocar de dados, o ângulo inicial também muda (mesmo sem alterar o <code>rotation</code>).
{: .text-justify}

Também podemos alterar a orientação do texto dentro das fatias, mudando o parâmetro <code>insidetextorientation</code> para 'radial' por exemplo.
{: .text-justify}

```python
df_aux = df[df['Bioma'] == df['Bioma'].unique()[0]] # Dividindo o data frame para ter apenas os dados de 1 bioma
traco = [go.Pie(
                labels = df_aux['Ano'], # adicionando os labels das fatias de pizza
                values = df_aux['Total'], # adicionando o tamanho das fatais de pizza
                rotation=-30, # mudando a posição inicial de preenchimento das fatias
                insidetextorientation='radial', # mudando a orientação do texto dentro das fatias
)]

layout = go.Layout(
                    title_text='Total de focos de queimadas ao longo de todo o período avaliado no bioma: ' +
                    df['Bioma'].unique()[0], # adicionando um titulo
                  )
# Criando a figura
fig = go.Figure(data = traco, layout = layout)
pyo.plot(fig, filename = 'pie-plot.html')# gerando o arquivo
```

*Figura 8* - Gráfico de pizza obtido com o Plotly para o total de focos de queimadas no bioma Amazônia ao longo de todo o período avaliado.
{: .text-center}

<img src="{{ site.url }}{{ site.baseurl }}/images/dashboards/parte-2/plotly-8.PNG" alt="print do gráfico de pizza que foi gerado com o Plotly." >
{: .text-center}

Você pode ver o <a href="/images/dashboards/parte-2/pie-plot-1.html" target="_blank">gráfico interativo
clicando aqui</a>.
{: .text-justify}

Por fim, eu vou alterar o gráfico de pizza para um gráfico de rosquinha (donut). Ou seja, vou adicionar um buraco no centro da pizza, e inserir nesse buraco um texto indicando qual tipo de dado a que os dados correspondem. Para fazer isto, basta adicionar o parâmetro <code>hole</code> para o traço indicando o tamanho do buraco. E também precisamos passar a anotação texto que desejamos inserir, o que é feito através do parâmetro <code>annotations</code> que deve ser passado para o layout:
{: .text-justify}

```python
df_aux = df[df['Bioma'] == df['Bioma'].unique()[0]] # Dividindo o data frame para ter apenas os dados de 1 bioma
traco = [go.Pie(
                labels = df_aux['Ano'], # adicionando os labels das fatias de pizza
                values = df_aux['Total'], # adicionando o tamanho das fatais de pizza
#                 rotation=-45, # mudando a posição inicial de preenchimento das fatias
                insidetextorientation='radial', # mudando a orientação do texto dentro das fatias
                hole=.3, # transformando a pizza em uma rosquinha

)]

layout = go.Layout(
                    title_text='Total de focos de queimadas ao longo de todo o período avaliado no bioma: ' +
                    df['Bioma'].unique()[0], # adicionando um titulo
                    annotations=[dict(text = 'Total', # Colocando o que será inserido dentro do buraco
                                      x = .5, # posição de x do centro do buraco da rosquinha
                                      y = 0.5, # posição de y do centro do buraco da rosquinha
                                      font_size = 20, # tamanho da fonte
                                      font_family = "Roboto", # alterando a fonte do texto
                                      showarrow = False, # removendo a seta que vem por padrão inserida
                                     )],
                  )
# Criando a figura
fig = go.Figure(data = traco, layout = layout)
pyo.plot(fig, filename = 'pie-plot.html')# gerando o arquivo
```

*Figura 9* - Gráfico de rosquinha obtido com o Plotly para o total de focos de queimadas no bioma Amazônia ao longo de todo o período avaliado.
{: .text-center}

<img src="{{ site.url }}{{ site.baseurl }}/images/dashboards/parte-2/plotly-9.PNG" alt="print do gráfico de rosquinha que foi gerado com o Plotly." >
{: .text-center}

Você pode ver o <a href="/images/dashboards/parte-2/pie-plot-2.html" target="_blank">gráfico interativo
clicando aqui</a>.
{: .text-justify}

Essa biblioteca é muito poderosa, gostaria de tê-la conhecido anteriormente 😅.
{: .text-justify}

Você pode baixar o notebook construído até aqui <a href = "/assets/files/dashboards/queimadas-biomas-parte-2.ipynb" download="queimadas-biomas-parte-2.ipynb">neste link</a>.
{: .text-justify}

Com isso fecho esta parte com o Plotly, mas não encerramos com ele não. No <a href="/Dashboards-Parte-3/">Parte 3</a> vou utilizar os gráficos desenhados com o Plotly para criar os Dashboards utilizando o Dash. Te vejo lá 💪!
