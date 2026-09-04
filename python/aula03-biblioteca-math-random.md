# Python — Aula 03: Biblioteca Math e Random

## Como funciona uma biblioteca

Biblioteca é basicamente um conjunto de recursos prontos
que o Python disponibiliza pra usarmos. Ao invés de
escrever tudo do zero, apenas importamos o que precisa.

```python
import math
```

Isso faz o Python pegar todos os recursos de matemática
da biblioteca e disponibilizar pra uso.

Também dá pra importar algo específico:

```python
from math import sqrt
```

Uma diferença importante: quando importo com `from math import ceil`,
não preciso escrever `math.ceil` — só `ceil` já funciona.
Mas se importar tudo com `import math`, aí é obrigatório
escrever `math.floor`, `math.sqrt` e assim por diante.

## Exercícios resolvidos

**Número aleatório entre 1 e 10**
```python
import random
num = random.randint(1, 10)
print(num)
```

O `random.randint(1, 10)` gera um número inteiro aleatório
dentro do intervalo informado, incluindo os dois extremos.

---

**Conversão de Celsius para Fahrenheit**
```python
c = float(input('Informe um valor em Celsius: '))
f = 9 * c / 5 + 32
print(f'A temperatura é {f}°F!')
```

---

**Cálculo de aluguel de carro**
```python
d = int(input('Quantos dias o carro foi alugado? '))
km = float(input('Quantos kms o carro percorreu? '))
total_dias = d * 60
total_km = km * 0.15
print(f'O preço a pagar é: R${(total_dias + total_km):.2f}')
```

Cada dia custa R$60 e cada km custa R$0,15.
O `.2f` formata o resultado com duas casas decimais.

---

**Parte inteira de um número real**
```python
from math import trunc
n = float(input('Digite um numero real: '))
n = trunc(n)
print(f'A parte inteira é {n}')
```

O `trunc` simplesmente corta a parte decimal sem arredondar.

---

**Hipotenusa com Teorema de Pitágoras**
```python
from math import sqrt

a = float(input('Qual é o cateto oposto? '))
b = float(input('Qual é o cateto adjacente? '))
c = sqrt(a**2 + b**2)

print(f'A hipotenusa é: {c:.2f}')
```

A fórmula é `c = √(a² + b²)` — o `sqrt` calcula a raiz
quadrada e o `**2` eleva ao quadrado.

---

**Seno, cosseno e tangente de um ângulo**
```python
import math
an = float(input('Digite o ângulo que você deseja: '))
seno = math.sin(math.radians(an))
cosseno = math.cos(math.radians(an))
tangente = math.tan(math.radians(an))
print(f'O ângulo de {an}° tem seno {seno:.2f}')
print(f'O ângulo de {an}° tem cosseno {cosseno:.2f}')
print(f'O ângulo de {an}° tem tangente {tangente:.2f}')
```

O Python trabalha com radianos internamente, então o
`math.radians()` converte o ângulo em graus para radianos
antes de calcular.

---

**Sorteio de um aluno**
```python
import random
n1 = input('Primeiro aluno: ')
n2 = input('Segundo aluno: ')
n3 = input('Terceiro aluno: ')
n4 = input('Quarto aluno: ')
alunos = [n1, n2, n3, n4]
escolhido = random.choice(alunos)
print(f'O aluno escolhido foi {escolhido}')
```

O `random.choice()` escolhe um elemento aleatório de
uma lista — aqui foi a primeira vez que usei lista
em Python. Uma lista é uma coleção de valores entre
colchetes `[]`, separados por vírgula.

---

**Embaralhar ordem dos alunos**
```python
from random import shuffle
n1 = input('Nome do aluno: ')
n2 = input('Nome do aluno: ')
n3 = input('Nome do aluno: ')
n4 = input('Nome do aluno: ')
nome = [n1, n2, n3, n4]
shuffle(nome)
print(f'A ordem de apresentação é: {nome}')
```

O `shuffle` embaralha a lista diretamente — ele não
retorna uma nova lista, ele modifica a lista original.
