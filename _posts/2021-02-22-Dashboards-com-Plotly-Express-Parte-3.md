---
title: "Dashboards com Plotly Express - Parte 3"
data: 2021-02-22
tags: [dashboard, python, plotly, dash, amazônia, plotly express, pantanal, queimadas, bioma, INPE]
header:
  image: "/images/chess.jpg"
  image_description: "Chess pieces"
excerpt: "Comparando todos os estados do Brasil individualmente"
locale: "pt-br"
---


Olá 😀!

Vamos agora para a terceira parte desse artigo barra tutorial de dashboard utilizando plotly express e Dash. Na <a href="/Dashboards-com-Plotly-Express">Parte 1</a> eu montei o layout básico e criei o Dashboard para dados do Brasil, comparando o número de focos a cada ano. Na <a href="/Dashboards-com-Plotly-Express-Parte-2">Parte 2</a> eu criei o Dashboard para dados de focos de queimadas por Região do Brasil. Nesta parte, vou seguir utilizando os dados de focos de queimadas no Brasil, mas agora vou gerar gráficos para os estados individualmente!
{: .text-justify}

Para deixar o código mais limpo eu vou adicionar apenas os elementos criados aqui para os estado.  Sem mais delongas, vamos lá!
{: .text-justify}


* <a href="#introducao">Introdução;</a>
  + <a href="#grafico-dispersao">Gráfico de dispersão com linhas para comparar os meses;</a>
  + <a href="#grafico-barras-estados">Gráfico de barras para comparar os anos;</a>

* <a href="#layout">Layout;</a>
  + <a href="#elemento-titulo">Título;</a>
  + <a href="#elemento-texto-popover">Texto simples e Popover;</a>
  + <a href="#elemento-dropdown">Dropdown;</a>
  + <a href="#elemento-grafico-dispersao-linhas">Gráfico de dispersão com linhas;</a>
  + <a href="#elemento-grafico-barras">Gráfico de barras;</a>
+ <a href="#script-finalizado">Script finalizado;</a>









<!-- breve introdução -->
<h2><a style="color:black" id="introducao">Introdução</a></h2>

Nesta parte vamos analisar os dados separados por estado brasileiro. Para isto, vou criar um gráfico de dispersão com linhas para avaliar o número de focos identificados por mês a cada ano, e um gráfico de barras para o número de focos totais identificados por ano.
{: .text-justify}


A versão final ficou assim:

*Figura 1* - Estado final do Dashboard desenvolvido neste post.
{: .text-center}

<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/dashboards-plotly-express/parte-3/print-06.png" alt="Print do dashboard com os elementos criados para comparar o número de focos de queimadas dentro de cada estado do Brasil." >
{: .text-center}

Lembrando que a ideia aqui é aprender a utilizar os elementos do ploty express, e não avaliar os dados de focos de queimadas precisamente. Por exemplo, temos estados que tem mais de um bioma e isto não esta sendo levado em conta.
{: .text-justify}







<!-- grafico-barras-regioes-estado -->
<h3><a style="color:black" id="grafico-dispersao">Gráfico de dispersão com linhas para comparar os meses</a></h3>

EU vou começar pelo gráfico de dispersão com linhas. Este gráfico vai ter no eixo <code>x</code> os meses do ano, e no eixo <code>y</code> o número de queimada por mês em todos os anos da série histórica. Mas para começar, precisamos importar os dados:
{: .text-justify}

```python
df = pd.read_csv('historico_estados_queimadas.csv', encoding='latin-1')
```

Agora é preciso filtrar os dados para um único estado, que eu vou utilizar como exemplo o Acre, mas no Dashboard vai ser a escolha do usuário através do dropdown:
{: .text-justify}

```python
estado = 'Acre' # variável para o nome do estado
df_estado = df[df['UF'] == estado] # novo df com os dados de apenas 1 estado por vez
```

Agora precisamos juntar todas as colunas referente aos meses em uma única coluna. Eu vou escolher criar um novo DataFrame com os dados de todos os meses. Esse DataFrame vai ter de ter colunas para o Ano, para o número de focos de queimadas por mês, a unidade federativa, a região e uma para o mês:
{: .text-justify}

```python
df_scatter = pd.DataFrame(columns=['Ano', 'Focos de queimadas', 'UF', 'Regiao', 'Mes']) # criando um novo dataframe vazio para o gráfico de dispersão
```

Este novo DataFrame <code>df_scatter</code> será preenchido com os dados que precisamos. Para preencher, precisamos dos dados que estão no <code>df_estado</code>, mas que é preciso filtrar e selecionar as colunas corretas. Eu vou criar um novo DataFrame (<code>df_aux</code>) com as colunas 'Ano', 'Nome do mês', 'UF' e 'Regiao',  (onde 'Nome do mês' é Janeiro, Fevereiro, ..., Dezembro) através de uma cópia do <code>df_estado</code>, substituir o nome da coluna 'Nome do mes' por 'Foco de queimadas', criar uma lista (com o mesmo número de linhas que o <code>df_estado</code>) onde todos os valores são o nome do mês, adicionar esta lista no <code>df_aux</code> em uma coluna chamada 'Mes' e finalmente concatenar o <code>df_aux</code> no <code>df_scatter</code>. Mas como é preciso fazer isto para todos os 12 meses, os passos acima devem se repetidos para cada mês, sendo que a cada iteração o <code>df_aux</code> é concatenado abaixo do mês seguinte.
{: .text-justify}

Para facilitar no for loop, vou criar uma lista com o nome dos meses:
{: .text-justify}

```python
column_names = list(df_estado.columns)[1:13]
```

Agora crio a cópia do recorte do DataFrame <code>df_estado</code> para o primeiro mês:
{: .text-justify}

```python
i = 0 # setando a posição da lista column_names, para depois iterar ao longo do tamanho dessa lista
df_aux = df_estado[['Ano', column_names[i], 'UF', 'Regiao']].copy() # criando uma copia do df_estado com as colunas necessárias para o gráfico de dispersão
```

Agora renomeio a coluna com o nome do mês para "Focos de queimadas":
{: .text-justify}

```python
df_aux.rename(columns={column_names[i]: 'Focos de queimadas'}, inplace = True) # renomeando a coluna com nome "column_names[i] para "Focos de queimadas"
```

Agora crio uma nova lista que vai conter em cada elemento apenas o nome do mês:
{: .text-justify}

```python
nome_mes = [] # lista vazia
for j in range(df_aux.shape[0]): # iterando ao longo de todos os anos para o mês
    nome_mes.append(column_names[i]) # appendando o nome do mês
```

Agora basta colocar esta nova lista em uma nova coluna (chamada 'Mes') no DataFrame auxiliar:
{: .text-justify}

```python
df_aux['Mes'] = nome_mes # adicionando a lista contendo o nome do mes a uma nova coluna "Mes" no df_aux
```

E então concatenar o df_aux no df_scatter:
{: .text-justify}
```python
df_scatter = pd.concat([df_scatter, df_aux]) # concatenando o df_scatter com o df_aux
```

Agora basta colocar todas as linhas acima dentro de um loop for e iterar ao longo dos 12 meses:
{: .text-justify}

```python
df_scatter = pd.DataFrame(columns=['Ano', 'Focos de queimadas', 'UF', 'Regiao', 'Mes']) # criando um novo dataframe vazio para o gráfico de dispersão
column_names = list(df_estado.columns)[1:13]
for i in range(len(column_names)):
    df_aux = df_estado[['Ano', column_names[i], 'UF', 'Regiao']].copy() # criando uma copia do df_estado com as colunas necessárias para o gráfico de dispersão
    df_aux.rename(columns={column_names[i]: 'Focos de queimadas'}, inplace = True) # renomeando a coluna com nome "column_names[i] para "Focos de queimadas"
    nome_mes = [] # lista vazia
    for j in range(df_aux.shape[0]): # iterando ao longo de todos os anos para o mês
        nome_mes.append(column_names[i]) # appendando o nome do mês
    df_aux['Mes'] = nome_mes # adicionando a lista contendo o nome do mes a uma nova coluna "Mes" no df_aux
    df_scatter = pd.concat([df_scatter, df_aux]) # concatenando o df_scatter com o df_aux
df_scatter.head(10)   
```

*Figura 2* - DataFrame contendo os dados ajustados para todos os meses.
{: .text-center}

<img src="{{ site.url }}{{ site.baseurl }}/images/dashboards-plotly-express/parte-3/print-01.PNG" alt="print do output gerado ao apresentar o DataFrame com os dados ajustados para todos os meses fiquem em uma única coluna" >
{: .text-center}

Agora vem a parte muito fácil do plotly express: gerar o gráfico interativo. Basta criar uma figura do tipo <code>px.scatter</code>, passar como primeiro parâmetro o DataFrame <code>df_scatter</code>, e então atribuir aos eixos as respectivas colunas do DataFrame. Para diferenciar as séries (cada ano), passamos o parâmetro <code>color</code> com a coluna que desejamos separar, que neste caso é a coluna 'Ano'. Podemos dar o nome para o hover (neste caso, cada mes), e ainda podemos definir o que será apresentado ao passar o mouse por cima do dado, através do <code>hover_data</code>.
{: .text-justify}

Mas para gerar o gráfico de dispersão com linhas é necessário	atualizar os traços para o modo 'lines+markers', pois o plotly express tem ou um gráfico de dispersão <code>(px.scatter)</code> ou um gráfico de linhas <code>(px.lines)</code>.
{: .text-justify}

Vou aproveitar e adicionar linhas pretas no eixos, alterar formato dos ticks, adicionar um titulo, dentre outras formatações que já utilizamos anteriormente. Estas atualizações de estilo deve ser feitas através do <code>fig.update_layout()</code>.
{: .text-justify}

```python
fig = px.scatter(
                df_scatter, # o data frame contendo os dados
                x = 'Mes', # a coluna para os dados de x
                y = 'Focos de queimadas', # a coluna para os dados de y
                color = 'Ano', # a coluna para diferenciar as séries com cores diferentes
                hover_name = 'Mes', # o nome que aparece ao passar o nome
                hover_data = {'Mes': False}, # Removendo o Mes para que não fique repetido no título do hover e no conteúdo do hover
                )
fig.update_traces(mode='lines+markers') # Deixando o gráfico com linhas e marcadores (por default px.scatter é apenas dispersão e px.lines é apenas linhas)
fig.update_layout(xaxis = dict(linecolor='rgba(0,0,0,1)', # adicionando linha em y = 0
                               title = 'Mês', # Alterando o nome do eixo
                            ),
             yaxis = dict(title = 'Focos de queimadas por mês',  # alterando o titulo do eixo y
                          linecolor='rgba(0,0,0,1)', # adicionando linha em x = 0
                          tickformat=False, # removendo a formatação no eixo y
                         ),
              title_text = 'Focos de queimadas identificados no estado do Acre por mês.',  # adicionando titulo ao gráfico
              title_x = 0.5, # reposicionando o titulo para que ele fique ono centro do gráfico
              )
pyo.offline.plot(fig, filename = "scatter-plot.html")
```

*Figura 3* - Gráfico de dispersão com linhas para o número de focos de queimadas no estado do Acre ao longo dos meses entre os anos de 1998 e 2020.
{: .text-center}

<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/dashboards-plotly-express/parte-3/print-02.png" alt="print do gráfico interativo obtido para o número de focos de queimadas identificado ao longo dos meses, separado por anos, para o estado do Acre." >
{: .text-center}

Você pode ver o <a href="/images/dashboards-plotly-express/parte-3/scatter-plot.html" target="_blank">gráfico interativo clicando aqui</a>.
{: .text-justify}

A parte complicada de desenhar este gráfico foi adaptar o DataFrame para poder utilizar no plotly express, mas desenhar o gráfico é realmente muito simples.
{: .text-justify}

Para gerar o mesmo gráfico para os outros estados, bastaria trocar o filtro utilizado para criar o DataFrame <code>df_estado</code>.
{: .text-justify}

<!-- Gráfico de barras -->
<h3><a style="color:black" id="grafico-barras-estados">Gráfico de barras para comparar os anos</a></h3>


Desenhar o gráfico de barras com o plotly express também é muito simples. Basta criar uma figura do tipo gráfico de barras, passar o DataFrame como primeiro argumento, o nome da coluna do DataFrame que será utilizado para o eixo x, o nome da coluna do DataFrame que será utilizada para o eixo y e o nome da coluna para ser o título do hover. E como eu vou desenhar o gráfico de barras para comparar o total de focos de queimadas por ano em um estado, posso utilizar o <code>df_estado</code> sem fazer nenhuma alteração.
{: .text-justify}

Também vou aplicar alteração de estilo como fiz para o gráfico de dispersão com linhas, utilizando novamente o <code>fig.update_layout()</code>.
{: .text-justify}


```python
fig = px.bar(df_estado, # data frame com os dados
            x = 'Ano', # coluna para os dados do eixo x
            y = 'Total', # coluna para os dados do eixo y
            hover_name = 'UF', # coluna para setar o titulo do hover
            )
fig.update_layout(xaxis = dict(linecolor='rgba(0,0,0,1)', # adicionando linha em y = 0
                                tickmode = 'array', # alterando o modo dos ticks
                                tickvals = df_estado['Ano'], # setando o valor do tick de x
                                ticktext = df_estado['Ano']), # setando o valor do tick de x
                 yaxis = dict(title = 'Total de focos de queimadas por ano',  # alterando o titulo do eixo y
                              linecolor='rgba(0,0,0,1)', # adicionando linha em x = 0
                              tickformat=False, # removendo a formatação no eixo y
                              ),
                  title_text = 'Total de focos de queimadas identificados no estado do Acre por ano',  # adicionando titulo ao gráfico
                  title_x = 0.5, # reposicionando o titulo para que ele fique ono centro do gráfico
                 )
pyo.offline.plot(fig, filename = "bar-plot.html")
```

*Figura 4* - Gráfico de barras para o total de focos de queimadas identificados no estado do Acre entre 1998 e 2020.
{: .text-center}

<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/dashboards-plotly-express/parte-3/print-03.png" alt="print do gráfico de barras interativo para o total de focos de queimadas identificados no estado do Acre entre 1998 e 2020." >
{: .text-center}

Você pode ver o <a href="/images/dashboards-plotly-express/parte-3/bar-plot.html" target="_blank">gráfico interativo clicando aqui</a>.
{: .text-justify}


E com isso finalizo os gráficos para um único estado, e podemos gerar o dashboard.
{: .text-justify}












<h2><a style="color:black" id="layout">Layout</a></h2>

O layout para este dashboard é muito semelhante aos anteriores, com a principal diferença de que ele não tem uma tabela. Então ele é composto de uma linha para o título (que é atualizado com um dropdown), uma linha com um texto fixo e um popover (que é atulizado com o mesmo dropdown), uma linha com um dropdown, uma linha com o gráfico de dispersão com linhas e uma linha com um gráfico de barras.
{: .text-justify}

O layout base fica desta forma (omitindo os elementos feitos na Parte 1 e Parte 2.):
{: .text-justify}


```python
app.layout = html.Div([ # Div geral
                    html.Div(), # Div para o Modal (otimido)
                    html.Div(),# Div para o Titulo Geral (omitido)
                    html.Div(), # Div para a primeira parte (omitido)
                    html.Div(), # Div para a segunda parte (omitido),
                    html.Div( # Div para os dados das estados
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
                            dbc.Row(), # Grafico de dispersão com linhas
                            dbc.Row(), # Grafico de barras
                        ]
                    ),
])
```









<h3><a style="color:black" id="elemento-titulo">Título</a></h3>

Vamos começar pelo título. O título (que na verdade é um subtítulo) é gerado com um elemento <code>html.H2()</code>m que vai receber apenas um <code>id='title-states'</code>, que será utilizado por uma função para atualizar o nome do estado. Também vou utilizar um estilo para centralizar o texto e um espaçamento.
{: .text-justify}

```python
app.layout = html.Div([ # Div geral
                    html.Div( # Div para os dados das estados
                        [
                            # Titulo
                            dbc.Row(
                                dbc.Col(
                                    html.H2(id='title-states') # adicionando uma ID
                                ), style = {'textAlign': 'center', 'paddingTop': '40px', 'paddingBottom': '20px'} # aplicando estilo
                            ),
                        ]
                    ),
])
```
Agora é preciso escrever a função que atualiza este título. Esta função vai receber o valor setado no dropdown (que ainda não foi feito, mas terá uma <code>id='state-picker'</code>), e retornar um texto concatenado com o nome do estado. O retorno vai ter como output o elemento <code>html.H2()</code> com <code>id='title-states'</code>.
{: .text-justify}

```python
# Titulo da Div para os estados
@app.callback(Output('title-states', 'children'),
             [Input('state-picker', 'value')])
def update_graficos_estado(selected_state):
    return "Focos de queimadas identificados no estado: " + str(selected_state)
```






<h3><a style="color:black" id="elemento-texto-popover">Texto simples e Popover</a></h3>


Agora vamos para a próxima linha, onde temos dois elementos: um texto simples e o popover. O texto simples é adicionado através de um elemento <code>html.Label()</code>, onde podemos passar o texto diretamente neste elemento (<code>'children'</code>). Também precisamos setar o número de colunas que o elemento deve expandir (<code>width=3</code>), e algumas opções de edição do elemento.
{: .text-justify}

O popover deve ser inserido em uma <code>html.Div()</code>, que vai ter um botão e o popover em si. O elemento de botão (<code>dbc.Button()</code>) deve ter uma <code>id</code> que será utilizada para controlar o estado (<code>True or False</code) do popover. O elemento <code>dbc.Popover()</code> deve ter uma <code>id</code> (que vai ser utilizado em uma função) e um <code>target</code> (que liga o popover ao botão, e por isso, o <code>target</code> deve receber a <code>id</code> do botão) e também o parâmetro <code>target</code>, que liga o popover ao botão (deve receber o <code>id</code> do botão).  O popover é composto de dois elementos: o cabeçalho (<code>dbc.PopoverHeader()</code>), que como vai ser atualizado sempre que o usuário alterar o estado, precisa receber apenas uma <code>id</code>; e um corpo (<code>dbc.PopoverBody()</code>), que vai receber um elemento de Markdown (<code>dcc.Markdown()</code>), pois o texto que será adicionado no corpo do popover vai ter marcação. Esse elemento precisa de um <code>id</code>.
{: .text-justify}

A coluna do popover também deve ter definido um tamanho para expandir (<code>width=2</code>), e podemos adicionar estilos. Também podemos adicionar estilos a linha, e determinar que as colunas que "sobram" devem ser alocadas entre as duas colunas da linha.
{: .text-justify}

```python
app.layout = html.Div([ # Div geral
...
                            # texto simples + popover
                            dbc.Row(
                                [
                                    dbc.Col( # texto simples
                                        html.Label("Escolha um estado:"), # texto do texto simples
                                        width = 3, # número e coluna que o elemento deve ocupar
                                        align = 'left', # setando o alinhamento do texto
                                        style = {'display': 'inline-block'} # add estido
                                    ),
                                    dbc.Col( # coluna para o popover
                                        html.Div(
                                            [
                                                dbc.Button('+ info', # botão do popover
                                                           outline=True, # colocando contorno no botão
                                                           id = 'popovertarget-estado', # adicionando o id do botão
                                                           style= {'fontFamily': 'Garamond', }, # alterando a fonte do botão
                                                           className="mr-2", # aplicando um tipo de botão do bootstrap
                                                           color="success", # alterando a cor do botão
                                                           size="sm", # alterando o tamanho do botão
                                                          ),
                                                dbc.Popover( # elemento do popover
                                                    [
                                                        # cabeçalho
                                                        dbc.PopoverHeader(id='popover-header-estado'), # id do cabeçalho do popover
                                                        # corpo
                                                        dbc.PopoverBody(
                                                            # add um elemento de markdonw para as marcações funcionarem vindas do texto nodata frame
                                                            dcc.Markdown(
                                                                        id = 'popover-body-estado', # id do markdown
                                                                        style={'textAlign': 'justify',} # deixando o texto no markdown justificado
                                                                        ),
                                                            style= {'overflow': 'auto', 'max-height': '500px'} # deixando o body do popover com uma barra de rolamento e fixando um tamanho máximo
                                                        ),
                                                    ],
                                                    id ='popover-estado', # adicionando um id ao popover
                                                    target = "popovertarget-estado", # definindo o elemento target do popover (tem de ser a id do botão)
                                                    placement='bottom-end', # definindo a posição em que o popover vai popar
                                                    is_open = False, # definindo que o estado inicial do popover é fechado
                                                ),
                                            ]
                                        ),
                                        width = 2, # definindo o número de colunas que o popover deve expandir
                                        align = 'right' # definindo o seu alinhamento na linha
                                    ),
                                ], style = {'paddingLeft': '12%', 'paddingRight': '5%'}, # adicionando um espaçamento para a linha
                                    justify='between' # definindo que as colunas que "sobram" deve ser alocadas entre as colunas
                            ),
...
])
```

Agora vamos as funções relacionadas ao popover, começando pelo seu cabeçalho. A função que vai atualizar o texto do cabeçalho deve receber como input o valor setado no dropdown (que ainda não criei, mas que vai ter <code>id='state-picker'</code>), e retornar o nome do estado setado para o elemento de cabeçalho do popover (<code>dbc.PopoverHeader()</code>) que tem <code>id='popover-header-estado'</code>.
{: .text-justify}

```python
# Header para o popover do estado
@app.callback(Output('popover-header-estado', 'children'),
             [Input('state-picker', 'value')])
def update_pop_over_header_estado(selected_state):
    return str(selected_state)
```

Agora vamos adicionar a função para o corpo do popover. A função que vai atualizar o texto do corpo do popover vai receber como input o valor setado no dropdown (que ainda não criei, mas que vai ter <code>id='state-picker'</code>), e retornar o texto filtrado de um DataFrame que contém informações sobre a geografia do estado. Esse DataFrame (que ainda não importei) tem duas colunas: uma ('Estado') contém o nome de cada um dos estados brasileiros; a segunda ('Texto') contém um resumo da geografia do estado. Esse resumo contém marcação para que seja interpretado pelo Markdown (por exemplo, dois espaços em branco ao final da linha para indicar que é uma quebra de linha).
{: .text-justify}

*Figura 5* - Captura de tela do arquivo csv contendo informações sobre a geografia de cada estado.
{: .text-center}

<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/dashboards-plotly-express/parte-3/print-04.png" alt="print do arquivo csv contendo informações sobre a geografia de cada estado." >
{: .text-center}

Você pode fazer o <a href="/assets/files/dashboards/info-estados.csv" download="info-estados.csv">download deste arquivo clicando aqui</a>.
{: .text-justify}

Mas para poder utilizar este arquivo, é preciso importa-lo antes:
{: .text-justify}

```python
# importando o resumo dos geograficos dos estados
df_texto_estados = pd.read_csv('info-estados.csv', encoding='latin-1', sep=";")
```

E a função fica desta forma:
{: .text-justify}

```python
# Conteudo do body para o popover do estado
@app.callback(Output('popover-body-estado', 'children'),
             [Input('state-picker', 'value')])
def update_pop_over_body_estado(selected_state):
    return df_texto_estados[df_texto_estados['Estado'] == selected_state]['Texto']
```

Agora é preciso adicionar a função para o botão. Essa função vai receber como input o número de clicks (<code>n_clicks</code>) do botão com <code>id='popovertarget-estado'</code>, e utilizar o número de clicks para alterar o parâmetro <code>is_open</code> entre <code>False</code> (popover fechado) e <code>True</code> (popover aberto). Para funcionar, a função deve retornar o valor de <code>is_open</code> como output para o popover de <code>id='popover-estado'</code>, que tem como target o botão com <code>id='popovertarget-estado'</code>. Essa função precisa ter um <code>Stete()</code> com os mesmos parâmetros que o <code>Output()</code>.
{: .text-justify}

```python
# Botao para o popover dos estados
@app.callback(Output("popover-estado", "is_open"),
            [Input('popovertarget-estado',"n_clicks")],
            [State("popover-estado", "is_open")])
def toggle_popover_estado(n, is_open):
    if n:
        return not is_open
    return is_open
```










<h3><a style="color:black" id="elemento-dropdown">Dropdown</a></h3>

Com isso finalizamos esta linha, e partimos para a próxima que irá conter apenas o dropdown. O elemento <code>dcc.Dropdown()</code> deve ter pelo menos um <code>id='state-picker'</code>, um valor inicial (<code>value</code>) e uma lista com os valores que o usuário pode escolher (<code>options</code>). Esta lista pode ser facilmente obtida a partir do DataFrame <code>df</code>:
{: .text-justify}

```python
state_options = []
for state in df['UF'].unique():
    state_options.append({'label':state, 'value':state})
```

E o layout fica desta forma:
{: .text-justify}

```python
app.layout = html.Div([ # Div geral
...
                            # linha para o dropdown
                            dbc.Row(
                                dbc.Col( # coluna unica para o dropdown
                                    dcc.Dropdown(id = 'state-picker', # id do dropdown
                                        value = 'Acre', # seta o valor inicial,
                                        options = state_options, # as opções que vão aparecer no dropdown
                                        clearable = False, # permite remover o valor (acho importante manter false para evitar problemas)
                                        style = {'width': '50%'} # setando que o tamanho do dropdown deve preencher metade do espaço disponível
                                    ),
                                ), style = {'paddingTop': "5px",'paddingLeft': '10%',} # dando um espaçamento entre as linhas
                            ),
...
])
```







<h3><a style="color:black" id="elemento-grafico-dispersao-linhas">Gráfico de dispersão com linhas</a></h3>

Agora falta apenas adicionar os gráficos, começando pelo gráfico de dispersão com linhas. Como é apenas um gráfico na linha toda, precisamos apenas uma linha, uma coluna, e então um elemento de gráfico (<code>dcc.Graph()</code>) com um <code>id</code> que será utilizado na função de callback.
{: .text-justify}


{: .text-justify}

```python
app.layout = html.Div([ # Div geral
...
                            # grafico de dispersão com linhas
                            dbc.Row(
                                dbc.Col( # coluna para o gra´fico de dispersão
                                    dcc.Graph(id='scatter-plot-states'), # adicionado ID para o gráfico de dispersão com linhas
                                    style = {'textAlign': 'center', 'paddingBottom': '60px'} # adicoinado um estilo para a coluna
                                ),
                            ),
...
])
```
A função para este gráfico deve receber como input o valor setado no dropdown que tem <code>id='state-picker'</code>, gerar o gráfico de dispersão com linhas baseado neste valor, e retornar a figura para o output com <code>id='scatter-plot-states'</code>. O script para desenhar o gráfico é o mesmo que fizemos aqui, com atenção para o título do gráfico que agora está dinâmico.
{: .text-justify}

```python
# Gráfico de dispersão para um único estado
@app.callback(Output('scatter-plot-states', 'figure'),
             [Input('state-picker', 'value')])
def update_scatter_states(selected_state):
    df_estado = df[df['UF']== selected_state] # Filtrando os dados para o estado
    # criando um novo dataframe vazio para o gráfico de dispersão
    df_scatter = pd.DataFrame(columns=['Ano', 'Focos de queimadas', 'UF', 'Regiao', 'Mes'])
    # lista com o nome dos estados
    column_names = list(df_estado.columns)[1:13]
    for i in range(len(column_names)):
        df_aux = df_estado[['Ano', column_names[i], 'UF', 'Regiao']].copy() # criando uma copia do df_estado com as colunas necessárias para o gráfico de dispersão
        df_aux.rename(columns={column_names[i]: 'Focos de queimadas'}, inplace = True) # renomeando a coluna com nome "column_names[i] para "Focos de queimadas"
        nome_mes = [] # lista vazia
        for j in range(df_aux.shape[0]): # iterando ao longo de todos os anos para o mês
            nome_mes.append(column_names[i]) # appendando o nome do mês
        df_aux['Mes'] = nome_mes # adicionando a lista contendo o nome do mes a uma nova coluna "Mes" no df_aux
        df_scatter = pd.concat([df_scatter, df_aux]) # concatenando o df_scatter com o df_aux


    fig = px.scatter(
                df_scatter, # o data frame contendo os dados
                x = 'Mes', # a coluna para os dados de x
                y = 'Focos de queimadas', # a coluna para os dados de y
                color = 'Ano', # a coluna para diferenciar as séries com cores diferentes
                hover_name = 'Mes', # o nome que aparece ao passar o nome
                hover_data = {'Mes': False}, # Removendo o Mes para que não fique repetido no título do hover e no conteúdo do hover
                )
    fig.update_traces(mode='lines+markers') # Deixando o gráfico com linhas e marcadores (por default px.scatter é apenas dispersão e px.lines é apenas linhas)
    fig.update_layout(xaxis = dict(linecolor='rgba(0,0,0,1)', # adicionando linha em y = 0
                                   title = 'Mês', # Alterando o nome do eixo
                                ),
                 yaxis = dict(title = 'Focos de queimadas por mês',  # alterando o titulo do eixo y
                              linecolor='rgba(0,0,0,1)', # adicionando linha em x = 0
                              tickformat=False, # removendo a formatação no eixo y
                             ),
                  title_text = 'Focos de queimadas identificados no estado ' + selected_state + ' por mês.',  # adicionando titulo ao gráfico
                  title_x = 0.5, # reposicionando o titulo para que ele fique ono centro do gráfico
                     )
    return fig
```

*Figura 6* - Captura de tela do Dashboard com o gráfico de dispersão com linhas.
{: .text-center}

<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/dashboards-plotly-express/parte-3/print-05.png" alt="print do Dashboard com o gráfico de dispersão com linhas." >
{: .text-center}







<h3><a style="color:black" id="elemento-grafico-barras">Gráfico de barras</a></h3>


Agora falta apenas o gráfico de barras. O layout dele é exatamente igual ao layout do gráfico de dispersão:
{: .text-justify}


```python
app.layout = html.Div([ # Div geral
...
                            # grafico de barras para os estados
                            dbc.Row(
                                dbc.Col(
                                    dcc.Graph(id='bar-plot-states'),
                                    style = {'textAlign': 'center'}
                                ),
                            ),
...
])
```

Agora falta apenas a função, que é semelhante a anterior. A função deve receber o valor que está no dropdown com <code>id='state-picker'</code>, utilizar este valor para gerar o gráfico de barras, e retornar para o output com <code>id='bar-plot-states'</code> a figura gerada. O script é o mesmo que utilizei para desenhar o gráfico de barras anteriormente, apenas alterei o título do gráfico para que fique dinâmico:
{: .text-justify}

```python
# Gráfico de barras para um único estado
@app.callback(Output('bar-plot-states', 'figure'),
             [Input('state-picker', 'value')])
def update_bar_plot_states(selected_state):
    df_estado = df[df['UF']== selected_state] # Filtrando os dados para o estado
    fig = px.bar(df_estado, # data frame com os dados
            x = 'Ano', # coluna para os dados do eixo x
            y = 'Total', # coluna para os dados do eixo y
            hover_name = 'UF', # coluna para setar o titulo do hover
            )
    fig.update_layout(xaxis = dict(linecolor='rgba(0,0,0,1)', # adicionando linha em y = 0
                                    tickmode = 'array', # alterando o modo dos ticks
                                    tickvals = df_estado['Ano'], # setando o valor do tick de x
                                    ticktext = df_estado['Ano']), # setando o valor do tick de x
                     yaxis = dict(title = 'Total de focos de queimadas por ano',  # alterando o titulo do eixo y
                                  linecolor='rgba(0,0,0,1)', # adicionando linha em x = 0
                                  tickformat=False, # removendo a formatação no eixo y
                                  ),
                      title_text = 'Total de focos de queimadas identificados no estado ' + selected_state + ' por ano',  # adicionando titulo ao gráfico
                      title_x = 0.5, # reposicionando o titulo para que ele fique ono centro do gráfico
                     )
    return fig
```

*Figura 7* - Captura de tela do Dashboard com o gráfico de dispersão com linhas e o gráfico de barras.
{: .text-center}

<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/dashboards-plotly-express/parte-3/print-06.png" alt="print do Dashboard com o gráfico de dispersão com linhas e o gráfico de colunas." >
{: .text-center}

E com isso finalizo este dashboard. Agora falta apenas juntar os três dashboards em um único, o que é bem simples pois cada dashboard foi inserido em um <code>html.Div</code>, e vai ser basicamente copiar e color. Mas isto fica para a <a href="/Dashboards-com-Plotly-Express-Parte-4">última parte</a>.








<h2><a style="color:black" id="script-finalizado">Script finalizado</a></h2>

O script desta etapa ficou assim:

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

# importando os dados
df = pd.read_csv('historico_estados_queimadas.csv', encoding='latin-1')
# importando o resumo dos geograficos dos estados
df_texto_estados = pd.read_csv('info-estados.csv', encoding='latin-1', sep=";")
# criando uma lista para conter as opções que o usuario terá para escolher - estados
state_options = []
for state in df['UF'].unique():
    state_options.append({'label':state, 'value':state})

app = dash.Dash(external_stylesheets=[dbc.themes.BOOTSTRAP, dbc.themes.GRID]) # Criando a instancia da aplicação
app.layout = html.Div([ # Div geral
                    html.Div( # Div para os dados das estados
                        [
                            # Titulo
                            dbc.Row(
                                dbc.Col(
                                    html.H2(id='title-states') # adicionando uma ID
                                ), style = {'textAlign': 'center', 'paddingTop': '40px', 'paddingBottom': '20px'} # aplicando estilo
                            ),
                            # texto simples + popover
                            dbc.Row(
                                [
                                    dbc.Col( # texto simples
                                        html.Label("Escolha um estado:"), # texto do texto simples
                                        width = 3, # número e coluna que o elemento deve ocupar
                                        align = 'left', # setando o alinhamento do texto
                                        style = {'display': 'inline-block'} # add estido
                                    ),
                                    dbc.Col( # coluna para o popover
                                        html.Div(
                                            [
                                                dbc.Button('+ info', # botão do popover
                                                           outline=True, # colocando contorno no botão
                                                           id = 'popovertarget-estado', # adicionando o id do botão
                                                           style= {'fontFamily': 'Garamond', }, # alterando a fonte do botão
                                                           className="mr-2", # aplicando um tipo de botão do bootstrap
                                                           color="success", # alterando a cor do botão
                                                           size="sm", # alterando o tamanho do botão
                                                          ),
                                                dbc.Popover( # elemento do popover
                                                    [
                                                        # cabeçalho
                                                        dbc.PopoverHeader(id='popover-header-estado'), # id do cabeçalho do popover
                                                        # corpo
                                                        dbc.PopoverBody(
                                                            # add um elemento de markdonw para as marcações funcionarem vindas do texto nodata frame
                                                            dcc.Markdown(
                                                                        id = 'popover-body-estado', # id do markdown
                                                                        style={'textAlign': 'justify',} # deixando o texto no markdown justificado
                                                                        ),
                                                            style= {'overflow': 'auto', 'max-height': '500px'} # deixando o body do popover com uma barra de rolamento e fixando um tamanho máximo
                                                        ),
                                                    ],
                                                    id ='popover-estado', # adicionando um id ao popover
                                                    target = "popovertarget-estado", # definindo o elemento target do popover (tem de ser a id do botão)
                                                    placement='bottom-end', # definindo a posição em que o popover vai popar
                                                    is_open = False, # definindo que o estado inicial do popover é fechado
                                                ),
                                            ]
                                        ),
                                        width = 2, # definindo o número de colunas que o popover deve expandir
                                        align = 'right' # definindo o seu alinhamento na linha
                                    ),
                                ], style = {'paddingLeft': '12%', 'paddingRight': '5%'}, # adicionando um espaçamento para a linha
                                    justify='between' # definindo que as colunas que "sobram" deve ser alocadas entre as colunas
                            ),
                            # linha para o dropdown
                            dbc.Row(
                                dbc.Col( # coluna unica para o dropdown
                                    dcc.Dropdown(id = 'state-picker', # id do dropdown
                                        value = 'Acre', # seta o valor inicial,
                                        options = state_options, # as opções que vão aparecer no dropdown
                                        clearable = False, # permite remover o valor (acho importante manter false para evitar problemas)
                                        style = {'width': '50%'} # setando que o tamanho do dropdown deve preencher metade do espaço disponível
                                    ),
                                ), style = {'paddingTop': "5px",'paddingLeft': '10%',} # dando um espaçamento entre as linhas
                            ),
                            # grafico de dispersão com linhas
                            dbc.Row(
                                dbc.Col( # coluna para o gra´fico de dispersão
                                    dcc.Graph(id='scatter-plot-states'), # adicionado ID para o gráfico de dispersão com linhas
                                    style = {'textAlign': 'center', 'paddingBottom': '60px'} # adicoinado um estilo para a coluna
                                ),
                            ),
                            # grafico de barras para os estados
                            dbc.Row(
                                dbc.Col(
                                    dcc.Graph(id='bar-plot-states'),
                                    style = {'textAlign': 'center'}
                                ),
                            ),
                        ]
                    ),
])

# Gráfico de barras para um único estado
@app.callback(Output('bar-plot-states', 'figure'),
             [Input('state-picker', 'value')])
def update_bar_plot_states(selected_state):
    df_estado = df[df['UF']== selected_state] # Filtrando os dados para o estado
    fig = px.bar(df_estado, # data frame com os dados
            x = 'Ano', # coluna para os dados do eixo x
            y = 'Total', # coluna para os dados do eixo y
            hover_name = 'UF', # coluna para setar o titulo do hover
            )
    fig.update_layout(xaxis = dict(linecolor='rgba(0,0,0,1)', # adicionando linha em y = 0
                                    tickmode = 'array', # alterando o modo dos ticks
                                    tickvals = df_estado['Ano'], # setando o valor do tick de x
                                    ticktext = df_estado['Ano']), # setando o valor do tick de x
                     yaxis = dict(title = 'Total de focos de queimadas por ano',  # alterando o titulo do eixo y
                                  linecolor='rgba(0,0,0,1)', # adicionando linha em x = 0
                                  tickformat=False, # removendo a formatação no eixo y
                                  ),
                      title_text = 'Total de focos de queimadas identificados no estado ' + selected_state + ' por ano',  # adicionando titulo ao gráfico
                      title_x = 0.5, # reposicionando o titulo para que ele fique ono centro do gráfico
                     )
    return fig

# Gráfico de dispersão para um único estado
@app.callback(Output('scatter-plot-states', 'figure'),
             [Input('state-picker', 'value')])
def update_scatter_states(selected_state):
    df_estado = df[df['UF']== selected_state] # Filtrando os dados para o estado
    # criando um novo dataframe vazio para o gráfico de dispersão
    df_scatter = pd.DataFrame(columns=['Ano', 'Focos de queimadas', 'UF', 'Regiao', 'Mes'])
    # lista com o nome dos estados
    column_names = list(df_estado.columns)[1:13]
    for i in range(len(column_names)):
        df_aux = df_estado[['Ano', column_names[i], 'UF', 'Regiao']].copy() # criando uma copia do df_estado com as colunas necessárias para o gráfico de dispersão
        df_aux.rename(columns={column_names[i]: 'Focos de queimadas'}, inplace = True) # renomeando a coluna com nome "column_names[i] para "Focos de queimadas"
        nome_mes = [] # lista vazia
        for j in range(df_aux.shape[0]): # iterando ao longo de todos os anos para o mês
            nome_mes.append(column_names[i]) # appendando o nome do mês
        df_aux['Mes'] = nome_mes # adicionando a lista contendo o nome do mes a uma nova coluna "Mes" no df_aux
        df_scatter = pd.concat([df_scatter, df_aux]) # concatenando o df_scatter com o df_aux


    fig = px.scatter(
                df_scatter, # o data frame contendo os dados
                x = 'Mes', # a coluna para os dados de x
                y = 'Focos de queimadas', # a coluna para os dados de y
                color = 'Ano', # a coluna para diferenciar as séries com cores diferentes
                hover_name = 'Mes', # o nome que aparece ao passar o nome
                hover_data = {'Mes': False}, # Removendo o Mes para que não fique repetido no título do hover e no conteúdo do hover
                )
    fig.update_traces(mode='lines+markers') # Deixando o gráfico com linhas e marcadores (por default px.scatter é apenas dispersão e px.lines é apenas linhas)
    fig.update_layout(xaxis = dict(linecolor='rgba(0,0,0,1)', # adicionando linha em y = 0
                                   title = 'Mês', # Alterando o nome do eixo
                                ),
                 yaxis = dict(title = 'Focos de queimadas por mês',  # alterando o titulo do eixo y
                              linecolor='rgba(0,0,0,1)', # adicionando linha em x = 0
                              tickformat=False, # removendo a formatação no eixo y
                             ),
                  title_text = 'Focos de queimadas identificados no estado ' + selected_state + ' por mês.',  # adicionando titulo ao gráfico
                  title_x = 0.5, # reposicionando o titulo para que ele fique ono centro do gráfico
                     )
    return fig

# Botao para o popover dos estados
@app.callback(Output("popover-estado", "is_open"),
            [Input('popovertarget-estado',"n_clicks")],
            [State("popover-estado", "is_open")])
def toggle_popover_estado(n, is_open):
    if n:
        return not is_open
    return is_open

# Conteudo do body para o popover do estado
@app.callback(Output('popover-body-estado', 'children'),
             [Input('state-picker', 'value')])
def update_pop_over_body_estado(selected_state):
    return df_texto_estados[df_texto_estados['Estado'] == selected_state]['Texto']


# Header para o popover do estado
@app.callback(Output('popover-header-estado', 'children'),
             [Input('state-picker', 'value')])
def update_pop_over_header_estado(selected_state):
    return str(selected_state)

# Titulo da Div para os estados
@app.callback(Output('title-states', 'children'),
             [Input('state-picker', 'value')])
def update_graficos_estado(selected_state):
    return "Focos de queimadas identificados no estado: " + str(selected_state)


# Rodando a aplicação através de um servidor
if __name__ == '__main__':
    app.run_server(debug = True, use_reloader = False)
```
