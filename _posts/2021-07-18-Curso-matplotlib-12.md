---
title: "Curso matplotlib - Tipos de fontes"
data: 2021-07-18
tags: []
header:
  image: "/images/chess.jpg"
  image_description: "Chess pieces"
excerpt: "matplotlib"
locale: "pt-br"
---

<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/generico/banner.png" alt="banner provisório " >
{: .text-center}

<br>

Um ponto muito importante em um gráfico é o tipo (ou família) de fonte utilizada. Algumas revistas científicas limitam as figuras em alguns tipos de fontes para garantir uma boa leitura do gráfico. Alterar a fonte utilizada nos elementos de texto e numéricos do gráfico do **matplotlib** é bem simples.
{: .text-justify}


É possível alterar as fontes de duas formas:

- alterar a fonte padrão de todos os elementos (recomendado);

- alterar a fonte de cada elemento individualmente;

A primeira forma é a recomendada para evitar discrepâncias no gráfico. O gráfico é um elemento único, que tem uma mensagem a ser passada, e esta mensagem deve estar padronizada para não confundir o leitor. Em poucos casos será necessário alterar a fonte apenas de um ou outro elemento, e por isto esta opção ***não será abordada***.
{: .text-justify}

Para alterar a fonte padrão no **matplotlib**, podemos utilizar a classe `rc` do **matplotlib**. Através desta classe, podemos alterar qualquer configuração padrão do **matplotlib** (gerenciamento de backend). Uma lista com todas as opções pode ser acessada [neste link](https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.rc.html)
{: .text-justify}


Para alterar a fonte padrão, precisamos alterar o valor do tipo da família da fonte. Para alterar a fonte padrão (que é a **DejaVu Sans**) para a fonte **Arial** por exemplo, podemos fazer da seguinte forma:
{: .text-justify}

```python
matplotlib.rc('font', family = 'Arial')
```

O primeiro argumento `font` se refere a qual característica será alterada. Já o argumento `family` se refere ao tipo de fonte que será utilizado. Para utilizar esta ferramenta, precisamos importar a *root* do **matplotlib**:
{: .text-justify}

```python
import matplotlib as mpl
```

E então aplicar o método da seguinte forma:

```python
mpl.rc('font', family = 'Arial')
```

Em todos os gráficos que forem criados a partir de agora será utilizada a fonte <span style="font-family: Arial">Arial</span> ao invés da fonte <span style="font-family: DejaVu Sans">DejaVu Sans</span>. Por exemplo:
{: .text-justify}

*Figura 1* - Gráfico de dispersão desenhado com a fonte <span style="font-family: Arial">Arial</span>.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/12/grafico-dispersao-tipos-fonte-01.png" alt="gráfico de dispersão desenhado utilizando o **matplotlib** com a fonte alterada para Arial" >
{: .text-center}

<br>


Observe que todos os elementos de texto/numéricos agora estão na fonte <span style="font-family: Arial">Arial</span>. Um inconveniente desta forma de alterar o fonte, é que para retornar ao padrão temos de aplicar o método novamente, mas com a fonte padrão (<span style="font-family: DejaVu Sans">DejaVu Sans</span>) ou reiniciar todo o notebook.
{: .text-justify}

Para saber quais fontes temos disponíveis para utilizar, utilizamos o `mpl.font_manager.get_fontconfig_fonts()`, que retorna uma `list` com o caminho de todos os arquivos de fontes disponíveis.
{: .text-justify}

Para obter os nomes que são utilizados para alterar o tipo da fonte, podemos fazer desta forma:
{: .text-justify}

```python
flist = mpl.font_manager.get_fontconfig_fonts()
names = [mpl.font_manager.FontProperties(fname=fname).get_name() for fname in flist]
names = sorted(names)
nomes_fontes = set(names)
```

> Aviso: o passo a passo de como foi escrito o código acima não foi detalhado pois ele foge, e muito, dos objetivos desse curso.

Agora, a variável `nomes_fontes` contém todos os nomes únicos disponíveis armazenados em ordem alfabética. Para saber a quantidade de nomes disponíveis, basta utilizar a função `len()`:
{: .text-justify}

```python
len(nomes_fontes)
```

> 254

Quais fontes estarão disponíveis irá depender de uma série de fatores, como a versão do Python, a versão do **matplotlib** e sistema operacional utilizado.
{: .text-justify}

Para alterar a fonte de <span style="font-family: Arial">Arial</span> para <span style="font-family: Times New Roman">Times New Roman</span>, basta aplicar o método `mpl.rc()` novamente, mas passando o nome da nova fonte para o parâmetro `font`:
{: .text-justify}

```python
mpl.rc('font', family = 'Times New Roman')
```

Agora, todos os gráficos desenhados terão a fonte <span style="font-family: Times New Roman">Times New Roman</span> como fonte para as letras e números. Por exemplo:

```python
plt.figure(figsize=(8,6))
plt.scatter(x,y, s = 100.1, marker = "D", edgecolors = 'k', facecolors='none',
            label="Raças de cachorros")
plt.legend()
plt.xlabel("Peso (kg)")
plt.ylabel("Altura (cm)")
plt.title("Relação entre peso e altura de diversas raças de cachorro", pad=40, loc='right')
plt.show()
```

*Figura 2* - Gráfico de dispersão desenhado com a fonte <span style="font-family: Times New Roman">Times New Roman</span>.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/12/grafico-dispersao-tipos-fonte-02.png" alt="gráfico de dispersão desenhado utilizando o **matplotlib** com a fonte alterada para Times New Roman" >
{: .text-center}

<br>


<h2><a style="color:black" id="tamanho-fonte">Tamanho da fonte</a></h2>

<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/generico/banner.png" alt="banner provisório " >
{: .text-center}

Outro ponto muito importante para obter um gráfico adequado é o tamanho da fonte. As informações do gráfico devem estar claras, e ter um tamanho de fonte adequado é essencial para isto.
{: .text-justify}

Podemos alterar o tamanho da fonte diretamente em cada elemento (como fizemos para a legenda), mas é mais comum manter um tamanho padrão no gráfico todo. Então, para alterar o tamanho da fonte de todos os elementos gráficos, podemos aplicar o método `mpl.rc()`novamente, mas agora passando o parâmetro `size` com um número correspondente ao tamanho de fonte desejada.
{: .text-justify}

Por exemplo, passando `size = 30`:

```python
mpl.rc('font', size = 30)
```

A partir de agora, todos os elementos de texto/números terão o tamanho `30`. Por exemplo:

```python
plt.figure(figsize=(8,6))
plt.scatter(x,y, s = 100.1, marker = "D", edgecolors = 'k', facecolors='none',
            label="Raças de cachorros")
plt.legend()
plt.xlabel("Peso (kg)")
plt.ylabel("Altura (cm)")
plt.title("Relação entre peso e altura de diversas raças de cachorro", pad=40, loc='right')
plt.show()
```

*Figura 3* - Gráfico de dispersão desenhado com o tamanho da fonte igual a `30`.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/12/grafico-dispersao-tipos-fonte-03.png" alt="gráfico de dispersão desenhado utilizando o **matplotlib** com o tamanho de fonte alterado para 30" >
{: .text-center}

<br>

Mas o gráfico acabou ficando com o tamanho do texto muito grande. Um valor adequado geralmente gira em torno de `12`, mas isto depende da fonte utilizada e do tamanho da figura.
{: .text-justify}


```python
mpl.rc('font', size = 12)
```

Uma boa prática é aplicar o método `mpl.rc('font', family = 'string', size = number)` logo no início do notebook ou na mesma célula do gráfico, de forma que ao rodar o script, a atualização dos valores padrão é feita automaticamente.
{: .text-justify}

Contudo, em alguns casos é interessante alterar o tamanho do texto de algum elemento específico do gráfico, e não todos os elementos. Para fazer isto, podemos passar o parâmetro `prop`, que recebe um `dict` com a chave `size` e como `value` o novo tamanho do texto do elemento.
{: .text-justify}

```python
prop={"size": tamanho_desejado}
```

Por exemplo, para alterar apenas o tamanho do texto da legenda para `20`, basta passar `prop={"size": 20}` em `plt.legend()`:
{: .text-justify}

```python
plt.figure(figsize=(8,6))
plt.scatter(x,y, s = 100.1, marker = "D", edgecolors = 'k', facecolors='none',
            label="Raças de cachorros")
plt.legend(prop={"size":20})
plt.xlabel("Peso (kg)")
plt.ylabel("Altura (cm)")
plt.title("Relação entre peso e altura de diversas raças de cachorro", pad=40, loc='right')
plt.show()
```

*Figura 4* - Gráfico de dispersão desenhado com o tamanho da fonte da legenda alterado utilizando o parâmetro `prop`.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/12/grafico-dispersao-tipos-fonte-04.png" alt="gráfico de dispersão desenhado utilizando o **matplotlib** com o tamanho de fonte da legenda alterado para 20" >
{: .text-center}

<br>


Também existe a possibilidade de, ao invés de passar o parâmetro `prop = {"size": 20}`, passar diretamente o parâmetro `fontsize = 20` para o elemento de gráfico que terá o tamanho de fonte alterado.
{: .text-justify}

```python
plt.figure(figsize=(8,6))
plt.scatter(x,y, s = 100.1, marker = "D", edgecolors = 'k', facecolors='none',
            label="Raças de cachorros")
plt.legend(fontsize=20)
plt.xlabel("Peso (kg)")
plt.ylabel("Altura (cm)")
plt.title("Relação entre peso e altura de diversas raças de cachorro", pad=40, loc='right')
plt.show()
```

*Figura 5* - Gráfico de dispersão desenhado com o tamanho da fonte da legenda alterado utilizando o parâmetro `fontsize`.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/12/grafico-dispersao-tipos-fonte-05.png" alt="gráfico de dispersão desenhado utilizando o **matplotlib** com o tamanho de fonte da legenda alterado para 20" >
{: .text-center}

<br>

Observe que as Figuras 4 e 5 são idênticas, mas foram desenhadas de formas diferentes. A diferença entre estas duas formas é que o parâmetro `prop` permite a alteração de diversas outras propriedades, enquanto que o parâmetro `fontsize` permite a mudança apenas o tamanho da fonte. Por exemplo, caso queira alterar tanto a fonte como o tamanho da fonte apenas da legenda, seria necessário utilizar o parâmetro `prop` com a `key` `size` para alterar o tamanho da fonte, e a `key` `family` para alterar a fonte.
{: .text-justify}

Por exemplo, para alterar o tamanho da fonte e o tipo de fonte (para `Comic Sans MS`) apenas na legenda, seria necessário utilizar o parâmetro `prop` da seguinte maneira:
{: .text-justify}

```python
plt.figure(figsize=(8,6))
plt.scatter(x,y, s = 100.1, marker = "D", edgecolors = 'k', facecolors='none',
            label="Raças de cachorros")
plt.legend(prop={"size":20, 'family': 'Comic Sans MS'})
plt.xlabel("Peso (kg)")
plt.ylabel("Altura (cm)")
plt.title("Relação entre peso e altura de diversas raças de cachorro", pad=40, loc='right')
plt.show()
```

*Figura 6* - Gráfico de dispersão desenhado com  o tamanho da fonte e o tipo de fonte da legenda alterado utilizando o parâmetro `prop`.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/12/grafico-dispersao-tipos-fonte-06.png" alt="gráfico de dispersão desenhado utilizando o **matplotlib** com o tamanho de fonte e o tipo de fonte da legenda alterado" >
{: .text-center}

<br>


<form id = "quiz" name = "quiz">

<p><strong>Como alterar o tipo de fonte geral para Arial no matplotlib</strong></p>

<input type = "radio" id = "mc" name = "question1" value = "a"> Passando o parâmetro <code>matplotlib.Arial()</code> após criar o canvas da figura (<code>plt.figure()</code>)
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "b"> Passando o parâmetro <code>matplotlib.Arial()</code> após criar os elementos do gráfico (<code>plt.scatter()</code>)
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "c"> Setando a familia da fonte da seguinte forma: <code>mpl.rc('font', family='Arial')</code> antes de gera o gráfico
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "d"> Setando a familia da fonte da seguinte forma: <code>mpl.rc('font', family='Arial)</code> antes de gera o gráfico
<p style="font-size: 50%"></p>
<p></p>
<input id = "button" type = "button" class="btn btn--info" value = "Enviar" onclick = "check();">
</form>

<div id = "after_submit">
<p style="font-size: 120%" id = "message"></p>
</div>



<p style="text-align: center">
  <a href="/Curso-matplotlib-11" class="btn btn--success">Anterior</a>
  <a href="/Curso-matplotlib-13" class="btn btn--success">Próximo</a>
</p>


<script>
function check(){
	var question1 = document.quiz.question1.value;
	var messages = [" Incorreto! 😔 <br> Não existe o método <code>matplotlib.Arial()</code>!",
  " 😔 Incorreto! 😔  <br> Não existe o método <code>matplotlib.Arial()</code>.",
  "🎉 Correto! 🥳️ <br> Esta é uma das formas de alterar o tipo de fonte no matplotlib!",
  " 😔 Incorreto! <br> Apesar do comando estar correto, esta faltando fechar as aspas no final da linha.",
  "☕️"];
	var score;

	if (question1 == "a") {
		score = 0;
	}	else if (question1 == "b") {
		score = 1;
	} else if (question1 == "c") {
    score = 2;
  } else if (question1 == "d") {
    score = 3;    
  } else {
    score = 4;
  }

	document.getElementById("after_submit").style.visibility = "visible";
	document.getElementById("message").innerHTML = messages[score];

};

</script>
