---
title: "Legendas (Bordas da caixa da legenda)"
data: 2021-08-08
tags: []
header:
  image: "/images/chess.jpg"
  image_description: "Chess pieces"
excerpt: "matplotlib"
locale: "pt-br"
---

<br>


<h2><a style="color:black" id="estilo-borda">Estilo da borda da legenda</a></h2>

É possível alterar os cantos (bordas) da legenda, variando o parâmetro `fancybox` para `True` (padrão), o que deixa as bordas arredondadas, ou para `False`, o que deixa as bordas retas.
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
plt.legend(ncol=2, fancybox=False)
plt.show()
```

*Figura 1* - Caixa da legenda com cantos quadrados.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/legendas/64/legendas-01.png" alt="gráfico de dispersão combinado com gráfico de linhas desenhado com matplotlib, caixa da legenda com cantos quadrados." >
{: .text-center}

<br>

<h2><a style="color:black" id="sombra-caixa">Sombra na caixa da legenda</a></h2>

É possível adicionar uma sombra na caixa da legenda, o que fornece uma noção de profundidade e estilo a caixa da legenda. Para adicionar este efeito, basta passar um `True` para o parâmetro `shadow`. O valor padrão é `False`, que não insere a sombra na caixa da legenda.
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
plt.legend(ncol=2, shadow=True)
plt.show()
```

*Figura 2* - Caixa da legenda com sombreamento.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/legendas/64/legendas-02.png" alt="gráfico de dispersão combinado com gráfico de linhas desenhado com matplotlib, caixa da legenda com sombreamento." >
{: .text-center}

<br>


<h2><a style="color:black" id="cor-fundo">Cor de fundo</a></h2>

Para alterar a cor de fundo da caixa da legenda, basta passar uma `str` com o nome da cor desejada (padrão é `'white'`) para o parâmetro `facecolor`. As cores disponíveis são as mesmas vistas <a href="/Curso-matplotlib-08/#cor-marcadores">anteriormente</a>.
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
plt.legend(ncol=2, shadow=True, facecolor="lightgray")
plt.show()
```

*Figura 3* - Caixa da legenda com cor de fundo cinza.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/legendas/64/legendas-03.png" alt="gráfico de dispersão combinado com gráfico de linhas desenhado com matplotlib, caixa da legenda com de fundo cinza." >
{: .text-center}

<br>

<h2><a style="color:black" id="transparencia-caixa">Transparência da caixa da legenda</a></h2>

Para alterar a transparência da caixa da legenda, basta passar um número `float` entre `0.0` (completamente transparente) e `1.0`(sem nenhuma transparência) para o parâmetro `framealpha`. O valor padrão é `0.8`.
{: .text-justify}

Por exemplo, para uma transparência de `0.1`:

```python
plt.figure(figsize=(8,6))
plt.scatter(cachorro_peso, cachorro_altura, label="Cachorros")
plt.scatter(gatos_peso, gatos_altura, label="Gatos")
plt.plot(pinguins_peso, pinguins_altura, marker="o", c="g", label="Pinguins")
plt.xlabel("Peso (kg)")
plt.ylabel("Altura (cm)")
plt.title("Relação entre peso e altura de diferentes animais")
plt.ylim([0,125])
plt.legend(ncol=2, shadow=True, facecolor="lightgray", loc=7, framealpha=0.1)
plt.show()
```

*Figura 4* - Caixa da legenda com transparência de 0.1.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/legendas/64/legendas-04.png" alt="gráfico de dispersão combinado com gráfico de linhas desenhado com matplotlib, caixa da legenda com transparência de 0.1." >
{: .text-center}

<br>

Já para uma transparência de `0.9`:

```python
plt.figure(figsize=(8,6))
plt.scatter(cachorro_peso, cachorro_altura, label="Cachorros")
plt.scatter(gatos_peso, gatos_altura, label="Gatos")
plt.plot(pinguins_peso, pinguins_altura, marker="o", c="g", label="Pinguins")
plt.xlabel("Peso (kg)")
plt.ylabel("Altura (cm)")
plt.title("Relação entre peso e altura de diferentes animais")
plt.ylim([0,125])
plt.legend(ncol=2, shadow=True, facecolor="lightgray", loc=7, framealpha=0.9)
plt.show()
```

*Figura 5* - Caixa da legenda com transparência de 0.9.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/legendas/64/legendas-05.png" alt="gráfico de dispersão combinado com gráfico de linhas desenhado com matplotlib, caixa da legenda com transparência de 0.9." >
{: .text-center}

<br>

<h2><a style="color:black" id="cor-borda">Cor da borda</a></h2>

Para alterar a cor da borda (padrão `'black'`), passamos o nome da cor, utilizando uma `str`, através do parâmetro `edgecolor`. Observe que por padrão a cor das bordas é preta, mas, visualmente, ela tem um tom acinzentado. Isto ocorre, pois por padrão, as legendas tem transparência de 80%, o que também deixa a cor preta da borda 80% transparente (tom acinzentado).
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
plt.legend(ncol=2, shadow=True, facecolor="lightgray", edgecolor="m")
plt.show()
```

*Figura 6* - Caixa da legenda com borda na cor magenta.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/legendas/64/legendas-06.png" alt="gráfico de dispersão combinado com gráfico de linhas desenhado com matplotlib, caixa da legenda com borda na cor magenta" >
{: .text-center}

<br>

<h2><a style="color:black" id="espessura-borda">Espessura da borda</a></h2>

É possível alterar a espessura da borda da legenda. Entretanto, é necessário acessar as propriedades da legenda criada antes, para depois alterar a espessura. Isto é feito através do `set_linewidth()`, que é acessado através do `get_frame()`, que por sua vez esta em um objeto de legenda.
{: .text-justify}

Dessa forma, precisamos criar um objeto de legenda, o que é feito atribuindo o `plt.legend()`para uma nova variável, da seguinte forma:
{: .text-justify}

```python
leg = plt.legend()
```   

Agora, a variável `leg` contém todas as informações da legenda, inclusive o `get_frame().set_linewidth()`. Basta então passar a nova espessura para borda (número, `int` ou `float`), da seguinte forma:
{: .text-justify}

```python
leg.get_frame().set_linewidth(10)
```

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
leg = plt.legend(ncol=2, shadow=True, facecolor="lightgray", edgecolor="m")
leg.get_frame().set_linewidth(10)
plt.show()
```

*Figura 7* - Caixa da legenda com borda mais espessa.
{: .text-center}
<img style="border: solid 1px black" src="{{ site.url }}{{ site.baseurl }}/images/curso-matplotlib/legendas/64/legendas-07.png" alt="gráfico de dispersão combinado com gráfico de linhas desenhado com matplotlib, caixa da legenda com borda mais espessa" >
{: .text-center}

<br>

<form id = "quiz" name = "quiz">

<p><strong>O que irá ocorrer caso o parâmetro fancybox seja passado como False em plt.legend()?</strong></p>

<input type = "radio" id = "mc" name = "question1" value = "a"> Será adicionado uma "sombra" nas bordas da legenda
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "b"> As bordas das legendas ficarão com os cantos arredondados.
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "c"> As bordas das legendas ficarão com os cantos retos
<p style="font-size: 50%"></p>
<input type = "radio" id = "mc" name = "question1" value = "d"> Não será adicionado uma "sombra" nas bordas das legendas
<p style="font-size: 50%"></p>
<p></p>
<input id = "button" type = "button" class="btn btn--info" value = "Enviar" onclick = "check();">
</form>

<div id = "after_submit">
<p style="font-size: 120%" id = "message"></p>
</div>


<br>


<p style="text-align: center">
  <a href="/Curso-matplotlib-63" class="btn btn--success">Anterior</a>
  <a href="/Curso-matplotlib-65" class="btn btn--success">Próximo</a>
</p>



<script>
function check(){
	var question1 = document.quiz.question1.value;
	var messages = [" Incorreto! 😔 <br> O parâmetro <code>fancybox</code> controla o estilo dos cantos da borda. O parâmetro que controla o estilo de sombra nas legendas é o parâmetro <code>shadow</code>.",
  " 😔 Incorreto! <br> Ao passar <code>False</code> para o parâmetro <code>fancybox</code> os cantos da borda ficarão retos, não arredondados!",
  " 🎉 Correto! 🥳️ <br> Esta é a forma de deixar os cantos das bordas retos!",
  " 🎉 Correto! 🥳️ <br> Caso o parâmetro <code>fancybox</code> receba como valor o <code>bool False</code>, não será adicionado nenhuma sombra as bordas das legendas. Entretanto, o parâmetro <code>fancybox</code> não tem nenhuma relação com a adição de sombra nas bordas das legendas. Este comportamento é controlado através do parâmetro <code>shadow</code>.",
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
