---
title: "Legendas (Labels)"
data: 2021-08-08
tags: []
header:
  image: "/images/chess.jpg"
  image_description: "Chess pieces"
excerpt: "matplotlib"
locale: "pt-br"
---


<br>

Os `labels` são os somes de cada elemento adicionado no gráfico. Em geral, eles são adicionados no momento que o elemento é criado, que é a forma que estamos utilizando. Em alguns casos, é interessante alterar alguns parâmetros dos `labels` de forma a melhorar a estética e a apresentação dos resultados.
{: .text-justify}

<h2><a style="color:black" id="tamanho-fonte">Tamanho da fonte</a></h2>

O tamanho da fonte da legenda pode ser alterado passando o  parâmetro `fontsize` para o `plt.legend()`. Este parâmetro recebe um  número (`int` ou `float`) ou uma `str` de referência, que é utilizado para controlar o tamanho da fonte utilizada. As opções de `str` são:
{: .text-justify}

* `'xx-small'`;
* `'x-small'`;
* `'small'`;
* `'medium'`;
* `'large'`;
* `'x-large'`;
* `'xx-large'`;

Por exemplo, para utilizar o tamanho de fonte `'xx-large'`, basta passar `fontsize='xx-large'`, da seguinte forma:
{: .text-justify}

```python
plt.figure(figsize=(8,6))
plt.scatter(cachorro_peso, cachorro_altura, label="Cachorros")
plt.scatter(gatos_peso, gatos_altura, label="Gatos")
plt.plot(pinguins_peso, pinguins_altura, marker="o", c="g", label="Pinguins")
plt.xlabel("Peso (kg)")
plt.ylabel("Altura (cm)")
plt.title("Relação entre peso e altura de diferentes animais")
plt.ylim([0,125])
plt.legend(fontsize='xx-large')
plt.show()
```


*Figura 1* - Legendas com tamanho de fonte alterado.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/legendas/62/legendas-01.png" alt="gráfico de dispersão combinado com gráfico de linhas desenhado com matplotlib, com o tamanho da fonte da legenda alterado." >
{: .text-center}

<br>

<h2><a style="color:black" id="cor-labels">Cor dos labels nas legendas</a></h2>

A cor dos `labels` nas legendas pode ser alterada passando uma `str` com o nome da cor, ou uma sequência (`list`, `tuple`, etc) contendo `str` em cada elemento com o nome da cor desejada, para o parâmetro `labelcolor`. As cores disponíveis são as mesmas vistas <a href="/Curso-matplotlib-08/#cor-marcadores">anteriormente</a>.
{: .text-justify}

Por exemplo, para alterar a cor dos labels para <span style="color: red">vermelho</span>:

```python
plt.figure(figsize=(8,6))
plt.scatter(cachorro_peso, cachorro_altura, label="Cachorros")
plt.scatter(gatos_peso, gatos_altura, label="Gatos")
plt.plot(pinguins_peso, pinguins_altura, marker="o", c="g", label="Pinguins")
plt.xlabel("Peso (kg)")
plt.ylabel("Altura (cm)")
plt.title("Relação entre peso e altura de diferentes animais")
plt.ylim([0,125])
plt.legend(fontsize='xx-large', labelcolor='red')
plt.show()
```

*Figura 2* - Legendas com a cor do label alterada.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/legendas/62/legendas-02.png" alt="gráfico de dispersão combinado com gráfico de linhas desenhado com matplotlib, com a cor do label alterada." >
{: .text-center}

<br>

Para personalizar cada label individualmente, basta passar uma sequência com as cores desejadas para o parâmetro `labelcolor` (esta sequência deve ter o mesmo número de elementos adicionados na legenda).
{: .text-justify}

Por exemplo, dada esta sequência de cores:

```python
cores = ['red', 'green', 'blue']
```

E então fazendo `labelcolor = cores`, obtemos:

```python
plt.figure(figsize=(8,6))
plt.scatter(cachorro_peso, cachorro_altura, label="Cachorros")
plt.scatter(gatos_peso, gatos_altura, label="Gatos")
plt.plot(pinguins_peso, pinguins_altura, marker="o", c="g", label="Pinguins")
plt.xlabel("Peso (kg)")
plt.ylabel("Altura (cm)")
plt.title("Relação entre peso e altura de diferentes animais")
plt.ylim([0,125])
plt.legend(fontsize='xx-large', labelcolor=cores)
plt.show()
```

*Figura 3* - Legendas com a cor do label alterada.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/legendas/62/legendas-03.png" alt="gráfico de dispersão combinado com gráfico de linhas desenhado com matplotlib, com a cor do label alterada." >
{: .text-center}

<br>

#### Atenção

O parâmetro `labelcolor` funciona apenas na versão 3.2 ou superior do **matplotlib**.


Também podemos passar três `str` de referência para coincidir com as cores do marcador. As `str` de referência são as seguintes:
{: .text-justify}

* `'linecolor'`: o texto terá a mesma cor que a cor da linha;
* `'markerfacecolor'` ou `'mfc'`: o texto terá a mesma cor que a cor de dentro do marcador;
* `'markeredgecolor'` ou `'mec'`: o texto terá a mesma cor que a cor da borda do marcador;


```python
plt.figure(figsize=(8,6))
# plt.scatter(cachorro_peso, cachorro_altura, label="Cachorros")
# plt.scatter(gatos_peso, gatos_altura, label="Gatos")
plt.plot(pinguins_peso, pinguins_altura, marker="o", c="g", markerfacecolor="y", markeredgecolor="m", label="Pinguins")
plt.xlabel("Peso (kg)")
plt.ylabel("Altura (cm)")
plt.title("Relação entre peso e altura de diferentes animais")
plt.ylim([0,125])
plt.legend(fontsize='xx-large', labelcolor='mfc')
plt.show()
```

*Figura 4* - Legendas com a cor do label combinando com a cor da face do marcador.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/legendas/62/legendas-04.png" alt="gráfico de dispersão combinado com gráfico de linhas desenhado com matplotlib, com a cor do label combinando com a cor da face do marcador." >
{: .text-center}

<br>

```python
plt.figure(figsize=(8,6))
# plt.scatter(cachorro_peso, cachorro_altura, label="Cachorros")
# plt.scatter(gatos_peso, gatos_altura, label="Gatos")
plt.plot(pinguins_peso, pinguins_altura, marker="o", c="g", markerfacecolor="y", markeredgecolor="m", label="Pinguins")
plt.xlabel("Peso (kg)")
plt.ylabel("Altura (cm)")
plt.title("Relação entre peso e altura de diferentes animais")
plt.ylim([0,125])
plt.legend(fontsize='xx-large', labelcolor='mec')
plt.show()
```

*Figura 5* - Legendas com a cor do label combinando com a cor da borda do marcador.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/legendas/62/legendas-05.png" alt="gráfico de dispersão combinado com gráfico de linhas desenhado com matplotlib, com a cor do label combinando com a cor da borda do marcador." >
{: .text-center}

<br>


```python
plt.figure(figsize=(8,6))
# plt.scatter(cachorro_peso, cachorro_altura, label="Cachorros")
# plt.scatter(gatos_peso, gatos_altura, label="Gatos")
plt.plot(pinguins_peso, pinguins_altura, marker="o", c="g", markerfacecolor="y", markeredgecolor="m", label="Pinguins")
plt.xlabel("Peso (kg)")
plt.ylabel("Altura (cm)")
plt.title("Relação entre peso e altura de diferentes animais")
plt.ylim([0,125])
plt.legend(fontsize='xx-large', labelcolor='linecolor')
plt.show()
```

*Figura 6* - Legendas com a cor do label combinando com a cor da linha.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/legendas/62/legendas-06.png" alt="gráfico de dispersão combinado com gráfico de linhas desenhado com matplotlib, com a cor do label combinando com a cor da linha." >
{: .text-center}

<br>

#### ATENÇÃO

Os parâmetros acima não funcionam corretamente para a versão 3.3.4 do **matplotlib** para `plt.scatter()`. Mas para o `plt.scatter()`, elas funcionam corretamente.
{: .text-justify}

<br>

<form id = "quiz" name = "quiz">

<p><strong>Por qual motivo seria interessante alterar a cor dos labels na legenda?</strong></p>

<input type = "radio" id = "mc" name = "question1" value = "a"> Para reforçar a ligação entre o elemento e a sua respectiva legenda
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "b"> Nenhum motivo
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "c"> Apenas para fins estéticos
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "d"> Para destacar algum elemento específico
<p style="font-size: 50%"></p>
<p></p>
<input id = "button" type = "button" class="btn btn--info" value = "Enviar" onclick = "check();">
</form>

<div id = "after_submit">
<p style="font-size: 120%" id = "message"></p>
</div>

<br>

<p style="text-align: center">
  <a href="/Curso-matplotlib-61" class="btn btn--success">Anterior</a>
  <a href="/Curso-matplotlib-63" class="btn btn--success">Próximo</a>
</p>



<script>
function check(){
	var question1 = document.quiz.question1.value;
	var messages = [" 🎉 Correto! 🥳️ <br> Combinar a cor do elemento com a cor do label por ser uma forma de reforçar a ligação entre a legenda e o elemento que esta sendo legendado",
  " 😔 Incorreto! <br> Temos diversos motivos para utilizar cores nos labels, como reforçar a ligação entre elementos ou destacar algum elemento dos demais",
  " 😔 Incorreto! <br> Apesar de que a estética do gráfico é um motivo para alterar a cor dos labels, este não é o único motivo",
  " 🎉 Correto! ️<br> Alterar a cor de um label é uma forma de destacar os elementos do gráfico",
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
