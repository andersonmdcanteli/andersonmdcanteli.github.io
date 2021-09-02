---
title: "Curso matplotlib - Legendas (Conjunto de dados)"
data: 2021-08-08
tags: []
header:
  image: "/images/chess.jpg"
  image_description: "Chess pieces"
excerpt: "matplotlib"
locale: "pt-br"
---

<img style="float: center;" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/generico/cao-gato-pinguim.png" alt="Imagem com cão, gato e pinguim" width="600">
{: .text-center}

<p style="text-align: center;" >Fonte: <a href="https://www.umsabadoqualquer.com/tirinhas/caes-e-gatos">umsabadoqualquer.com.br</a> e <a href="https://dreamworksanimation.fandom.com/pt-br/wiki/Kowalski">dreamworksanimation.com.br</a></p>

<br>

<h2><a style="color:black" id="">Conjunto de dados</a></h2>

O conjunto de dados utilizado para exemplificar o comportamento das legendas, é o conjunto que relaciona a altura (cm) e o peso (kg) de <a href="https://www.dimensions.com/">cães, gatos e pinguins </a>.
{: .text-justify}

```python
### Dados de cães
## weight
cachorro_peso = [45.36, 68.04, 37.42, 30.62, 22.68, 22.68, 10.88, 8.16, 1.59, 4.53, 10.2] # peso em kilos
## height
cachorro_altura = [62.23, 67.31, 60.96, 57.15, 52.07, 54.61, 36.83, 26.67, 19.05, 25.4 , 29.21] # altura em em centímetros
## breed
raca_cachoros = ['Rottweiler', 'Saint Bernard', 'German Shepherd Dog', 'Labrador Retriever', 'Chow Chow', 'Siberian Husky',
         'Beagle', 'Pug', 'Chihuahua', 'Poodle Toy', 'French Bulldog'] # nome da respectiva raça

### Dados de gatos
## weight
gatos_peso = [7.0, 4.5, 6.0, 7.0, 4.5, 4.0, 5.5, 4.5, 4.5, 3.5, 4.5, 4.0, 4.0, 8.0, 4.5, 7.5, 3.5, 5.0, 4.0, 6.5, 6.5,
             5.5, 8.0, 5.0, 4.5, 3.5, 5.5, 5.5, 5.0, 5.5] # peso em kilos
## height
gatos_altura = [25.5, 22.5, 22.5, 22.5, 22.5, 32.0, 38.0, 27.5, 25.5, 27.5, 25.5, 27.5, 27.5, 32.5, 27.5, 26.5, 22.5,
                 25.5, 22.5, 25.5, 25.5, 22.5, 35.5, 22.5, 22.5, 17.5, 22.5, 22.5, 22.5, 25.5]  # altura em em centímetros
## breed
raca_gatos = ['Siberian Cat', 'Abyssinian Cat', 'American Shorthair Cat', 'Bengal Cat', 'Birman Cat', 'Bombay Cat',
             'British Shorthair Cat', 'Burmese Cat', 'Chartreux Cat', 'Devon Rex Cat', 'Havana Brown Cat', 'Himalayan Cat',
             'Korat Cat', 'Maine Coon Cat', 'Manx Cat', 'Norwegian Forest Cat', 'Oriental Cat', 'Oriental Shorthair Cat',
             'Persian Cat', 'Ragamuffin Cat', 'Ragdoll Cat', 'Russian Blue Cat', 'Savannah Cat', 'Scottish Fold Cat',
              'Siamese Cat', 'Singapura Cat', 'Somali Cat', 'Sphynx Cat', 'Tonkinese Cat', 'Turkish Van Cat']

### Dados de pinguis
## weight
pinguins_peso = [4.8, 4.25, 33.5, 6.7, 13.65, 4.8] # peso em kilos
## height
pinguins_altura = [58.5, 72, 120, 70.5, 85, 65] # altura em em centímetros
## breed
raca_pinguins = ['Adélie Penguin', 'Chinstrap Penguin', 'Emperor Penguin', 'Gentoo Penguin', 'King Penguin',
                 'Macaroni Penguin']
```


Para ter uma melhor visualização do comportamento das legendas, vamos criar o gráfico utilizando o `plt.scatter()` para os dados dos Cachorros e dos Gatos.
{: .text-justify}

Já os dados dos Pinguins, estes são inseridos utilizando o `plt.plot()`. É importante salientar que esta não é a forma correta de inserir os dados que relacionam peso e altura dos pinguins, pois *não existe uma sequência lógica* dos dados. Esta forma é utilizada apenas para deixar mais claro as mudanças que ocorrem ao editar as legendas. Assim, temos na legenda elementos com linhas e também elementos sem linhas.
{: .text-justify}

Dito isto, podemos desenhar o gráfico:

```python
plt.figure(figsize=(8,6))
plt.scatter(cachorro_peso, cachorro_altura, label="Cachorros")
plt.scatter(gatos_peso, gatos_altura, label="Gatos")
plt.plot(pinguins_peso, pinguins_altura, marker="o", c="g", label="Pinguins")
plt.xlabel("Peso (kg)")
plt.ylabel("Altura (cm)")
plt.title("Relação entre peso e altura de diferentes animais")
plt.ylim([0,125])
plt.legend()
plt.show()
```

*Figura 1* - Gráfico base para estudar as legendas.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/legendas/61/legendas-01.png" alt="gráfico de dispersão combinado com gráfico de linhas desenhado com matplotlib." >
{: .text-center}

<br>

Nós já estudamos anteriormente como inserir as legendas, o que deve ser feito passando o parâmetro `label` para o elemento gráfico que esta sendo inserido, e também é necessário utilizar o `plt.legend()` para efetivamente inserir as legendas.
{: .text-justify}

Entretanto, não é necessário passar o parâmetro `label` para nomear as legendas. Os nomes dos elementos podem ser passados diretamente em `plt.legend()`, através de uma sequência (`list`, `tuple`, `ndarray`, etc) contendo o nome de cada elemento inserido no gráfico. Por exemplo, ao invés de passar em cada elemento o `label`, poderia ter sido passado uma `list` com os nomes diretamente em `plt.legend()`. Por exemplo:
{: .text-justify}

```python
lista_labels = ['Dog', 'Cat', 'Penguin']
```

#### ATENÇÃO:

A `lista_labels` contém os nomes dos animais em inglês apenas para diferenciar dos nomes originais. Além disso, os nomes dos elementos estão ordenados na mesma sequência em que os elementos são inseridos no gráfico, e isto é *vital* para que as legendas sejam inseridas de forma correta.
{: .text-justify}

Ao passar a `lista_labels` em `plt.legend()` e removendo o `label` de cada elemento:

```python
plt.figure(figsize=(8,6))
plt.scatter(cachorro_peso, cachorro_altura)#, label="Cachorros")
plt.scatter(gatos_peso, gatos_altura)#, label="Gatos")
plt.plot(pinguins_peso, pinguins_altura, marker="o", c="g")#, label="Pinguins")
plt.xlabel("Peso (kg)")
plt.ylabel("Altura (cm)")
plt.title("Relação entre peso e altura de diferentes animais")
plt.ylim([0,125])
plt.legend(lista_labels)
plt.show()
```

*Figura 2* - Gráfico com os `labels` da legenda passada em `plt.legend()`.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/legendas/61/legendas-02.png" alt="gráfico de dispersão combinado com gráfico de linhas desenhado com matplotlib." >
{: .text-center}

<br>

Esta forma pode ser muito útil em alguns casos, mas ela pode trazer problemas também. Observe atentamente as legendas da Figura 1 e da Figura 2. Mesmo que a ordem da `lista_labels` *realmente está correta*, os dados desenhados não batem com a legenda gerada. Isto ocorreu pois o gráfico gerado contém elementos `plt.scatter()` e `plt.plot()`, que tem prioridade diferente. Caso todos os elementos fossem do mesmo tipo, as legendas teriam sido criadas da forma correta:
{: .text-justify}

```python
plt.figure(figsize=(8,6))
plt.scatter(cachorro_peso, cachorro_altura)#, label="Cachorros")
plt.scatter(gatos_peso, gatos_altura)#, label="Gatos")
plt.scatter(pinguins_peso, pinguins_altura, marker="o", c="g")#, label="Pinguins")
plt.xlabel("Peso (kg)")
plt.ylabel("Altura (cm)")
plt.title("Relação entre peso e altura de diferentes animais")
plt.ylim([0,125])
plt.legend(lista_labels)
plt.savefig("legendas-03.png", dpi=300, bbox_inches='tight')
plt.show()
```

*Figura 3* - Gráfico com os `labels` da legenda passada em `plt.legend()`.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/legendas/61/legendas-03.png" alt="gráfico de dispersão desenhado com matplotlib." >
{: .text-center}

<br>

Dessa forma, tenha muito cuidado ao passar os nomes das legendas diretamente em `plt.legend()`, ***especialmente*** quando o gráfico estiver sendo criado com diversos elementos.
{: .text-justify}

Também estudamos como alterar a posição da legenda no gráfico, o que é feito através do parâmetro `loc`. Agora, vamos estudar como editar a caixa onde as legendas foram inseridas. Estas alterações são feitas passando outros parâmetros para o `plt.legend()`, de forma similar ao feito utilizando o `loc`.
{: .text-justify}

Você encontra mais detalhes sobre o `plt.legend()` na [documentação](https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.legend.html).
{: .text-justify}

<br>

<form id = "quiz" name = "quiz">

<p><strong>Qual problema pode ocorrer quando a legenda é criada diretamente em plt.legend() e temos vários elementos gráficos inseridos?</strong></p>

<input type = "radio" id = "mc" name = "question1" value = "a"> Nenhum tipo de problema irá aparecer
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "b"> O gráfico pode não será desenhado
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "c"> As legendas podem não corresponder ao nome correto devido a prioridade dos elementos
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "d"> As legendas podem não corresponder ao nome correto pois, gatos e cachorros são mais legais que os pinguins!
<p style="font-size: 50%"></p>
<p></p>
<input id = "button" type = "button" class="btn btn--info" value = "Enviar" onclick = "check();">
</form>

<div id = "after_submit">
<p style="font-size: 120%" id = "message"></p>
</div>

<br>

<p style="text-align: center">
  <a href="/Curso-matplotlib-60" class="btn btn--success">Anterior</a>
  <a href="/Curso-matplotlib-62" class="btn btn--success">Próximo</a>
</p>


<script>
function check(){
	var question1 = document.quiz.question1.value;
	var messages = [" Incorreto! 😔 <br> Pode acontecer das legendas não corresponderem ao valor passado devido a prioridade dos elementos, e isto é um tipo (grave) de problema",
  " 😔 Incorreto! <br> A não ser que exista algum erro no código, o gráfico será normalmente desenhado, mesmpo que algumas imprecisões ocorram.",
  " 🎉 Correto! 🥳️ <br> Devido a uma questão relacionada a ordem de prioridade dos elementos, pode acontecer das legendas são corresponderem ao valor correto.",
  " 😔 Incorreto! <br> O matplotlib não interpreta os textos passados para as legendas. Além disto, cachorros 🐶 são muito mais legais do que pinguins 🐧, que também são mais legais que gatos 😺!",
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
