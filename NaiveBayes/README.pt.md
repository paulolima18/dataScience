[![Price](https://img.shields.io/badge/price-FREE-0098f7.svg)](https://github.com/froala/design-blocks/blob/master/LICENSE)

* Ler o documento num linguagem diferente: [Inglês](README.md), [Português](README.pt.md)

# Classificação Naive Bayes

Os modelos Naive Bayes são um grupo de algoritmos de classificação extremamente rápidos e simples que costumam ser adequados para conjuntos de dados de dimensões muito altas.
Por serem tão rápidos e terem poucos parâmetros ajustáveis, eles acabam sendo muito úteis como uma linha de base rápida e suja para um problema de classificação.
Esta seção se concentrará em uma explicação intuitiva de como os classificadores Bayes ingênuos funcionam, seguida por alguns exemplos deles em ação em alguns conjuntos de dados.

## Datasets testados
- [GaussianNB](/NaiveBayes/gaussian_nb.ipynb)
- [MultinomialNB](/NaiveBayes/multinomial_nb.ipynb)

## Classificação Bayesiana

Classificadores Naive Bayes são construídos em métodos de classificação Bayesianos.
Eles se baseiam no teorema de Bayes, que é uma equação que descreve a relação de probabilidades condicionais de quantidades estatísticas.
Na classificação bayesiana, estamos interessados ​​em encontrar a probabilidade de um rótulo dados alguns recursos observados, que podemos escrever como **P(L∣ features)**.
O teorema de Bayes nos diz como expressar isso em termos de quantidades que podemos calcular mais diretamente:

**P(L ∣ features) =  P(features ∣ L) P(L) / P(features)**

Se estivermos tentando decidir entre dois rótulos - vamos chamá-los de **L1** and **L2** então uma maneira de tomar essa decisão é calcular a razão das probabilidades posteriores para cada rótulo:

**P(L1 | features) / P (L2 | features) = P (features | L1) P(L1) / P(features | L2) P(L2)**

Tudo que precisamos agora é algum modelo pelo qual possamos calcular **P(features | Li)** para cada rótulo.
Esse modelo é chamado de *generative model*( modelo generativo) porque especifica o processo aleatório hipotético que gera os dados.
Especificar esse modelo gerador para cada rótulo é a parte principal do treinamento desse classificador bayesiano.
A versão geral de tal etapa de treinamento é uma tarefa muito difícil, mas podemos torná-la mais simples por meio do uso de algumas suposições simplificadoras sobre a forma desse modelo.

É aqui que entra o *Naive*(ingênuo) em *Naive Bayes": se fizermos suposições muito ingênuas sobre o modelo gerador para cada rótulo, podemos encontrar uma aproximação grosseira do modelo generativo para cada classe e, em seguida, prosseguir com a classificação bayesiana.
Diferentes tipos de classificadores Bayes ingênuos baseiam-se em diferentes suposições ingênuas sobre os dados, e examinaremos alguns deles nas seções seguintes.


## Quando usar Naive Bayes

Como os classificadores bayesianos ingênuos fazem suposições tão rigorosas sobre os dados, eles geralmente não terão um desempenho tão bom quanto um modelo mais complicado.
Dito isso, eles têm várias vantagens:

- Eles são extremamente rápidos para treinamento e previsão
- Eles fornecem uma previsão probabilística direta
- Muitas vezes são facilmente interpretáveis
- Eles têm muito poucos (se houver) parâmetros ajustáveis

Essas vantagens significam que um classificador bayesiano ingênuo costuma ser uma boa escolha como uma classificação de linha de base inicial.
Se funcionar adequadamente, então parabéns: você tem um classificador muito rápido e muito interpretável para o seu problema.
Se não funcionar bem, você pode começar a explorar modelos mais sofisticados, com algum conhecimento básico de quão bem eles devem funcionar.

Os classificadores Naive Bayes tendem a ter um desempenho especialmente bom em uma das seguintes situações:

- Quando as suposições ingênuas realmente correspondem aos dados (muito raro na prática)
- Para categorias muito bem separadas, quando a complexidade do modelo é menos importante
- Para dados dimensionais muito elevados, quando a complexidade do modelo é menos importante

Os dois últimos pontos parecem distintos, mas na verdade estão relacionados: conforme a dimensão de um conjunto de dados cresce, é muito menos provável que quaisquer dois pontos sejam encontrados próximos (afinal, eles devem estar próximos em * cada dimensão * para estar perto no geral).
Isso significa que os clusters em dimensões altas tendem a ser mais separados, em média, do que os clusters em dimensões baixas, supondo que as novas dimensões realmente adicionem informações.
Por esse motivo, classificadores simplistas como Bayes ingênuo tendem a funcionar tão bem ou melhor do que classificadores mais complicados conforme a dimensionalidade aumenta: uma vez que você tenha dados suficientes, até mesmo um modelo simples pode ser muito poderoso.

