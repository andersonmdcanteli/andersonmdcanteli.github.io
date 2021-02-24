---
title: "Dashboards com Plotly Express - Parte 2"
data: 2021-02-21
tags: [dashboard, python, plotly, dash, amazônia, plotly express, pantanal, queimadas, bioma, INPE]
header:
  image: "/images/chess.jpg"
  image_description: "Chess pieces"
excerpt: "Comparando todos as Regiões do Brasil"
locale: "pt-br"
---


Olá 😀!

Vamos para a segunda parte desse artigo barra tutorial de dashboard utilizando plotly express e Dash. Na <a href="/Dashboards-com-Plotly-Express">Parte 1</a> eu montei o layout básico e criei o Dashboard para dados do Brasil, comparando o número de focos a cada ano. Eu vou seguir utilizando os dados de focos de queimadas no Brasil, mas agora vou gerar gráficos e tabelas para os dados de focos de queimadas separados por Região brasileira.
{: .text-justify}

Para deixar o código mais limpo, eu vou adicionar apenas os elementos criados aqui para as regiões, deixando o que foi feito na <a href="/Dashboards-com-Plotly-Express">Parte 1</a> separado. Sem mais delongas, vamos lá!
{: .text-justify}


* <a href="#introducao">Introdução;</a>
* <a href="#grafico-plotly">Gráficos e tabelas com plotly express;</a>
  + <a href="#grafico-barras-regioes-estado">Gráfico de barras para comparar os estados dentro da sua região;</a>
  + <a href="#grafico-barras-regioes">Gráfico de barras para cada região;</a>
  + <a href="#tabela-barras-regioes">Tabela para comparar os dados médios da Região;</a>

* <a href="#layout">Layout;</a>
  + <a href="#elemento-titulo">Título;</a>
  + <a href="#elemento-texto-popover">Texto simples e Popover;</a>
  + <a href="#elemento-dropdown">Dropdown;</a>
  + <a href="#elemento-grafico-agrupado">Gráfico de barras agrupado;</a>
  + <a href="#elemento-grafico-tabela">Gráfico de barras e tabela;</a>
+ <a href="#script-finalizado">Script finalizado;</a>







<!-- breve introdução -->
<h2><a style="color:black" id="introducao">Introdução</a></h2>

Nesta parte vamos analisar os dados separados pelas regiões brasileiras. Para isto, vou criar dois gráficos de barras (um separado por estado dentro da região, e outro com os dados totais da região) e uma tabela que apresenta os valores totais e médios para cada estado da região e um comparativo com a média da própria região e a média do Brasil.
{: .text-justify}

A versão final ficou assim:

*Figura 1* - Estado final do Dashboard desenvolvido neste post.
{: .text-center}

<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/dashboards-plotly-express/parte-2/print-08.png" alt="Print do dashboard com os elementos criados para comparar o número de focos de queimadas nas regiões do brasil." >
{: .text-center}

Lembrando que a ideia aqui é aprender a utilizar os elementos do plotly express do Dash, e não avaliar os dados de focos de queimadas precisamente. Por exemplo, eu vou calcular a média da região e a média do Brasil todo, mas pensando na diversidade de biomas e tamanho das regiões, esta comparação absoluta talvez não seja adequada.
{: .text-justify}




<h2><a style="color:black" id="grafico-plotly">Gráficos e tabelas com plotly express</a></h2>

<!-- grafico-barras-regioes-estado -->
<h3><a style="color:black" id="grafico-barras-regioes-estado">Gráfico de barras para comparar os estados dentro da sua região</a></h3>

Desenhar um gráfico de barras agrupado utilizando o plotly express é bem simples quando temos os dados em um DataFrame. Precisamos apenas setar o parâmetro <code>barmode</code> como <code>'group'</code> e setar o parâmetro <code>color</code> como a coluna do DataFrame que irá separar os dados por cor da barra dentro do grupo.
{: .text-justify}

Mas para começar, precisamos filtrar o DataFrame <code>df</code> para que ele contenha os dados de todos os estados de apenas uma região:
{: .text-justify}


```python
regiao = 'Norte' # variável para o nome do estado que será substituído depois pelo callback do dropdown
df_regiao = df[df['Regiao']== regiao] # novo df com os dados de apenas 1 estado por vez
```

Agora que temos o DataFrame com os dados filtrados, podemos gerar o gráfico de barras. Criamos uma figura que recebe o <code>px.bar()</code>, e passamos alguns parâmetros. O primeiro é o dataframe que contém os dados (<code>df_regiao</code>). Depois, passamos através do parâmetro <code>x</code> o nome da coluna que deve ser utilizada para o eixo x. Em seguida, passamos o nome da coluna que deve ser utilizada para o eixo y, através do parâmetro <code>y</code>.
{: .text-justify}

Agora setamos que o gráfico de barras dever ser um gráfico agrupado, passando o argumento 'group' para o parâmetro <code>barmode</code>. Em seguida definimos através do parâmetro <code>color</code> qual coluna deve ser utilizada para separar dentro dos grupos (neste caso, a coluna 'UF'). E por fim podemos dar um nome para o hover, através do parâmetro <code>hover_name</code>.
{: .text-justify}

Então basta gerar o gráfico:
{: .text-justify}

*Figura 2* - Gráfico de barras agrupado para o total de focos de queimadas identificados na região Norte entre 1998 e 2020.
{: .text-center}

<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/dashboards-plotly-express/parte-2/print-01.png" alt="print do gráfico de barras agrupado interativo para o total de focos de queimadas identificados na região Norte entre 1998 e 2020." >
{: .text-center}

Você pode ver o <a href="/images/dashboards-plotly-express/parte-2/bar-plot-01.html" target="_blank">gráfico interativo clicando aqui</a>.
{: .text-justify}

```python
fig = px.bar(df_regiao, # data frame com os dados
            x = 'Ano', # coluna para os dados do eixo x
            y = 'Total', # coluna para os dados do eixo y
            barmode = 'group', # setando que o gráfico é do tipo group
            color = 'UF', # setando a coluna que irá serparar as colunas dentro do grupo
            hover_name = 'UF', # coluna para setar o titulo do hover
            )
pyo.offline.plot(fig, filename = "bar-plot-01.html")
```


Mas este gráfico pode ser melhorado, e a forma mais tranquila de edita-lo é aplicando um <code>fig.update_layout()</code>. Através deste método, é bem simples de atualizar o gráfico com algumas mudanças de estilo.
{: .text-justify}

Para editar o eixo x, podemos passar as mudanças através de um dicionário para o parâmetro <code>xaxis</code>. Eu vou adicionar uma linha preta em y = 0 (<code>linecolor='rgba(0,0,0,1)'</code>) e vou alterar os xticks para que todos os grupos apresentem o ano em baixo da barra do grupo. Para fazer isto, é preciso alterar o <code>tickmode</code> para <code>'array'</code>, setar a posição que os ticks vão aparecer (<code>tickvals = df_estado['Ano']</code>) e setar o texto que será impresso nestas posições (<code>ticktext = df_estado['Ano'])</code>)
{: .text-justify}

Para editar o eixo y, podemos passar as mudanças através de um dicionário para o parâmetro <code>yaxis</code>. Eu vou alterar o titulo do eixo, passando o parâmetro <code>title = 'Total de focos de queimadas por ano'</code>. também vou adicionar uma linha preta, mas agora em x = 0 (<code>linecolor='rgba(0,0,0,1)'</code>). Também vou remover a formatação padrão do eixo, pois eu prefiro que apareça o número inteiro (<code>tickformat=False</code>).
{: .text-justify}

Por fim, vou adicionar um título ao gráfico, passando o nome do título através do parâmetro <code>title_text</code>, e vou setar que o título deve estar centralizado, passando o parâmetro <code>title_x=0.5</code>.
{: .text-justify}

```python
fig.update_layout(xaxis = dict(linecolor='rgba(0,0,0,1)', # adicionando linha em y = 0
                                tickmode = 'array', # alterando o modo dos ticks
                                tickvals = df_regiao['Ano'], # setando a posição do tick de x
                                ticktext = df_regiao['Ano']), # setando o valor do tick de x
                 yaxis = dict(title = 'Total de focos de queimadas por ano',  # alterando o titulo do eixo y
                              linecolor='rgba(0,0,0,1)', # adicionando linha em x = 0
                              tickformat=False), # removendo a formatação no eixo y
                 title_text = 'Total de focos de queimadas identificados por ano para cada estado na região Norte', # adicionando titulo ao gráfico
                 title_x = 0.5, # reposicionando o titulo para que ele fique ono centro do gráfico
                 )
```

*Figura 3* - Gráfico de barras (editado) agrupado para o total de focos de queimadas identificados na região Norte entre 1998 e 2020.
{: .text-center}

<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/dashboards-plotly-express/parte-2/print-02.png" alt="print do gráfico de barras (editado) agrupado interativo para o total de focos de queimadas identificados na região Norte entre 1998 e 2020." >
{: .text-center}

Você pode ver o <a href="/images/dashboards-plotly-express/parte-2/bar-plot-02.html" target="_blank">gráfico interativo clicando aqui</a>.
{: .text-justify}






<!-- Gráfico de barras para a região toda -->
<h3><a style="color:black" id="grafico-barras-regioes">Gráfico de barras para cada região</a></h3>

Um outro gráfico interessante é o gráfico de barras para o total de focos para toda a região (somando os focos de todos os estados de cada região a cada ano). Para gerar este gráfico, vamos precisar filtrar os dados por Região e somar o número de total de focos de queimadas de todos os estado dessa região em cada ano. Uma vez com estas somas, basta desenhar o gráfico de barras como fizemos anteriormente, mas sem o <code>'group'</code>.
{: .text-justify}

A ideia é construir um novo DataFrame (<code>df_total</code>) que tenha três colunas:
{: .text-justify}

* A coluna 'Ano'; que contém todos os anos da série histórica;
{: .text-justify}
  Esta coluna é bem simples de obter, basta criar uma lista com os valores únicos da coluna 'Ano' do DataFrame <code>df</code>:
{: .text-justify}

```python
lista_ano = df['Ano'].unique() # lista onde cada elemento é uma ano da serie histórica
```

* A coluna 'Total de focos', que contém o somatório de todos o focos identificados na região por ano;
{: .text-justify}

Para obter esta coluna, é preciso filtrar o DataFrame <code>df_regiao</code> para cada ano, depois selecionar apenas a coluna 'Total' e então somar todos os valores.
{: .text-justify}

Para filtrar os valores para cada ano, podemos fazer da seguinte forma:
{: .text-justify}
```python
df_regiao['Ano'] == ano] # 'ano' é uma variável de iteração do loop for
```

Para selecionar apenas a coluna 'Total, basta:
{: .text-justify}
```python
df_regiao[df_regiao['Ano'] == ano]['Total'] # 'ano' é uma variável de iteração do loop for
```

E para somar todos os valores dessa coluna, basta aplicar o método <code>sum()</code> dos DataFrames:
{: .text-justify}
```python
df_regiao[df_regiao['Ano'] == ano]['Total'].sum() # 'ano' é uma variável de iteração do loop for
```

Agora é criar uma lista vazia (<code>lista_regiao</code>) e appendar o somatório de cada ano dentro dessa lista. Para isto, basta utilizar o loop for:

{: .text-justify}
```python
lista_regiao = [] # lista vazia para armazernar o nome da região e facilitar para setar o hover
for ano in lista_ano: # iterando o ano dentro da lista com os anos
    total_regiao.append(df_regiao[df_regiao['Ano'] == ano]['Total'].sum()) # filtrando o ano da lista_ano[i] contido no data frame df_regiao e somando todos os valores da coluna 'Total' do data frame auxiliar que contém apenas dados do lista_ano[i], e appendando esse valor a lista total_regiao
```

* A coluna 'Regiao', que contém o nome da região;
{: .text-justify}

Para criar esta coluna é preciso de uma lista do mesmo tamanho da lista <code>lista_ano</code>. Então, basta criar um lista vazia e utilizar o loop for acima para inserir o nome da região a cada iteração:
{: .text-justify}


```python
lista_regiao = [] # lista vazia para armazernar o nome da região e facilitar para setar o hover
for ano in lista_ano: # iterando o ano dentro da lista com os anos
    ...
    lista_regiao.append(regiao) # appendando o nome da região escolhida a cada iteração
```

Agora que temos as três listas necessárias, basta criar o novo DataFrame (<code>df_total</code>) que será utilizado para desenhar o gráfico:
{: .text-justify}

```python
# Criando um novo data frame para plotar o gráfico com os valores totais da região selecionada com o plotly express
df_total = pd.DataFrame({'Ano': lista_ano, # coluna com os anos da série
'Total de focos de queimadas por ano': total_regiao, # coluna com o total de focos na região
'Regiao': lista_regiao} # coluna com o nome da região
)    
```

O código completo ficou desta forma:
{: .text-justify}

```python
total_regiao = [] # lista vazia para armazenar o valor somado para cada região
lista_ano = df['Ano'].unique() # lista onde cada elemento é uma ano da serie historica
lista_regiao = [] # lista vazia para armazernar o nome da região e facilitar para setar o hover

for ano in lista_ano: # iterando o ano dentro da lista com os anos
    total_regiao.append(df_regiao[df_regiao['Ano'] == ano]['Total'].sum()) # filtrando o ano da lista_ano[i] contido no data frame df_regiao e somando todos os valores da coluna 'Total' do data frame auxiliar que contém apenas dados do lista_ano[i], e appendando esse valor a lista total_regiao
    lista_regiao.append(regiao) # appendando o nome da região escolhida a cada iteração
# Criando um novo data frame para plotar o gráfico com os valores totais da região selecionada com o plotly express
df_total = pd.DataFrame({'Ano': lista_ano, # coluna com os anos da série
                         'Total de focos de queimadas por ano': total_regiao, # coluna com o total de focos na região
                         'Regiao': lista_regiao} # coluna com o nome da região
                       )    
```

Como temos os dados certinhos em um DataFrame, podemos utilizar o plotly express de forma bem direta. Já vou corrigir os ticks do eixo x, no eixo y e fazer pequenas alterações no gráfico final utilizando o <code>fig.update_layout()</code>.
{: .text-justify}

```python
fig = px.bar(df_total,
            x = 'Ano', # coluna para os dados do eixo x
            y = 'Total de focos de queimadas por ano', # coluna para os dados do eixo y
            hover_name = 'Regiao'
            )
fig.update_layout(xaxis = dict(linecolor='rgba(0,0,0,1)', # adicionando linha em y = 0
                                tickmode = 'array', # alterando o modo dos ticks
                                tickvals = df_regiao['Ano'], # setando o valor do tick de x
                                ticktext = df_regiao['Ano']), # setando o valor do tick de x
                 yaxis = dict(linecolor='rgba(0,0,0,1)', # adicionando linha em x = 0
                              tickformat=False), # removendo a formatação no eixo y
                title_text = 'Total de focos de queimadas identificados na região ' + selected_regiao,  # adicionando titulo ao gráfico
                title_x = 0.5, # reposicionando o titulo para que ele fique ono centro do gráfico
                 )
pyo.offline.plot(fig, filename = "bar-plot-04.html")
```

*Figura 4* - Gráfico de barras para o total de focos de queimadas por ano na Região Norte.
{: .text-center}

<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/dashboards-plotly-express/parte-2/print-03.png" alt="print do gráfico barras para o total de focos de queimadas por ano na Região Norte." >
{: .text-center}

Você pode ver o <a href="/images/dashboards-plotly-express/parte-2/bar-plot-03.html" target="_blank">gráfico interativo
clicando aqui</a>.
{: .text-justify}







<h3><a style="color:black" id="tabela-barras-regioes">Tabela para comparar os dados médios da Região</a></h3>

Agora vamos criar a tabela para os dados da região. Eu quero que esta tabela tenha 5 colunas. A primeira coluna com o nome dos estados que compõem a região selecionada. Na segunda, eu quero o total de focos acumulados em todo o período avaliado. Na terceira, eu quero a média dos dados acumulados. Na quarta eu quero uma única linha, com a média da região. E na quinta, a média do Brasil também em uma única linha.
{: .text-justify}

Para começar, vou criar uma lista vazia (<code>lista_total_por_estado</code>) que vai receber os valores totais de focos de queimadas em cada estado. Então vou fazer um for loop para iterar através dos estados contidos no <code>df_regiao</code> e utilizar o método <code>sum()</code> para somar todos os valores da coluna 'Total' para cada estado:
{: .text-justify}

```python
# calculando o total por estado na região
lista_total_por_estado = [] # lista vazia para o total por estado

for state in df_regiao['UF'].unique():
    lista_total_por_estado.append(df_regiao[df_regiao['UF'] == state]['Total'].sum()) # somando todos os focos de queimadas para cada estado
```
Agora vou fazer exatamente a mesma coisa, mas ao invés de utilizar o método <code>sum()</code>, vou utilizar o método <code>mean()</code> para obter a média do estado:
{: .text-justify}

```python
lista_media_por_estado = [] # lista vazia para a média pode estado

for state in df_regiao['UF'].unique():
    lista_media_por_estado.append(df_regiao[df_regiao['UF'] == state]['Total'].mean()) # calculando a média de focos de queimadas para cada estado
```

Agora é a vez de calcular a média da região. Vou criar uma outra lista vazia (<code>lista_media_regiao</code>), e utilizar um for loop para adicionar a média de toda a lista <code>lista_media_por_estado</code> apenas na primeira iteração. Nas demais iterações, vou appendar uma string vazia, pois região tem apenas uma única média global.
{: .text-justify}

```python
# calculando a média da regiao e do pais
lista_media_regiao = [] # lista vazia para a média da regiao
for i in range(len(lista_total_por_estado)):
    if i == 0: # como eu quero apenas uma linha (e a primeira), vou appendar a média da região e do país apenas em i = 0
        lista_media_regiao.append(np.mean(lista_media_por_estado))

    else: # nos demais casos, eu quero um que appende uma string em branco
        lista_media_regiao.append(" ")
```

Agora vou de fazer a mesma coisa para a média do Brasil, mas vou utilizar o DataFrame <code>df['Total']</code>:
{: .text-justify}

```python
lista_media_pais = [] # lista vazia para a média do pais
for i in range(len(lista_total_por_estado)):
    if i == 0: # como eu quero apenas uma linha (e a primeira), vou appendar a média da região e do país apenas em i = 0
        lista_media_pais.append(df['Total'].mean())
    else: # nos demais casos, eu quero um que appende uma string em branco
        lista_media_pais.append(" ")
```

Agora criamos um novo DataFrame para preencher todas as colunas necessárias com as listas que criamos:
{: .text-justify}

```python
# criando o novo dataframe que será utilizado para a tabela
df_regiao_tabela = pd.DataFrame(columns=['UF']) # criando um novo data frame com uma única coluna 'UF'
```

E agora é ir criando as colunas e inserimdo a lista na coluna:
{: .text-justify}

* Preenchendo a coluna com o nomes do estado da região selecionada:
{: .text-justify}
```python
df_regiao_tabela['UF'] = df_regiao['UF'].unique() # preenchendo a coluna 'UF' com os estados da região selecionada
```

* Criando e preenchendo a coluna 'Total acumulado':
{: .text-justify}

```python
df_regiao_tabela['Total acumulado'] = lista_total_por_estado # preenchendo a coluna 'Total acumulado' com os dados somados por estado
```

* Criando e preenchendo a coluna 'Média acumulada':
{: .text-justify}

```python
df_regiao_tabela['Média acumulada'] = lista_media_por_estado # preenchendo a coluna 'Média acumulada' com a média por estado
```

* Criando e preenchendo a coluna 'Média da Região' concatenada com o nome da região selecionada:
{: .text-justify}

```python
nome_aux = 'Média da Região ' + selected_regiao # criando uma string com o nome da região selecionada que vai virar uma coluna no df_regiao_tabela
df_regiao_tabela[nome_aux] = lista_media_regiao # preenchendo a média da região
```

* Criando e preenchendo a coluna 'Média da Brasil'
{: .text-justify}

```python
df_regiao_tabela['Média Brasil'] = lista_media_pais # preenchendo a média do brasil
```

*Figura 5* - Captura de tela do output gerado para o DataFrame df_regiao_tabela.
{: .text-center}

<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/dashboards-plotly-express/parte-2/print-04.png" alt="print do output gerado para o DataFrame df_regiao_tabela." >
{: .text-center}

Agora que temos o DataFrame, basta criar a tabela em si. Criar a tabela utilizando o <code>go.Table()</code> é bem direto. Basta passar o nome das colunas para o <code>header</code>, e os valores células para o <code>cells</code>.


```python
# Criando a figura da tabela (sim, figura da tabela)
fig = go.Figure(data=[go.Table(
    header=dict(values=list(df_regiao_tabela.columns),), # dados do cabeçalho
    cells=dict(values=[df_regiao_tabela["UF"], df_regiao_tabela['Total acumulado'], # dados do corpo da tabela
                       df_regiao_tabela['Média acumulada'], df_regiao_tabela[nome_aux],
                      df_regiao_tabela['Média Brasil']],
              ))
])
pyo.offline.plot(fig, filename = "tabela-01.html") # criando o arquivo html
```

*Figura 6* - Tabela comparando as médias dos estados dentro da Região Norte.
{: .text-center}

<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/dashboards-plotly-express/parte-2/print-05.png" alt="print da tabela gerada para comparar as médias dos estados da Região Norte." >
{: .text-center}

Você pode ver a <a href="/images/dashboards-plotly-express/parte-2/tabela-01.html" target="_blank">tabela gerada clicando aqui</a>.
{: .text-justify}

Eu não vou ficar editando esta tabela pois eu vou utilizar outra forma para gerar a tabela para o dashboard (da mesma forma que fiz na parte 1), mas fica o registro de como é simples fazer com o <code>go.Table()</code>.
{: .text-justify}

















<h2><a style="color:black" id="layout">Criando o Layout do Dashboard</a></h2>

O layout para esta parte muito semelhante ao layout desenvolvido na primeira parte. A diferença é que neste temos um gráfico após a linha do dropdown, e uma linha a mais após este último gráfico, que contém um gráfico de uma tabela. Eu vou omitir a Div do Modal, do Titulo geral e da Div da primeira parte, para focar apenas nesta nova Div. Ficamos com esta estrutura:
{: .text-justify}

```python
app.layout = html.Div([ # Div geral
                    html.Div(), # Div para o Modal (otimido)
                    html.Div(),# Div para o Titulo Geral (omitido)
                    html.Div(), # Div para a primeira parte (omitido)
                    html.Div( # Div para os dados das regiões
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
                            dbc.Row(), # Grafico de barras agrupado
                            dbc.Row(# Grafico de barras acumulado + tabela                            
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











<h3><a style="color:black" id="elemento-titulo">Título</a></h3>

O título (que na verdade é um subtítulo), vai ser um elemento de <code>html.H2()</code> dentro de uma coluna, que vai ser atualizado toda vez que o usuário alterar a região selecionada. Então teremos de ter uma função para atualizar o texto apresentado.
{: .text-justify}

```python
app.layout = html.Div([ # Div geral
                    html.Div( # Div para os dados das regiões
                        [
                            dbc.Row(# Titulo
                                dbc.Col(
                                    html.H2(id = 'title-regioes') # add uma id para o titulo
                                ), style = {'textAlign': 'center', 'paddingTop': '40px', 'paddingBottom': '20px'} # centralizando o texto e adicionando um espaçamento
                            ),

                        ]
                    ),
])

```

A função do subtítulo vai receber a região selecionada no dropdown e retornar um título concatenado com o nome da região. Como Input no callback, a função recebe o valor contido no id do dropdown (ainda não foi adicionado, mas que eu vou chamar de <code>id='regiao-picker'</code>). Já como output, vamos ter o elemento do título, que tem <code>id='title-regioes'</code>.
{: .text-justify}

```python
# Titulo da Div para as regiões
@app.callback(Output('title-regioes', 'children'),
             [Input('regiao-picker', 'value')])
def update_graficos_estado(selected_regiao):
    return "Focos de queimadas identificados na regiao: " + str(selected_regiao)
```













<h3><a style="color:black" id="elemento-texto-popover">Texto simples e Popover</a></h3>

Em seguida, temos um texto simples para informar o usuário que ele pode alterar a região e, na mesma linha, o Popover. O texto é um elemento <code>html.Label()</code>, que tem um simples texto como <code>'children'</code>, o número de colunas que o elemento deve ocupar (<code>width</code>), o alinhamento (<code>align</code>) e um estilo simples (<code>style</code>).
{: .text-justify}

```python
app.layout = html.Div([ # Div geral
...
                            dbc.Row( # texto e popover
                                [
                                    dbc.Col( # texto
                                        html.Label("Escolha uma Região:"), # texto de aviso
                                        width = 3, # número de colunas para expandir
                                        align = 'left', # alinhamento
                                        style = {'display': 'inline-block'} # estilo
                                    ),
                                ]
                            ),
...
])
```

O popover tem uma estrutura mais complexa, mas é igualzinho ao que fiz na parte 1. Ele é disposto em uma <code>html.Div()</code>, que é composta de dois elementos: um elemento de botão (<code>dbc.Button()</code>) que é o botão que faz o popover abrir e fechar, e o elemento de popover em si (<code>dbc.Popover()</code>). Por sua vez, o elemento do popover é composto de outros dois elementos, o cabeçalho (<code>cdb.PopoverHeader()</code>) e o corpo (<code>dbc.PopoverBody()</code>).
{: .text-justify}

O cabeçalho será atualizado toda vez que o dropdown for alterado, então ele precisa apenas de um ID. Já o body é mais complexo, pois eu vou utilizar a mesma forma de alimentar o texto: através do <code>dcc.Markdown()</code>. O Markdown precisa de um ID, e eu também adicionei um estilo para que o texto dentro do Markdown fique justificado. E também coloquei um estilo para que o body tenha barra de rolamento, e uma altura máxima de 500 px.
{: .text-justify}

E o elemento do <code>dbc.Popover()</code> tem de ter um id, um target (que deve corresponder a ID do botão) e o parametro <code>is_open = False</code>, para que o estado inicial do popover seja fechado.
{: .text-justify}

A Div do popover eu deixei um espaço de 2 colunas, com alinhamento à esquerda. Eu adicionei um espaçamento na linha (a direta e a esquerda), bem como defini que as colunas que "sobram" devem estar entre as duas colunas da linha.
{: .text-justify}

```python
app.layout = html.Div([ # Div geral
...
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
                                                    placement='bottom-end', # definindo a posição que o popover deve abrir na tela em relação ao botão
                                                    is_open = False, # definindo que o estado inicial do popover é fechado
                                                ),
                                            ]
                                        ),
                                        width = 2, # definindo o número de colunas que o popover deve ocupar
                                        align = 'right', # alimento do popover nas colunas
                                    ),
                                ], style = {'paddingLeft': '12%', 'paddingRight': '5%'}, # dando um pequeno espaçamento ao popover
                                            justify='between'), # definindo que as colunas que sobram na linha devem ocupar o centro
...
])
```

Agora vamos criar as funções para colocar o popover em funcionamento. O cabeçalho deve receber como input o valor que esta setado no dropdown da região (que eu ainda não fiz, mas terá <code>id='regiao-picker'</code>). Esse valor, que vai ser o nome da região, deve ser concatenado a "Região " e se retornado pela função para o Output, que é o cabeçalho de <code>id='popover-header-regiao'</code>.
{: .text-justify}

```python
# Header para o popover da regiao
@app.callback(Output('popover-header-regiao', 'children'),
             [Input('regiao-picker', 'value')])
def update_pop_over_header_regiao(selected_regiao):
    return "Região " + str(selected_regiao)
```

Agora a função para o body. Essa função deve receber o valor que esta setado no dropdown da região (que eu ainda não fiz, mas terá <code>id='regiao-picker'</code>) e utilizar esse valor (que é o nome da região) para filtrar informações em um DataFrame (não falei dele ainda), e retornar o texto contido neste DataFrame para o body do popover que tem <code>id='popover-body-regiao'</code>.
{: .text-justify}

Esse DataFrame é um DataFrame montado igual ao que fizemos para o popover dos anos (para o mapa) na parte 1. Neste caso, temos duas colunas: uma com o nome da região, e a outra com um texto com informações sobre a geografia da região. Esta segunda coluna tem o texto (retirado de fontes online) que foi editado com marcação de Markdown para aplicar html ao conteúdo do body. Por exemplo, para ir para o próximo parágrafo, foram adicionados dois espaços em branco após o ponto final. Locais onde eu quis destacar um palavra em negrito, a palavra esta entre dois * (um de cada lado). Também adicionei link para a fonte das informações. E dessa forma, é possível aplicar alguns estilos diretamente do arquivo csv.
{: .text-justify}

*Figura 5* - Captura de tela do arquivo csv contendo informações sobre a geografia das regiões brasileiras.
{: .text-center}

<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/dashboards-plotly-express/parte-2/print-06.png" alt="Print do arquivo csv contendo informações sobre a geografia das regiões brasileiras." >
{: .text-center}

Você pode fazer o <a href="/assets/files/dashboards/info-regioes.csv" download="info-regioes.csv">download deste arquivo clicando aqui</a>.
{: .text-justify}

Mas para poder utilizar este arquivo aqui, é preciso importa-lo:
{: .text-justify}

```python
# importando dados para o popover das regiões
df_texto_regiao = pd.read_csv('info-regioes.csv', encoding='latin-1', sep=";")
```
Então, a função para o body do popover fica assim:
{: .text-justify}

```python
# Conteudo do body para o popover da regiao
@app.callback(Output('popover-body-regiao', 'children'),
             [Input('regiao-picker', 'value')])
def update_pop_over_body_regiao(selected_regiao):
    return df_texto_regiao[df_texto_regiao['Regiao'] == selected_regiao]['Texto']
```

Agora temos a função para o botão do popover. Essa função tem de receber como input o <code>n_clicks</code> do botão com <code>id='popovertarget-regiao'</code> e retonar como output o valor boleano de <code>is_open</code>, baseado no número de vezes que o botão foi clicado. A função basicamente fica alterando de <code>False</code> (estado original) para <code>True</code> a cada vez que o usuário clicar no botão. Esta função também precisa do parâmetro <code>State()</code> com os mesmos parâmetros do <code>Output()</code>.
{: .text-justify}


```python
# Botão do popover para os gráficos dseparados por Regiao
@app.callback(Output("popover-regiao", "is_open"),
            [Input('popovertarget-regiao',"n_clicks")],
            [State("popover-regiao", "is_open")])
def toggle_popover_regiao(n, is_open):
    if n:
        return not is_open
    return is_open
```







<h3><a style="color:black" id="elemento-dropdown">Dropdown</a></h3>


Assim, finalizamos esta linha e vamos para a próxima que é onde vai ficar o dropdown. O elemento <code>dcc.Dropdown()</code> tem de ter uma id (<code>id='regiao-picker',</code>), um valor inicial (eu escolhi a região Norte), e as opções que vão aparecer para o usuário, que são as cinco regiões do Brasil. Então é preciso criar uma lista com o nome das regiões:
{: .text-justify}

```python
# criando uma lista com os valores únicos de região para utilizar no dropdown da região
regiao_options = []
for reg in df['Regiao'].unique():
    regiao_options.append({'label':reg, 'value':reg})
```

O layout fica desta forma (com algumas adições não comentadas de estilos):
{: .text-justify}

```python
app.layout = html.Div([ # Div geral
...
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
...
])
```







<h3><a style="color:black" id="elemento-grafico-agrupado">Gráfico de barras agrupado</a></h3>

Agora podemos partir para a próxima linha, que vai conter o gráfico de barras agrupado. O layout é bem simples, basta uma linha, uma única coluna, e nesta coluna o elemento <code>dcc.Graph()</code>, com o <code>id='bar-grouped-regioes'</code>:
{: .text-justify}

```python
app.layout = html.Div([ # Div geral
...
                            dbc.Row( # linha para o gráfico de barras agrupado
                                dbc.Col(
                                    dcc.Graph(id = 'bar-grouped-regioes')
                                ),
                            ),
...
])
```

Agora vamos a função que vai retornar o elemento de figura para este gráfico. Esta função deve receber como input o valor do dropdown com <code>id='regiao-picker'</code>, utilizar a região selecionada para filtrar o DataFrame, gerar a figura com o gráfico de barras agrupado, e retornar essa figura para o elemento de gráfico com <code>id='bar-grouped-regioes'</code>. A estrutura e estilo do gráfico de barras é igual a que fizemos anteriormente neste artigo, com a atenção para o <code>title_text</code>, onde eu substitui o texto fixo de "Norte" para <code>selected_regiao</code>, de forma que o título do gráfico fique sempre condizente.
{: .text-justify}

```python
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
```

*Figura 6* - Dashboard para os dados filtrados para a região sudeste.
{: .text-center}

<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/dashboards-plotly-express/parte-2/print-07.png" alt="Print do dashboard com dados filtrados para a região sudeste, mostrando o popover aberto." >
{: .text-center}










<h3><a style="color:black" id="elemento-grafico-tabela">Gráfico de barras e tabela</a></h3>

Agora vamos para a próxima linha, que vai ter um gráfico de barras (com o somatório de todos os focos de queimadas na região) e uma tabela que compara a média dos estados, com a média da região e do país.
{: .text-justify}

O elemento <code>dcc.Graph()</code> é coloca-do dentro de um coluna que esta dentro da linha. E como parâmetro, passamos apenas uma <code>id='bar-regioes-total'</code>, pois o gráfico será criado através da função. Mas esta coluna precisa ter um <code>width</code> especificado, para que o gráfico ocupe a quantidade escolhida da tela.
{: .text-justify}

Para a tabela, temos um layout semelhante, onde precisamos alterar o elemento (agora é um <code>html.Div()</code>, que vai ter apenas uma <code>id='bar-regiao-data-table'</code>) e a quantidade de colunas que o elemento deve ocupar.
{: .text-justify}

```python
app.layout = html.Div([ # Div geral
...
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
...  
])
```

Agora vamos as funções. A função para o gráfico de barras deve receber como input o valor selecionado no dropdown com <code>id='regiao-picker'</code> e utilizar este valor para filtrar o DataFrame <code>df</code>, e utilizar o DataFrame filtrado para gerar o gráfico (como fizemos no anteriormente desta parte). O output (uma <code>fig</code>) deve ser encaminhado para o elemento gráfico com <code>id='bar-regioes-total'</code>. O script para gerar o gráfico é exatamente igual ao que fizemos, com a atenção para deixar o título do gráfico dinâmico (baseado na região selecionada).
{: .text-justify}

A função da tabela para as médias de cada estado da região selecionada deve receber como input o valor do dropdown com <code>id='regiao-picker'</code>, utilizar este valor para filtrar o DataFrame <code>df</code> e gerar o DataFrame <code>df_regiao_total</code> como fizemos anteriormente. Mas o retorno da função, que deve ter como output o elemento <code>html.Div()</code> com <code>id='bar-regiao-data-table'</code>, vai ser feito com um <code>dash_table.DataTable()</code> ao invés do <code>go.Table()</code>.
{: .text-justify}

Para utilizar o elemento <code>dash_table.DataTable()</code> eu basicamente adaptei a minha tabela ao descrito na documentação, com algumas adaptações para o estilo da tabela.
{: .text-justify}

```python
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
```

*Figura 7* - Dashboard para os focos de queimadas para comparar as regiões do Brasil.
{: .text-center}

<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/dashboards-plotly-express/parte-2/print-08.png" alt="Print do dashboard com os elementos criados para comparar o número de focos de queimadas nas regiões do brasil." >
{: .text-center}


E com isso eu finalizo esta segunda parte. Na <a href="/Dashboards-com-Plotly-Express-Parte-3">Parte 3</a> vamos montar gráficos para a análise dos dados por estado individualmente. Vejo você lá 😀!
{: .text-justify}





<h2><a style="color:black" id="script-finalizado">Script finalizado</a></h2>

O código completo ficou assim:
{: .text-justify}

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

# carregando os dados
df = pd.read_csv('historico_estados_queimadas.csv', encoding='latin-1')

# importando dados para o popover das regiões
df_texto_regiao = pd.read_csv('info-regioes.csv', encoding='latin-1', sep=";")

# criando uma lista com os valores únicos de região para utilizar no dropdown da região
regiao_options = []
for reg in df['Regiao'].unique():
    regiao_options.append({'label':reg, 'value':reg})

app = dash.Dash(external_stylesheets=[dbc.themes.BOOTSTRAP, dbc.themes.GRID]) # Criando a instancia da aplicação
app.layout = html.Div([ # Div geral
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
                                                    placement='bottom-end', # definindo a posição que o popover deve abrir na tela em relação ao botão
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


                        ]
                    ),
])

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

# Rodando a aplicação através de um servidor
if __name__ == '__main__':
    app.run_server(debug = True, use_reloader = False)
```
