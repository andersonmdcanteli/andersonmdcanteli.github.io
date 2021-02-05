---
title: "Teste de Shapiro-Wilk"
data: 2021-02-04
tags: [shapiro, wilk, shapiro wilk, gauss, gaussiana, normal, normalidade, distribuição normal]
header:
  image: "/images/chess.jpg"
  image_description: "Chess pieces"
excerpt: "Como aplicar o teste de Shapiro-Wilk!"
locale: "pt-br"
---

Olá 😀! Neste texto, você irá aprender sobre o teste de Shapiro-Wilk, um teste muito utilizado (talvez o mais utilizado) para verificar se um conjunto de dados segue ou não a distribuição Normal.
{: .text-justify}
Serão abordados os seguintes tópicos:

* <a style="scroll-margin-top: 100px;" href="#introdução">Introdução (vantagens/desvantagens e características do teste);</a>
* <a href="#descricao">Descrição do teste;</a>
* <a href="#exemplonumerico">Exemplo numérico;</a>
* <a href="#comentarios">Comentários;</a>
* <a href="#tutorialexcel">Exemplo no Excel;</a>
* <a href="#tutorialpython">Exemplo no Python;</a>
* <a style="scroll-margin-top: 200px;" href="#referencias">Referências.</a>



<h2><a style="color:black" id="introdução">Introdução</a></h2>

O teste de <a href="#shapiro-wilk">Shapiro & Wilk (1965)</a> é possivelmente o teste mais utilizado para verificar se um determinado conjunto de dados independentes segue a distribuição Normal. Este teste tem um maior poder de decisão do que outros testes <a href="#nist-sematech">(NIST/SEMATECH, 2013)</a>, como o teste de Kolmogorov-Sminorv <a href="#rodrigues-iemma">(Rodrigues & Iemma, 2009)</a> por exemplo.
{: .text-justify}

As principais vantagens e desvantagens do teste são:

**Vantagens:**

* É específico para a distribuição Normal;
* Alto poder de decisão;

**Desvantagens:**

* Limitado a amostras com tamanho entre 3 e 50 observações;
* Sensível a valores iguais ou muito próximos;
* Dificilmente rejeita a hipótese nula de Normalidade dos para amostras pequenas;
* Tende a rejeitar a hipótese nula de Normalidade quando os dados apresentam pequenas discrepâncias quanto a normalidade dos dados em amostras muito grandes.


A hipótese nula do teste é que os dados seguem, pelo menos aproximadamente, a distribuição Normal. Já a hipótese alternativa, é de que os dados não seguem a distribuição Normal. Formalmente, temos o seguinte:
{: .text-justify}

<p style="text-align: center">\(H_{0}\): Os dados seguem uma distribuição <em>Normal</em>.</p>
<p style="text-align: center">\(H_{1}\): Os dados não seguem uma distribuição <em>Normal</em>.</p>

*Observação:*

Utilizamos o termo “uma” distribuição Normal, pois temos infinitas distribuições Normais, uma para cada par de média e desvio padrão.

Para testar a hipótese do teste precisamos estimar a estatística do teste de Shapiro-Wilk (\\(D_{S-W}\\)), e compara-la com o valor tabelado (\\(D_{S-W}^{critico}\\)) para um determinado nível de confiança. Os valores tabelados foram originalmente descritos no livro “Biometrica Tables for Statisticians, Vol 2” <a href="#pearson-hartley">(Pearson & Hartley, 1972)</a>, embora eu não tenha tido acesso ao original para confirmar a informação. Os valores tabelados para amostras com até 10 observações (99, 95 e 90% de confiança) estão listados na Tabela 1. Você encontra a tabela  completa no <a href="#portal-action">Portal Action</a> ou pode baixar ela no formato .xlsx <a href = "/assets/files/shapiro-wilk/valores_criticos.xlsx" download="valores_criticos.xlsx">clicando aqui</a>.
{: .text-justify}


**Tabela 1** – Valores críticos para o teste de Shapiro-Wilk.
{: .text-center}

| N | 90% |	95% |	99% |
| :---: | :---: |	:---: |	:---: |
| 3 | 0,753 |	0,767 |	0,789 |
| 4 | 0,687	 |	0,748 |	0,792 |
| 5 | 0,686 |	0,762 |	0,806 |
| 6 | 0,713 |	0,788 |	0,826 |
| 7 | 0,730 |	0,803 |	0,838 |
| 8 | 0,749 |	0,818 |	0,851 |
| 9 | 0,764 |	0,829 |	0,859 |
| 10 | 0,781 |	0,842 |	0,869 |



Se o valor da estatística de Shapiro-Wilk for **menor do que o valor tabelado**, *temos evidências* para rejeitar a hipótese nula de Normalidade dos dados. **Caso contrário**, *não temos evidências* para rejeitar a hipótese de Normalidade dos dados.
{: .text-justify}

Também podemos testar a hipótese do teste calculando o valor de p-valor para a estática obtida e comparar com um nível de significância estabelecido previamente (α (%)). Neste caso, é necessário o uso de um software que estime o p-valor, pois os cálculos são demasiadamente longos.
{: .text-justify}

A conclusão do teste baseado no p-valor é feita da seguinte forma:
{: .text-justify}

Se o **p-valor for maior do que α**, *temos evidências* para rejeitar a hipótese de Normalidade dos dados. **Caso contrário**, *não temos evidências* para rejeitar a hipótese de Normalidade dos dados.
{: .text-justify}

<h2><a style="color:black" id="descricao">Descrição do Teste </a></h2>

O procedimento para calcular a estatística de Shapiro-Wilk é um pouco longo e depende de alguns passos que parecem complicados à primeira vista, mas nada impossível de ser feito. O passo a passo detalhado a seguir foi adaptado do <a href="#portal-action">Portal Action</a>, que é uma fonte muito boa de informações (sério, abra o link e dê uma conferida!).
{: .text-justify}

A estatística do teste de Shapiro-Wilk é obtida através da seguinte forma:
{: .text-justify}

\\(D_{S-W} = \frac{b^{2}}{\sum_{i=1}^n(x_{i}-\bar{x})^2 }\\) &emsp; &emsp; &emsp; (1)
{: .text-center}

onde \\(x_{i}\\) é o valor de cada medida independente que foi obtida, \\(\bar{x}\\) é a média de todas as medidas obtidas, e \\(b\\) é um parâmetro que deve ser calculado e que depende de um outro parâmetro \\(a\\) e também da quantidade de observações (\\(n\\)) que temos de \\(x_{i}\\).
{: .text-justify}

Caso \\(n\\) seja **par**, o valor de \\(b\\) é obtido da seguinte forma:

\\(b = \sum_{i=1}^{n/2}a_{n-1+1}(x_{n-i+1}-x_{i})\\) &emsp; &emsp; &emsp; (2)
{: .text-center}
E caso seja \\(n\\) **ímpar**, \\(b\\) é obtido desta outra forma:

\\(b = \sum_{i=1}^{(n+1)/2}a_{n-1+1}(x_{n-i+1}-x_{i})\\) &emsp; &emsp; &emsp; (3)
{: .text-center}

Observe que a diferença entre as equações 2 e 3 está apenas no limite superior do somatório.
{: .text-justify}

O valor de \\(a\\) é um valor tabelado e que necessita que os valores de \\(x\\) estejam ordenados de forma crescente, pois ele depende da posição de cada medida devido a ordem das operações que devem ser feitas. As tabelas de \\(a\\) geralmente são apresentadas como na Tabela 2, onde as colunas representam o número de observações e as linhas representam a posição ordenada das observações. Os valores tabelados foram originalmente descritos no livro “Biometrica Tables for Statisticians, Vol 2” <a href="pearson-hartley">(Pearson & Hartley, 1972)</a>, embora eu não tenha tido acesso ao original para confirmar a informação.
{: .text-justify}


**Tabela 2** – Valores de \\(a\) para um grupo com até 13 observações.
{: .text-center}

| i\N | 2 |	3 |	4 |	5 |	6 |	7 |	8 |	9 |	10 |	11 |	12 |	13 |
| :---: | :---: |	:---: |	:---: |	:---: |	:---: |	:---: |	:---: |	:---: |	:---: |	:---: |	:---: |	:---: |
| 1 | 0,7071 |	0,7071 |	0,6872 |	0,6646 |	0,6431 |	0,6233 |	0,6062 |	0,5888 |	0,5739 |	0,5601 |	0,5475 |	0,5359 |
| 2 | - |	- |	0,1677 |	0,2413 |	0,2806 |	0,3031 |	0,3164 |	0,3244 |	0,3291 |	0,3315 |	0,3325 |	0,3325 |
| 3 | - |	- |	- |	- |	0,0875 |	0,1401 |	0,1743 |	0,1976 |	0,2141 |	0,2260 |	0,2347 |	0,2412 |
| 4 | - |	- |	- |	- |	- |	- |	0,0561 |	0,0947 |	0,1224 |	0,1429 |	0,1586 |	0,1707 |
| 5 | - |	- |	- |	- |	- |	- |	- |	- |	0,0399 |	0,0695 |	0,0922 |	0,1099 |
| 6 | - |	- |	- |	- |	- |	- |	- |	- |	- |	- |	0,0303 |	0,0539 |


Você pode baixar a tabela completa (arquivo ".xlsx") com os valores de \\(a\\) <a href = "/assets/files/shapiro-wilk/valores_a.xlsx" download="valores_a.xlsx">clicando aqui</a>.
{: .text-justify}

<h2><a style="color:black" id="exemplonumerico">Exemplo numérico</a></h2>

Agora vamos a um exemplo numérico. Para isso, eu dividi as etapas em 6 passos, para simplificar o entendimento.
{: .text-justify}

Dado o conjunto de dados abaixo, vamos verificar se ele segue, pelo menos aproximadamente, a distribuição Normal utilizando o teste de Shapiro-Wilk e adotando α=5%.
{: .text-justify}

**Tabela 3** – Conjunto de dados não ordenados.
{: .text-center}

| nº da observação | Comprimento (cm) |
| :---: | :---: |
| 1 | 1,69742 |
| 2 | 1,99568 |
| 3 | 1,90642 |
| 4 | 2,61826 |
| 5 | 3,15435 |
| 6 | 1,98492 |
| 7 | 1,52229 |
| 8 | 1,42738 |
| 9 | 2,10288 |
| 10 | 2,22488 |

1) Ordenar os dados de forma crescente. Sim, apenas ordene de menor para o maior.

**Tabela 4** – Conjunto de dados ordenados.
{: .text-center}    

| nº da observação | Comprimento (cm) |
| :---: | :---: |
| 1 | 1,42738 |
| 2 | 1,52229 |
| 3 | 1,69742 |
| 4 | 1,90642 |
| 5 | 1,98492 |
| 6 | 1,99568 |
| 7 | 2,10288 |
| 8 | 2,22488 |
| 9 | 2,61826 |
| 10 | 3,15435 |


2) Calcular o valor de \\(b\\).

O valor de \\(b\\) depende do número de observações realizadas. Como neste caso temos 10 observações (número par), \\(b\\) é calculado utilizando a Equação 2. Observe que o intervalo de \\(b\\) é entre 1 e \\(n/2\\), ou seja, entre 1 e 5. Vamos fazer um por um, para depois somar todos os termos:
{: .text-justify}

- Primeiro termo do somatório:

Começamos pelo valor de \\(a\\). Neste caso precisamos do \\(a_{n-1+1} = a_{10-1+1} = a_{10}\\). Então basta observar o valor de \\(a\\) na coluna 10 (Tabela 2) para o **primeiro termo**, que neste caso é \\(0,5739\\).
{: .text-justify}

Agora vamos calcular o termo das diferenças: \\((x_{n-i+1}-x_{i})\\). O termo \\(x_{n-i+1}\\) é o termo \\(x_{10-1+1} = x_{10} = 3,14532\\). E o termo \\(x_{i} = x_{1} = 1,42738\\).
{: .text-justify}

Portanto, \\((x_{n-i+1}-x_{i}) = (3,14532-1,42738)=1,72697\\)

Dessa forma, o primeiro termo do somatório de \\(b\\) é:

\\(a_{10}(x_{10}-x_{1}) = 0,5739(1,72697) = 0,991108\\)
{: .text-center}

- Segundo termo do somatório:

Agora temos \\(a_{n-1+1} = a_{10-1+1} = a_{10}\\). Então basta apenas observar o valor de \\(a\\) na coluna 10 (Tabela 2) para o **segundo termo**, que neste caso é \\(0,3291\\).
{: .text-justify}

Agora vamos calcular o termo das diferenças: \\((x_{n-i+1}-x_{i})\\). O termo \\(x_{n-i+1}\\) é o termo \\(x_{10-2+1} = x_{9} = 2,61826\\). E o termo \\(x_{i} = x_{2} = 1,52229\\).
{: .text-justify}

Portanto, \\((x_{n-i+1}-x_{i}) = (2,61826-1,52229)=1,09597\\).

Dessa forma, o segundo termo do somatório de \\(b\\) é:

\\(a_{10}(x_{9}-x_{2}) = 0,3291(1,09597) = 0,360684\\)
{: .text-center}


- Terceiro termo do somatório:

Agora temos \\(a_{n-1+1} = a_{10-1+1} = a_{10}\\). Então basta apenas observar o valor de \\(a\\) na coluna 10 (Tabela 2) para o **terceiro termo**, que neste caso é \\(0,2141\\).
{: .text-justify}

Agora vamos calcular o termo das diferenças: \\((x_{n-i+1}-x_{i})\\). O termo \\(x_{n-i+1}\\) é o termo \\(x_{10-3+1} = x_{8} = 2,22488\\). E o termo \\(x_{i} = x_{3} = 1,69742\\).
{: .text-justify}

Portanto, \\((x_{n-i+1}-x_{i}) = (2,22488-1,69742) = 0,52746\\).

Dessa forma, o terceiro termo do somatório de \\(b\\) é:

\\(a_{10}(x_{8}-x_{3}) = 0,2141(0,52746) = 0,112929\\)
{: .text-center}  

- Quarto termo do somatório:

Agora temos \\(a_{n-1+1} = a_{10-1+1} = a_{10}\\). Então basta apenas observar o valor de \\(a\\) na coluna 10 (Tabela 2) para o **quarto termo**, que neste caso é \\(0,1224\\).
{: .text-justify}

Agora vamos calcular o termo das diferenças: \\((x_{n-i+1}-x_{i})\\). O termo \\(x_{n-i+1}\\) é o termo \\(x_{10-4+1} = x_{7} = 2,10288\\). E o termo \\(x_{i} = x_{4} = 1,90642\\).
{: .text-justify}

Portanto, \\((x_{n-i+1}-x_{i}) = (2,10288-1,90642) = 0,19646\\).

Dessa forma, o quarto termo do somatório de \\(b\\) é:

\\(a_{10}(x_{7}-x_{4}) = 0,1224(0,19646) = 0,024047\\)
{: .text-center}

- Quinto termo do somatório:

Agora temos \\(a_{n-1+1} = a_{10-1+1} = a_{10}\\). Então basta apenas observar o valor de \\(a\\) na coluna 10 (Tabela 2) para o **quinto termo**, que neste caso é \\(0,0399\\).
{: .text-justify}

Agora vamos calcular o termo das diferenças: \\((x_{n-i+1}-x_{i})\\). O termo \\(x_{n-i+1}\\) é o termo \\(x_{10-5+1} = x_{6} = 1,99568\\). E o termo \\(x_{i}=x_{5} = 1,98492\\).
{: .text-justify}

Portanto, \\((x_{n-i+1}-x_{i}) = (1,99568-1,98492) = 0,01076\\).

Dessa forma, o quarto termo do somatório de \\(b\\) é:

\\(a_{10}(x_{6}-x_{5}) = 0,0399(0,01076) = 0,000429\\)
{: .text-center}


*Observações:*

 ✔ O valor de \\(a_{n-1+1}\\) estará sempre na mesma coluna para um mesmo conjunto de dados, mudando apenas a linha;

 ✔ Sempre calculamos a diferença entre o maior e o menor número;

 ✔ Caso o conjunto de dados fosse ímpar, não utilizaríamos o valor central (mediana) nos cálculos, mas ele conta para o número total de observações;

 ✔ Caso os valores das observações sejam muito parecidos (ou iguais), a contribuição para o somatório será muito pequena.


Agora que temos todos os valores do somatório, basta soma-los para encontrar o valor de \\(b\\):

  \\(b= \sum_{i=1}^{n/2}(0,991108 + 0,360684 + 0,112929 + 0,024047 + 0,000429)\\)
  {: .text-center}
  \\(b=1,489197\\)
  {: .text-center}

3) Calcular o termo quadrático.

  \\(\sum_{i=1}^{n}(x_{i}-\bar{x})^{2}\\)
  {: .text-center}

A média (\\(\bar{x}\\)) desse conjunto de dados é \\(2,063448\\). Fazendo os cálculos do somatório acima, obtemos: \\(2,392327\\).

4) Calcular o valor da estatística do teste.

  \\(D_{S-W} = \frac{b^{2}}{\sum_{i=1}^n(x_{i}-\bar{x})^2} = \frac{1,489197^{2}}{2,392327} = 0,927\\)
  {: .text-center}

5) Obter o valor tabelado do teste.

Para acessar o valor tabelado basta determinar um nível de significância e observar na Tabela 1 a linha que corresponde ao número total de observações do conjunto de dados. Adotando 95% de confiança (5% de significância) e com 10 observações, temos que o valor \\(D_{S-W}^{critico} = 0,842\\).
{: .text-justify}

6) Concluir o teste.

Para concluir o teste basta comparar o valor tabelado com o valor calculado. Como \\(D_{S-W}^{critico}(0,842) < D_{S-W}(0,927)\\), não temos evidências para rejeitar a hipótese de Normalidade dos dados, e podemos concluir com 95% de confiança que o conjunto de dados seguem, pelo menos aproximadamente, a distribuição Normal segundo o teste de Shapiro-Wilk.
{: .text-justify}

<h2><a style="color:black" id="comentarios">Comentários</a></h2>

Eu trabalhei com diversos testes de Normalidade (Shapiro-Wilk, Anderson-Darling, Kolmogorov-Smirnov, Lilliefors, entre outros) para diversos conjuntos de dados e finalidades (normalidade de dados, normalidade de resíduos, ANOVA, MANOVA, entre outros), mas sempre foi o teste de Shapiro-Wilk que retornou resultados mais consistentes. Ele não é necessariamente o melhor, mas em geral, é o que eu mais confio.
{: .text-justify}

Como você deve ter percebido, aplicar este teste é relativamente simples, mas é trabalhoso e pode facilmente levar a erros de procedimento (esquecer de ordenar os dados por exemplo). Por isso o uso de softwares é o mais recomendado, além do plus de que a maioria dos softwares nos fornecem o valor de p como resultado, o que facilita a interpretação do teste. Contudo, muitos destes softwares são caros, o que inviabiliza seu uso, ou são algoritmos desenvolvidos em linhas de comando, o que afasta a muitas pessoas que não tem conhecimento algum dessa área.
{: .text-justify}

Pensando nestas possibilidades, eu criei uma série de tutoriais onde você tem acesso de forma simples e rápida, como aplicar o teste de Shapiro-Wilk em alguns softwares e algumas linguagens de programação. Como estes tutoriais foram feitos em épocas diferentes, o conjunto de dados pode não ser o mesmo, mas sempre temos a aplicação do teste de forma bem simples. Vamos lá!
{: .text-justify}

<h2><a style="color:black" id="tutorialexcel">Teste de Shapiro-Wilk: Tutorial utilizando Excel</a></h2>

Neste tutorial eu utilizo a versão do Microsoft Office 2016 em português brasileiro (pt-br) e com a virgula (,) como separador de casas decimais. Estas informações são importantes, pois caso seu sistema seja diferente do meu, provavelmente será necessário alterar alguns detalhes de sintaxe, mas nada muito complexo.
{: .text-justify}

A planilha foi desenvolvida pensando em ficar o mais automatizada possível. Dessa forma, muitos passos são utilizados além dos cálculos em si. Tirando isto, a planilha nada mais é do que uma sequência lógica do passo a passo apresentado no <a href="#exemplonumerico">item 3</a>.
{: .text-justify}

Por enquanto o vídeo está hospedado no YouTube e está todo em português-br. Uma versão em inglês talvez seja feita algum dia, a depender de demanda.
{: .text-justify}

<div class="tabela-centralizado">
  <iframe width="853" height="480" src="https://www.youtube.com/embed/flZa3Y8uiUk" frameborder="0"
  allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>


Você pode baixar a planilha desenvolvida no vídeo acima <a href = "/assets/files/shapiro-wilk/Shapiro_Wilk.xlsx" download="Shapiro_Wilk.xlsx">clicando aqui</a>.
{: .text-justify}


<h2><a style="color:black" id="tutorialpython">Teste de Shapiro-Wilk: Tutorial utilizando Python</a></h2>

Agora vamos a um tutorial utilizando minha linguagem de programação favorita, o Python. Neste caso, eu utilizei a versão 3.6 do Python, obtida com a distribuição Anaconda, e a IDE utilizada foi o Jupyter Notebook. Mas tem uma opção muito mais simples, que não necessita ter nada instalado no seu PC, o google Colab. Acesse <a href="https://colab.research.google.com">colab.com</a>, crie um novo notebook (você precisa estar logado no Google), e é só seguir os mesmos passos do tutorial.
{: .text-justify}

<div class="tabela-centralizado">
  <iframe width="853" height="480" src="https://www.youtube.com/embed/c8534_OfQPQ" frameborder="0" allow="accelerometer; autoplay;
  clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>
<br>

O teste de Shapiro-Wilk está na biblioteca SciPy. Então, a primeira coisa que precisamos fazer é importar esta biblioteca para o ambiente de trabalho:
{: .text-justify}

```python
import scipy.stats as stats
```

Em seguida, entramos com os dados em uma lista (uma lista é uma variável, neste caso o y, que recebe um vetor dentro de colchetes. Cada valor numérico é separado por vírgulas, e o separador de casas decimais é o ponto (.). Poderia ser um numpy array sem problemas nenhum (seria até melhor).
{: .text-justify}

```python
y = [1.69742, 1.99568, 1.90642, 2.61826, 3.15435, 1.98492, 1.52229, 1.42738, 2.10288, 2.22488]
```

Para calcular o valor da estatística de Shapiro-Wilk, basta utilizar o comando <code>stats.shapiro()</code> passando como argumento a lista com os dados (\\(y\\)). Você encontra mais detalhes sobre esta função na <a target="_blank" href="https://docs.scipy.org/doc/scipy/reference/generated/scipy.stats.shapiro.html">documentação do SciPy</a>.
{: .text-justify}

```python
shapiro_stat, shapiro_p_valor = stats.shapiro(x)
```

A variável <code>shapiro_stat</code> terá recebido o valor de \\(D_{S-W}\\). O valor crítico deve ser observado em uma tabela (Tabela 1), pois esta função não retorna o valor tabelado. Já a variável <code>shapiro_p_valor</code> terá recebido o valor de \\(p\\).
{: .text-justify}

Para imprimir os resultados, basta utilizar a função <code>print()</code>, passando como argumento a variável que quiser que seja impressa. Ou, melhor ainda, podemos escrever um breve texto para deixar claro o que está sendo impresso:
{: .text-justify}

```python
<p class="">print(“O valor da estatística de Shapiro-Wilk = “ + str(Shapiro_stat))
<p class="">print(“O valor de p de Shapiro-Wilk = “ + str(shapiro_p_valor))
```

Como resultado, obtemos o valor da estatística do teste de \\(0,9266\\), que é muito próximo ao que obtemos no <a href="#exemplonumerico">item 3</a>.
{: .text-justify}

Já o valor de p foi de \\(0,416\\), e podemos utilizar ele para concluir o teste.
{: .text-justify}

```python
if shapiro_p_valor > 0.05:
  print("Com 95% de confiança, os dados são similares a uma distribuição normal segundo o teste de Shapiro-Wilk")
else:
  print("Com 95% de confiança, os dados NÃO são similares a uma distribuição normal segundo o teste de Shapiro-Wilk")
```

E concluímos que os dados são similares a uma distribuição Normal. Muito mais e fácil utilizando Python do que o Excel (pelo menos é minha opinião 😛)
{: .text-justify}

Você pode baixar o notebook <a href = "/assets/files/shapiro-wilk/shapiro-wilk-test.ipynb" download="shapiro-wilk-test.ipynb">clicando aqui</a>.
{: .text-justify}

<h2><a style="color:black" id="referencias">Referências</a></h2>

<p id="portal-action" >Action, P. (n.d.). Teste de Shapiro Wilk. Retrieved January 8, 2021, from <a target="_blank" href="http://www.portalaction.com.br/inferencia/64-teste-de-shapiro-wilk">http://www.portalaction.com.br/inferencia/64-teste-de-shapiro-wilk</a>.</p>


<p id="nist-sematech">NIST/SEMATECH. (2013). e-Handbook of Statistical Methods. DOI: <a target = "_blank" href="https://www.itl.nist.gov/div898/handbook/prc/section2/prc213.htm">https://www.itl.nist.gov/div898/handbook/prc/section2/prc213.htm</a>.</p>

<p id="pearson-hartley">Pearson, A. V., & Hartley, H. O. (1972). Biometrica Tables for Statisticians, Vol 2. Cambridge University Press.</p>

<p id="rodrigues-iemma">Rodrigues, M. I., & Iemma, A. F. (2009). Planejamento de Experimentos & Otimização de Processos (2nd ed.). Casa do Espírito Amigo Fraternidade Fé e Amor.</p>

<p id="shapiro-wilk">Shapiro, A. S. S., & Wilk, M. B. (1965). An Analysis of Variance Test for Normality (Complete Samples). Biometrika, 52(3/4), 591–611. Link: <a target = "_blank" href="https://doi.org/https://doi.org/10.2307/2333709">https://doi.org/https://doi.org/10.2307/2333709</a>.</p>
