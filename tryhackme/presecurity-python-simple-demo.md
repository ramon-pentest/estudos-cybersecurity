# TryHackMe — Pre-Security: Python Simple Demo

Python é uma linguagem de programação de alto nível e
de propósito geral.

## Variáveis

Guardam valores que o programa precisa usar:
```python
secret = 13
guess = 8
tries = 0
```

`=` faz atribuição.

## Entrada e saída

```
print()  → mostra informação na saída
input()  → recebe entrada do usuário, retorna como texto (string)
int()    → converte texto numérico pra inteiro
```

Fluxo:
```
input() → "8" → int() → 8
```

## Condicionais

```python
if condição:
    ...
elif outra_condição:
    ...
else:
    ...
```

```
if    → testa uma condição
elif  → testa outra condição caso as anteriores sejam falsas
else  → executa o caso restante
```

## Operadores usados

```
<   menor que
>   maior que
!=  diferente de
or  OU
```

## Loops

```python
while condição:
    ...
```

Repete o bloco enquanto a condição for verdadeira.

No jogo:
```python
while guess != secret:
```

Significa: "continue repetindo enquanto o usuário ainda
não acertou."
