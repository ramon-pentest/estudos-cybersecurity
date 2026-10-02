# TryHackMe — Pre-Security: Python Core Concepts

Essa sala retoma o que apareceu no jogo e amplia o
vocabulário necessário pra ler e escrever programas.

## Variáveis e tipos

Uma variável guarda um valor que pode ser usado ou
atualizado:
```python
food = "ice cream"  # str
money = 2000         # int
```

Tipos básicos:
```
str   → texto
int   → números inteiros
float → números com casas decimais
bool  → True ou False
```

Listas também aparecem como coleção ordenada de valores.

`type()` mostra o tipo de um valor. Linhas começando
com `#` são comentários — ajudam quem lê o código, mas
não são executadas.

## Conversão e saída

Como `input()` sempre devolve texto:
```python
int(text)    → transforma entrada numérica em inteiro
float(text)  → converte pra número decimal
str(valor)   → transforma um valor em texto
```

Se o texto não representar um número válido, a
conversão pode falhar.

**F-string** pra inserir variáveis dentro de uma frase:
```python
f"User {username} is on port {port}"
```

**Incremento abreviado:**
```python
tries = tries + 1   # forma completa
tries += 1           # forma abreviada
```
Mesmo padrão pra subtrair, multiplicar, dividir:
`count -= 1`, etc.

## Strings

Sequência de caracteres. Cada posição tem um índice
começando em 0:
```python
word = "Python"
word[0]   # P
word[-1]  # n (índice negativo conta do final)
```

**Fatiamento:**
```python
word[0:3]  # "Pyt" — início entra, fim não entra
word[2:]   # da posição 2 até o final
```

**Métodos úteis:**
```
.upper() / .lower()  → maiúscula/minúscula
.strip()              → remove espaços das pontas
.replace()            → troca trechos
.split()               → separa o texto em partes
.startswith() / .endswith() → verifica começo/fim
.count()               → conta ocorrências
```

**Verificando tipo de caractere (retornam True/False):**
```
.isdigit()  → é dígito?
.isupper()  → é maiúscula?
.islower()  → é minúscula?
.isalpha()  → é letra?
.isalnum()  → é letra ou número?
```

**Operador in:**
```python
"tryhackme" in url  # True se esse texto aparecer na URL
```

## Listas

Guarda vários valores em ordem:
```python
ports = [22, 80, 443]
ports[0] = 2222  # troca o primeiro item
```

```
.append()  → adiciona ao final
.remove()  → remove o primeiro item com esse valor
.pop()     → remove e devolve um item
.sort()    → ordena
.reverse() → inverte a ordem
len()      → quantidade de elementos
in         → verifica se um valor está na lista
```

## Dicionários — NOVO

Associa chaves a valores:
```python
services = {22: "SSH", 80: "HTTP"}
services[22]  # retorna "SSH"
```

A chave funciona como identificador pra encontrar seu
valor. Dá pra adicionar/atualizar uma entrada
atribuindo valor à chave, e remover com `del`.

```
.keys()   → acessa as chaves
.values() → acessa os valores
.items()  → acessa os pares chave-valor
.get()    → busca uma chave com valor alternativo
            se ela não existir:
            services.get(9999, "Unknown")
            → retorna "Unknown" em vez de dar erro
```

## Operadores

```
**  → potência
//  → divisão inteira (arredonda pra baixo)
%   → resto da divisão
```

O resto ajuda a verificar paridade:
```python
number % 2 == 0  # par?
```

```
not in → inverso de in, verifica se NÃO está numa coleção
and    → exige as duas condições verdadeiras
or     → exige pelo menos uma verdadeira
```

`any()` apareceu num exemplo percorrendo os caracteres
de uma senha pra verificar se algum é dígito — a sala
deixou o funcionamento detalhado dessa expressão pra
depois.

## Loops

```python
while condição:   # repete enquanto for verdadeiro
    ...

for item in sequência:  # percorre itens (IPs, caracteres, etc)
    ...
```

`range()` fornece sequência de números:
```python
range(5)        # 0, 1, 2, 3, 4 (limite final não incluído)
range(0, 20, 5) # início, fim, passo
```

**Percorrendo dicionário com items():**
```python
for port, name in services.items():
```

**Dentro de loops:**
```
break    → encerra a repetição
continue → pula o resto daquela volta, segue pra próxima
```

---
