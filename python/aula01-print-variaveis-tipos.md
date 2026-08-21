# Python — Aula 01: Print, Variáveis e Tipos Primitivos

## Print

Todo comando no Python é uma função. O `print` é a
ordem de "escreva isso na tela".

Para executar qualquer função é necessário abrir e
fechar parênteses `()`. Para exibir texto, o conteúdo
vai entre aspas simples:

```python
print('olá mundo')
```

Para exibir só números, as aspas não são necessárias:

```python
print(5 + 5)   # resultado: 10
```

Para misturar texto e número:

```python
print('olá', 5)   # resultado: olá 5
```

Atenção: `'5' + '4'` resulta em `54` — porque quando
os números estão entre aspas, o Python os trata como
texto e junta os dois, não soma.

## Variáveis

Variável é um espaço na memória onde um valor fica
salvo. Em Python, o `=` significa "receber" — não é
comparação, é atribuição.

```python
nome = 'Carlos'
```

Todo valor guardado numa variável é um objeto no Python.

## F-string — inserindo variáveis dentro de texto

```python
nome = 'Carlos'
print(f'Olá, {nome}!')
```

O que acontece por baixo:
1. O `print` lê o que está dentro dos parênteses
2. O `f` antes das aspas avisa que há expressões `{}`
   dentro do texto
3. O Python vai até a memória, pega o valor de `nome`
4. Substitui `{nome}` pelo valor `Carlos`
5. A string final `"Olá, Carlos!"` é montada na memória
6. O `print` exibe o resultado na tela

Dentro das chaves `{}` o Python executa expressões
antes de substituir:
```python
print(f'{nome.upper()}')   # CARLOS
print(f'{10 + 5}')         # 15
```

## Tipos primitivos

### int — números inteiros

```python
n1 = int(input('digite um numero: '))
n2 = int(input('digite outro numero: '))
soma = n1 + n2
print(f'a soma entre {n1} e {n2} é {soma}')
```

O `int()` converte o que o usuário digitou de texto
para número inteiro — sem ele, o Python trataria o
input como string.

### float — números com casas decimais

```python
n = float(input('digite um numero: '))
print(type(n))
```

O `float` identifica e trabalha com números quebrados
(com vírgula/ponto decimal).

### type() — descobrir o tipo de um valor

```python
n = input('Digite algo: ')
print(type(n))
```

O `type()` retorna qual é o tipo daquele valor —
útil para entender o que o Python está vendo.

### Métodos úteis para strings

```python
print(n.isalpha())   # True se for só letras
print(n.isalnum())   # True se for letras e/ou números
print(n.isdigit())   # True se for só dígitos
```
