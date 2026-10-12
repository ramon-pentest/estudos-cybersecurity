# Python — Aula 12: Dicionários

## Situação de um aluno

```python
aluno = {}
aluno['nome'] = str(input('Nome: '))
aluno['media'] = float(input(f'Média de {aluno["nome"]}: '))

if aluno['media'] >= 7:
    aluno['situacao'] = 'Aprovado'
else:
    aluno['situacao'] = 'Reprovado'

print('-' * 30)
for chave, valor in aluno.items():
    print(f'{chave.capitalize()}: {valor}')
```

Um dicionário guarda dados em pares de chave e valor. O método `items()` permite percorrer os dois ao mesmo tempo, e `capitalize()` deixa a primeira letra da chave maiúscula.

---

## Jogo de dados e ranking

```python
import random

jogadores = {}
for jogador in range(1, 5):
    nome = f'Jogador {jogador}'
    jogadores[nome] = random.randint(1, 6)
    print(f'{nome} tirou {jogadores[nome]}')

print('-' * 30)
print('Ranking dos jogadores:')
ranking = sorted(jogadores.items(), key=lambda item: item[1], reverse=True)
for posicao, (nome, valor) in enumerate(ranking, start=1):
    print(f'{posicao}º lugar: {nome}, com {valor}')
```

`sorted()` cria uma nova sequência ordenada; `reverse=True` coloca os maiores primeiro. O parâmetro `key` escolhe o critério de ordenação. Nesse caso, `lambda item: item[1]` usa o valor de cada par. `enumerate(..., start=1)` numera o ranking a partir do primeiro lugar.

---

## Cadastro de trabalhador

```python
from datetime import date

cadastro = {}
cadastro['nome'] = str(input('Nome: '))
ano_nascimento = int(input('Ano de nascimento: '))
ano_atual = date.today().year
cadastro['idade'] = ano_atual - ano_nascimento
cadastro['ctps'] = int(input('Carteira de trabalho (0 se não tem): '))

if cadastro['ctps'] != 0:
    cadastro['contratacao'] = int(input('Ano de contratação: '))
    cadastro['salario'] = float(input('Salário: R$ '))
    anos_contribuicao = ano_atual - cadastro['contratacao']
    cadastro['aposentadoria'] = cadastro['idade'] + max(0, 35 - anos_contribuicao)

print('-' * 30)
for chave, valor in cadastro.items():
    print(f'{chave.capitalize()}: {valor}')
```

`date.today().year` obtém o ano atual do computador. `max()` escolhe o maior entre os valores recebidos; aqui impede que o tempo restante de contribuição fique negativo.

---

## Aproveitamento de um jogador

```python
jogador = {}
jogador['nome'] = str(input('Nome do jogador: '))
partidas = int(input(f'Quantas partidas {jogador["nome"]} jogou? '))
jogador['gols'] = []

for partida in range(partidas):
    gols = int(input(f'Quantos gols na partida {partida + 1}? '))
    jogador['gols'].append(gols)

jogador['total'] = sum(jogador['gols'])
print('-' * 30)
print(jogador)
print(f'O jogador {jogador["nome"]} fez {jogador["total"]} gols em {partidas} partidas.')
for partida, gols in enumerate(jogador['gols'], start=1):
    print(f'  Na partida {partida}, fez {gols} gol(s).')
```

`sum()` soma os valores de uma sequência. A lista `gols` guarda um valor por partida dentro do dicionário do jogador.

---

## Cadastro de pessoas

```python
pessoas = []
continuar = 'S'

while continuar == 'S':
    pessoa = {}
    pessoa['nome'] = str(input('Nome: '))
    pessoa['sexo'] = str(input('Sexo [M/F]: ')).strip().upper()
    while pessoa['sexo'] not in ('M', 'F'):
        print('Digite M para masculino ou F para feminino.')
        pessoa['sexo'] = str(input('Sexo [M/F]: ')).strip().upper()
    pessoa['idade'] = int(input('Idade: '))
    pessoas.append(pessoa)
    continuar = str(input('Quer continuar? [S/N] ')).strip().upper()
    while continuar not in ('S', 'N'):
        continuar = str(input('Digite S para sim ou N para não: ')).strip().upper()

media_idade = sum(pessoa['idade'] for pessoa in pessoas) / len(pessoas)
mulheres = [pessoa['nome'] for pessoa in pessoas if pessoa['sexo'] == 'F']

print('-' * 30)
print(f'Ao todo, foram cadastradas {len(pessoas)} pessoas.')
print(f'A média de idade do grupo é {media_idade:.1f} anos.')
print(f'Mulheres cadastradas: {", ".join(mulheres) if mulheres else "nenhuma"}.')
```

`strip()` remove espaços extras no começo e no fim do texto. `upper()` converte a resposta para maiúsculas. As expressões entre colchetes criam listas filtrando os dicionários cadastrados.

---

## Cadastro de vários jogadores

```python
jogadores = []

while True:
    jogador = {}
    jogador['nome'] = str(input('Nome do jogador: '))
    partidas = int(input(f'Quantas partidas {jogador["nome"]} jogou? '))
    jogador['gols'] = []
    for partida in range(partidas):
        jogador['gols'].append(
            int(input(f'  Quantos gols na partida {partida + 1}? '))
        )
    jogador['total'] = sum(jogador['gols'])
    jogadores.append(jogador)
    continuar = str(input('Quer cadastrar outro jogador? [S/N] ')).strip().upper()
    while continuar not in ('S', 'N'):
        continuar = str(input('Digite S para sim ou N para não: ')).strip().upper()
    if continuar == 'N':
        break

print('-' * 40)
print(f'{"Cód.":<6}{"Nome":<20}{"Gols":<10}{"Total"}')
for codigo, jogador in enumerate(jogadores):
    print(f'{codigo:<6}{jogador["nome"]:<20}{str(jogador["gols"]):<10}{jogador["total"]}')

while True:
    codigo = int(input('Mostrar dados de qual jogador? (999 para parar): '))
    if codigo == 999:
        break
    if 0 <= codigo < len(jogadores):
        jogador = jogadores[codigo]
        print(f'Levantamento do jogador {jogador["nome"]}:')
        for partida, gols in enumerate(jogador['gols'], start=1):
            print(f'  Na partida {partida}, fez {gols} gol(s).')
        print(f'Total: {jogador["total"]} gol(s).')
    else:
        print('Código de jogador inválido.')
```

`enumerate()` também pode percorrer uma lista de jogadores com um código para cada posição. O teste `0 <= codigo < len(jogadores)` confirma que o índice informado existe antes de acessar a lista.
