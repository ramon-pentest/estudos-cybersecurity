# Python — Aula 10: Listas

## Mexendo numa lista

```python
num = [2,5,9,1]
num[2] = 3 #substitui o 9 pelo 3, isso só é possível por ser lista
num.append(7) #Adiciona o 7 na lista
num.sort(reverse=True) #Sort organiza em ordem, com o reverse True, ele faz o oposto
num.insert(2,0) # na posição 2, ele insere o número 0, sabendo que, na lista cada número tem sua posição.
num.pop(2) #somente num.pop() excluiria somente o último número
num.remove(3) #remove o 3 da lista.
print(num)
print(f'Essa lista tem {len(num)} elementos.')
```

Diferente da tupla, a lista é mutável: dá pra trocar um valor direto pela posição, adicionar e tirar itens.

- `append()` adiciona no final
- `insert(posição, valor)` insere numa posição específica
- `sort()` ordena, e com `reverse=True` fica decrescente
- `pop(posição)` remove pela posição, e sem argumento remove o último
- `remove(valor)` remove pelo valor, não pela posição
- `len()` diz quantos elementos a lista tem

---

## Percorrendo a lista com enumerate

```python
valores = []
valores.append(5)
valores.append(9)
valores.append(4)
for c, v in enumerate(valores): #c e enumerate marcam o índice (posição) a cada volta
    print(f'Na posição {c} encontrei o valor {v}!')
print('Cheguei ao final da lista.')
```

O `enumerate` entrega a posição (`c`) e o valor (`v`) juntos a cada volta do `for`.

**Mesma ideia, com valores digitados**
```python
valores = []
for cont in range(0,5):
    valores.append(int(input('Digite um valor: ')))
for c, v in enumerate(valores):
    print(f'Na posição {c} encontrei o valor {v}!')
print('Cheguei ao final da lista')
```

---

## Copiando uma lista

```python
a = [2,3, 4, 7]
b = a[:] # isso faz com que todos os valores de a vão para o b como uma cópia.
b[2] = 8
print(f'Lista A: {a}')
print(f'Lista B: {b}')
```

Se eu fizesse `b = a`, as duas variáveis apontariam pra mesma lista e mexer numa mudaria a outra. Com `a[:]` sai uma cópia independente, por isso mudar o `b[2]` não altera a lista A.

---

## Exercícios

**Maior e menor valor com a posição**
```python
valores = []
for i in range(5):
    numero = int(input(f'Digite um valor para a posição {i}: '))
    valores.append(numero)
maior = max(valores)
menor = min(valores)
print(f'Você digitou os valores: {valores}')
print(f'O maior valor foi {maior}, na posição {valores.index(maior)}')
print(f'O menor valor foi {menor}, na posição {valores.index(menor)}')
```

O `max()` e o `min()` pegam o maior e o menor da lista de uma vez, e o `.index()` devolve a posição desse valor. Se o valor se repetir, o `.index()` mostra só a primeira posição onde ele aparece.

---

**Valores únicos em ordem crescente**
```python
numeros = []
continuar = 'S'
while continuar == 'S':
    n = int(input('Digite um número'))
    if n not in numeros:
        numeros.append(n)
    else:
        print('Valor duplicado, não irei adicionar.')
    continuar = str(input('Quer continuar? [S/N]')).upper()
numeros.sort()
print(f'Valores únicos em ordem crescente: {numeros}')
```

O `not in` confere se o número ainda não está na lista antes de adicionar, então ela só guarda valores sem repetição. O `.sort()` no final deixa tudo em ordem crescente.

---

**Montando a lista já ordenada, sem usar sort**
```python
lista = []
for i in range(5):
    n = int(input('Digite um valor: '))
    if len(lista) == 0 or n >= lista[-1]:
        lista.append(n)
    else:
        posicao = 0
        while n > lista[posicao]:
            posicao += 1
        lista.insert(posicao, n)
print(f'Lista ordenada: {lista}')
```

A lista vai se ordenando sozinha enquanto os valores entram. Se o número é maior ou igual ao último (`lista[-1]` pega o último elemento), vai direto pro final com `append`. Senão o `while` anda pelas posições até achar onde ele se encaixa, e o `insert` coloca ele ali.

---

**Contar, ordem decrescente e procurar o 5**
```python
numeros = []
continuar = 'S'
while continuar == 'S':
    numeros.append(int(input('Digite um número')))
    continuar = str(input('Quer continuar? [S/N]')).upper()
print(f'Foram digitados {len(numeros)} números')
numeros.sort(reverse=True)
print(f'Em ordem decrescente: {numeros}')
if 5 in numeros:
    print('O valor 5 foi encontrado na lista')
else:
    print('O valor 5 não foi encontrado na lista')
```

---

**Separando pares e ímpares**
```python
numeros = []
pares = []
impares = []
continuar = 'S'
while continuar == 'S':
    numeros.append(int(input('Digite um número: ')))
    continuar = str(input('Quer continuar? [S/N] ')).upper()
for n in numeros:
    if n % 2 == 0:
        pares.append(n)
    else:
        impares.append(n)
print(f'Todos os números: {numeros}')
print(f'Pares: {pares}')
print(f'Impares: {impares}')
```

Guardo tudo numa lista só e depois separo em duas, uma pros pares (`n % 2 == 0`) e outra pros ímpares.

---

**Validando parênteses de uma expressão**
```python
expressão = str(input('Digite a expressão: '))
contador = 0
for caractere in expressão:
    if caractere == '(':
        contador += 1
    elif caractere == ')':
        contador -= 1
        if contador < 0:
            break
if contador == 0:
    print('Expressão válida')
else:
    print('Expressão inválida')
```
Cada `(` soma 1 no contador e cada `)` subtrai 1. Se o contador ficar negativo em algum momento, significa que fechei um parêntese sem ter aberto, então dou `break`. No final a expressão só é válida se o contador terminar em 0, ou seja, todo parêntese aberto foi fechado.
