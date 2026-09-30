# Python — Aula 11: Listas Dentro de Listas e Matrizes

## Parte teórica

**Guardando uma cópia antes de mudar o original**
```python
# estrutura de lista dentro da lista
teste = list()
teste.append('Gustavo')
teste.append(40)
galera = list()
galera.append(teste[:])
teste[0] = 'Maria'
teste[1] = 22
galera.append(teste[:])
print(galera)
```

O `teste[:]` cria uma cópia independente da lista no
momento em que é adicionada — por isso a primeira
entrada em `galera` fica com "Gustavo, 40" mesmo depois
de eu mudar `teste` pra "Maria, 22". Sem o `[:]`, as
duas listas ficariam ligadas e a mudança em `teste`
afetaria também o que já tinha sido guardado.

---

**Acessando lista dentro de lista**
```python
galera = [['João', 19], ['Ana', 33], ['Joaquim', 13], ['Maria', 45]]
print(galera[0][0])
```

Se fosse só `galera[0]`, pegaria o bloco inteiro do
João (`['João', 19]`). Colocando os dois colchetes
`[0][0]`, pego só o primeiro item dentro daquele bloco
— o nome.

---

**Percorrendo listas de listas**
```python
galera = [['João', 19], ['Ana', 33], ['Joaquim', 13], ['Maria', 45]]
for p in galera:
    print(f'{p[0]} tem {p[1]} anos de idade')
```

---

**Cadastro com clear() pra reaproveitar a mesma variável**
```python
galera = list()
dado = list()
totmai = totmen = 0
for c in range(0,5):
    dado.append(str(input('Nome: ')))
    dado.append(int(input('Idade:')))
    galera.append(dado[:])
    dado.clear()
print(galera)

for p in galera:
    if p[1] >= 21:
        print(f'{p[0]} é maior de idade.')
        totmai += 1
    else:
        print(f'{p[0]} é menor de idade.')
        totmen += 1
print(f'Temos {totmai} maiores e {totmen} menores')
```

O `dado.clear()` esvazia a lista temporária depois de
cada pessoa cadastrada, pra poder reutilizar ela na
próxima volta do loop sem misturar dados de pessoas
diferentes.

---

## Exercícios

**Validando parênteses**
```python
expressao = str(input('Digite a expressão: '))
contador = 0
for caractere in expressao:
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

---

**Pares e ímpares ordenados**
```python
pares = []
impares = []
for i in range(7):
    n = int(input('Digite um valor: '))
    if n % 2 == 0:
        pares.append(n)
    else:
        impares.append(n)
pares.sort()
impares.sort()
print(f'Pares em ordem crescente: {pares}')
print(f'Ímpares em ordem crescente: {impares}')
```

---

**Matriz 3x3 — criando e exibindo**
```python
matriz = []

for linha in range(3):
    linha_atual = []
    for coluna in range(3):
        valor = int(input(f'Digite o valor [{linha}][{coluna}]: '))
        linha_atual.append(valor)
    matriz.append(linha_atual)

for linha in matriz:
    for valor in linha:
        print(f'{valor:>5}', end='')
    print()
```

Duas listas aninhadas: a lista de fora representa as
linhas, cada uma guardando uma lista de valores das
colunas. O `end=''` no print evita quebrar linha depois
de cada valor, deixando tudo na mesma linha até o
`print()` vazio de fora, que aí sim pula pra próxima
linha da matriz.

---

**Matriz 3x3 — com estatísticas**
```python
matriz = []

for linha in range(3):
    linha_atual = []
    for coluna in range(3):
        valor = int(input(f'Digite o valor [{linha}][{coluna}]: '))
        linha_atual.append(valor)
    matriz.append(linha_atual)
for linha in matriz:
    for valor in linha:
        print(f'{valor:>5}', end='')
    print()
soma_pares = 0
for linha in matriz:
    for valor in linha:
        if valor % 2 == 0:
            soma_pares += valor
soma_terceira_coluna = 0
for linha in matriz:
    soma_terceira_coluna += linha[2]
maior_segunda_linha = matriz[1][0]
for valor in matriz[1]:
    if valor > maior_segunda_linha:
        maior_segunda_linha = valor
print(f'Soma dos pares: {soma_pares}')
print(f'Soma da terceira coluna: {soma_terceira_coluna}')
print(f'Maior valor da segunda linha: {maior_segunda_linha}')
```

`matriz[1]` pega a segunda linha inteira. `linha[2]`
dentro do loop pega sempre a terceira coluna de cada
linha, somando uma coluna vertical em vez de uma linha
horizontal.

---

**Gerador de jogos da loteria**
```python
import random
jogos = int(input('Quantos jogos você quer gerar? '))
for i in range(jogos):
    numeros_sorteados = []
    while len(numeros_sorteados) < 6:
        numero = random.randint(1, 60)
        if numero not in numeros_sorteados:
            numeros_sorteados.append(numero)
    numeros_sorteados.sort()
    print(f'Jogo {i + 1}: {numeros_sorteados}')
```

O `while` continua sorteando até ter 6 números únicos
naquele jogo — o `not in` evita repetir número dentro
do mesmo jogo.

---

**Boletim de alunos com busca**
```python
alunos = []
quantidade = int(input('Quantos alunos? '))
for i in range(quantidade):
    nome = str(input('Nome do aluno: '))
    nota1 = float(input('Primeira nota: '))
    nota2 = float(input('Segunda nota: '))
    media = (nota1 + nota2) / 2
    alunos.append([nome, media])
print('--- Boletim ---')
for aluno in alunos:
    print(f'{aluno[0]}: média {aluno[1]:.1f}')
ver = str(input('Quer ver a nota de algum aluno específico? [S/N] ')).upper()
while ver == 'S':
    nome_procurado = str(input('Nome do aluno: '))
    for aluno in alunos:
        if aluno[0] == nome_procurado:
            print(f'{aluno[0]} tem média {aluno[1]:.1f}')
    ver = str(input('Quer ver outro? [S/N] ')).upper()
```

---

**Cadastro de peso — mais pesado e mais leve**
```python
pessoas = []
continuar = 'S'
while continuar == 'S':
    nome = str(input('Nome: '))
    peso = float(input('Peso: '))
    pessoas.append([nome, peso])
    continuar = str(input('Quer continuar? [S/N] ')).upper()
print(f'Foram cadastradas {len(pessoas)} pessoas')
maior_peso = pessoas[0][1]
for p in pessoas:
    if p[1] > maior_peso:
        maior_peso = p[1]
menor_peso = pessoas[0][1]
for p in pessoas:
    if p[1] < menor_peso:
        menor_peso = p[1]
print('Pessoas mais pesadas:')
for p in pessoas:
    if p[1] == maior_peso:
        print(p[0])
print('Pessoas mais leves:')
for p in pessoas:
    if p[1] == menor_peso:
        print(p[0])
```

Esse trata empate corretamente — se duas pessoas
tiverem o mesmo peso máximo, as duas aparecem na lista
de "mais pesadas", porque percorre tudo de novo
comparando com o valor já descoberto, em vez de guardar
só um nome.
