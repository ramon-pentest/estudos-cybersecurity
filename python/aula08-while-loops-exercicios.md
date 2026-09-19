# Python — Aula 08: While e Exercícios

## Loop while básico com continuação
```python
r = 'S'
while r == "S":
    n = int(input('Digite um valor '))
    r = str(input('Quer continuar? [S/N]')).upper()
```

O while repete enquanto a condição for verdadeira —
aqui, enquanto `r` for `'S'`. É diferente do `for`
porque não sei de antemão quantas vezes vai repetir,
depende da resposta do usuário a cada rodada.

---

## Contando pares e ímpares digitados
```python
n = 1
par = impar = 0
while n != 0:
    n = int(input('Digite um valor '))
    if n % 2 == 0:
        par += 1
    else:
        impar += 1
print(f'Você digitou {par} números pares e {impar} números impar')
```

`par = impar = 0` atribui zero pras duas variáveis de
uma vez. O loop continua até o usuário digitar 0,
que é o sinal de parada.

---

## Validando entrada M ou F
```python
n = 1
while n != 'M' and n != 'F':
    n = str(input('Digite seu sexo: ')).upper()
    if n != 'M' or n != 'F':
        print('Digite seu sexo corretamente')
print('Correto')
```

---

## Adivinhando o número (com while)
```python
import random
n = random.randint(0, 5)
palpite = -1
while palpite != n:
    palpite = int(input('Tenta advinhar o numero: '))
    if palpite == n:
        print('Você acertou! ')
    else:
        print('Tente novamente! ')
print(f'O numero que pensei foi {n}')
```

Diferença do exercício parecido que fiz antes com `if`:
aqui o `while` obriga a pessoa a continuar tentando até
acertar, ao invés de só dar uma chance e mostrar o
resultado.

---

## Menu de opções com dois números
```python
import random
n1 = int(input('Digite um número: '))
n2 = int(input('Digite outro número: '))
escolha = 1
while escolha != 5:
    escolha = int(input("""Escolha uma opção: \n[1]Somar \n[2]Multiplicar \n[3]Maior \n[4]Novos números \n[5]Sair do programa\n: """))
    if escolha == 1:
        print(f'A soma entre ambos os números é: {n1 + n2}')
    elif escolha == 2:
        print(f'A multiplicação entre ambos os números é: {n1 * n2}')
    elif escolha == 3:
        if n1 > n2:
            print('n1 é maior')
        else:
            print('n2 é maior')
    elif escolha == 4:
        n1 = int(input('Digite um novo número: '))
        n2 = int(input('Digite outro novo número: '))
    else:
        print('Programa encerrado.')
```

Esse foi o primeiro exercício que juntou menu + while +
elif tudo numa estrutura só — o programa fica rodando
até a pessoa escolher a opção 5.

---

## Fatorial
```python
fatorial = 1
n1 = int(input('Digite um numero e veja seu fatorial: '))
for i in range(1, n1+1):
    fatorial = fatorial * i
print(f'O fatorial é {fatorial}')
```

Fatorial é a multiplicação de todos os números de 1 até
o número digitado — por isso o `range` vai até
`n1+1`, porque o range normalmente para antes do
último número.

---

## Progressão aritmética (10 termos fixos)
```python
termo = int(input('Digite um numero: '))
razao = int(input('Digite um numero: '))
contador = 1
while contador <= 10:
    print(termo)
    termo = termo + razao
    contador = contador + 1
```

---

## Progressão aritmética com quantidade escolhida pelo usuário
```python
termo = int(input('Digite um número: '))
razao = int(input('Digite um número: '))
quantidade = int(input('Quantos termos quer ver? '))
while quantidade != 0:
    i = 1
    while i <= quantidade:
        print(termo)
        termo = termo + razao
        i = i + 1
    quantidade = int(input('Quantos termos a mais você quer ver? (Digite 0 para sair)'))
```

Esse tem um while dentro de outro while — o de fora
controla se o programa continua perguntando, o de
dentro controla quantos termos mostrar em cada rodada.

---

## Sequência de Fibonacci
```python
n = int(input('Digite um numero para ver sua fibonacci '))
a = 0
b = 1
for i in range(n):
    print(a)
    proximo = a + b
    a = b
    b = proximo
```

Fibonacci é a sequência onde cada número é a soma dos
dois anteriores (0, 1, 1, 2, 3, 5, 8...). As variáveis
`a` e `b` vão "andando" a cada volta — `a` vira o
próximo e `b` vira a soma seguinte.

---

## Contando quantos números até digitar 999
```python
n1 = 1
soma = 0
contador = 0
while n1 != 999:
    n1 = int(input('Para parar o programa digite 999: '))
    if n1 != 999:
        soma = soma + 1
        contador = contador + 1
print(f'A quantidade de números digitados foi: {contador}')
print(f'A soma entre eles é {soma}')
```

---

## Estatísticas de vários números digitados
```python
soma = 0
contador = 0
maior = 0
menor = 9999999999
continuar = 'S'
while continuar == 'S':
    n = int(input('Digite um numero: '))
    soma = soma + n
    contador = contador + 1
    if n > maior:
        maior = n
    if n < menor:
        menor = n
    continuar = str(input('Quer continuar digitando (S/N):')).upper()

media = soma / contador
print(f'Média: {media}')
print(f'Maior valor: {maior}')
print(f'Menor valor: {menor}')
```

