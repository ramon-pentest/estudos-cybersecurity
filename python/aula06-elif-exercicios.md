# Python — Aula 06: elif e Múltiplas Condições

## Financiamento de casa
```python
casa = float(input('Quanto custa a casa?: '))
salario = float(input('Quanto você ganha?: '))
anos = int(input('Por quantos anos você pretende pagar?: '))
meses = anos * 12
prestacao = casa / meses
limite = salario * 0.30

if prestacao <= limite:
    print('Você pode parcelar a casa! ')
    print(f'A prestação mensal seria de R$ {prestacao:.2f}')
else:
    print('Você não pode pagar a casa!')
    print(f'A prestacao mensal seria {prestacao:.2f}')
    print(f'Seu limite para financiamento seria de R$ {limite:.2f}')
```

---

## Conversão de base numérica
```python
numero = int(input('Escreva qualquer numero: '))
print('Decida qual será a base de conversão: ')
print('-1 para binário')
print('-2 para octal ')
print('-3 para hexadecimal ')
opcao = int(input('Qual sua opção? '))
if opcao == 1:
    print(f'Você escolheu binário: {bin(numero)[2:]}')
elif opcao == 2:
    print(f'Você escolheu octal: {oct(numero)[2:]}')
elif opcao == 3:
    print(f'Você escolheu hexadecimal: {hex(numero)[2:]}')
else:
    print('Opção invalida! ')
```

---

## Comparando dois números
```python
n1 = int(input('Digite um número: '))
n2 = int(input('Digite outro número: '))
if n1 > n2:
    print('o primeiro valor é maior:')
elif n1 < n2:
    print('o segundo valor é maior:')
else:
    print('Não existe valor maior, ambos são iguais. ')
```

---

## Alistamento militar
```python
from datetime import date
ano = int(input('Em que ano você nasceu?'))
atual = date.today().year
idade = atual - ano
if idade >= 18: 
    print('Voce precisa se alistar')
else:
    print('Você ainda tá novo para isso.')
```
---

## Média com recuperação
```python
nota = float(input('Qual sua nota? '))
nota2 = float(input('Qual sua segunda nota?'))
resultado = (nota + nota2) / 2
if resultado >= 7:  
    print('você foi aprovado!')
    print(f'Essa foi sua nota: {resultado}')
elif resultado >= 5:  
    print('Você está de recuperação.')
    print(f'Essa foi sua nota: {resultado}')
else:
    print('Você foi reprovado.')
    print(f'Essa foi sua nota: {resultado}')
```

---

## Categoria de natação por idade
```python
from datetime import date
ano = int(input('Em que ano você nasceu? '))
atual = date.today().year
idade = atual - ano
if idade <= 9:
    print('sua categoria na natação nacional é Mirim!')
elif idade <= 14:  
    print('Sua categoria na natação nacional é Infantil!')
elif idade <= 19: 
    print('Sua categoria na natação nacional é Junior!')
elif idade >= 20: 
    print('Sua categoria na natação nacional é Sênior!')
else:
    print('Sua categoria na natação nacional é Master!')
```

## Cálculo de IMC — duas versões

**Versão 1 — mais enxuta**
```python
peso = float(input('Digite seu peso: '))
altura = float(input('Digite sua altura: '))
imc = peso / (altura ** 2)
if imc < 18.5:
    print('Você está abaixo do peso! ')
elif imc < 25:
    print('Você está no Peso ideal! ')
elif imc < 30:
    print('Você está com sobrepeso ')
elif imc < 40:
    print('Você está obeso')
else:
    print('Você está com obesidade mórbiida! ')
```

**Versão 2 — mesma lógica, com and explícito (redundante mas funcional)**
```python
peso = float(input('Digite seu peso: '))
altura = float(input('Digite sua altura: '))
elevado = altura ** 2
resultado = peso / elevado
if resultado <= 18.5:
    print('Você está abaixo do peso! ')
elif resultado <= 25:
    print('Você está no Peso ideal! ')
elif resultado <= 30: 
    print('Você está com sobrepeso ')
elif resultado <= 40:
    print('Você está obeso')
else:
    print('Você está com obesidade mórbiida! ')
```

---

## Forma de pagamento com desconto/parcelamento
```python
p = float(input('Qual o preço do produto? R$ '))
fp = int(input("""
=== FORMAS DE PAGAMENTO ===
[1] À vista (dinheiro/cheque) - 10% de desconto
[2] À vista no cartão         - 5% de desconto
[3] Parcelado no cartão       - Até 2x sem juros | 3x+ com 20% de juros
===========================
Escolha a opção: """))

if fp == 1:
    total = p * 0.90
    print(f'\n À vista: R$ {total:.2f} (Economia de R$ {p*0.10:.2f})')

elif fp == 2:
    total = p * 0.95
    print(f'\n Cartão à vista: R$ {total:.2f} (Economia de R$ {p*0.05:.2f})')

elif fp == 3:
    np = int(input('Quantas parcelas? (1 a 12): '))

    if np <= 0:
        print('❌ Número de parcelas inválido!')
    elif np <= 2:
        parcela = p / np
        print(f'\n {np}x de R$ {parcela:.2f} sem juros')
        print(f'   Total: R$ {p:.2f}')
    else:
        total = p * 1.20
        parcela = total / np
        print(f'\n {np}x de R$ {parcela:.2f} com juros')
        print(f'   Total a prazo: R$ {total:.2f} (Juros: R$ {total-p:.2f})')

else:
    print(' Opção inválida! Digite 1, 2 ou 3.')
```


---

## Triângulo — tipo e classificação
```python
r1 = float(input('Primeiro segmento: '))
r2 = float(input('Segundo segmento: '))
r3 = float(input('Terceiro segmento:'))
if r1 < r2 + r3 and r2 < r1 + r3 and r3 < r1 + r2:
    print('Os segmentos acima PODEM formar um triângulo! ')
    if r1 == r2 == r3:
        print('Equilátero!')
    elif r1 != r2 and r2 != r3 and r3 != r1: 
        print('Escaleno!')
    else:
        print('Isósceles!')
else:
    print('Os segmentos acimas NÂO podem formar um triângulo! ')
```
