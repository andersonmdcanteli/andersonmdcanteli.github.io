---
title: "Curso matplotlib - Gráfico com barras de erros (barra de erro no eixo x)"
data: 2021-08-01
tags: []
header:
  image: "/images/chess.jpg"
  image_description: "Chess pieces"
excerpt: "matplotlib"
locale: "pt-br"
---

<br>

Para adicionar barras de erro no eixo x (barras horizontais), basta utilizar o parâmetro `xerr` ao invés do parâmetro `yerr` em `plt.errorbar()`. Os demais parâmetros seguem a mesma lógica.
{: .text-justify}

Para seguir o exemplo com os mesmos dados, é utilizado a variável `dias` no eixo `y` e a variável `media` no eixo `x`, de modo que o `xerr` possa ser utilizado de forma correta, pois a variável `dias` contém `str`, e as `str` não contém erro para ser inserido.
{: .text-justify}

```python
plt.figure(figsize=(8,6))
plt.errorbar(media, dias, xerr=desv_pad, ecolor='red', elinewidth=1, capsize=5, capthick=1,
             color='k', linestyle="none",)
plt.scatter(media, dias, label="Meus dados")
plt.legend()
plt.show()
```

*Figura 1* - Gráfico de erros relacionando a temperatura média na cidade de Birigui-SP em três dias diferentes do ano de 2021.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-erros/33/grafico-erros-01.png" alt="gráfico de dispersão desenhado com o matplotlib relacionando o dia e a temperatura média do dia" >
{: .text-center}

<br>

Para inserir barra de erro tanto na vertical, quanto na horizontal, basta inserir o parâmetro `xerr` e o parâmetro `yerr` no elemento `plt.errorbar()` ao mesmo tempo. Contudo, as edições aplicadas serão iguais para as barras verticais e horizontais.
{: .text-justify}

<form id = "quiz" name = "quiz">

<p><strong>Qual método é a principal diferença entre os parâmetros xerr e yerr?</strong></p>

<input type = "radio" id = "mc" name = "question1" value = "a"> O parâmetro <code>xerr</code> é utilizado para inserir barras de erro paralelas ao eixo <code>x</code>, enquanto que o parâmetro <code>yerr</code> é utilizado para inserir barras de erro paralelas ao eixo <code>y</code>.
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "b"> O parâmetro <code>xyerr</code> é utilizado para inserir barras de erro paralelas ao eixo <code>x</code>, enquanto que o parâmetro <code>xerr</code> é utilizado para inserir barras de erro paralelas ao eixo <code>y</code>.
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "c"> Estes dois parâmetros tem a mesma função
<p style="font-size: 50%"></p>
<p></p>
<input id = "button" type = "button" class="btn btn--info" value = "Enviar" onclick = "check();">
</form>

<div id = "after_submit">
<p style="font-size: 120%" id = "message"></p>
</div>

<br>


<p style="text-align: center">
  <a href="/Curso-matplotlib-32" class="btn btn--success">Anterior</a>
  <a href="/Curso-matplotlib-34" class="btn btn--success">Próximo</a>
</p>


<script>
function check(){
	var question1 = document.quiz.question1.value;
	var messages = [" 🎉 Correto! 🥳️ <br> ",
  " Incorreto! 😔 <br> O parâmetro <code>xerr</code> tem como função inserir barras de erro paralelas ao eixo <code>x</code>, enquanto que o parâmetro <code>yerr</code> tem como função inserir barras de erro paralelas ao eixo <code>y</code>, ",
  " 😔 Incorreto! 😔  <br> O parâmetro <code>xerr</code> tem como função inserir barras de erro paralelas ao eixo <code>x</code>, enquanto que o parâmetro <code>yerr</code> tem como função inserir barras de erro paralelas ao eixo <code>y</code>, ",  
  "☕️"];
	var score;

	if (question1 == "a") {
		score = 0;
	}	else if (question1 == "b") {
		score = 1;
	} else if (question1 == "c") {
    score = 2;
  } else {
    score = 3;
  }

	document.getElementById("after_submit").style.visibility = "visible";
	document.getElementById("message").innerHTML = messages[score];

};

</script>
