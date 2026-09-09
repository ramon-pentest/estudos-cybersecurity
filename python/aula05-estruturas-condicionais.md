# Python — Aula 05: Estruturas Condicionais

## if

Testa uma condição. Se ela for verdadeira (True), o
bloco indentado abaixo roda. Se for falsa, o Python
simplesmente pula o bloco e segue em frente.

```python
if n >= 6:
    print('aprovado')
```

Sozinho, o if não garante que algo aconteça caso a
condição seja falsa — ele só cobre o caso em que ela
é verdadeira.

## else

Sempre vem depois de um if. Significa "senão" — roda
quando a condição do if é falsa. Junto, if/else garante
que um dos dois blocos sempre executa, nunca os dois.

```python
if n >= 6:
    print('aprovado')
else:
    print('reprovado')
```

dois if soltos no lugar de if/else: os
dois são testados de forma independente, então é
possível (e às vezes indesejado) que as duas condições
sejam verdadeiras ao mesmo tempo e as duas mensagens
apareçam juntas.

## elif

Contração de "else if". Usado quando há mais de duas
possibilidades. O Python testa as condições em ordem,
de cima para baixo, e para no primeiro if/elif que
for verdadeiro — não continua testando os de baixo.

```python
if media >= 9:
    print('A')
elif media >= 7:
    print('B')
elif media >= 5:
    print('C')
else:
    print('D')
```

Diferença importante em relação a vários if separados:
no elif, assim que uma condição bate, o Python já sai
da estrutura — não verifica as próximas, mesmo que
também sejam verdadeiras.

## and

Operador lógico que exige que as duas condições ao
redor dele sejam verdadeiras ao mesmo tempo para o
resultado ser True. Se qualquer uma das duas for falsa,
o resultado já é False.

```python
if n1 > n2 and n1 > n3:
    maior = n1
```

Esse bloco só roda se n1 for maior que n2 E maior que
n3 — vencer só um dos dois não é suficiente.

| Condição | Resultado |
|----------|-----------|
| True and True | True |
| True and False | False |
| False and False | False |

## or

Operador lógico que basta UMA das duas condições ser
verdadeira para o resultado ser True. Só é False quando
as duas são falsas.

```python
if dia == 'sabado' or dia == 'domingo':
    print('fim de semana')
```

Aqui basta o dia ser sábado OU domingo — não precisa
das duas coisas ao mesmo tempo (o que, aliás, seria
impossível).

| Condição | Resultado |
|----------|-----------|
| True or True | True |
| True or False | True |
| False or False | False |

## Resumo rápido

- **if** → roda se a condição for verdadeira
- **else** → roda quando a condição do if é falsa (o "resto dos casos")
- **elif** → testa outra condição, só quando a de cima foi falsa; para no primeiro que bater
- **and** → precisa das duas condições verdadeiras
- **or** → basta uma das duas condições ser verdadeira

---

## Exercícios resolvidos

**Adivinhando um número aleatório**
```python
import random
n = random.randint(0, 5)
palpite = int(input('tente acertar: '))
if palpite == n:
    print('você acertou')
else:
    print('Tá perto, mas não é esse..')
print(f'Pensei no numero {n}')
```

---

**Multa por excesso de velocidade**
```python
v = float(input('Qual velocidade passou esse carro? '))
if v > 80:
    print('Voce foi multado por exceder o limite de velocidade')
    m = (v-80) * 7.00
    print(f'O valor da multa é: {m}')
```

---

**Par ou ímpar**
```python
n = int(input('Digite um numero'))
if n % 2 == 0:
    print('Par')
else:
    print('Impar')
```

O `%` (módulo) retorna o resto da divisão — se o resto
da divisão por 2 é 0, o número é par.

---

**Preço de passagem com desconto para viagem longa**
```python
d = float(input('Quantos kms é a viagem?'))
preco = d * 0.50
longa = d * 0.45
print(f'A viagem custa {preco:.2f}')
if d >= 200:
    print(f'o preço da passagem é: {longa:.2f}')
```

---

**Mesma lógica, com if/else em vez de dois blocos separados**
```python
km = float(input('Qual a distância em (Km) você deseja percorrer? '))
if km <= 200:
    print(f'Sua passagem vai custar {km * .5} reais.')
else:
    print(f'Sua passagem vai custar {km * .45} reais.')
```

---

**Ano bissexto**
```python
ano = int(input('Que ano estamos?: '))
if ano % 4 == 0 and ano % 100 != 0 or ano % 400 == 0:
    print('É bissexto')
else:
    print('Não é bissexto')
```

---

**Comparando três números — primeira tentativa (interpretei errado)**

O enunciado pedia só o maior e o menor, mas acabei
comparando cada número com os outros dois, dizendo
qual é maior em cada par:

```python
n1 = int(input('Digite um numero'))
n2 = int(input('Digite outro numero'))
n3 = int(input('Digite mais um numero'))
if n1 > n2:
    print(f'{n1} é maior que {n2}')
else:
    print(f'{n2} é maior que {n1}')
if n2 > n3:
    print(f'{n2} é maior que {n3}')
else:
    print(f'{n3} é maior que {n2}')
if n3 > n1:
    print(f'{n3} é maior que {n1}')
else:
    print(f'{n1} é maior que {n3}')
```

**Versão correta — usando max() e min()**
```python
n1 = int(input('digite o primeiro numero : '))
n2 = int(input('digite um segundo numero : '))
n3 = int(input('digite o terceiro numero : '))

print('o maior:', max(n1, n2, n3))
print('o menor:', min(n1, n2, n3))
```

`max()` e `min()` já fazem a comparação entre vários
valores de uma vez, sem precisar de if — muito mais
direto pra esse tipo de problema.

---

**Aumento de salário condicional**
```python
n = float(input('Qual teu sálario ?'))
menor = (n * 0.10)
maior = (n * 0.15)
if n >= 1250:
    novo_salario = n + menor
    print(f'Seu salário aumenteu 10% {novo_salario + menor}')
else:
    novo_salario = n + maior
    print(f'Seu salário aumentou 15% agora é {novo_salario + maior}')
```

---

**Verificando se três segmentos formam um triângulo**
```python
r1 = float(input('Primeiro segmento: '))
r2 = float(input('Segundo segmento: '))
r3 = float(input('Terceiro segmento:'))
if r1 < r2 + r3 and r2 < r1 + r3 and r3 < r1 + r2:
    print('Os segmentos acima PODEM formar um triângulo! ')
else:
    print('Os segmentos acimas NÂO podem formar um triângulo! ')
```

Usa a regra da desigualdade triangular — cada lado
precisa ser menor que a soma dos outros dois.

---

**Média com feedback — versão com if/else tradicional**
```python
n1 = float(input('Digite sua nota: '))
n2 = float(input('Digite a outra nota: '))
m = (n1 + n2)/2
print(f'A sua média foi {(m):.1f}')
if m >= 6:
    print('A sua média foi boa')
else:
    print('A sua média não foi boa')
```

**Mesma lógica — versão condensada numa linha**
```python
n1 = float(input('Digite sua nota'))
n2 = float(input('Digite a outra nota'))
m = (n1 + n2)/2
print(f'A sua média foi{(m):.1f}')
print('parabens' if m >= 6 else 'estude mais')
```

Essa é a sintaxe de operador ternário — `valor_se_true
if condição else valor_se_false`, tudo numa linha só.
Faz a mesma coisa que o if/else de cima, mas mais
compacto.
