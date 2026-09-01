# Python — Aula 02: Operações Aritméticas e Exercícios

## Operadores aritméticos

```python
n1 = int(input('digite um numero:'))
n2 = int(input('digite outro numero:'))
s = n1 + n2
m = n1 * n2
d = n1 / n2
di = n1 // n2
e = n1 ** n2
print(f'A soma é {s}, \n o produto é {m}, \n e a divisão é {d}')
print(f'A divisão inteira é {di}, \n e potência {e}')
```

Os operadores disponíveis:
- `+` → soma
- `*` → multiplicação
- `/` → divisão normal (resultado com decimais)
- `//` → divisão inteira (descarta o resto)
- `**` → potência

O `\n` dentro da f-string pula uma linha na saída.

## Exercícios resolvidos

**Soma e antecessor/sucessor**
```python
n = int(input('Digite um número: '))
n2 = int(input('digite outro número: '))
print(f'A soma de {n} e {n2} é igual a {n + n2}')
print(f'O antecessor de {n} é {n - 1} e o sucessor é {n + 1}')
```

---

**Dobro, triplo e raiz quadrada**
```python
n = int(input('Digite um numero:'))
print(f'O dobro de {n} é {n*2}, o triplo é {n*3} e a raiz quadrada é {n**(1/2)}')
```

A raiz quadrada é feita com `**(1/2)` — elevar à potência 1/2
é o mesmo que calcular a raiz quadrada.

---

**Média entre duas notas**
```python
n = int(input('qual a sua nota?'))
n2 = int(input('qual sua outra nota?'))
print(f'Sua nota geral foi {n+n2} e sua média é {(n+n2)/2}')
```

---

**Conversão de metros para centímetros e milímetros**
```python
m = float(input('Digite um valor em metros: '))
print(f'O valor em centímetros é {m*100} e em milímetros é {m*1000}')
```

---

**Tabuada sem loop**
```python
n = int(input('Digite um numero qualquer e veja sua tabuada: '))
print(f'{n} x 1 = {n*1}')
print(f'{n} x 2 = {n*2}')
print(f'{n} x 3 = {n*3}')
print(f'{n} x 4 = {n*4}')
print(f'{n} x 5 = {n*5}')
print(f'{n} x 6 = {n*6}')
print(f'{n} x 7 = {n*7}')
print(f'{n} x 8 = {n*8}')
print(f'{n} x 9 = {n*9}')
print(f'{n} x 10 = {n*10}')
```

Funcionou, mas está repetitivo — quando eu aprender sobre loops isso será mais prático.

---

**Conversão de reais para dólares**
```python
n = float(input('Quanto dinheiro você tem? R$'))
print(f'Você tem R${n} e pode comprar US${n/3.27:.2f} dólares.')
```

---

**Área da parede e quantidade de tinta**
```python
l = int(input('Qual a largura? '))
a = int(input('Qual a altura? '))
area = l * a
litros = area / 2
print(f'A área da parede é de {area} m².')
print(f'Para pintá-la são necessários {litros} litros de tinta.')
```


---

**Desconto de 5%**
```python
p = float(input('Quanto custa o produto? R$'))
d = p * 0.05
print(f'O novo preço com desconto é R${p-d:.2f}')
```

---

**Aumento de 15% no salário**
```python
s = float(input('Qual o seu salário? R$'))
aumento = s * 0.15
print(f'Seu novo salário com 15% de aumento é R${s+aumento:.2f}')
```
