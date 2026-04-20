# Estudo de Caso A1 - O Problema da Entrega Inteligente

**Aluno:** Matheus Aredes Santos Silva  
**Disciplina:** Estruturas de Dados e Analise de Algoritmos  
**Professor:** Alexandre Montanha

## Questao 1 - Classificacao do Problema

### a)
Na minha opiniao, esse problema pode ser considerado **NP-Completo**, pensando na versao de decisao. Eu entendi assim porque ele parece com problemas conhecidos como o **TSP (Problema do Caixeiro Viajante)** e o **VRP (Problema de Roteamento de Veiculos)**, que sao problemas dificeis.

De um jeito mais simples:

- **P**: problema que da para resolver rapido
- **NP**: problema que talvez seja dificil de resolver, mas e mais facil de verificar a resposta
- **NP-Completo**: problema que e bem dificil e parecido com outros problemas dificeis da computacao

No caso da FastBite, se alguem ja entregar uma rota pronta, da para verificar. O mais dificil e descobrir qual e a melhor combinacao entre pedidos, entregadores e ordem das entregas.

### b)
Da para relacionar o problema da FastBite com o **TSP (Problema do Caixeiro Viajante)**.

Se a gente imaginar um caso mais simples, com:

- um entregador so
- varios lugares para visitar
- distancias entre esses lugares

isso fica parecido com o TSP, porque o entregador teria que passar pelos pontos em uma ordem que gaste menos tempo.

No caso da FastBite e ainda mais complicado, porque:

- tem varios entregadores
- tem limite de pedidos por entregador
- tem pedidos urgentes
- o entregador tem que pegar no restaurante antes de entregar ao cliente

Entao, se uma versao mais simples ja parece com o TSP, isso mostra que o problema da FastBite tambem e bem dificil.

### c)
A forca bruta e inviavel porque teria combinacao demais para testar.

Por exemplo, com **8 pedidos**, so para mudar a ordem desses pedidos ja teriamos:

`8! = 40.320`

Ou seja, so nessa parte ja aparecem **40.320 possibilidades**.

Mas o problema nao e so colocar em ordem. O sistema tambem precisa decidir:

- qual pedido vai para qual entregador
- em que ordem cada entregador vai fazer as entregas

Entao o total real fica maior ainda.

Na minha visao, isso mostra que testar tudo na forca bruta nao vale a pena, porque o sistema precisa responder muito rapido. Como a FastBite tem que decidir em ate **2 segundos**, nao da para ficar testando milhares de possibilidades.

A complexidade cresce muito rapido, entao da para dizer que ela e parecida com crescimento **fatorial**, o que acaba sendo inviavel em um sistema real.

## Questao 2 - Abordagem Gulosa

### a)
O algoritmo guloso funciona assim:

1. Pega um pedido que ainda nao foi atribuido.
2. Ve qual entregador esta mais perto do restaurante.
3. Entrega esse pedido para ele, se ele ainda tiver capacidade.
4. Faz isso ate acabar os pedidos.
5. Depois, monta a rota indo sempre para o ponto mais perto.

No cenario dado, uma possibilidade seria:

- **P1** vai para o **E1**, porque ele esta mais perto do restaurante
- **P2** tambem vai para o **E1**
- **P3** vai para o **E2**
- **P4** vai para o **E2**
- **P5** vai para o **E3**, se o E2 ja estiver cheio

Entao ficaria assim:

- **E1:** P1 e P2
- **E2:** P3 e P4
- **E3:** P5

Depois disso, cada entregador vai seguindo para o ponto mais proximo.

### b)
Esse algoritmo e guloso porque ele escolhe o que parece melhor naquele momento.

No caso:

- escolhe o entregador mais perto
- depois escolhe o proximo ponto mais perto

Ele resolve uma parte por vez, sem analisar muito o resultado final.

### c)
Um exemplo simples seria assim:

- o **E1** esta mais perto de um restaurante agora
- mas o **E2** estaria em uma posicao melhor para continuar outras entregas depois

Mesmo assim, o algoritmo escolhe o **E1** so porque ele esta mais perto naquele instante.

Isso pode acabar piorando o resto da rota. Entao, no final, a resposta gulosa pode nao ser a melhor.

### d)
Se tiver **n pedidos** e **m entregadores**, o algoritmo compara os pedidos com os entregadores e depois monta as rotas.

Por isso, a complexidade pode ser escrita assim:

**O(n.m + n^2)**

Basicamente quando o numero de pedidos aumenta, o trabalho do algoritmo tambem aumenta.

## Questao 3 - Programacao Dinamica e Divisao e Conquista

### a)
Sim, a **Programacao Dinamica** pode ser usada no problema de um entregador so, com os pedidos ja separados para ele.

O subproblema seria mais ou menos:

"Qual e o menor custo para sair do ponto atual e visitar os pontos que ainda faltam?"

A vantagem da Programacao Dinamica e que ela reaproveita contas ja feitas. Isso ajuda a nao repetir calculos.

Mas mesmo assim ela pode ficar pesada, porque conforme aumenta a quantidade de pedidos, a quantidade de calculos e de combinacoes cresce muito.

Entao ela pode gastar bastante tempo e bastante memoria.

Na pratica, eu acho que com muitos pedidos para um entregador isso ja fica complicado. Em tempo real, talvez com **15 ou 20 pedidos** ja comece a pesar bastante, ou ate antes, dependendo do sistema.

Entao ela pode funcionar em casos menores, mas nao parece a melhor escolha para momentos de pico.

### b)
A **Divisao e Conquista** pode ajudar separando a cidade em partes menores.

Por exemplo:

- zona norte
- zona sul
- zona central

Assim, o sistema resolve uma parte de cada vez, em vez de tentar resolver tudo junto.

Isso ajuda quando os pedidos de cada regiao estao mais concentrados.

O problema e quando o pedido fica perto da fronteira de uma zona. Nesses casos, talvez um entregador de outra regiao fosse melhor, mas a divisao pode atrapalhar isso.

Entao essa abordagem ajuda bastante, mas nao resolve tudo sozinha.

## Questao 4 - Comparacao das Abordagens

| Criterio | Greedy | Programacao Dinamica | Divisao e Conquista |
|---|---|---|---|
| Qualidade da solucao | Boa, mas nem sempre a melhor | Muito boa em casos pequenos | Media |
| Complexidade de tempo | Baixa | Alta | Media |
| Complexidade de espaco | Baixa | Alta | Media |
| Viabilidade em tempo real (<= 2s) | Boa | Ruim em casos grandes | Boa |
| Escalabilidade com aumento de n | Boa | Ruim | Boa |
| Facilidade de adaptacao a mudancas | Boa | Mais dificil | Media |

Na minha opiniao, a melhor opcao para a FastBite seria usar a abordagem **gulosa** como base, porque ela e mais rapida. A **Programacao Dinamica** pode ser boa em casos pequenos, mas pesa bastante quando o problema cresce. Ja a **Divisao e Conquista** ajuda a organizar por regioes. Entao eu usaria uma solucao gulosa junto com a separacao por areas e alguns ajustes depois.

## Questao 5 - Solucao de Engenharia Real

### a)
Heuristica e uma maneira de achar uma solucao **boa o suficiente**, mesmo que nao seja a melhor de todas.

Ela e melhor nesse caso porque:

- o sistema tem pouco tempo
- existem muitas combinacoes
- uma resposta boa e rapida vale mais do que uma resposta perfeita e demorada

### b)
Pensando de um jeito mais pratico, eu acho que a FastBite primeiro tentaria organizar os pedidos por partes da cidade, para nao misturar tudo de uma vez. Depois disso, o sistema poderia fazer uma distribuicao inicial mais rapida, colocando os pedidos nos entregadores que parecem estar em melhor posicao naquele momento.

Se depois dessa primeira escolha algumas rotas ficarem muito ruins, o sistema ainda poderia testar pequenas mudancas, como passar um pedido para outro entregador ou trocar a ordem de duas entregas. Nao precisa testar tudo, so algumas mudancas simples que possam melhorar o resultado.

Tambem acho importante ter um limite de tempo bem claro. Se estiver chegando no tempo maximo, o sistema para e usa a melhor resposta que conseguiu ate ali. Para mim, faz mais sentido uma resposta boa e rapida do que uma perfeita que demora demais.

Eu acho essa ideia boa porque junta rapidez com uma tentativa de melhorar o resultado.

### c)
Vale a pena buscar a solucao otima quando o problema e pequeno e da para gastar mais tempo calculando.

Um exemplo seria uma operacao com poucos pedidos, como **3 ou 4 entregas programadas**. Nesse caso, daria para calcular melhor sem atrapalhar o tempo de resposta.

## Questao 6 - Reflexao Critica

Em sistemas grandes, "bom o suficiente" muitas vezes e a melhor escolha. Isso acontece porque tentar achar a solucao perfeita pode demorar demais. No caso da FastBite, a resposta precisa sair em ate 2 segundos. Entao nao adianta achar a melhor rota se ela vier tarde. A complexidade computacional mostra que alguns problemas crescem muito rapido. Por isso, em varios casos, e melhor usar uma solucao mais rapida e que funcione bem, mesmo sem ser perfeita.
