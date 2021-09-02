---
title: "Curso matplotlib - Elementos auxiliares (retas)"
data: 2021-08-01
tags: []
header:
  image: "/images/chess.jpg"
  image_description: "Chess pieces"
excerpt: "matplotlib"
locale: "pt-br"
---

<br>

Em alguns casos é interessante adicionar retas no gráfico com a intenção de separar o gráfico em várias partes, indicar padrões, intervalos de confiança, entre outros motivos. Temos várias formas de adicionar retas, vamos estudar as principais.
{: .text-justify}

<h2><a style="color:black" id="reta-generica">Reta genérica</a></h2>

Para desenhar uma linha genérica que passe por todo o gráfico, podemos utilizar o ```plt.axline()```, que pode ser utilizado de duas formas.
{: .text-justify}

A primeira é passando as coordenadas dos pontos iniciais e finais da reta, para os parâmetros ```xy1``` e ```xy2``` utilizando tuplas com dois elementos cada.
{: .text-justify}


**Exemplo:**

```python
plt.figure(figsize=(8,6))
plt.scatter(x,y)
plt.axline(xy1=(0.5,1), xy2=(1.2,1.5))
plt.show()
```


*Figura 1* - Gráfico de dispersão com reta adicionada utilizando o `plt.axline()`.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-elementos-auxiliares/37/grafico-elementos-auxiliares-01.png" alt="gráfico de dispersão genérico desenhado com o **matplotlib**, como uma reta inserida  " >
{: .text-center}

<br>


A segunda forma é passando a coordenada inicial através do ```xy1```, e o coeficiente angular da reta através do ```slope```.
{: .text-justify}

**Exemplo:**

```python
plt.figure(figsize=(8,6))
plt.scatter(x,y)
plt.axline(xy1=(0.5,1), slope=0.5)
plt.show()
```

*Figura 2* - Gráfico de dispersão com reta adicionada utilizando o `plt.axline()`.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/grafico-elementos-auxiliares/37/grafico-elementos-auxiliares-02.png" alt="gráfico de dispersão genérico desenhado com o **matplotlib**, como uma reta inserida  " >
{: .text-center}

<br>

<form id = "quiz" name = "quiz">

<p><strong>Qual a função do parâmetro slope em plt.axline()?</strong></p>

<input type = "radio" id = "mc" name = "question1" value = "a"> Passar a segunda coordenada da reta
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "b"> Passar o coeficiente linear da reta
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "c"> Passar o coeficiente angular da reta
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "d"> Passar a primeira coordenada da reta
<p style="font-size: 50%"></p>
<p></p>
<input id = "button" type = "button" class="btn btn--info" value = "Enviar" onclick = "check();">
</form>

<div id = "after_submit">
<p style="font-size: 120%" id = "message"></p>
</div>

<br>

<p style="text-align: center">
  <a href="/Curso-matplotlib-36" class="btn btn--success">Anterior</a>
  <a href="/Curso-matplotlib-38" class="btn btn--success">Próximo</a>
</p>

<script>
function check(){
	var question1 = document.quiz.question1.value;
	var messages = [" Incorreto! 😔 <br> O parâmetro <code>slope</code> é utilizado para passar o coeficiente angular da reta! O parâmetro que passa a segunda coordenada da reta é o parâmetro <code>xy2</code>",
  " 😔 Incorreto! 😔  <br> Para desenhar uma reta utilizando o <code>plt.axline()</code> não é necessário passar o valor do intercepto da reta (afinal de contas, o intercepto é apenas o ponto da reta onde x = 0, e este valor não é <i>necessário</i> para desenhar nenhum reta )",
  "🎉 Correto! 🥳️ <br> Inclusive, <code>slope</code> <i>significa</i> coeficiente angular ",
  " 😔 Incorreto! <br> O parâmetro <code>slope</code> é utilizado para passar o coeficiente angular da reta! O parâmetro que passa a primeira coordenada da reta é o parâmetro <code>xy1</code>",
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
