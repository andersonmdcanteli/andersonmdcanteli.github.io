---
title: "Gráfico de Pareto (exemplos)"
data: 2021-07-25
tags: []
header:
  image: "/images/chess.jpg"
  image_description: "Chess pieces"
excerpt: "gráficos de pareto"
locale: "pt-br"
---

<br>

Desenhar um **gráfico de pareto** utilizando **Python/matplotlib** é uma tarefa relativamente simples, uma vez que você já tenha os valores dos efeitos estimados para cada variável e o valor crítico da distribuição *t* de Student.
{: .text-justify}

Para fazer um exemplo, inicialmente importamos o **matplotlib** e o **NumPy**:

```python
import matplotlib.pyplot as plt
import matplotlib as mpl
import numpy as np
```

Depois entramos com os dados, sendo necessário criar 3 variáveis. A primeira (`efeitos`) deve armazenar os valores dos efeitos estimados para cada variável:
{: .text-justify}

```python
efeitos = [-4.79532, -3.01580, 7.37839, -2.90623, -0.68464]
```

Como temos efeitos positivos e negativos, é importante deixar todos com o mesmo sinal, de forma a facilitar a visualização. Para deixar todos os valores armazenados na variável `efeitos` positivos, podemos utilizar o método `np.abs()`:
{: .text-justify}

```python
efeitos = np.abs(efeitos)
```


A segunda (`t_tabelado`), deve armazenar o valor de *t* crítico (preferencialmente o valor de *t* à direita, pois ele é positivo):

```python
t_tabelado = 2.57
```

A terceira variável (`nomes_variaveis`) deve armazenar o nome de cada variável:

```python
nomes_variaveis = ['$pH$', '$pH^{2}$', '$r$', '$r^{2}$', '$pH \\times r $']
```

**Observação 1**: O nome das variáveis esta entre dois sinais de dólar (`$`) para que elas sejam renderizados como uma expressão matemática (dessa forma: "\\(pH\\)") e não como texto (dessa forma: "pH").
{: .text-justify}

**Observação 2**: A exponenciação e a multiplicação é feita com *Latex*.

**Observação 3**: O efeito da **média** não esta inserido, pois, o seu efeito é sempre significativo e o mais forte. Em geral, ao adicionar a média no gráfico de pareto, ele fica mais dificil de ler, e por isso ela geralmente não é incluida. Mas, esta é apenas uma questão estética.
{: .text-justify}

Agora podemos criar o gráfico. Começando criando o canvas, que neste caso vai ter 8 x 6 polegadas, como fundo na cor branca:
{: .text-justify}

```python
plt.figure(figsize=(8,6), facecolor='w')
```

Em seguida desenhamos o gráfico de barra horizontal, passando a variável `nomes_variaveis` como primeiro parâmetro, e os valores dos efeitos (`efeitos`) como segundo parâmetro. Para deixar a cor das barras horizontais branca, basta adicionar o parâmetro `color = 'white'`. Também vou deixar as bordas das barras na cor cinza, passando o parâmetro `edgecolor='gray'`. E vou adicionar textura as barras, passando o parâmetro `hatch='////'`.
{: .text-justify}

```python
plt.barh(nomes_variaveis, efeitos, color = 'white', edgecolor='gray', hatch='////')
```

Em seguida vou adicionar os elementos de texto no gráfico, começando pelo título do eixo x:

```python
plt.xlabel("Estimativa de efeito padronizado $ t $ de Student (abs)")
```

Depois o título do eixo y:

```python
plt.ylabel('Variáveis')
```

E o título do gráfico, mas com uma fonte maior e com um espaçamento:

```python
plt.title("Gráfico de pareto", fontsize=18, pad=15)
```

Como é um gráfico de pareto, é importante adicionar a linha que separa os fatores que foram considerados significativos dos fatores que não foram considerados significativos. Essa separação é determinada pelo valor de `t_tabelado`.
{: .text-justify}

Para adicionar esta linha, podemos utilizar o `plt.axvline()`, passando o `t_tabelado` para o parâmetro `x`, o valor de `0` para o parâmetro `ymin` e o valor de `1` para o parâmetro `ymax`. É intressante deixar esta linha na cor preta, passando o parâmetro `color = 'k'`, com uma espessura de `1`, passando o parâmetro  `lw = 1`, e com estilo tracejado, passando o parâmetro `linestyle='--'`. Também podemos adicionar um nome a esta linha através do parâmetro `label`, para que seja utilizado como nome da legenda. Como esta linha representa o valor de *t* de Student para 5% de significância, podemos identificar a linha como `$p = 0.05$`:
{: .text-justify}

```python
plt.axvline(x=t_tabelado, ymin=0, ymax=1, color='k', lw = 1, linestyle='--', label='$p = 0.05$')
```

Para efetivamente adicionar a legenda é necessário utilizar o método:

```python
plt.legend(fontsize=12)
```

Então, basta apresentar o gráfico utilizando o:

```python
plt.show()
```


*Figura 1* - Gráfico de pareto.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/grafico-pareto/pareto-01.png" alt="gráfico de pareto " >
{: .text-center}



Caso queira, é possível exportar o gráfico gerado, adicionando o método `plt.savefig()` antes de `plt.show()`:

```python
plt.savefig("pareto-01.png", bbox_inches='tight', dpi=300)  
```

O primeiro parâmetro deve ser o nome do arquivo que será exportado, incluindo a extensão desejada. Também podemos passar o parâmetro `bbox_inches='tight'`, que irá adequar o gráfico a todo o tamanho da figura. E é através do parâmetro `dpi` que definimos a quantidade de *dpi's* que a figura exportada terá.
{: .text-justify}



Uma outra adição importante ao gráfico de pareto, são os valores dos efeitos ao lado de cada barra, que facilitam a visualização dos resultados. Para adiciona-los, podemos utilizar o `plt.annotate()` inserido dentro de um loop `for`:
{: .text-justify}

```python
for i in range(len(efeitos)):
    plt.annotate(str(round(efeitos[i],2)), xy=(efeitos[i]+0.1, i-0.1))
```

É importante utilizar o loop `for` para adicionar o texto, pois o `plt.annotate()` faz uma única anotação "por vez".
{: .text-justify}

No cabeçalho do loop `for` acima, informamos que desejamos percorrer o valor da `i` de `0` até o número de elementos dentro da lista `efeitos`. No corpo do loop, entramos com o `plt.annotate()`, que recebe como primeiro parâmetro o texto que será anotado, que neste caso é o valor de cada elemento (`[i]`) contido em `efeitos`. Neste caso, o valor de `efeitos[i]` esta dentro da função `round()` para limitar o número de casas decimais para `2`. E como o `plt.annotate()` anota apenas texto, é necessário transformar o valor de um `string`.
{: .text-justify}

O segundo parâmetro (`xy`), deve recer uma `tuple` com a posição de `x` e `y` onde o texo será anotado. Como valor de `x`, utilizamos o próprio valor de `efeitos[i]`, acrescido de `0.1` apenas para dar um espaçamento entre a borda da coluna e o texto anotado. Como valor de `y`, passamos o valor de `i` menos `0.1` para centralizar o texto com a respectiva coluna. Observe que esta forma funciona pois os valores passados para o eixo `y` (`nomes_variaveis`) em `plt.barh()` são `strings`, e por este movido, eles são adicionados pela posição dentro da lista, e não pelo seu valor numérico (`strings` obviamente não são números).
{: .text-justify}

Entretanto, a anotação do maior efeito (`r`) irá ficar fora dos limites do gráfico. Para resolver este problema, basta alterar os limites do eixo x, através do método `plt.xlim()`:
{: .text-justify}

```python
plt.xlim(0.0,max(efeitos)*1.1)
```

O método `plt.xlim()` recebe como primeiro parâmetro o valor inicial de `x`, que neste caso é `0`. Como segundo parâmetro, ele recebe o valor final de `x`. Neste caso, podemos passar o maior valor da lista `efeitos` mais um pequeno ajuste (neste caso, adicionando 10% do valor máximo contido na `list` `efeitos`).
{: .text-justify}


*Figura 2* - Gráfico de pareto.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/grafico-pareto/pareto-02.png" alt="gráfico de pareto " >
{: .text-center}



**Observação**: Os gráficos acima apresentados foram desenhados com a fonte `Times New Roman` e com `fontsize=14`. Para utilizar estes parâmetros, basta adicionar a seguinte linha antes de criar o canvas:
{: .text-justify}

```python
mpl.rc('font', family='Times New Roman', size=14)
```

Você encontra o notebook com o código completo clicando [neste link](https://github.com/andersonmdcanteli/matplotlib-course/blob/main/auxiliary-scripts/pareto-chart/grafico-pareto.ipynb).

A seguir você encontra uma série outros gráficos de pareto com outros tipos de edições e outros estilos (o último é apenas para diversão).
{: .text-justify}

Para maiores informações, entre em contato pelo e-mail andersonmdcanteli@gmail.com

<hr>

<br>

<h3><a style="color:black" id="">Gráfico com grid e valor tabelado incluído no eixo x</a></h3>

*Figura 3* - Gráfico de pareto.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/grafico-pareto/pareto-03.png" alt="gráfico de pareto " >
{: .text-center}

<br>


<h3><a style="color:black" id="">Colunas na cor `silver`</a></h3>

*Figura 4* - Gráfico de pareto.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/grafico-pareto/pareto-04.png" alt="gráfico de pareto " >
{: .text-center}

<br>

<h3><a style="color:black" id="">Colunas não significativas diferenciadas por cor</a></h3>

*Figura 5* - Gráfico de pareto.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/grafico-pareto/pareto-05.png" alt="gráfico de pareto " >
{: .text-center}

<br>


<h3><a style="color:black" id="">Gráfico com fundo na cor `snow`</a></h3>

*Figura 6* - Gráfico de pareto.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/grafico-pareto/pareto-06.png" alt="gráfico de pareto " >
{: .text-center}

<br>


<h3><a style="color:black" id="">Gráfico com barras na cor `lightsteelblue` com fonte `Arial`</a></h3>

*Figura 7* - Gráfico de pareto.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/grafico-pareto/pareto-07.png" alt="gráfico de pareto " >
{: .text-center}

<br>


<h3><a style="color:black" id="">Gráfico com fundo na cor `mistyrose` e linha `vermelha`</a></h3>

*Figura 8* - Gráfico de pareto.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/grafico-pareto/pareto-08.png" alt="gráfico de pareto " >
{: .text-center}

<br>

<h3><a style="color:black" id="">Gráfico com fundo na cor `lightgray` e colunas na cor `snow`</a></h3>

*Figura 9* - Gráfico de pareto.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/grafico-pareto/pareto-09.png" alt="gráfico de pareto " >
{: .text-center}

<br>


<h3><a style="color:black" id="">Gráfico com os sinais dos efeitos negativos e positivos</a></h3>

*Figura 10* - Gráfico de pareto.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/grafico-pareto/pareto-10.png" alt="gráfico de pareto " >
{: .text-center}

<br>

<h3><a style="color:black" id="">Gráfico com os sinais dos efeitos negativos e positivos com fonte `Time New Roman`</a></h3>

*Figura 11* - Gráfico de pareto.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/grafico-pareto/pareto-11.png" alt="gráfico de pareto " >
{: .text-center}

<br>


<h3><a style="color:black" id="">Versão xkcd 😇</a></h3>

*Figura 12* - Gráfico de pareto.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/grafico-pareto/pareto-12.png" alt="gráfico de pareto " >
{: .text-center}

<br>


<h3><a style="color:black" id="">Versão xkcd 😀</a></h3>

*Figura 13* - Gráfico de pareto.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/grafico-pareto/pareto-13.png" alt="gráfico de pareto " >
{: .text-center}

<br>


<h3><a style="color:black" id="">Versão xkcd 😉</a></h3>

*Figura 14* - Gráfico de pareto.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/grafico-pareto/pareto-14.png" alt="gráfico de pareto " >
{: .text-center}

<br>
