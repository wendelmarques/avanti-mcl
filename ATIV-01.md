# Atividades 01 E 02

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

# Atividade 02 (ATIV-02)

---

## Parte 1 — Python

### 1. Escreva uma função que receba uma lista de números e retorne outra lista com os números ímpares.

```python
def filtrar_impares(numeros):
    return [n for n in numeros if n % 2 != 0]

# Exemplo:
filtrar_impares([1, 2, 3, 4, 5, 6, 7, 8, 9, 10])
# -> [1, 3, 5, 7, 9]
```

Percorre a lista com uma list comprehension e mantém apenas os números cujo resto da divisão por 2 é diferente de zero.

---

### 2. Escreva uma função que receba uma lista de números e retorne outra lista com os números primos presentes.

```python
def eh_primo(n):
    if n < 2:
        return False
    for i in range(2, int(n ** 0.5) + 1):
        if n % i == 0:
            return False
    return True

def filtrar_primos(numeros):
    return [n for n in numeros if eh_primo(n)]

# Exemplo:
filtrar_primos([1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11])
# -> [2, 3, 5, 7, 11]
```

Uma função auxiliar `eh_primo` testa a divisibilidade apenas até a raiz quadrada do número, uma otimização válida porque, se existisse um divisor maior que a raiz, também existiria um divisor menor correspondente.

---

### 3. Escreva uma função que receba duas listas e retorne outra lista com os elementos que estão presentes em apenas uma das listas.

```python
def apenas_em_uma(lista1, lista2):
    return list(set(lista1).symmetric_difference(set(lista2)))

# Exemplo:
apenas_em_uma([1, 2, 3, 4], [3, 4, 5, 6])
# -> [1, 2, 5, 6]
```

Utiliza a diferença simétrica de conjuntos (`symmetric_difference`), que retorna os elementos que existem em uma lista, mas não na outra, excluindo os elementos comuns (3 e 4, no exemplo).

---

### 4. Dada uma lista de números inteiros, escreva uma função para encontrar o segundo maior valor na lista.

```python
def segundo_maior(numeros):
    unicos = sorted(set(numeros), reverse=True)
    if len(unicos) < 2:
        raise ValueError("A lista precisa ter ao menos dois valores distintos")
    return unicos[1]

# Exemplo:
segundo_maior([5, 1, 9, 9, 3, 7])
# -> 7
```

Primeiro remove duplicatas com `set()` — importante, pois se o maior valor aparecer repetido ele não deve ocupar as duas primeiras posições — depois ordena de forma decrescente e retorna o segundo elemento.

---

### 5. Crie uma função que receba uma lista de tuplas, cada uma contendo o nome e a idade de uma pessoa, e retorne a lista ordenada pelo nome das pessoas em ordem alfabética.

```python
def ordenar_por_nome(pessoas):
    return sorted(pessoas, key=lambda pessoa: pessoa[0])

# Exemplo:
ordenar_por_nome([("Carlos", 30), ("Ana", 25), ("Bruno", 40)])
# -> [('Ana', 25), ('Bruno', 40), ('Carlos', 30)]
```

Usa `sorted()` com uma `key` que extrai o primeiro elemento da tupla (o nome), garantindo a ordenação alfabética.

---

## Parte 2 — Visualização e análise de dados

### 6. Como identificar e tratar outliers em uma coluna numérica usando desvio padrão ou quartis?

**Pelo desvio padrão** (assume distribuição aproximadamente normal): considera-se outlier todo valor que está a mais de 2 ou 3 desvios padrão da média.

```python
import pandas as pd

media = df['coluna'].mean()
desvio = df['coluna'].std()
limite_inferior = media - 3 * desvio
limite_superior = media + 3 * desvio

outliers = df[(df['coluna'] < limite_inferior) | (df['coluna'] > limite_superior)]
```

**Pelo IQR (quartis)** — método mais robusto, não assume normalidade:

```python
Q1 = df['coluna'].quantile(0.25)
Q3 = df['coluna'].quantile(0.75)
IQR = Q3 - Q1

limite_inferior = Q1 - 1.5 * IQR
limite_superior = Q3 + 1.5 * IQR

outliers = df[(df['coluna'] < limite_inferior) | (df['coluna'] > limite_superior)]
```

Para **tratar** os outliers identificados, as opções mais comuns são: remover as linhas, substituir pelos valores de mediana/média, ou aplicar "capping" (limitar o valor ao limite superior/inferior calculado).

---

### 7. Como concatenar vários DataFrames (empilhando linhas ou colunas), mesmo que tenham colunas diferentes? Dica: Utiliza-se pd.concat() especificando axis=0 (linhas) ou axis=1 (colunas). Quando há colunas diferentes, os valores ausentes sãopreenchidos com NaN.


```python
import pandas as pd

# Empilhar linhas (axis=0), mesmo com colunas diferentes
df_concatenado = pd.concat([df1, df2], axis=0)

# Concatenar colunas (axis=1)
df_concatenado_colunas = pd.concat([df1, df2], axis=1)
```

Quando as colunas diferem entre os DataFrames, o `pd.concat()` alinha automaticamente pelas colunas em comum e preenche com `NaN` os valores que não existem em um dos DataFrames para aquela linha.

---

### 8. Utilizando pandas, como realizar a leitura de um arquivo CSV em um DataFrame e exibir as primeiras linhas?

```python
import pandas as pd

df = pd.read_csv('arquivo.csv')
print(df.head())      # primeiras 5 linhas por padrão
print(df.head(10))    # ou especificando a quantidade de linhas
```

---

### 9. Utilizando pandas, como selecionar uma coluna específica e filtrar linhas em um DataFrame com base em uma condição?

```python
# Selecionar uma coluna específica (retorna uma Series)
coluna = df['idade']

# Selecionar múltiplas colunas (retorna um DataFrame)
colunas = df[['nome', 'idade']]

# Filtrar linhas com base em uma condição
maiores_de_idade = df[df['idade'] >= 18]

# Combinando múltiplas condições
filtro = df[(df['idade'] >= 18) & (df['cidade'] == 'Goiânia')]
```

---

### 10. Utilizando pandas, como lidar com valores ausentes (NaN) em um DataFrame?

```python
# Verificar quantos valores ausentes existem por coluna
df.isnull().sum()

# Remover linhas com qualquer valor ausente
df_sem_na = df.dropna()

# Remover apenas colunas inteiras com valores ausentes
df_sem_na_colunas = df.dropna(axis=1)

# Preencher com um valor fixo
df_preenchido = df.fillna(0)

# Preencher com a média da coluna
df['coluna'] = df['coluna'].fillna(df['coluna'].mean())

# Preencher usando o valor anterior/seguinte (forward/backward fill)
df_ffill = df.fillna(method='ffill')
```

