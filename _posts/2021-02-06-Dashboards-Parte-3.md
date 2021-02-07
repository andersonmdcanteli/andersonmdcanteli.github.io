---
title: "Dashboards com Python (Parte 3)"
data: 2021-02-06
tags: [dashboard, python, plotly, dash, matplotlib, amazônia, pantanal, queimadas, bioma, INPE]
header:
  image: "/images/chess.jpg"
  image_description: "Chess pieces"
excerpt: "Aprendendo a fazer Dashboards com Python!"
locale: "pt-br"
---

# Desenvolvendo gráficos com matplotlib, Plotly e Dash (Parte 3 de 3)!

Olá 😀!

Neste texto vou dar sequência a criação de Dashboards com Python,onde vou estudar como gerar Dashboards com Dash. Na <a href="/Dashboards-Parte-1/">Parte 1</a> preparei os dados e criei os gráficos com o matplotlib. Já na <a href="/Dashboards-Parte-2/">Parte 2</a> criei os gráficos com o Plotly.
{: .text-justify}

Você pode baixar o notebook construído até aqui <a href = "/assets/files/dashboards/queimadas-biomas-parte-2.ipynb" download="queimadas-biomas-parte-2.ipynb">neste link</a> e a planilha com os dados <a href = "/assets/files/dashboards/historico_bioma_completo.csv" download="historico_bioma_completo.csv">neste outro link</a>.
{: .text-justify}

* <a href="#dashboards-dash">Introdução;</a>
  + <a href="#dashboards-titulo">Título do Dashboard;</a>
  + <a href="#dashboards-dropdown">Dropdown;</a>
  + <a href="#dashboards-dispersao">Gráfico de dispersão com linhas;</a>
  + <a href="#dashboards-barras">Gráfico de barras;</a>
  + <a href="#dashboards-pizza">Gráfico de pizza;</a>
  + <a href="#dashboards-finais">Ajustes finais;</a>
* <a href="#conclusao">Conclusão.</a>


  <!-- Dashboards com Dash -->
<h2><a style="color:black" id="dashboards-dash">Introdução</a></h2>

Agora finalmente vamos construir o Dashboard. Dashboards são planilhas interativas que o usuário pode alterar algumas propriedades de forma bem simples, mantendo a interatividade. O que vou fazer aqui é um Dashboard para um bioma, e o usuário irá poder trocar de bioma utilizando um dropdown. O potencial aqui é muito grande, mas é necessário ter um servidor rodando Python para que ele funcione. Por isso o Dashborad será hospedado no <a href="https://www.heroku.com/" target="_blank">heroku</a> (plataforma gratuita até certo ponto) que permite rodar Python online. Mas como eu utilizo esta plataforma para testes, o dashboard não ficará disponível por muito tempo. Mas os códigos e os prints vão estar aqui, não se preocupe.
{: .text-justify}

Então **vamos lá!**

Para começar precisamos importar o Dash, juntamente com os componentes de html, os core, e as dependências
de Input e Output:
{: .text-justify}

```python
import dash
import dash_core_components as dcc
import dash_html_components as html
from dash.dependencies import Input, Output
```

O dash funciona justamente com tags de html, onde geramos uma tag no dash que vai fazer a função que a mesma tag faria no HTML. Então temos os Div, o H1, H2, ..., H6, p, etc. Dai, vamos criando uma aplicação com diversos blocos (Divs) que contém os elementos (gráficos, tabelas, texto, etc). É importante ter em mente como é a estrutura da aplicação, pois facilita ter um rumo na vida. Além das divisões com os elementos, podemos utilizar funções que ficam "ouvindo" o Dashborad o tempo todo esperando por alterações. Quando a alteração é feita pelo usuário, a função é chamada e ocorre a mudança no Dashboard. Vou utilizar esta função para trocar os dados de um bioma para o outro.
{: .text-justify}

A primeira coisa é ter um *rumo na vida*:
{: .text-justify}

*Figura 1* - Esquema inicial do Dashboard desenhado a mão.
{: .text-center}

<img src="{{ site.url }}{{ site.baseurl }}/images/dashboards/parte-3/rumo-vida.jpg" alt="A figura mostra um esquema que contém um titulo, seguido de um dropdown, um gráfico de dispersão, um gráfico de barras e um gráfico de pizza" >
{: .text-center}

A ideia inicial é ter um titulo, um dropdown (para selecionar o bioma), e três gráficos, um abaixo do outro.
{: .text-justify}

A estrutura mínima que precisamos montar um Dashboard com Dash é esta:
{: .text-justify}

* Criar uma instância da aplicação:
```python
app = dash.Dash()
```

* Criar um layout (é aqui que vai todos os blocos):
```python
app.layout = html.Div([])
```

* Rodar o servidor (é necessário ter um servidor rodando por trás):
```python
if __name__ == '__main__':
    app.run_server(debug=True, use_reloader=False) # os parâmetros são para facilitar o desenvolvimento, mas devem ser removidos nos finalmentes</code></pre>
```

<h3><a style="color:black" id="dashboards-titulo">Titulo do Dashboard</a></h3>

Para começar, vou criar apenas o titulo do Dashboard. Basta apenas adicionar um elemento H1 ao elemento
Div inicial:
{: .text-justify}

```python
app = dash.Dash() # Criando a aplicação

# Criando o layout
app.layout = html.Div([
    html.H1("Esse é o titulo do Dashboard") # adicionando um titulo
])
# Rodando a aplicação através de um servidor
if __name__ == '__main__':
    app.run_server(debug = True, use_reloader = False)
```

*Figura 2* - Dashboard com apenas o título.
{: .text-center}

<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/dashboards/parte-3/dash-board-1.png" alt="Print do dashboard gerado com apenas um titulo" >
{: .text-center}

Mas o título sozinho dessa forma não fica bom. Para melhorar eu vou expandir esse titulo para um cabeçalho, que vai ter o título e um dropdown, e acima desse dropdown eu vou colocar um aviso para o usuário alterar o Bioma.
{: .text-justify}

Vou começar apenas recolocando o titulo dentro de uma Div, e vou aproveitar e adicionar estilo para deixar o titulo centralizado, com outra fonte e com um espaçamento acima para que não fique grudado no início da página.
{: .text-justify}

```python
app = dash.Dash() # Criando a aplicação

# Criando o layout
app.layout = html.Div([
    # cabeçalho
    html.Div([
        # Titulo
        html.H1("Dados de focos de queimadas por Bioma no Brasil entre os anos de 1998 e 2020",
                style = {'textAlign': 'center', # alinhando o titulo ao centro
                         'fontFamily': 'Roboto', # alterando a fonte do H1
                         'paddingTop': 20}), # adicionando um padding no topo
    ])
])
# Rodando a aplicação através de um servidor
if __name__ == '__main__':
    app.run_server(debug = True, use_reloader = False)
```

*Figura 3* - Dashboard com apenas o título modificado.
{: .text-center}

<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/dashboards/parte-3/dash-board-2.png" alt="Print do dashboard gerado com apenas um titulo, mas modificado." >
{: .text-center}

<h3><a style="color:black" id="dashboards-dropdown">Dropdown</a></h3>

Para adicionar o dropdown basta colocar elemento de Dropdown abaixo do elemento de H1. Mas eu vou coloca-lo dentro de uma outra Div para que o estilo seja aplicado especificamente na Div onde o Dropdown está. Precisamos passar alguns parâmetros dentro do elemento de Dropdown. Dentre os diversos parâmetros posíveis, três são essenciais:
{: .text-justify}

* O parâmetro <code class="python">id</code>:
  Este vai ser utilizado para o Dashboard saber qual valor esta selecionado.
{: .text-justify}

* O parâmetro <code class="python">value</code>:
  Este parâmetro vai ser o parâmetro inicial, o que vai aparecer quando o usuário entrar no Dashboard.
{: .text-justify}

* O parâmetro <code class="python">options</code>:
  Este parâmetro  vai fornecer quais são as opções para o usuário escolher (neste caso, os diferentes biomas). Ele deve ser uma lista onde cada elemento da lista contém um dicionário com as chaves <code>'label'</code> e <code>'value'</code>. O <code>'label'</code> é o que vai aparecer para o usuário escolher e deve ser um string. Já o <code>'value'</code> é o valor que será utilizado nos códigos para acessar o DataFrame com os dados. Por enquanto vou utilizar apenas alguns valores gerais.
{: .text-justify}

Mas eu não quero que este dropdown ocupe a tela inteira, e por isso vou adicionar um estilo a Div em que o elemento do dropdown foi criado de forma que ele ocupe apenas uma parte da tela.
{: .text-justify}

```python
app = dash.Dash() # Criando a aplicação

# Criando o layout
app.layout = html.Div([
    # cabeçalho
    html.Div([
        # Titulo
        html.H1("Dados de focos de queimadas por Bioma no Brasil entre os anos de 1998 e 2020",
                style = {'textAlign': 'center', # alinhando o titulo ao centro
                         'fontFamily': 'Roboto', # alterando a fonte do H1
                         'paddingTop': 20}), # adicionando um padding no topo
        # Dropdown
        html.Div([
            dcc.Dropdown(id = 'biome-picker', # id do dropdown
                     value = 'Amazônia', # seta o valor inicial,
                     options = [{'label': 'Amazônia', 'value': 0},
                               {'label': 'Pampa', 'value': 1},
                               {'label': 'Pantanal', 'value': 2}], # as opções que vão aparecer no dropdown
                    )
        ], style = {'width': '33%',
                            'display': 'inline-block'})
    ])
])
# Rodando a aplicação através de um servidor
if __name__ == '__main__':
    app.run_server(debug = True, use_reloader = False)
```

*Figura 4* - Dashboard com título e dropdown.
{: .text-center}

<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/dashboards/parte-3/dash-board-3.png" alt="Print do dashboard gerado com título e Dropdown." >
{: .text-center}

Para concluir a parte visual do cabeçalho, falta apenas adicionar um aviso para o usuário que
ele pode alterar o bioma. Para fazer isto, vou adicionar um parágrafo antes do dropdown.
{: .text-justify}

```python
# Aviso
  html.P("Selecione um bioma:",
        style = {'fontFamily': 'Roboto'}),</code></pre>
```

<h3><a style="color:black" id="dashboards-dispersao">Gráfico de dispersão</a></h3>

Agora vou adicionar o gráfico de dispersão. Para fazer isto, vou criar uma nova Div após o parênteses da Div do cabeçalho (precisa de uma vírgula aqui). Eu vou colocar dentro dessa Div um titulo (H3) para o gráfico (não irei utilizar o titulo do próprio gráfico) e o próprio gráfico, mas vou focar apenas nesste título por enquanto.
{: .text-justify}

Eu quero que este título seja atualizado com o nome do bioma toda vez que o usuário alterar o bioma. Mas para fazer isto, eu preciso adicionar uma função que fica aguardando a mudança no dropdown, e que quando o valor no dropdown for alterado, que essa função seja chamada e altere o valor dentro deste título.
{: .text-justify}

Dentro deste elemento H3 eu vou adicionar apenas um id e um estilo:
{: .text-justify}

```python
html.Div([
    # Titulo do gráfico de dispersão
        html.H3(id='titulo-scatter',
                style={'textAlign': 'center',
                       'fontFamily' : "Roboto",
                       'paddingTop': 15
                      }
               )
])
```

Agora vou criar a função que vai ficar atualizando este H3 que tem <code>id='titulo-scatter'</code>. Vou chamar esta função de <code>update_titulo_scatter()</code>, e dentro dela eu vou passar um parâmetro qualquer (não importa o nome), que eu vou chamar de <code>selected_biome</code>. Essa função vai apenas retornar o texto que vai aparecer no Dashboard:
{: .text-justify}

```python
return "Número de focos de queimadas por mês no bioma: " + selected_state
```

Mas agora que vem o pulo do gato do Dash: o uso de *decorators*. Através de um decorator o Dash permite chamar a função <code>callback()</code> que vai fazer o papel de receber o valor atual e retornar um novo valor. A estrutura do callback é esta:
{: .text-justify}

```python
@app.callback(Output('ID do TITULO', 'o que será alterado'),
        [Input('ID DO Dropdown', 'value')])
```

Para o título do gráfico de dispersão, temos este bloco de código:
{: .text-justify}

```python
# Titulo do gráfico de dispersão
@app.callback(Output('titulo-scatter', 'children'),
             [Input('biome-picker', 'value')])
def update_titulo_scatter(selected_biome):
    return "Número de focos de queimadas por mês no bioma: " + str(selected_biome)
```

Repare que por enquanto é necessário transformar o <code>selected_biome</code> em <code>string</code>, pois o <code>children</code> recebe o valor correspondente ao <code>label</code> fornecido em <code>options</code>, e eu utilizei números (por enquanto).
{: .text-justify}

O código está assim neste momento:
{: .text-justify}

```python
app = dash.Dash() # Criando a aplicação

# Criando o layout
app.layout = html.Div([
    # cabeçalho
    html.Div([
        # Titulo
        html.H1("Dados de focos de queimadas por Bioma no Brasil entre os anos de 1998 e 2020",
                style = {'textAlign': 'center', # alinhando o titulo ao centro
                         'fontFamily': 'Roboto', # alterando a fonte do H1
                         'paddingTop': 20}), # adicionando um padding no topo
        # Aviso
        html.P("Selecione um bioma:",
              style = {'fontFamily': 'Roboto'}),
        # Dropdown
        html.Div([
            dcc.Dropdown(id = 'biome-picker', # id do dropdown
                     value = 'Amazônia', # seta o valor inicial,
                     options = [{'label': 'Amazônia', 'value': 0},
                               {'label': 'Pampa', 'value': 1},
                               {'label': 'Pantanal', 'value': 2}], # as opções que vão aparecer no dropdown
                    )
        ], style = {'width': '33%',
                            'display': 'inline-block'})
    ]),
    html.Div([
        # Titulo do gráfico de dispersão
            html.H3(id='titulo-scatter',
                    style={'textAlign': 'center',
                           'fontFamily' : "Roboto",
                           'paddingTop': 15
                          }
                   )
    ])
])



# Titulo do gráfico de dispersão
@app.callback(Output('titulo-scatter', 'children'),
             [Input('biome-picker', 'value')])
def update_titulo_scatter(selected_biome):
    return "Número de focos de queimadas por mês no bioma: " + str(selected_biome)


# Rodando a aplicação através de um servidor
if __name__ == '__main__':
    app.run_server(debug = True, use_reloader = False)
```

*Figura 5* - Dashboard com título do gráfico de dispersão responsivo.
{: .text-center}

<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/dashboards/parte-3/dash-board-4.png" alt="Print do dashboard gerado com título responsivo." >
{: .text-center}

Agora vou adicionar o gráfico de dispersão. Dentro do layout e dentro da Div do gráfico de dispersão e abaixo do H3 do título interativo, vou adicionar o elemento de gráfico que é o <code>dcc.Graph()</code>. Vou passar apenas uma id para o gráfico, e vou aproveitar e colocar um estilo na Div que contém o titulo do gráfico e o gráfico, para que o elemento todo fica centralizado e com um espaço nas margens:
{: .text-justify}

```python
# O gráfico de dispersão
dcc.Graph(id = 'scatter-plot')
 ], style = {'paddingLeft': '10%',
             'padingRight': '10%',
             'width': '80%',
             'display': 'inline-block'}),
```

E agora é preciso criar o gráfico e colocar ele dentro do elemento com <code>id='scatter-plot'</code>. Vou fazer isto utilizando a função callback. Esta função vai fazer exatamente a mesma coisa que a função <code>update_titulo_scatter()</code>, ou seja, vai receber o gráfico que está inicialmente setado, e quando houver mudança no dropdown ele vai atualizar o gráfico.
{: .text-justify}

A estrutura basica da função é esta:
{: .text-justify}

```python
# Grafico de dispersão
@app.callback(Output('scatter-plot', 'figure'),
              [Input('biome-picker', 'value')])
def update_scatter(selected_biome):

    return pass
```

O retorno da função vai ser um dicionário com os traços e o layout do gráfico, de forma muito similar ao que fizemos para gerar os gráficos no Plotly. Dentro da função precisamos apenas gerar os traços.
{: .text-justify}

Começamos filtrando os dados:
{: .text-justify}

```python
df_aux = df[df['Bioma'] == selected_biome] # data frame filtrado baseado no selected_biome
df_aux.reset_index(drop=True, inplace=True) # resetando o indice para facilitar a vida
```

*Observação*: é importante que a leitura dos dados ocorra apenas uma vez (ou o mínimo de vezes possível) ao longo da aplicação (logo quando a aplicação é iniciada). Dessa forma o tempo de execução é menor. Então no algoritmo finalizado vamos adicionar uma linha logo após a inicialização do app para ler os dados. Depois, sempre filtramos os dados para economizar tempo de execução.
{: .text-justify}

Agora criamos os traços dentro de um for loop (copie e colei do que fizemos no plotly):
{: .text-justify}

```python
tracos = [] # lista vazia para apendar os traços
for i in range(df_aux.shape[0]):
    tracos.append(go.Scatter(
                        x = df_aux.columns.values[1:13], # os dados do eixo x
                        y = df_aux.loc[i][1:13], # acessando os dados dos meses (dados do eixo y)
                        mode = 'lines+markers', # define o tipo de gráfico, neste caso vai ter linhas e marcadores
                        name = str(df_aux['Ano'][i]), # adiciono o nome do traço
                        hovertemplate = df_aux.columns.values[1:13] + ' de ' + str(df_aux['Ano'][i]) + '<br>nº de focos: '
                        + [str(i) for i in list(df_aux.loc[i][1:13])] , # alterando o template do hover
    ))
```

E agora basta retornar os traços e o layout do gráfico. A estrutura de retorno do gráfico é a seguinte:
{: .text-justify}

```python
return {
    'data': tracos,
    'layout': go.Layout('código do estilo')
    }
```

Então vou apenas copiar o estilo que fizemos para este gráfico (no Plotly) e colar em cima de <code>go.Layout()</code>.
{: .text-justify}

```python
return {
        'data': tracos,
        'layout': go.Layout(
                           showlegend=True, # garante que a legenda será mostrada
                           hovermode = "closest", # garante que o hover irá mostrar os dados do ponto mais próximo a seta do mouse
                           hoverlabel=dict(bgcolor="white", # altera a cor de fundo
                                            font_size=16, # altera o tamanho da fonte
                                            font_family="Roboto"), # altera a fonte de texto
                           xaxis = dict(title = 'Meses', linecolor='rgba(0,0,0,1)'), # Nome do eixo x / adiciona uma linha preta em y=0
                           yaxis = dict(title = 'Número de focos de queimadas', linecolor='rgba(0,0,0,1)'),
                          )
        }
```

Mas para que funcione corretamente, precisamos de uma lista contendo os dicionários de opções para o dropdown. Eu vou criar uma lista contendo os diferentes biomas. Neste caso, tanto o <code>label</code> como o <code>value</code> vão ter exatamente o mesmo valor.
{: .text-justify}

```python
biome_options = []
for biome in df['Bioma'].unique():
    biome_options.append({'label': biome, 'value': biome})
```

Agora é só substituir a lista contendo dicionários dentro do Dropdown por <code>biome_options</code>. Vou aproveitar e adicionar o parâmetro <code>clearable = False</code> para não permitir que o Dropdown fique em branco.
{: .text-justify}

O código por enquanto está assim:
{: .text-justify}

```python
df = pd.read_csv('biomas_dados_historicos.csv', encoding='latin-1') # lendo os dados

app = dash.Dash() # Criando a aplicação


# criando uma variável para armazenar os estados, para o usuario poder utilizar o dropdown e trocar de estado
biome_options = []
for biome in df['Bioma'].unique():
    biome_options.append({'label': biome, 'value': biome})

# Criando o layout
app.layout = html.Div([
    # cabeçalho
    html.Div([
        # Titulo
        html.H1("Dados de focos de queimadas por Bioma no Brasil entre os anos de 1998 e 2020",
                style = {'textAlign': 'center', # alinhando o titulo ao centro
                         'fontFamily': 'Roboto', # alterando a fonte do H1
                         'paddingTop': 20}), # adicionando um padding no topo
        # Aviso
        html.P("Selecione um bioma:",
              style = {'fontFamily': 'Roboto'}),
        # Dropdown
        html.Div([
            dcc.Dropdown(id = 'biome-picker', # id do dropdown
                     value = 'Amazônia', # seta o valor inicial,
                     options = biome_options, # as opções que vão aparecer no dropdown
                     clearable = False, # permite remover o valor (acho importante manter false para evitar problemas)
                     )
        ], style = {'width': '33%',
                            'display': 'inline-block'})
    ]),
    html.Div([
        # Titulo do gráfico de dispersão
        html.H3(id='titulo-scatter',
                style={'textAlign': 'center',
                       'fontFamily' : "Roboto",
                       'paddingTop': 15
                      }
               ),
        # O gráfico de dispersão
        dcc.Graph(id = 'scatter-plot')
         ], style = {'paddingLeft': '10%',
                     'padingRight': '10%',
                     'width': '80%',
                     'display': 'inline-block'}),

])


# Grafico de dispersão
@app.callback(Output('scatter-plot', 'figure'),
              [Input('biome-picker', 'value')])
def update_scatter(selected_biome):

    df_aux = df[df['Bioma'] == selected_biome] # data frame filtrado baseado no selected_biome
    df_aux.reset_index(drop=True, inplace=True) # resetando o indice para facilitar a vida

    tracos = [] # lista vazia para apendar os traços
    for i in range(df_aux.shape[0]):
        tracos.append(go.Scatter(
                            x = df_aux.columns.values[1:13], # os dados do eixo x
                            y = df_aux.loc[i][1:13], # acessando os dados dos meses (dados do eixo y)
                            mode = 'lines+markers', # define o tipo de gráfico, neste caso vai ter linhas e marcadores
                            name = str(df_aux['Ano'][i]), # adiciono o nome do traço
                            hovertemplate = df_aux.columns.values[1:13] + ' de ' + str(df_aux['Ano'][i]) + '<br>nº de focos: '
                            + [str(i) for i in list(df_aux.loc[i][1:13])] , # alterando o template do hover
        ))
    return {
        'data': tracos,
        'layout': go.Layout(
                           showlegend=True, # garante que a legenda será mostrada
                           hovermode = "closest", # garante que o hover irá mostrar os dados do ponto mais próximo a seta do mouse
                           hoverlabel=dict(bgcolor="white", # altera a cor de fundo
                                            font_size=16, # altera o tamanho da fonte
                                            font_family="Roboto"), # altera a fonte de texto
                           xaxis = dict(title = 'Meses', linecolor='rgba(0,0,0,1)'), # Nome do eixo x / adiciona uma linha preta em y=0
                           yaxis = dict(title = 'Número de focos de queimadas', linecolor='rgba(0,0,0,1)'),
                          )
    }

# Titulo do gráfico de dispersão
@app.callback(Output('titulo-scatter', 'children'),
             [Input('biome-picker', 'value')])
def update_titulo_scatter(selected_biome):
    return "Número de focos de queimadas por mês no bioma: " + str(selected_biome)


# Rodando a aplicação através de um servidor
if __name__ == '__main__':
    app.run_server(debug = True, use_reloader = False)
```

*Figura 6* - Dashboard com título do gráfico de dispersão responsivo finalizado.
{: .text-center}

<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/dashboards/parte-3/dash-board-5.png" alt="Print do dashboard gerado com título e gráfico de dispersão responsivos." >
{: .text-center}

Os próximos passos para os demais gráficos são exatamente os mesmos, apenas tendo de alterar o gráfico em si.
{: .text-justify}

<h3><a style="color:black" id="dashboards-barras">Gráfico de barras</a></h3>

Começamos com o layout, montando uma nova Div apenas para o gráfico de barras. Dentro dessa Div, criamos um elemento H3 para colocar o titulo do gráfico, e um elemento de gráfico para colocar o gráfico de barras. E a Div recebe um estilo para centralizar o gráfico com o mesmo tamanho de margem do gráfico de dispersão.
{: .text-justify}


```python
# Grafico de barras
    html.Div([
        # Titulo do gráfico de dispersão
        html.H3(id = 'titulo-barplot',
               style = {'textAlign': 'center',
                        'fontFamily': 'Roboto',
                        'paddingTop': 10
                       }
               ),
        # Gráfico de barras
        dcc.Graph(id = 'bar-plot')
    ], style = {'paddingLeft': '10%',
                     'padingRight': '10%',
                     'width': '80%',
                     'display': 'inline-block'}
    ),
```

E agora precisamos criar as duas funções de callback, uma para o título:
{: .text-justify}

```python
# Titulo do gráfico de barras
@app.callback(Output('titulo-barplot', 'children'),
             [Input('biome-picker', 'value')])
def update_titulo_barplot(selected_biome):
    return "Número TOTAL focos de queimadas por ano durante todo o período no bioma: " + str(selected_biome)
```

E outra para o gráfico em si. Vou utilizar o mesmo código que construí quando montei o gráfico no Plotly, mas alguns ajustes são necessários (ajustar o <code>name</code> para <code>selected_biome</code> e remover o titulo).
{: .text-justify}

```python
# Grafico de barras
@app.callback(Output('bar-plot', 'figure'),
              [Input('biome-picker', 'value')])
def update_bar_plot(selected_biome):

    df_aux = df[df['Bioma'] == selected_biome] # data frame filtrado baseado no selected_biome
    df_aux.reset_index(drop=True, inplace=True) # resetando o indice para facilitar a vida

    traco = [go.Bar(
            x = df_aux['Ano'], # os dados do eixo x
            y = df_aux['Total'], # dados do eio y
            name = selected_biome, # nome do bioma
            hovertemplate = ['Total de focos de queimadas: ' + i for i in [str(i) for i in (df_aux['Total'])]],
                )
            ]
    return {
            'data': traco,
            'layout': go.Layout(
                              xaxis = dict(title = 'Anos', linecolor='rgba(0,0,0,1)', tickmode = 'array', tickvals = df_aux['Ano'], ticktext = df_aux['Ano']), # adicionando nome eo eixo x, barra (y=0) na cor preta, e fixando o ano abaixo de todas as barras
                              yaxis = dict(title = 'Total de queimadas por ano', linecolor='rgba(0,0,0,1)', tickformat=False), # adicionando nome no eixo y, passando uma linha preta em x = 0, e removendo a formatação padrão dos ticks, para que não apareça o K
                              showlegend=True, # adicionando a legenda
                              hoverlabel=dict(bgcolor="white", # alterando a cor de fundo do hover
                                                font_size=16, # alterando o tamanho da letra no hover
                                                font_family="Roboto") # alterando a fonte do hover

                                )
                }
```

*Figura 7* - Dashboard com gráfico de dispersão e gráfico de barras.
{: .text-center}

<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/dashboards/parte-3/dash-board-6.png" alt="Print do dashboard gerado com título e gráfico de dispersão e gráfico barras responsivos." >
{: .text-center}

<h3><a style="color:black" id="dashboards-pizza">Gráfico de pizza</a></h3>


Agora falta apenas o gráfico de pizza, e os passos são exatamente os mesmos.
{: .text-justify}

Começamos com o layout, montando uma nova Div apenas para o gráfico de pizza. Dentro dessa Div, criamos um elemento H3 para colocar o titulo do gráfico, e um elemento de gráfico para colocar o gráfico de pizza. E a Div recebe um estilo para centralizar o gráfico com o mesmo tamanho de margem do gráfico de dispersão.
{: .text-justify}

```python
# Grafico de pizza
    html.Div([
        #Titulo de gráfico de rosquinha
        html.H3(id = 'titulo-pie',
               style = {'textAlign': 'center',
                        'fontFamily': 'Roboto',
                        'paddingTop': 10
                       }
               ),
        # Gráfico de rosquinha
        dcc.Graph(id = 'pie-plot')
    ], style = {'paddingLeft': '10%',
                     'padingRight': '10%',
                     'width': '80%',
                     'display': 'inline-block'}
    ),
```

E agora precisamos criar as duas funções de callback, uma para o título:
{: .text-justify}

```python
# Titulo do gráfico de rosquinha
@app.callback(Output('titulo-pie', 'children'),
             [Input('biome-picker', 'value')])
def update_titulo_pie(selected_biome):
    return "Porcentagem do TOTAL focos de queimadas por ano durante todo o período no bioma: " + str(selected_biome)
```

E outra para o gráfico em si. Vou utilizar o mesmo código que construí quando montei o gráfico no Plotly, mas é necessário  remover o titulo.
{: .text-justify}

```python
# Grafico de rosquinha
@app.callback(Output('pie-plot', 'figure'),
              [Input('biome-picker', 'value')])
def update_pie_plot(selected_biome):

    df_aux = df[df['Bioma'] == selected_biome] # data frame filtrado baseado no selected_biome
    df_aux.reset_index(drop=True, inplace=True) # resetando o indice para facilitar a vida

    traco = [go.Pie(
                labels = df_aux['Ano'], # adicionando os labels das fatias de pizza
                values = df_aux['Total'], # adicionando o tamanho das fatais de pizza
                insidetextorientation='radial', # mudando a orientação do texto dentro das fatias
                hole=.3, # transformando a pizza em uma rosquinha
                )
            ]
    return {
            'data': traco,
            'layout': go.Layout(
                    annotations=[dict(text = 'Total', # Colocando o que será inserido dentro do buraco
                                      x = .5, # posição de x do centro do buraco da rosquinha
                                      y = 0.5, # posição de y do centro do buraco da rosquinha
                                      font_size = 24, # tamanho da fonte
                                      font_family = "Roboto", # alterando a fonte do texto
                                      showarrow = False, # removendo a seta que vem por padrão inserida
                                     )],
                  )
            }
```

*Figura 8* - Dashboard com gráfico de dispersão, gráfico de barras e gráfico de pizza responsivos.
{: .text-center}

<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/dashboards/parte-3/dash-board-7.png" alt="Print do dashboard gerado com título e gráfico de dispersão, e gráfico barras e gráfico de pizza responsivos." >
{: .text-center}

<h3><a style="color:black" id="dashboards-finais">Ajustes finais</a></h3>

Para finalizar este Dashboard eu vou colocar um link no final da página que leva ao site do INPE, que é a fonte dos dados. Para isso, basta colocar outra Div depois do gráfico de rosquinha, e chamar o elemento <code>Label</code>, e colocar um trecho com o elemento <code>html.A</code>, que é a tag responsável pelo link.
{: .text-justify}

E eu vou aproveitar e colocar nesta mesma Div meu contato, mas sem links.
{: .text-justify}

```python
# Referencia
    html.Div([
        html.Label(["Fonte: ",
                html.A('queimadas.dgi.inpe.br',
                       href='http://queimadas.dgi.inpe.br/queimadas/portal-static/estatisticas_estados/'),
                        ". Acesso em 27/01/2021"
                   ]),
        html.Label([
            html.P(["Desenvolvido por Anderson Canteli (andersonmdcanteli@gmail.com)"])
        ])
            ], style={'textAlign': 'center',
                       'fontFamily' : "Roboto",
                       'paddingTop': 15
                      }
    )
```

*Figura 9* - Dashboard do número de focos de queimadas nos biomas brasileiros entre 1998 e 2020.
{: .text-center}

<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/dashboards/parte-3/dash-board-8.png" alt="Print do dashboard finalizado." >
{: .text-center}

<!-- Conclusão -->
<h2><a style="color:black" id="conclusao">Conclusão</a></h2>

Uhuull 😇!Foi uma longa jornada neste estudo para gerar Dashboards. É uma ferramenta com muito potencial, e certamente vou utiliza-la em meus projetos! A interatividade do usuário com os elementos é bem tranquila, e consigo vislumbrar alguns projetos. Só tem de verificar a parte legal do uso comercial do Dash.
{: .text-justify}

Eu peguei este Dashboard e hospedei ele no Heroku, e funcionou corretamente. Eu segui os passos indicados pelo próprio Heroku para fazer o deployment. A dificuldade que apareceu foi relacionado as versões do NumPy na hora de criar o ambiente virtual, mas uma vez que isso foi solucionado, foi bem tranquilo. O problema com o NumPy provavelmente ocorreu devido a versão do Python que utilizei (3.7) não ser compatível com a versão 1.20 do NumPy (isso é um chute, ok?!). Instalando a versão 1.16, o deployment foi tranquilo.  PS: o NumPy é necessário pois ele é uma dependência do Pandas.
{: .text-justify}

 Talvez você consiga acessar ele <a href="#">clicando aqui</a>, mas eu faço atualizações neste site as vezes (utilizo como teste mesmo), então provavelmente o link estará quebrado ou te levará a um outro projeto.
{: .text-justify}

A planilha com os dados pode ser baixada <a href = "/assets/files/dashboards/biomas_dados_historicos.csv" download="biomas_dados_historicos.csv">clicando aqui</a>.

O notebook final pode ser baixado <a href = "/assets/files/dashboards/queimadas-biomas-parte-3.ipynb" download="queimadas-biomas-parte-3.ipynb">clicando aqui</a>.

De qualquer forma, o código completo esta disponível abaixo e <a href="https://github.com/andersonmdcanteli/dashboard_fires_in_bioma">no meu git-hub</a>.
{: .text-justify}


```python
import dash
import dash_core_components as dcc
import dash_html_components as html
from dash.dependencies import Input, Output
import pandas as pd
import plotly.offline as pyo
import plotly.graph_objs as go

df = pd.read_csv('biomas_dados_historicos.csv', encoding='latin-1') # lendo os dados

app = dash.Dash() # Criando a aplicação


# criando uma variável para armazenar os estados, para o usuario poder utilizar o dropdown e trocar de estado
biome_options = []
for biome in df['Bioma'].unique():
    biome_options.append({'label': biome, 'value': biome})

# Criando o layout
app.layout = html.Div([
    # cabeçalho
    html.Div([
        # Titulo
        html.H1("Dados de focos de queimadas por Bioma no Brasil entre os anos de 1998 e 2020",
                style = {'textAlign': 'center', # alinhando o titulo ao centro
                         'fontFamily': 'Roboto', # alterando a fonte do H1
                         'paddingTop': 20}), # adicionando um padding no topo
        # Aviso
        html.P("Selecione um bioma:",
              style = {'fontFamily': 'Roboto'}),
        # Dropdown
        html.Div([
            dcc.Dropdown(id = 'biome-picker', # id do dropdown
                     value = 'Amazônia', # seta o valor inicial,
                     options = biome_options, # as opções que vão aparecer no dropdown
                     clearable = False, # permite remover o valor (acho importante manter false para evitar problemas)
                     )
        ], style = {'width': '33%',
                            'display': 'inline-block'})
    ]),
    # Grafico de dispersão
    html.Div([
        # Titulo do gráfico de dispersão
        html.H3(id='titulo-scatter',
                style={'textAlign': 'center',
                       'fontFamily' : "Roboto",
                       'paddingTop': 15
                      }
               ),
        # O gráfico de dispersão
        dcc.Graph(id = 'scatter-plot')
         ], style = {'paddingLeft': '10%',
                     'padingRight': '10%',
                     'width': '80%',
                     'display': 'inline-block'}
    ),
    # Grafico de barras
    html.Div([
        # Titulo do gráfico de dispersão
        html.H3(id = 'titulo-barplot',
               style = {'textAlign': 'center',
                        'fontFamily': 'Roboto',
                        'paddingTop': 10
                       }
               ),
        # Gráfico de barras
        dcc.Graph(id = 'bar-plot')
    ], style = {'paddingLeft': '10%',
                     'padingRight': '10%',
                     'width': '80%',
                     'display': 'inline-block'}
    ),
    # Grafico de pizza
    html.Div([
        #Titulo de gráfico de rosquinha
        html.H3(id = 'titulo-pie',
               style = {'textAlign': 'center',
                        'fontFamily': 'Roboto',
                        'paddingTop': 10
                       }
               ),
        # Gráfico de rosquinha
        dcc.Graph(id = 'pie-plot')
    ], style = {'paddingLeft': '10%',
                     'padingRight': '10%',
                     'width': '80%',
                     'display': 'inline-block'}
    ),
    # Referencia
    html.Div([
        html.Label(["Fonte: ",
                html.A('queimadas.dgi.inpe.br',
                       href='http://queimadas.dgi.inpe.br/queimadas/portal-static/estatisticas_estados/'),
                        ". Acesso em 27/01/2021"
                   ]),
        html.Label([
            html.P(["Desenvolvido por Anderson Canteli (andersonmdcanteli@gmail.com)"])
        ])
            ], style={'textAlign': 'center',
                       'fontFamily' : "Roboto",
                       'paddingTop': 15
                      }
    )


])


# Grafico de rosquinha
@app.callback(Output('pie-plot', 'figure'),
              [Input('biome-picker', 'value')])
def update_pie_plot(selected_biome):

    df_aux = df[df['Bioma'] == selected_biome] # data frame filtrado baseado no selected_biome
    df_aux.reset_index(drop=True, inplace=True) # resetando o indice para facilitar a vida

    traco = [go.Pie(
                labels = df_aux['Ano'], # adicionando os labels das fatias de pizza
                values = df_aux['Total'], # adicionando o tamanho das fatais de pizza
                insidetextorientation='radial', # mudando a orientação do texto dentro das fatias
                hole=.3, # transformando a pizza em uma rosquinha
                )
            ]
    return {
            'data': traco,
            'layout': go.Layout(
                    annotations=[dict(text = 'Total', # Colocando o que será inserido dentro do buraco
                                      x = .5, # posição de x do centro do buraco da rosquinha
                                      y = 0.5, # posição de y do centro do buraco da rosquinha
                                      font_size = 24, # tamanho da fonte
                                      font_family = "Roboto", # alterando a fonte do texto
                                      showarrow = False, # removendo a seta que vem por padrão inserida
                                     )],
                  )
            }

# Titulo do gráfico de rosquinha
@app.callback(Output('titulo-pie', 'children'),
             [Input('biome-picker', 'value')])
def update_titulo_pie(selected_biome):
    return "Porcentagem do TOTAL de focos de queimadas por ano durante todo o período no bioma: " + str(selected_biome)



# Grafico de barras
@app.callback(Output('bar-plot', 'figure'),
              [Input('biome-picker', 'value')])
def update_bar_plot(selected_biome):

    df_aux = df[df['Bioma'] == selected_biome] # data frame filtrado baseado no selected_biome
    df_aux.reset_index(drop=True, inplace=True) # resetando o indice para facilitar a vida

    traco = [go.Bar(
            x = df_aux['Ano'], # os dados do eixo x
            y = df_aux['Total'], # dados do eio y
            name = selected_biome, # nome do bioma
            hovertemplate = ['Total de focos de queimadas: ' + i for i in [str(i) for i in (df_aux['Total'])]],
                )
            ]
    return {
            'data': traco,
            'layout': go.Layout(
                              xaxis = dict(title = 'Anos', linecolor='rgba(0,0,0,1)', tickmode = 'array', tickvals = df_aux['Ano'], ticktext = df_aux['Ano']), # adicionando nome eo eixo x, barra (y=0) na cor preta, e fixando o ano abaixo de todas as barras
                              yaxis = dict(title = 'Total de queimadas por ano', linecolor='rgba(0,0,0,1)', tickformat=False), # adicionando nome no eixo y, passando uma linha preta em x = 0, e removendo a formatação padrão dos ticks, para que não apareça o K
                              showlegend=True, # adicionando a legenda
                              hoverlabel=dict(bgcolor="white", # alterando a cor de fundo do hover
                                                font_size=16, # alterando o tamanho da letra no hover
                                                font_family="Roboto") # alterando a fonte do hover

                                )
                }


# Titulo do gráfico de barras
@app.callback(Output('titulo-barplot', 'children'),
             [Input('biome-picker', 'value')])
def update_titulo_barplot(selected_biome):
    return "Número TOTAL focos de queimadas por ano durante todo o período no bioma: " + str(selected_biome)


# Grafico de dispersão
@app.callback(Output('scatter-plot', 'figure'),
              [Input('biome-picker', 'value')])
def update_scatter(selected_biome):

    df_aux = df[df['Bioma'] == selected_biome] # data frame filtrado baseado no selected_biome
    df_aux.reset_index(drop=True, inplace=True) # resetando o indice para facilitar a vida

    tracos = [] # lista vazia para apendar os traços
    for i in range(df_aux.shape[0]):
        tracos.append(go.Scatter(
                            x = df_aux.columns.values[1:13], # os dados do eixo x
                            y = df_aux.loc[i][1:13], # acessando os dados dos meses (dados do eixo y)
                            mode = 'lines+markers', # define o tipo de gráfico, neste caso vai ter linhas e marcadores
                            name = str(df_aux['Ano'][i]), # adiciono o nome do traço
                            hovertemplate = df_aux.columns.values[1:13] + ' de ' + str(df_aux['Ano'][i]) + '<br>nº de focos: '
                            + [str(i) for i in list(df_aux.loc[i][1:13])] , # alterando o template do hover
        ))
    return {
        'data': tracos,
        'layout': go.Layout(
                           showlegend=True, # garante que a legenda será mostrada
                           hovermode = "closest", # garante que o hover irá mostrar os dados do ponto mais próximo a seta do mouse
                           hoverlabel=dict(bgcolor="white", # altera a cor de fundo
                                            font_size=16, # altera o tamanho da fonte
                                            font_family="Roboto"), # altera a fonte de texto
                           xaxis = dict(title = 'Meses', linecolor='rgba(0,0,0,1)'), # Nome do eixo x / adiciona uma linha preta em y=0
                           yaxis = dict(title = 'Número de focos de queimadas', linecolor='rgba(0,0,0,1)'),
                          )
    }

# Titulo do gráfico de dispersão
@app.callback(Output('titulo-scatter', 'children'),
             [Input('biome-picker', 'value')])
def update_titulo_scatter(selected_biome):
    return "Número de focos de queimadas por mês no bioma: " + str(selected_biome)


# Rodando a aplicação através de um servidor
if __name__ == '__main__':
    app.run_server(debug = True, use_reloader = False)
```
