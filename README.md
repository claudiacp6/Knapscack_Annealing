# Knapscack_Annealing

1. Codifica um algoritmo capaz de fazer uma procura pelo ótimo global.
   1.1 Funçao 'create_ksp'
   1.2 Funçao objective_function
   1.3 Funçao criar_vizinho
   1.4 Funçao simulated_annealing

3. Testa várias combinações de Temperatura Inicial e de método de atualização de Temperatura, e comenta sobre o impacto que esta atualização e valor tem no resultado final do modelo.
  
High Initial Temperature:

Impact: A high initial temperature increases the likelihood of accepting worse solutions early in the process. This can help in exploring a broader solution space but may slow down convergence.
Recommendation: Useful when the search space is complex and vast, or when the solution space has multiple local optima.

Low Initial Temperature:

Impact: A low initial temperature makes the algorithm more greedy and focused on exploitation rather than exploration. It may converge quickly but could get stuck in local optima.
Recommendation: Suitable when the solution space is relatively simple or when there's confidence in the starting solution.

4. O que acontece se o item adicionado for aquele que tiver um rácio de utilidade e peso maior em todas as iterações? A solução final com este método é melhor que a solução original?

   Impacto de Adicionar o Item com a Maior Razão Utilidade/Peso em Todas as Iterações:
Vantagens:

Eficiência na Utilização do Peso: O algoritmo está priorizando itens que oferecem a melhor relação de utilidade em relação ao peso. Isso pode levar a uma utilização mais eficiente da capacidade total da mochila.
Desvantagens:

Falta de Diversidade na Escolha: Se o algoritmo sempre escolhe o item com a maior razão utilidade/peso, pode não explorar adequadamente outros itens que, mesmo tendo uma razão um pouco menor, poderiam contribuir para uma solução globalmente melhor.
Solução Final Melhor que a Original?
A resposta a essa pergunta depende das características específicas do problema da mochila em questão:

Se a Melhor Razão é Suficiente: Se a razão utilidade/peso do item escolhido em todas as iterações é suficientemente alta e a capacidade da mochila é utilizada de maneira eficiente, então a solução final provavelmente será boa.

Se Outros Fatores Importam: No entanto, é crucial considerar se outros fatores estão sendo negligenciados. Por exemplo, se existirem itens com valores muito altos, mesmo que seus rácios utilidade/peso sejam um pouco menores, a solução final poderia ser melhor se esses itens fossem incluídos.
