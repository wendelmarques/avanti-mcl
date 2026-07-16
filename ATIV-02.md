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
