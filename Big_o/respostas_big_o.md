# Respostas dos Exercicios de Big-O

## Exercicio 1
Complexidade: `O(1)`

Justificativa: Esse codigo so olha o primeiro item da lista. Mesmo se a lista for grande, ele nao percorre ela toda.

## Exercicio 2
Complexidade: `O(n)`

Justificativa: Aqui ele passa por todos os elementos da lista para somar. Entao o tempo cresce junto com a quantidade de itens.

## Exercicio 3
Complexidade: `O(log n)`

Justificativa: A busca binaria vai cortando a lista pela metade a cada passo. Por isso ela nao precisa olhar elemento por elemento.

## Exercicio 4
Complexidade: `O(n^2)`

Justificativa: Tem um `for` dentro do outro para comparar pares da lista. Quando a lista cresce, a quantidade de comparacoes cresce bastante.

## Exercicio 5
Complexidade: `O(n^2)`

Justificativa: Primeiro ele faz um laco simples, mas depois faz dois lacos juntos para imprimir todos os pares. O que mais pesa e essa parte dos dois lacos.

## Exercicio 6
Complexidade: `O(log n)`

Justificativa: O valor de `i` vai dobrando (`1, 2, 4, 8...`). Entao a quantidade de repeticoes cresce devagar em relacao ao tamanho de `n`.

## Exercicio 7
Pulei esse porque achei mais dificil.

## Exercicio 8
Complexidade: `O(n^2)`

Justificativa: Esse algoritmo compara varios elementos repetidas vezes usando dois lacos. No geral ele percorre a lista muitas vezes ate organizar tudo.

## Exercicio 9
Pulei esse porque achei mais dificil.

## Exercicio 10
Pulei esse porque achei mais dificil.
