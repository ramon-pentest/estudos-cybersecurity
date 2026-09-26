# Python — Aula 09: Tuplas e Exercícios

## Três formas de percorrer uma tupla com for
```python
lanche = ('hambúrger', 'suco', 'pizza', 'pudim', 'batata frita')

for comida in lanche:
    print(f'Eu vou comer {comida}')

for cont in range(0,len(lanche)):
    print(f'Eu vou comer {lanche[cont]} na posição {cont}')

for pos, comida in enumerate(lanche):
    print(f'Eu vou comer {comida} na posição {pos}')

print('Comi pra caramba!')
```

`enumerate()` já entrega posição e valor juntos, sem
precisar acessar pelo índice manualmente — é a forma
mais direta das três.

---

## Soma com break
```python
n = s = 0
while True:
    n = int(input('Digite um número(Digite 999 para parar)'))
    if n == 999:
        break
    s += n
print(f'A soma dos números são {s}')
```

`while True` cria um loop que só para com `break` —
útil quando não sei de antemão quantas vezes vai
repetir.

---

## Tabuada com validação de negativo
```python
n = int(input('Digite um número e veja sua tabuada: '))
if n < 0:
    print('Numero negativo, programa encerrado.')
else:
    for i in range(1, 11):
        print(f'{n} x {i} = {n * i}')
```

---

## Jogo de Par ou Ímpar contra o computador
```python
import random
print('Jogaremos Par ou Impar, se perder o jogo acaba.')
vitorias = 0
for i in range(1, 11):
    escolha = str(input('Você quer torcer para Par ou Impar? ')).capitalize()
    pessoa = int(input('Digite um número: '))
    computador = random.randint(1, 10)
    soma = pessoa + computador
    if soma % 2 == 0:
        resultado = 'Par'
    else:
        resultado = 'Impar'
    if escolha == resultado:
        print(f'Você acertou! {pessoa} + {computador} = {soma}, que é {resultado}.')
        vitorias = vitorias + 1
    else:
        print(f'Você errou! {pessoa} + {computador} = {soma}, que é {resultado}. Fim de jogo.')
        break
print(f'Você venceu {vitorias} vezes.')
```

Primeiro exercício que junta `random`, `for` com limite
máximo de rodadas, condicional e `break` — o jogo
continua até 10 rodadas ou até a pessoa errar, o que
vier primeiro.

---

## Cadastro com múltiplas condições
```python
maiores = 0
homens = 0
mulheres = 0
continuar = 'S'
while continuar == 'S':
    idade = int(input('Qual sua idade? '))
    sexo = str(input('Qual seu sexo? [M/F]')).upper()
    if idade > 18:
        maiores = maiores + 1
    if sexo == 'M':
        homens = homens + 1
    if sexo == 'F' and idade < 20:
        mulheres = mulheres + 1
        continuar = str(input('Quer continuar? [S/N]')).upper()
print(f'Pessoas com mais de 18 anos {maiores}')
print(f'Homens cadastrados {homens}')
print(f'Mulheres com menos de 20 anos {mulheres}')
```

---

## Controle de compras
```python
total_gasto = 0
caro = 0
nome_mais_barato = ''
barato = 9999999999
continuar = 'S'
while continuar == 'S':
    produto = str(input('Qual o nome deste produto? '))
    preco = float(input('Quanto custa este produto? '))
    total_gasto = total_gasto + preco
    if preco > 1000:
        caro = caro + 1
    if preco < barato:
        barato = preco
        nome_mais_barato = produto
    continuar = str(input('Quer continuar? [S/N]')).strip().upper()
print(f'O preço total das compras foi R$ {total_gasto:.2f}')
print(f'Os produtos que custaram mais de R$1000 foram: {caro}')
print(f'O nome do produto mais barato é {nome_mais_barato}')
```

---

## Cédulas de saque
```python
valor = int(input('Qual valor você quer sacar? R$ '))

cedulas50 = valor // 50
valor = valor % 50
cedulas20 = valor // 20
valor = valor % 20
cedulas10 = valor // 10
valor = valor % 10
cedulas1 = valor // 1

print(f'Cédulas de R$ 50: {cedulas50}')
print(f'Cédulas de R$ 20: {cedulas20}')
print(f'Cédulas de R$ 10: {cedulas10}')
print(f'Cédulas de R$ 1: {cedulas1}')
```

A lógica vai "descontando" o valor a cada divisão —
primeiro tira quantas notas de 50 cabem, guarda o
resto, depois quantas de 20 cabem no resto, e assim
por diante.

---

## Tupla como dicionário de números por extenso
```python
numero = ('zero', 'um', 'dois', 'três', 'quatro', 'cinco', 'seis', 'sete', 'oito', 'nove', 'dez', 'onze', 'doze', 'treze', 'catorze', 'quinze', 'dezesseis', 'dezessete', 'dezoito', 'dezenove', 'vinte')
n = -1
while n < 0 or n > 20:
    n = int(input('Digite um número entre 0 a 20: '))
print(f'O número digitado foi {numero[n]}')
```

Usa o próprio número digitado como índice da tupla —
já que a tupla começa em "zero" na posição 0, o índice
bate exatamente com o número.

---

## Times de futebol — ordenação e busca
```python
times = ('Corinthians', 'Palmeiras', 'Santos', 'Grêmio', 'Cruzeiro', 'Flamengo', 'Vasco', 'Chapecoense', 'Atlético-MG', 'Botafogo', 'Atlético-PR', 'Bahia', 'São Paulo', 'Fluminense', 'Sport', 'Vitória', 'Coritiba', 'Avaí', 'Ponte Preta', 'Atlético-GO')
times_ordenados = sorted(times)
posicao = times.index('Chapecoense') + 1
print(f'Os cinco primeiros colocados são: {times[:5]}')
print(f'e os ultimos colocados são: {times[-4:]}')
print(f'os times em ordem alfabetica são {times_ordenados}')
print(f'e a Chapecoense está na posição {posicao}')
```

`sorted()` ordena sem alterar a tupla original.
`.index()` acha a posição de um elemento específico.

---

## Números aleatórios em tupla — maior e menor
```python
import random
numeros = []
for i in range(5):
    numeros.append(random.randint(1,100))
numeros = tuple(numeros)
maior = 0
menor = 9999999999
for n in numeros:
    if n > maior:
        maior = n
    if n < menor:
        menor = n
print(f'Os números sorteados foram {numeros}')
print(f'O maior valor é {maior}')
print(f'O menor valor é {menor}')
```

Cria como lista primeiro (porque tupla não aceita
`.append()`) e só depois converte pra tupla com
`tuple()`.

---

## Análise de valores digitados
```python
valores = []
for i in range(4):
    valores.append(int(input('Digite um valor: ')))
valores = tuple(valores)
quantidade_noves = valores.count(9)
posicao_tres = valores.index(3)
pares = []
for n in valores:
    if n % 2 == 0:
        pares.append(n)
print(f'O valor 9 apareceu {quantidade_noves} vezes')
print(f'O primeiro 3 foi digitado na posição {posicao_tres}')
print(f'Os números pares foram: {pares}')
```

`.count()` conta quantas vezes um valor aparece.
`.index()` acha a primeira posição onde aquele valor
aparece.

---

## Tabela de produtos formatada
```python
produtos = ('Notebook', 3200, 'Mouse', 80, 'Monitor', 1500, 'Teclado', 150)
for i in range(0,len(produtos),2):
    nome = produtos[i]
    preço = produtos[i + 1]
    print(f'{nome:<15} R${preço:>8}')
```

O `range` pula de 2 em 2 porque a tupla alterna nome e
preço no mesmo nível — `i` pega o nome, `i+1` pega o
preço correspondente. O `:<15` e `:>8` alinham o texto
à esquerda e o número à direita, formatando como tabela.

---

## Vogais de cada palavra
```python
palavras = ('python', 'programação', 'teclado', 'estudo')
for palavra in palavras:
    vogais = []
    for letra in palavra:
        if letra in 'aeiou':
            vogais.append(letra)
    print(f'{palavra}: {vogais}')
```

Loop dentro de loop — o de fora percorre cada palavra,
o de dentro percorre cada letra daquela palavra
verificando se é vogal.
