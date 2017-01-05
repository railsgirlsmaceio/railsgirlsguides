---
layout: default
title: Desenvolvimento Guiado por Testes
permalink: test-driven-development
---

# Desenvolvimento Guiado por Testes

*Escrito por Gregory McIntyre, [@gregmcintyre](https://twitter.com/gregmcintyre)*

*Traduzido por Marina Limeira, [@marinalimeira_](https://twitter.com/marinalimeira_)

Este exercício tem como objetivo te ensinar o que quer dizer *Desenvolvimento Guiado por Testes* (TDD).

## Background information

**Numerais Romanos**

Se você não está familiar com números Romanos, por favor leia
[como números romanos funcionam][Roman numerals] antes de continuar.

Em resumo, aqui estão alguns exemplos de como romanos escrevem números:

<style>
.roman-table th,
.roman-table td { padding: 0 1rem; }
.roman-table thead tr { border-bottom: 1px solid black; }
.roman-table tr:nth-child(even) td { background-color: #eee; }
</style>

<table class="roman-table">
  <thead>
    <tr>
      <th>Hindu-Arábico</th>
      <th>Romano</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>1</td>
      <td><tt>I</tt></td>
    </tr>
    <tr>
      <td>4</td>
      <td><tt>IIII</tt> (or <tt>IV</tt>)</td>
    </tr>
    <tr>
      <td>5</td>
      <td><tt>V</tt></td>
    </tr>
    <tr>
      <td>6</td>
      <td><tt>VI</tt></td>
    </tr>
    <tr>
      <td>7</td>
      <td><tt>VII</tt></td>
    </tr>
    <tr>
      <td>9</td>
      <td><tt>VIIII</tt> (or <tt>IX</tt>)</td>
    </tr>
    <tr>
      <td>10</td>
      <td><tt>X</tt></td>
    </tr>
    <tr>
      <td>50</td>
      <td><tt>L</tt></td>
    </tr>
    <tr>
      <td>100</td>
      <td><tt>C</tt></td>
    </tr>
    <tr>
      <td>500</td>
      <td><tt>D</tt></td>
    </tr>
    <tr>
      <td>1000</td>
      <td><tt>M</tt></td>
    </tr>
  </tbody>
</table>

Nós iremos escrever um programa que recebe um valor inteiro na coluna esquerda
e calcula o valor na string equivalente na coluna direita. Se nós finalizarmos
isto, iremos então fazer a *subtração de dígitos* como em *IV*.

**Guia para trabalhar em grupo**

Nós encorajamos fazer este exercícios em um grupo de 2-4 pessoas. As regras que
governam como isto funcionam são muito similares a como programadores fazem *programação
em par* e este exercício tem a intenção de te mostrar esta prática.

- Cada grupo possui uma **pessoa no comando** com um notebook e o editor de texto *Sublime Text* prontos.
- Todos os outros devem **fechar seus notebooks** e sentar ao redor de quem está no comando.
- Vocês todos irão regurlarmente levantar-se e **rodar as cadeiras** para que a próxima
pessoa esteja no comando. Os passos abaixo explicam quando fazer isso.
- Escolha alguém para começar no comando. Aquela pessoa deverá seguir todos os passos
até que a troca de assentos seja mencionada.

**Coach:** Explique como programação em par pode ser útil.

## *1.* Código inicial

Copie este código em um arquivo chamado `roman.rb`:

{% highlight ruby %}
def roman(n)
  return "?"
end

require "minitest/spec"
require "minitest/autorun"

describe "roman" do
  it "converte o número 1 na string I" do
    roman(1).must_equal "I"
  end
end
{% endhighlight %}

**Rode seus testes**

Se você utiliza *Sublime Text* no Linux, OSX Mavericks (ou superior) ou Windows, você
pode rodar os testes pressionando <kbd>Ctrl</kbd>+<kbd>B</kbd>. Caso contrário, você pode digitar
o seguinte no seu terminal:

{% highlight sh %}
ruby roman.rb
{% endhighlight %}

**Saída**

Você deverá ver a seguinte saída dos testes:

{% highlight sh %}
roman#test_0001_converte o número 1 na string I [tdd1.rb:11]:
Expected: "I"
  Actual: "?"

1 tests, 1 assertions, 1 failures, 0 errors, 0 skips
{% endhighlight %}

Reserve um momento para ler esta saída com cuidado. Há bastante informação.

Seus testes agora estão **vermelhos**, ou seja, um ou mais testes estão falhando. Você pode
perceber que você possui um teste falhando checando o resumo no final: `1 tests, 1
assertions, 1 failures, 0 errors, 0 skips`.

**Levante-se** e de o comando a próxima pessoa.

**Coach:** Explique como TDD pode ser útil

## *2.* Faça o teste passar

Agora é hora de fazer o teste passar. Faça como você achar melhor. Está bem se a
mudança é apenas uma condição extra `if` ou um caractere. De fato, isso é encorajado:
você geralmente não deveria escrever código desnecessário. Se você está preso,
você pode pedir a opinião de pessoas próximas.

Aqui está uma maneira de como você pode fazer este primeiro teste passar, apenas
para te deixar no ritmo das coisas:

{% highlight ruby %}
def roman(n)
  return "I"
end
{% endhighlight %}

Isso pode parecer engraçado, mas é uma solução válida porque faz todos os testes
passarem. Quando todos os testes passam, nós chamamos de **verde**.

## *3.* Refatore seu código

Olhe seu código e decida se é uma boa ideia **refatorar-lo** (limpar o código e
deixá-lo mais fácil de ler). Se você não decidir refatorar, pule este passo.

**Dica**: É uma boa hora para refatorar quando você notar *repetição*. Se você preferir,
pode também refatorar os testes.

Rode seus testes após refatorar. Se eles falharem, você acidentalmente quebrou alguma coisa.


**Coach:** Explique como focar em algo pequeno o suficiente para testar pode ser útil.

## *4.* Escreva um novo teste que falha

Se vocês todos concordam que o código deve funcionar no geral, e você não consegue pensar
em outros casos de teste e tudo passa, você pode parar por aqui. Você ganhou!

Caso contrário, seu último trabalho no comando é escrever um novo teste. Nós atualmente 
temos um teste que checa se o número 1 é transformado em `"I"`, mas nós precisamos
adicionar mais testes para verificar que todos os outros números são convertidos como esperado.
Quando você adicionar um novo teste para outro número, lembre-se de rodar os testes para
ver seu teste falhando. Se você está preso, existem algumas sugestões no final da página.

Você pode copiar e colar o teste anterior e alterá-lo. Você pode altera-lo para
ser o que você quiser. Seus testes deverão p

Você pode copiar e colar o texto anterior e alterá-lo. Você pode alterá-lo para
ser qualquer coisa que você quiser. Seus testes devem provavelmente testar alguma
outra situação complicada, mas se você sente em voltar e adicionar um caso mais simples,
está ok desde que o teste falhe.

Os outros membros do grupo podem concordar e fazer perguntas ou apontar problemas para você.

Aqui está um exemplo de como expandir seus casos de teste:

{% highlight ruby %}
describe "roman" do
  it "converte o número 1 na string I" do
    roman(1).must_equal "I"
  end

  it "converte o número 2 na string II" do
    roman(2).must_equal "II"
  end
end
{% endhighlight %}

Seus testes agora estão **vermelhos** de novo; ao menos um está falhando.

**Levante-se** e ofereça o comando para a próxima pessoa o seu grupo.

## Repita!

Continue repetindo os passos 2 a 4, tendo certeza de continuar trocando ao fim do passo 4.
Você terá terminado quando seu time sentir que está tudo pronto.

Não se preocupe em finalizar todos os acasos. O objetivo é praticar os passos e aprender
a trabalharem juntos dessa maneira. Se acostume a escrever testes e faze-los passar.
Pratique. Boa sorte!

## Dicas

Se você está sem ideias, aqui está uma lista de numerais romanos para escrever casos
de teste, nesta ordem. Note a maneira que a complexidade aumenta.

:--------- | :-----------
Entrada    | Saída
:--------- | :-----------
 `1`       | `"I"`
 `5`       | `"V"`
 `4`       | `"IIII"`
 `6`       | `"VI"`
 `7`       | `"VII"`
 `10`      | `"X"`

Se você chegou até aqui, você ganha crédito parcial. Romanos costumavam utilizar `IIII` para 4.
É por isso que 4 em um relógio analogico é escrito como `IIII`. Mais tarde, foram adicionados
dígitos *subtrativos*. Estes são mais difíceis de programar. Quando você se sentir
confiante de que seu programa funciona para todos os números acima, tente lidar com 
dígitos subtrativos.

:--------- | :-----------
Entrada    | Saída
:--------- | :-----------
`4`        | `"IV"`
`14`       | `"XIV"`
`2896`     | `"MMDCCCXCVI"`

[Roman numerals]: http://www.onlineconversion.com/roman_numerals_advanced.htm
