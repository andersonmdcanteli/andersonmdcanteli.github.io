---
title: "Legendas (Título da legenda)"
data: 2021-08-08
tags: []
header:
  image: "/images/chess.jpg"
  image_description: "Chess pieces"
excerpt: "matplotlib"
locale: "pt-br"
---

<br>

É possível adicionar um título para a legenda, o que é feito passando o nome do título, como uma `str`, para o parâmetro `title` em `plt.legend()`.
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
plt.legend(ncol=2, title="Animais")
plt.show()
```

*Figura 1* - Caixa da legenda com título.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/legendas/65/legendas-01.png" alt="gráfico de dispersão combinado com gráfico de linhas desenhado com matplotlib, caixa da legenda com título." >
{: .text-center}

<br>

<h2><a style="color:black" id="alinhamento-titulo">Alinhamento do título</a></h2>

É possível alterar o alinhamento do titulo da legenda, o que é feito utilizando um método da própria legenda, que é o método `._legend_box.align()`, que deve receber uma `str` com o tipo de alinhamento desejado:
{: .text-justify}


* `"center"` (centralizado, padrão);
* `"left"` (esquerda);
* `"right"` (direita);


Para utilizar este parâmetro, precisamos criar um objeto de legenda, da mesma forma utilizada para alterar a espessura da borda da legenda.
{: .text-justify}

```python
leg = plt.legend()
```
E então aplicar o método `._legend_box.align(x)`, onde `x` é uma `str` com uma das opções listadas acima. Por exemplo, para deixar o titulo da legenda alinhadas à esquerda:
{: .text-justify}

```python
leg._legend_box.align = "left"
```

Então:

```python
plt.figure(figsize=(8,6))
plt.scatter(cachorro_peso, cachorro_altura, label="Cachorros")
plt.scatter(gatos_peso, gatos_altura, label="Gatos")
plt.plot(pinguins_peso, pinguins_altura, marker="o", c="g", label="Pinguins")
plt.xlabel("Peso (kg)")
plt.ylabel("Altura (cm)")
plt.title("Relação entre peso e altura de diferentes animais")
plt.ylim([0,125])
leg = plt.legend(ncol=2, title="Animais")
leg._legend_box.align = "left"
plt.show()
```

*Figura 2* - Caixa da legenda com título alinhado à esquerda.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/legendas/65/legendas-02.png" alt="gráfico de dispersão combinado com gráfico de linhas desenhado com matplotlib, caixa da legenda com título à esquerda." >
{: .text-center}

<br>

<h2><a style="color:black" id="tamanho-fonte-titulo">Tamanho da fonte do título</a></h2>

Para alterar o tamanho da fonte do título, basta passar uma `str` com o nome do tamanho da fonte ou um número (`int` ou `float`) para o parâmetro `title_fontsize`.
{: .text-justify}

A lista de opções para utilizar `str`:  

* `'xx-small'`;
* `'x-small'`;
* `'small'`;
* `'medium'`;
* `'large'`;
* `'x-large'`;
* `'xx-large'`;

Por exemplo:

```python
plt.figure(figsize=(8,6))
plt.scatter(cachorro_peso, cachorro_altura, label="Cachorros")
plt.scatter(gatos_peso, gatos_altura, label="Gatos")
plt.plot(pinguins_peso, pinguins_altura, marker="o", c="g", label="Pinguins")
plt.xlabel("Peso (kg)")
plt.ylabel("Altura (cm)")
plt.title("Relação entre peso e altura de diferentes animais")
plt.ylim([0,125])
leg = plt.legend(ncol=2, title="Animais", title_fontsize='xx-large')
leg._legend_box.align = "left"
plt.show()
```

*Figura 3* - Caixa da legenda com título alinhado com tamanho de fonte alterado.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/legendas/65/legendas-03.png" alt="gráfico de dispersão combinado com gráfico de linhas desenhado com matplotlib, caixa da legenda com título com tamanho de fonte alterado." >
{: .text-center}

<br>



<form id = "quiz" name = "quiz">

<p><strong>Como inserir um título centralizado na legenda?</strong></p>

<input type = "radio" id = "mc" name = "question1" value = "a"> Passando o nome da legenda através do parâmetro title em plt.legend()
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "b"> Não é preciso fazer nada
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "c"> Passando o parâmetro align como 'center' em plt.legend()
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "d"> Passando o nome da legenda através do parâmetro title e o parâmetro align como 'center' em plt.legend()
<p style="font-size: 50%"></p>
<p></p>
<input id = "button" type = "button" class="btn btn--info" value = "Enviar" onclick = "check();">
</form>

<div id = "after_submit">
<p style="font-size: 120%" id = "message"></p>
</div>

<br>

<p style="text-align: center">
  <a href="/Curso-matplotlib-64" class="btn btn--success">Anterior</a>
  <a href="/Curso-matplotlib-66" class="btn btn--success">Próximo</a>
</p>



<script>
function check(){
	var question1 = document.quiz.question1.value;
	var messages = [" 🎉 Correto! 🥳️ <br> Para inserir um título centralizado na legenda, basta apenas inserir o título, pois ele já é centralizado por padrão!",
  " 😔 Incorreto! <br> É necessário inserir o título desejado através do parâmero <code>title</code>.",
  " Incorreto 😔 <br> O método <code>plt.legend()</code> não tem um parâmetro <code>align</code>.",
  " 😔 Incorreto! 😔 <br> O método <code>plt.legend()</code> não tem um parâmetro <code>align</code>.",
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
