---
title: "Dashboards com Plotly Express - Parte 4"
data: 2021-02-23
tags: [dashboard, python, plotly, plotly express, dash, amazônia, pantanal, queimadas, bioma, INPE]
header:
  image: "/images/chess.jpg"
  image_description: "Chess pieces"
excerpt: "Finalizando o Dashboard"
locale: "pt-br"
---


Olá 😀!


Agora vamos para a parte final (ufa 😅) dessa série de posts sobre o desenvolvimento de Dashboards com plotly express. Na <a href="/Dashboards-com-Plotly-Express">Parte 1</a> eu montei o layout básico e criei o Dashboard para dados do Brasil, comparando o número de focos a cada ano. Na <a href="/Dashboards-com-Plotly-Express-Parte-2">Parte 2</a> eu criei o Dashboard para dados de focos de queimadas por Região do Brasil. Na <a href="/Dashboards-com-Plotly-Express-Parte-3">Parte 3</a> eu criei gráficos para os estados individualmente. E chegou a hora de juntar tudo que foi feito em um único Dashboard.
{: .text-justify}

Como o layout de cada Dasboard desenvolvido foi feito dentro de uma <code>html.Div()</code>, basta copiar e colar cada Div na posição desejada.
{: .text-justify}

De todos as Divs criadas, falta apenas a do footer, que é apenas o meu contato e um link para a fonte dos dados, e por ser muito simples, eu não vou detalhar o passo a passo aqui.
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
```
<br>

Eu vou fazer igual ao Jack (🎃), e criar o arquivo <code>.py</code> por partes.
{: .text-justify}

* Importações das bibliotecas utilizadas

Logo no inicio do script devem acontecer a importação das bibliotecas utilizadas, como é o usual.
{: .text-justify}

```python
# importação das bibliotecas utilizadas
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
from dash_table.Format import Format, Group, Scheme, Symbol
```
<br>

* Importação dos dados

Logo em seguida, devemos importar os dados (DataFrames e dados de geo localização). É importante que a importação dos dados ocorra uma única vez, para evitar gasto de banda larga repetido (importar o mesmo arquivo várias vezes).
{: .text-justify}

Neste Dashboard, temos quatro DataFrames para importar, além dos dados de geo localização:
{: .text-justify}

```python
### Carregando os dados
## carregando os DataFrames
# carregando os dados de focos de queimadas
df = pd.read_csv('historico_estados_queimadas.csv', encoding='latin-1')
# carregando os dados de texto com um resumo sobre os focos de queimadas separado por Ano
df_texto_ano = pd.read_csv('info-anos.csv', encoding='latin-1', sep=";")
# carregando os dados de texto com um resumo sobre a geografia das Regiões brasileiras
df_texto_regiao = pd.read_csv('info-regioes.csv', encoding='latin-1', sep=";")
# carregando os dados de texto com um resumo sobre a geografia dos estados brasileiros
df_texto_estados = pd.read_csv('info-estados.csv', encoding='latin-1', sep=";")

## Carregando o arquivo de geo localização
with open('estados_brasil.geojson') as data: # carregando o arquivo ".geojson"
    limites_brasil = json.load(data)
```
<br>

* Manipulação dos dados
{: .text-justify}

Em seguida, fazemos todas as manipulações que vão acontecer apenas uma vez nos dados. Por exemplo, o ajuste do dados de geo localização; a lista com os Anos para o Dropdown referente aos anos; a lisa com as Regiões para o Dropdown referente as Regiões, etc. Talvez tenha ficado alguma coisa para trás aqui, mas a maioria esta no lugar certo.
{: .text-justify}

```python
## manipulando os dados
# criando as opções que serão apresentadas para o usuario trocar de ano no mapa do Brasil
year_options = []
for ano in df['Ano'].unique():
    year_options.append({'label':str(ano), 'value':ano})

# criando uma lista com os valores únicos de região para utilizar no dropdown da região
regiao_options = []
for reg in df['Regiao'].unique():
    regiao_options.append({'label':reg, 'value':reg})

# criando uma lista para conter as opções que o usuario terá para escolher - estados
state_options = []
for state in df['UF'].unique():
    state_options.append({'label':state, 'value':state})    

# adicionando ID ao arquivo de geo localização    
for feature in limites_brasil ['features']: # adicionado o ID aos dados
    feature['id'] = feature['properties']['name']    
```
<br>

* Criando a instância da aplicação

Agora criamos a instância de <code>app</code>, com as planilhas de estilo externas (<code>external_stylesheets</code>) já aplicadas. Vou aproveitar e alterar o nome da aplicação.
{: .text-justify}

Você talvez tenha reparado que o ícone da aplicação nos prints é diferente do ícone do Dash. Esta diferente, pois, na pasta onde o servidor está sendo gerado tem uma subpasta chamada "assets", e nesta pasta em um arquivo chamado "favicon.ico" que é o ícone de um software que eu desenvolvi (o CAVS). O Dash automaticamente procura por um arquivo com nome "favicon.ico" caso exista uma pasta "assets" no root.
{: .text-justify}

```python
# Criando a instancia da aplicação
app = dash.Dash(external_stylesheets=[dbc.themes.BOOTSTRAP, dbc.themes.GRID])
# alterando o nome da aplicação
app.title = 'Histórico de focos de queimadas no Brasil'
```
<br>

* Em seguida criamos o Layout

Agora é necessário criar o Layout da nossa aplicação. Basta alocar um Dashboard abaixo do outro, sendo que cada um esta em uma <code>Div()</code>.
{: .text-justify}

```python
# Criando o Layout da aplicação

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
                            ), style = {'textAlign': 'center', 'color': 'white'} # deixando o conteúdo da coluna centralizado
                        ), style = {'paddingTop': "20px", 'paddingBottom': "20px", 'color':'white'} # adicionado espaçamento para a linha
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
                                                    placement='top-end', # definindo a posição que o popver deve abrir na tela em relação ao botão
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

                        ], style = {'paddingBottom': "30px",'border': '4px solid DarkBlue', 'backgroundColor': 'white'}
                    ),
                    html.Div( # Div para os dados das regiões
                        [
                            dbc.Row(# Titulo
                                dbc.Col(
                                    html.H2(id = 'title-regioes') # add uma id para o titulo
                                ), style = {'textAlign': 'center', 'paddingTop': '40px', 'paddingBottom': '20px'} # centralizando o texto e adicionando um espaçamento
                            ),
                            dbc.Row( # texto e popover
                                [
                                    dbc.Col( # texto
                                        html.Label("Escolha uma Região:"), # texto de aviso
                                        width = 3, # número de colunas para expandir
                                        align = 'left', # alinhamento
                                        style = {'display': 'inline-block'} # estilo
                                    ),
                                    dbc.Col( # popover
                                        html.Div(
                                            [
                                                dbc.Button("+ info", # texto do botão do popover
                                                        outline = True, # adiciona linha em torno do botão
                                                        id = "popovertarget-regiao", # id do botão
                                                        style = {'fontFamily': 'Garamond', }, # alterando o tipo de fonte do botão
                                                        className = 'mr-2', # adicionando uma classe de botão do bootstrap
                                                        color = "success", # alterando a cor do botão
                                                        size = "sm", # tamanho do botão
                                                ),
                                                dbc.Popover( # add o popover em si
                                                    [
                                                        dbc.PopoverHeader(id='popover-header-regiao'), # adicionando o ID do cabeçalho
                                                        dbc.PopoverBody( # corpo do popover
                                                            # utilizo o markdown para ter facilidade com o html
                                                            dcc.Markdown(id='popover-body-regiao', # adicionando um id ao markdown
                                                                         style={'textAlign': 'justify',} # deixando o texto do body justificado
                                                            ), style= {'overflow': 'auto', # adicionando barra de rolagem ao body
                                                                       'max-height': '500px'} # determinando a altura maxima do body
                                                        ),
                                                    ],
                                                    id ='popover-regiao', # id do popover
                                                    target = "popovertarget-regiao", # setando o botão de target
                                                    placement='top-end', # definindo a posição que o popover deve abrir na tela em relação ao botão
                                                    is_open = False, # definindo que o estado inicial do popover é fechado
                                                ),
                                            ]
                                        ),
                                        width = 2, # definindo o número de colunas que o popover deve ocupar
                                        align = 'right', # alimento do popover nas colunas
                                    ),
                                ], style = {'paddingLeft': '12%', 'paddingRight': '5%'}, # dando um pequeno espaçamento ao popover
                                   justify='between' # definindo que as colunas que sobram na linha devem ocupar o centro
                            ),
                            dbc.Row( # linha do dropdown
                                dbc.Col(
                                    dcc.Dropdown(id = 'regiao-picker', # id do dropdown
                                                 value = 'Norte', # seta o valor inicial,
                                                 options = regiao_options, # as opções que vão aparecer no dropdown
                                                 clearable = False, # permite remover o valor (acho importante manter false para evitar problemas)
                                                 style = {'width': '50%'}
                                    ),
                                ), style = {'paddingTop': "5px", 'paddingLeft': '10%',}
                            ),
                            dbc.Row( # linha para o gráfico de barras agrupado
                                dbc.Col(
                                    dcc.Graph(id = 'bar-grouped-regioes')
                                ),
                            ),
                            dbc.Row( # linha para o grafico de barras + tabela
                                [
                                    dbc.Col( # coluna para o gráfico de barras
                                        dcc.Graph(id='bar-regioes-total'), # id do grafico de barras para a região
                                        width = 7, # numero de colunas que o gráfico de ocupar
                                        align = 'center', # alinhamento dentro das colunas de width
                                        style = {'display': 'inline-block', 'paddingLeft': '2%', 'paddingRight': '2%'} # espaçamento
                                    ),
                                    dbc.Col( # coluna para a tabela
                                        html.Div(id='bar-regiao-data-table'), # id da tabela para a região
                                        width = 5, # numero de colunas que o gráfico de ocupar
                                        align = 'center', # alinhamento dentro das colunas de width
                                        style = {'display': 'inline-block', 'paddingRight': '4%', "paddingTop": "100px"} # espaçamento
                                    ),
                                ]
                            ),
                        ], style = {'paddingBottom': "30px",'border': '4px solid DarkBlue', 'backgroundColor': 'white'}
                    ),
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
                                                    placement='top-end', # definindo a posição em que o popover vai popar
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
                        ], style = {'paddingBottom': "30px",'border': '4px solid DarkBlue', 'backgroundColor': 'white'}
                    ),
                    # footer
                    html.Div([
                        # primeira linha do footer, adicionando a referência dos dados
                        dbc.Row(
                            dbc.Col(
                                html.Label([
                                    "Fonte: ",
                                    html.A(
                                        'queimadas.dgi.inpe.br',
                                        href='http://queimadas.dgi.inpe.br/queimadas/portal-static/estatisticas_estados/'
                                    ),
                                ])
                            ),
                        ),
                        # segunda linha do footer, adicionado a data de acesso dos dados
                        dbc.Row(
                            dbc.Col(
                                html.Label("Acesso em 27/01/2021")
                            ),
                        ),
                        # terceira linha do footer, adicionando meu contato
                        dbc.Row(
                            dbc.Col(
                                html.Label("Desenvolvido por Anderson Canteli (andersonmdcanteli@gmail.com)")
                            ),
                        ),

                    ], style = {'textAlign': 'center',
                           'fontFamily' : "Roboto",
                           'paddingTop': "15px",
                           'color': 'white',
                           'backgroundColor': 'DarkBlue',
                           "paddingBottom": "20px",}
                    )


            ], style = {'paddingRight': "1.5%", 'paddingLeft': "1.5%", 'backgroundColor': 'DarkBlue'}
)
```

Eu aproveitei e fiz algumas alterações no Layout. Adicionei alguns espaçamentos entre as Divs, coloquei um fundo azul no Dashboard, fundo branco em algumas Divs e também criei um footer. Tirando o footer, que é uma composição de elementos <code>html.Label()</code>, todas as alterações foram de estilo e fica ao gosto de cliente. Particularmente, eu não sou nada bom com estilização, mas até que não ficou muito feio 😵.
{: .text-justify}

<br>

* As funções da aplicação
{: .text-justify}

Agora adicionamos todas as funções que criamos para atualizar os elementos. A ordem delas não importa, mas elas não podem ter o mesmo nome.
{: .text-justify}


```python
### Funções

## Div do Modal
# Função para fechar o modal
@app.callback(Output('modal', 'is_open'),
              [Input('close-sm', 'n_clicks')],
              [State('modal', 'is_open')])
def close_modal(n, is_open):
    if n:
        return not is_open
    return is_open

## Div do mapa

# Função para atualizar a tabela do mapa quando o usuário alterar o dropdown
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




## Div para os dados separados por Região

# Tabela para o grafico de barras da regiao
@app.callback(Output('bar-regiao-data-table', 'children'),
            [Input('regiao-picker', 'value')])
def update_table_bar_regiao(selected_regiao):

    df_regiao = df[df['Regiao']== selected_regiao]
    df_regiao['UF'].unique() # primeira coluna com o nome dos estados
    df_regiao_tabela = pd.DataFrame(columns=['UF'])
    df_regiao_tabela['UF'] = df_regiao['UF'].unique() # primeira coluna com o nome dos estados
    # calculando o total por estado na região
    lista_total_por_estado = []
    lista_media_por_estado = []

    for state in df_regiao['UF'].unique():
        lista_total_por_estado.append(df_regiao[df_regiao['UF'] == state]['Total'].sum())
        lista_media_por_estado.append(df_regiao[df_regiao['UF'] == state]['Total'].mean())

    lista_media_estado = []
    lista_media_pais = []
    for i in range(len(lista_total_por_estado)):
        if i == 0:
            lista_media_estado.append(np.mean(lista_media_por_estado))
            lista_media_pais.append(df['Total'].mean())
        else:
            lista_media_estado.append(" ")
            lista_media_pais.append(" ")
    df_regiao_tabela['Total acumulado'] = lista_total_por_estado
    df_regiao_tabela['Média acumulada'] = lista_media_por_estado
    nome_aux = 'Média da Região ' + selected_regiao
    df_regiao_tabela[nome_aux] = lista_media_estado
    df_regiao_tabela['Média Brasil'] = lista_media_pais


    return [
            dash_table.DataTable(
                columns=[{"name": i, "id": i, 'type': 'numeric', 'format': Format(scheme=Scheme.fixed,
                            precision=1,
                            group=Group.yes,
                            groups=3,
                            group_delimiter='.',
                            decimal_delimiter=',')}
                            for i in df_regiao_tabela.columns],
                data=df_regiao_tabela.to_dict('records'),
                fixed_rows={'headers': True},
                style_table={'height': '400px', 'overflowY': 'auto'},
                style_header={'textAlign': 'center', 'whiteSpace':'normal', 'minWidth': '0px', 'maxWidth': '180px'},
                style_cell={'textAlign': 'center', 'font-size': '14px', },
                style_as_list_view=True,
                style_data_conditional=[
                                        {
                                            "if": {"state": "selected"},
                                            "backgroundColor": "rgba(205, 205, 205, 0.3)",
                                            "border": "inherit !important",
                                        }
                                        ],
                                )
                ]

# Grafico de barras com a soma de todos os estados da região
@app.callback(Output('bar-regioes-total','figure'),
             [Input('regiao-picker','value')])
def update_bar_regioes_total(selected_regiao):

    #Filtrando os dados para a região
    df_regiao = df[df['Regiao']== selected_regiao]
    total_regiao = [] # lista vazia para armazenar o valor somado para cada região
    lista_ano = df['Ano'].unique() # lista onde cada elemento é uma ano da serie historica
    lista_regiao = [] # lista vazia para armazernar o nome da região e facilitar para setar o hover

    for ano in lista_ano: # iterando o ano dentro da lista com os anos
        total_regiao.append(df_regiao[df_regiao['Ano'] == ano]['Total'].sum()) # filtrando o ano da lista_ano[i] contido no data frame df_regiao e somando todos os valores da coluna 'Total' do data frame auxiliar que contém apenas dados do lista_ano[i], e appendando esse valor a lista total_regiao
        lista_regiao.append(selected_regiao) # appendando o nome da região escolhida a cada iteração
    # Criando um novo data frame para plotar o gráfico com os valores totais da região selecionada com o plotly express
    df_total = pd.DataFrame({'Ano': lista_ano, # coluna com os anos da série
                             'Total de focos de queimadas por ano': total_regiao, # coluna com o total de focos na região
                             'Regiao': lista_regiao} # coluna com o nome da região
                           )
    fig = px.bar(df_total,
            x = 'Ano', # coluna para os dados do eixo x
            y = 'Total de focos de queimadas por ano', # coluna para os dados do eixo y
            hover_name = 'Regiao',

            )
    fig.update_layout(xaxis = dict(linecolor='rgba(0,0,0,1)', # adicionando linha em y = 0
                                    tickmode = 'array', # alterando o modo dos ticks
                                    tickvals = df_regiao['Ano'], # setando o valor do tick de x
                                    ticktext = df_regiao['Ano'], # setando o valor do tick de x
                                    tickangle = -45),
                     yaxis = dict(linecolor='rgba(0,0,0,1)', # adicionando linha em x = 0
                                  tickformat=False), # removendo a formatação no eixo y
                    title_text = 'Total de focos de queimadas identificados na região ' + selected_regiao,  # adicionando titulo ao gráfico
                    title_x = 0.5, # reposicionando o titulo para que ele fique ono centro do gráfico
                    margin={"r":0,"l":0,"b":0}, # resetando o tamanho das margens
                     )

    return fig



# Gráfico de barras agrupado para as regiões
@app.callback(Output('bar-grouped-regioes','figure'),
             [Input('regiao-picker','value')])
def update_bar_regioes(selected_regiao):
    # filtrando os dados para a região selecionada
    df_regiao = df[df['Regiao']== selected_regiao]

    fig = px.bar(df_regiao, # data frame com os dados
            x = 'Ano', # coluna para os dados do eixo x
            y = 'Total', # coluna para os dados do eixo y
            barmode = 'group', # setando que o gráfico é do tipo group
            color = 'UF', # setando a coluna que irá serparar as colunas dentro do grupo
            hover_name = 'UF', # coluna para setar o titulo do hover
            hover_data = {'UF': False}, # Removendo o Mes para que não fique repetido no título do hover e no conteúdo do hover
            )
    fig.update_layout(xaxis = dict(linecolor='rgba(0,0,0,1)', # adicionando linha em y = 0
                                    tickmode = 'array', # alterando o modo dos ticks
                                    tickvals = df_regiao['Ano'], # setando o valor do tick de x
                                    ticktext = df_regiao['Ano']), # setando o valor do tick de x
                     yaxis = dict(title = 'Total de focos de queimadas por ano',  # alterando o titulo do eixo y
                                  linecolor='rgba(0,0,0,1)', # adicionando linha em x = 0
                                  tickformat=False), # removendo a formatação no eixo y
                                  title_text = 'Total de focos de queimadas identificados por ano para cada estado na região ' + selected_regiao, # adicionando titulo ao gráfico
                                  title_x = 0.5, # reposicionando o titulo para que ele fique ono centro do gráfico
                     )
    return fig

# Botão do popover para os gráficos dseparados por Regiao
@app.callback(Output("popover-regiao", "is_open"),
            [Input('popovertarget-regiao',"n_clicks")],
            [State("popover-regiao", "is_open")])
def toggle_popover_regiao(n, is_open):
    if n:
        return not is_open
    return is_open

# Conteudo do body para o popover da regiao
@app.callback(Output('popover-body-regiao', 'children'),
             [Input('regiao-picker', 'value')])
def update_pop_over_body_regiao(selected_regiao):
    return df_texto_regiao[df_texto_regiao['Regiao'] == selected_regiao]['Texto']

# Header para o popover da regiao
@app.callback(Output('popover-header-regiao', 'children'),
             [Input('regiao-picker', 'value')])
def update_pop_over_header_regiao(selected_regiao):
    return "Região " + str(selected_regiao)

# Titulo da Div para as regiões
@app.callback(Output('title-regioes', 'children'),
             [Input('regiao-picker', 'value')])
def update_graficos_estado(selected_regiao):
    return "Focos de queimadas identificados na regiao: " + str(selected_regiao)




## Div para o dados separados por estado

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
                 margin={"r":0,"l":0,"b":0}, # resetando as margens
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

```

Eu fiz algumas pequenas modificações nos gráficos. A mais importante delas foi alterar o tamanho das margens, mas novamente, é apenas mudança de estilo.
{: .text-justify}

<br>

* Gerar o servidor para rodar a aplicação

Agora falta apenas rodar a aplicação:
{: .text-justify}

```python
# Rodando a aplicação através de um servidor
if __name__ == '__main__':
    app.run_server()
```

E obtemos este dashboard:
{: .text-justify}

*Figura 1* - Dashboard finalizado.
{: .text-center}

<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/dashboards-plotly-express/parte-4/dashboard.png" alt="Captura de página do dashboard finalizado." >
{: .text-center}


<br>

* Publicando em um servidor

Agora falta apenas publicar o dashboard em um servidor. Eu peguei este Dashboard e hospedei ele no Heroku, e funcionou corretamente. Eu segui os passos indicados pelo próprio Heroku para fazer o deployment. A dificuldade que apareceu foi relacionado as versões do NumPy na hora de criar o ambiente virtual, mas uma vez que isso foi solucionado, foi bem tranquilo. O problema com o NumPy provavelmente ocorreu devido a versão do Python que utilizei (3.7) não ser compatível com a versão 1.20 do NumPy (isso é um chute, ok?!). Instalando a versão 1.16, o deployment foi tranquilo. PS: o NumPy é necessário pois ele é uma dependência do Pandas.
{: .text-justify}

Talvez você consiga acessar ele clicando em <a target="_blank" href="https://andersoncanteli.herokuapp.com/"> andersoncanteli.herokuapp.com</a>, mas eu faço atualizações neste site as vezes (utilizo como teste mesmo), então provavelmente o link estará quebrado ou te levará a um outro projeto.
{: .text-justify}

Um outro problema, que até o momento não consegui resolver é o favicon no Heroku. Por algum motivo desconhecido, a aplicação acabou ficando sem ícone atualizado.  
{: .text-justify}

De qualquer forma, o código completo (incluindo os outros arquivos necessários para o deployment, como o Procfile, requirments, etc) esta disponível abaixo e no meu <a target="_blank" href="https://github.com/andersonmdcanteli/dashboard_fires_in_brazil">git-hub</a>.
{: .text-justify}
