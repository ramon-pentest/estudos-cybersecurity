# Python — Aula 13: Funções

## Área de um terreno

```python
def area(largura, comprimento):
    resultado = largura * comprimento
    print(f'A área de um terreno {largura:.2f} x {comprimento:.2f} é {resultado:.2f} m².')


print('Controle de Terrenos')
print('-' * 25)
largura = float(input('Largura (m): '))
comprimento = float(input('Comprimento (m): '))
area(largura, comprimento)
```

`def` cria uma função. Os parâmetros entre parênteses recebem os valores enviados na chamada.

---

## Mensagem com tamanho adaptável

```python
def escreva(texto):
    tamanho = len(texto) + 4
    print('~' * tamanho)
    print(f'  {texto}')
    print('~' * tamanho)


mensagem = str(input('Digite uma mensagem: '))
escreva(mensagem)
```

`len()` conta os caracteres do texto. Multiplicar uma string por um número repete esse caractere na tela.

---

## Contagem personalizada

```python
def contador(inicio, fim, passo):
    if passo == 0:
        passo = 1
    else:
        passo = abs(passo)

    if inicio > fim:
        passo = -passo

    print(f'Contagem de {inicio} até {fim}, de {abs(passo)} em {abs(passo)}:')
    valor = inicio
    if passo > 0:
        while valor <= fim:
            print(valor, end=' ')
            valor += passo
    else:
        while valor >= fim:
            print(valor, end=' ')
            valor += passo
    print('FIM!')


contador(1, 10, 1)
contador(10, 0, 2)
print('-' * 30)
inicio = int(input('Início: '))
fim = int(input('Fim: '))
passo = int(input('Passo: '))
contador(inicio, fim, passo)
```

`abs()` transforma o passo em valor absoluto, e o sinal é definido de acordo com o sentido da contagem. O argumento `end` de `print()` evita a quebra de linha automática.

---

## Maior valor entre vários números

```python
def maior(*numeros):
    if not numeros:
        print('Nenhum número foi informado.')
        return

    print(f'Foram informados {len(numeros)} números.')
    print(f'O maior valor é {max(numeros)}.')


maior(2, 9, 4, 5, 7)
maior(1, 2)
maior(6)
maior()
```

O `*` no parâmetro reúne uma quantidade variável de argumentos numa tupla. `return` encerra a função e, neste caso, evita processar uma sequência vazia.

---

## Sorteio e soma de pares

```python
from random import randint


def sorteia(lista):
    for numero in range(5):
        lista.append(randint(1, 10))


def somapar(lista):
    soma = 0
    for valor in lista:
        if valor % 2 == 0:
            soma += valor
    print(f'Valores sorteados: {lista}')
    print(f'Soma dos valores pares: {soma}')


numeros = []
sorteia(numeros)
somapar(numeros)
```

`from random import randint` importa uma função específica. `randint(1, 10)` sorteia um inteiro incluindo os dois limites.

---

## Situação eleitoral

```python
from datetime import date


def voto(ano_nascimento):
    idade = date.today().year - ano_nascimento
    if idade < 16:
        return f'Com {idade} anos: voto proibido.'
    if idade < 18 or idade >= 65:
        return f'Com {idade} anos: voto opcional.'
    return f'Com {idade} anos: voto obrigatório.'


ano = int(input('Em que ano você nasceu? '))
print(voto(ano))
```

`return` devolve um resultado ao ponto onde a função foi chamada. `or` permite combinar duas condições alternativas.

---

## Fatorial com opção de mostrar o cálculo

```python
def fatorial(numero, show=False):
    if numero < 0:
        raise ValueError('O fatorial não está definido para números negativos.')

    resultado = 1
    if show and numero == 0:
        print('0! = 1')
    for valor in range(numero, 0, -1):
        resultado *= valor
        if show:
            print(valor, end='')
            if valor > 1:
                print(' x ', end='')
            else:
                print(' = ', end='')
    if show:
        print(resultado)
    return resultado


numero = int(input('Digite um número para calcular o fatorial: '))
mostrar = str(input('Mostrar o cálculo? [S/N] ')).strip().upper() == 'S'
resultado = fatorial(numero, mostrar)
if not mostrar:
    print(f'O fatorial de {numero} é {resultado}.')
```

`show=False` define um argumento opcional. `raise ValueError(...)` sinaliza que o valor recebido não é válido para essa operação.

---

## Ficha de um jogador

```python
def ficha(nome='<desconhecido>', gols=0):
    print(f'O jogador {nome} fez {gols} gol(s) no campeonato.')


nome_jogador = str(input('Nome do jogador: ')).strip()
gols_jogador = str(input('Número de gols: ')).strip()
if gols_jogador.isdigit():
    ficha(nome_jogador or '<desconhecido>', int(gols_jogador))
else:
    ficha(nome_jogador or '<desconhecido>')
```

Valores padrão em `nome` e `gols` permitem chamar a função sem informar todos os argumentos. `isdigit()` verifica se o texto contém apenas dígitos; `or` usa o valor alternativo quando o nome está vazio.

---

## Leitura de número inteiro

```python
def leiaInt(mensagem):
    while True:
        valor = str(input(mensagem)).strip()
        try:
            return int(valor)
        except ValueError:
            print('\033[31mErro! Digite um número inteiro válido.\033[m')


numero = leiaInt('Digite um número inteiro: ')
print(f'Você digitou o número {numero}.')
```

`try` executa uma conversão que pode falhar. `except ValueError` trata especificamente o erro gerado quando o texto não representa um inteiro.

---

## Estatísticas de notas

```python
def notas(*valores, sit=False):
    resultado = {
        'total': len(valores),
        'maior': max(valores) if valores else None,
        'menor': min(valores) if valores else None,
        'media': sum(valores) / len(valores) if valores else 0,
    }
    if sit:
        media = resultado['media']
        if not valores:
            situacao = 'Sem notas'
        elif media < 5:
            situacao = 'Ruim'
        elif media < 7:
            situacao = 'Razoável'
        elif media < 9:
            situacao = 'Boa'
        else:
            situacao = 'Excelente'
        resultado['situacao'] = situacao
    return resultado


resultado = notas(7.5, 8.0, 6.5, sit=True)
print(resultado)
```

`*valores` aceita várias notas. O parâmetro nomeado `sit` controla se o dicionário também recebe a situação. A expressão `valor_a if condição else valor_b` escolhe entre dois resultados.

---

## Sistema de ajuda interativa

```python
cores = {
    'limpa': '\033[m',
    'azul': '\033[34m',
    'amarelo': '\033[33m',
    'pretoebranco': '\033[7;30m',
}

while True:
    print(f'{cores["pretoebranco"]} SISTEMA DE AJUDA PyHELP {cores["limpa"]}')
    comando = str(input('Função ou biblioteca (digite "fim" para sair): ')).strip()
    if comando.lower() == 'fim':
        break
    print(f'{cores["azul"]}Acessando o manual do comando "{comando}"...{cores["limpa"]}')
    help(comando)

print(f'{cores["amarelo"]}Até logo!{cores["limpa"]}')
```

`help()` mostra a documentação interativa de um objeto ou comando. `lower()` deixa o texto minúsculo para que `fim` seja reconhecido mesmo com outra combinação de maiúsculas. Os códigos `\033[...]` mudam as cores do terminal.
