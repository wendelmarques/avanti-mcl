# Atividade 01 (ATIV-01)

---

## 1. Explique, com suas palavras, o que é machine learning? 

Machine learning (aprendizado de máquina) é uma área da inteligência artificial em que um sistema aprende padrões a partir de dados, em vez de seguir regras explicitamente programadas. Ao invés de o programador escrever "se X, faça Y" para cada situação, o algoritmo recebe exemplos (dados) e ajusta seus parâmetros internos para conseguir generalizar e fazer previsões ou classificações em dados novos, que nunca viu antes.
 

---

## 2. Explique o conceito de conjunto de treinamento, conjunto de validação e conjunto de teste em machine learning.

- **Conjunto de treinamento:** é a parte dos dados usada para o modelo "aprender", ajustando seus parâmetros internos com base nesses exemplos.
- **Conjunto de validação:** usado durante o desenvolvimento para ajustar hiperparâmetros (como profundidade de uma árvore, taxa de aprendizado, etc.) e comparar diferentes versões do modelo, sem contaminar a avaliação final com os dados de teste.
- **Conjunto de teste:** um conjunto totalmente separado, usado apenas ao final, para avaliar o desempenho real do modelo em dados que ele nunca viu — simulando como ele se comportaria em produção.
---

## 3. Explique como você lidaria com dados ausentes em um conjunto de dados de treinamento.

Algumas estratégias comuns:

- **Remoção:** excluir linhas ou colunas com muitos valores ausentes, quando a perda de informação é aceitável.
- **Imputação simples:** preencher os valores ausentes com a média, mediana ou moda (para dados numéricos) ou com a categoria mais frequente (para dados categóricos).
- **Imputação avançada:** usar modelos (como KNN Imputer ou regressão) para estimar o valor ausente com base em outras colunas.
- **Criar uma variável indicadora:** adicionar uma coluna binária informando se aquele valor era ausente, o que pode preservar informação relevante, já que a própria ausência pode ser um padrão.

A escolha da estratégia depende da quantidade de dados ausentes, do motivo da ausência e do impacto que isso pode ter no modelo final.

---

## 4. O que é uma matriz de confusão e como ela é usada para avaliar o desempenho de um modelo preditivo?

A matriz de confusão é uma tabela que mostra o desempenho de um modelo de classificação, comparando os valores previstos com os valores reais. Para um problema binário, ela possui 4 células:

| | Previsto Positivo | Previsto Negativo |
|---|---|---|
| **Real Positivo** | Verdadeiro Positivo (VP) | Falso Negativo (FN) |
| **Real Negativo** | Falso Positivo (FP) | Verdadeiro Negativo (VN) |

A partir dela, calculam-se métricas como acurácia, precisão, recall e F1-score, que ajudam a entender não apenas se o modelo acerta, mas que tipo de erro ele comete. Por exemplo, em um diagnóstico médico, um falso negativo (dizer que a pessoa está saudável quando não está) pode ser muito mais grave do que um falso positivo.

---

## 5. Em quais áreas você acha mais interessante aplicar algoritmos de machine learning?

Embora o uso de IA em áreas vitais como saúde (no diagnóstico precoce de doenças) e agricultura (na otimização de colheitas) tenha um impacto social imenso, eu acho particularmente interessante aplicar algoritmos de machine learning no ambiente corporativo e no ecossistema de startups. O uso de modelos preditivos para estruturar estratégias de go-to-market (GTM) para o lançamento de novos produtos, prever a rotatividade de clientes (churn rate) ou aplicar inteligência na escala de vendas e relacionamento B2B me chama muita atenção. 
