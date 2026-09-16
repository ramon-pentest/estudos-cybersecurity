# Python — Aula 07: Loops (for) e Exercícios

## Contagem regressiva
```python
import time
for c in range(10,0,-1):
    time.sleep(1)
    print(c)
```

O `range(10,0,-1)` começa em 10, vai até antes do 0,
descendo de 1 em 1. O `time.sleep(1)` pausa 1 segundo
a cada volta do loop.

---

## Números de 1 a 50, marcando os pares
```python
for c in range(1,51):
    if c % 2 == 0:
        print(f'{c} Par')
    else:
        print(c)
```

---

## Soma de múltiplos de 3 que não são pares (1 a 500)
```python
soma = 0
for num in range(1, 501):
    if num % 2 != 0 and num % 3 == 0:
        soma += num
print(soma)
```

---

## Tabuada com for
```python
n = int(input('Escreva um numero e veja sua tabuada: '))
for i in range(1,11):
    print(f'{n} x {i} = {n*i}')
```

---

## Soma de números pares digitados
```python
soma = 0
for c in range(1,6):
    n = int(input('Digite 6 numeros'))
    if n % 2 == 0:
        soma += n
print(f'A soma dos pares foi: {soma}')
```

---

## Progressão aritmética
```python
termo = int(input('digite um numero'))
razao = int(input('digite um numero'))
avanco = 0
for i in range(1, 11):
    print(f'{termo+avanco}')
    avanco += razao
```

---

## Verificando número primo
```python
n = int(input('Digite um numero: '))
primo = True
for i in range(2,n):
    if n % i == 0:
        primo = False
        break
if primo:
    print(f'{n} é primo')
else:
    print(f'{n} Não é primo')
```

O `break` interrompe o loop assim que encontra o
primeiro divisor — não precisa continuar testando o
resto, já que um divisor já basta pra provar que não
é primo.

---

## Verificando palíndromo
```python
frase = input('Digite uma frase: ')
frase_sem_espaco = frase.replace(" ", "")
frase_invertida = frase_sem_espaco[::-1]

if frase_sem_espaco == frase_invertida:
    print('É um palíndromo')
else:
    print('Não é um palíndromo')
```

O `[::-1]` inverte a string inteira usando fatiamento
com passo negativo.

---

## Verificando maioridade de várias pessoas
```python
from datetime import date
atual = date.today().year
for i in range(1,7):
    ano = int(input('Em que ano você nasceu?'))
    if atual - ano >= 18:
        print('Você já é de maior')
    else:
        print('Você ainda é de menor')
```

---

## Contando maiores e menores de idade
```python
from datetime import date
ano_atual = date.today().year
maiores = 0
menores = 0

for i in range(1,7):
    ano = int(input('Em que ano você nasceu?'))
    if ano_atual - ano >= 18:
        maiores += 1
    else:
        menores += 1
print(f'Você já é de maior {maiores} ')
print(f'Você ainda é de menor {menores} ')
```

---

## Encontrando maior e menor peso
```python
maior = 0
menor = 9999999999
for i in range(5):
    peso = int(input('Digite seu peso '))
    if peso >= maior:
        maior = peso
    if peso <= menor:
        menor = peso
print(f'{maior} é maior que {menor}')
print(f'{menor} é menor que {maior}')
```

---

## Cadastro de grupo com estatísticas
```python
mediaidade = 0
somaidade = 0
maioridadehomem = 0
nomevelho = ''
totmulher20 = 0
for p in range(1,5):
    print(f'pessoa{p}')
    nome = str(input('Digite seu nome: ')).strip()
    idade = int(input('Digite sua idade: '))
    sexo = str(input('Digite seu sexo [m/f]: ')).strip()
    somaidade += idade
    if p == 1 and sexo in "Mm":
        maioridadehomem = idade
    if sexo in "Mm" and idade > maioridadehomem:
        maioridadehomem = idade
        nomevelho = nome
    if sexo in 'Ff' and idade < 20:
        totmulher20 += 1
mediaidade = somaidade / 4
print(f'A media de idade do grupo é de {mediaidade} anos')
print(f'O homem mais velho tem {maioridadehomem} e se chama {nomevelho} ')
print(f'São {totmulher20} mulheres com menos de 20 anos')
```
