---
title: "Curso matplotlib - Gráfico com barras de erros (linhas e pontos)"
data: 2021-07-31
tags: []
header:
  image: "/images/chess.jpg"
  image_description: "Chess pieces"
excerpt: "matplotlib"
locale: "pt-br"
---

<br>

Além das edições das barras de erros, o `plt.errobar()` também aceita parâmetros para controlar o tipo de marcador (`marker`), a cor do marcador (`markerfacecolor`), o tipo de linha (`linestyle`), o título do elemento (`label`), entre outros, de forma muito similar ao que foi apresentado anteriormente.
{: .text-justify}

Por exemplo:

```python
plt.figure(figsize=(8,6))
plt.errorbar(dias, media, yerr=desv_pad, ecolor='red', elinewidth=1, capsize=5, capthick=1,
             barsabove=True, marker = "o", markerfacecolor="g", markersize=4, color="red",
             linestyle="none", label="erro")
plt.legend()
plt.show()
```

*Figura 1* - Gráfico de erros relacionando a temperatura média na cidade de Birigui-SP em três dias diferentes do ano de 2021.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-erros/31/grafico-erros-01.png" alt="gráfico de dispersão desenhado com o **matplotlib** relacionando o dia e a temperatura média do dia" >
{: .text-center}

<br>

Entretanto, uma boa prática é utilizar o método `plt.errorbar()` apenas para inserir as barras de erro, e então utilizar o método `plt.scatter()` para adicionar os pontos, e/ou o `plt.plot()`para adicionar as linhas. Por exemplo:
{: .text-justify}

```python
plt.figure(figsize=(8,6))
plt.errorbar(dias, media, yerr=desv_pad, ecolor='red', elinewidth=1, capsize=5, capthick=1,
             color='k', linestyle="none",)
plt.scatter(dias, media, label="Meus dados")
plt.legend()
plt.show()
```

*Figura 2* - Gráfico de erros relacionando a temperatura média na cidade de Birigui-SP em três dias diferentes do ano de 2021.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-erros/31/grafico-erros-02.png" alt="gráfico de dispersão desenhado com o matplotlib relacionando o dia e a temperatura média do dia" >
{: .text-center}

<br>

Utilizar o `plt.errorbar()` tem a vantagem de ser um único elemento a ser adicionado. Entretanto, a sua edição pode se tornar mais complexa, e por este motivo, em alguns casos é melhor combinar os elementos. Além disto, repare nas legendas geradas. O símbolo da legenda gerada utilizando o `plt.errorbar()` inclui a barra de erro, enquanto que o símbolo da legenda gerada utilizando o `plt.scatter` não inclui a barra de erro.
{: .text-justify}

<br>

<form id = "quiz" name = "quiz">

<p><strong>Qual é a vantagem de utilizar o plt.errorbar() ao invés de utilizar o plt.scatter()?</strong></p>

<input type = "radio" id = "mc" name = "question1" value = "a"> Não existem nenhuma vantagem!
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "b"> A principal vantagem é a possibilidade de inserir barras de erro no gráfico
<p style="font-size: 50%"></p>
<p></p>
<input id = "button" type = "button" class="btn btn--info" value = "Enviar" onclick = "check();">
</form>

<div id = "after_submit">
<p style="font-size: 120%" id = "message"></p>
</div>

<br>

<p style="text-align: center">
  <a href="/Curso-matplotlib-30" class="btn btn--success">Anterior</a>
  <a href="/Curso-matplotlib-32" class="btn btn--success">Próximo</a>
</p>


<script>
function check(){
	var question1 = document.quiz.question1.value;
	var messages = [" Incorreto! 😔 <br> O uso do <code>plt.errobar()</code> permite a inserção de barras de erro, o que não é possível com o uso do <code>plt.scatter()</code>!",
  "🎉 Correto! 🥳️ <br> Esta é a principal vantagem! Entretanto, a edição do gráfico é um pouco mais complexa!",
  "☕️"];
	var score;

	if (question1 == "a") {
		score = 0;
	}	else if (question1 == "b") {
		score = 1;
  } else {
    score = 2;
  }

	document.getElementById("after_submit").style.visibility = "visible";
	document.getElementById("message").innerHTML = messages[score];

};

</script>
