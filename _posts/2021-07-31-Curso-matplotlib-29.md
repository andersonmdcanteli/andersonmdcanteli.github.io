---
title: "Curso matplotlib - Gráfico com barras de erros (barra de erro no eixo y)"
data: 2021-07-31
tags: []
header:
  image: "/images/chess.jpg"
  image_description: "Chess pieces"
excerpt: "matplotlib"
locale: "pt-br"
---

<br>

Para inserir uma barra de erro no eixo `y`, é necessário adicionar o parâmetro `yerr` em `plt.errorbar()`. Este parâmetro recebe um número (`float` ou `int`) ou uma sequência que pode ter uma ou duas dimensões.
{: .text-justify}

<h2><a style="color:black" id="constante">Utilizando uma constante</a></h2>

Utilize apenas uma constante quando desejar que todas as barras de erro tenham o mesmo tamanho. Por exemplo, vamos supor que o desvio padrão das temperaturas para os três dias seja de 3 °C:
{: .text-justify}

```python
plt.figure(figsize=(8,6))
plt.errorbar(dias, media, yerr=3)
plt.show()
```

*Figura 1* - Gráfico de erros relacionando a temperatura média na cidade de Birigui-SP em três dias diferentes do ano de 2021 - barras de tamanho fixo.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-erros/29/grafico-erros-01.png" alt="gráfico de dispersão desenhado com o **matplotlib** relacionando o dia e a temperatura média do dia, com as barras de tamanho fixo" >
{: .text-center}

<br>


<h2><a style="color:black" id="sequencia-uma-dimensao">Utilizando uma sequência de uma única dimensão</a></h2>

Essa é a forma mais útil, pois cada elemento da sequência irá representar o erro do respectivo ponto. Por exemplo, podemos passar a variável `desv_pad` para o parâmetro `yerr`:
{: .text-justify}

```python
plt.figure(figsize=(8,6))
plt.errorbar(dias, media, yerr=desv_pad)
plt.show()
```

*Figura 2* - Gráfico de erros relacionando a temperatura média na cidade de Birigui-SP em três dias diferentes do ano de 2021 - barras de tamanho baseado no desvio padrão.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-erros/29/grafico-erros-02.png" alt="gráfico de dispersão desenhado com o matplotlib relacionando o dia e a temperatura média do dia, com as barras de tamanho baseado no desvio padrão" >
{: .text-center}

<br>


<h2><a style="color:black" id="sequencia-duas-dimensoes">Utilizando uma sequência com duas dimensões</a></h2>

Ao utilizar esta forma, é possível especificar o tamanho da barra acima e/ou abaixo do ponto, de modo que fiquem com tamanhos diferentes. Por exemplo, para deixar a barra superior representando 5 °C e a barra inferior representando 1 °C, basta passar uma `list` contendo duas `lists`, da seguinte forma:
{: .text-justify}

```python
plt.figure(figsize=(8,6))
plt.errorbar(dias, media, yerr=[[1,1,1], [5,5,5]])
plt.show()
```


*Figura 3* - Gráfico de erros relacionando a temperatura média na cidade de Birigui-SP em três dias diferentes do ano de 2021 - barras com tamanho personalizado.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-erros/29/grafico-erros-03.png" alt="gráfico de dispersão desenhado com o matplotlib relacionando o dia e a temperatura média do dia, com as barras de tamanho personalizado" >
{: .text-center}

<br>


Observe que foi passado para o `yerr` uma `list` que contém duas `list`. A primeira `list` interna (`[1,1,1]`) irá determinar o tamanho da barra abaixo do ponto. A segunda `list` interna (`[5,5,5]`) irá determinar o tamanho da barra acima do ponto.
{: .text-justify}

**Atenção:** As sequências internas devem ter o mesmo tamanho do que as sequências passadas para `x` e `y`.
{: .text-justify}

<form id = "quiz" name = "quiz">

<p><strong>Qual a função de passar uma lista de duas dimensões para parâmetro yerr em plt.errorbar()?</strong></p>

<input type = "radio" id = "mc" name = "question1" value = "a"> Inserir uma barra de mesmo tamanho em todos os pontos do gráfico
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "b"> Inserir uma barra de tamanho diferente, acima e abaixo, de cada ponto do gráfico
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "c"> Um erro será retornado caso uma lista de duas dimensões seja passada para o parâmetro yerr
<p style="font-size: 50%"></p>
<p></p>
<input id = "button" type = "button" class="btn btn--info" value = "Enviar" onclick = "check();">
</form>

<div id = "after_submit">
<p style="font-size: 120%" id = "message"></p>
</div>



<p style="text-align: center">
  <a href="/Curso-matplotlib-28" class="btn btn--success">Anterior</a>
  <a href="/Curso-matplotlib-30" class="btn btn--success">Próximo</a>
</p>


<script>
function check(){
	var question1 = document.quiz.question1.value;
	var messages = [" Incorreto! 😔 <br> Para inserir uma barra de mesmo tamanho em todos os pontos do gráfico, é necessário passar uma constante para o parâmetro <code>yerr</code>",
  "🎉 Correto! 🥳️  <br>",
  " 😔 Incorreto! <br> Ao passar uma lista de duas dimensões para o parâmetro <code>yerr</code> em <code>plt.errorbar()</code>, uma barra de tamanho personalizado (acima e abaixo) será inserida em cada ponto do gráfico",
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
