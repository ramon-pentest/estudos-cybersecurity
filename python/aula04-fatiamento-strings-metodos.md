# Python — Aula 04: Fatiamento e Métodos de String

## Fatiamento

```python
frase = 'Curso em video'
print(frase[9:12])
```

O fatiamento pega uma fatia da string por posição.
Cada caractere tem um número, começando do 0 — inclusive
espaços contam como posição.

O detalhe que me confundiu no começo: `frase[9:12]`
pega do 9 até o 11, não até o 12. O Python sempre
ignora a última posição informada — por isso pra pegar
"vide" (e não "video") o resultado veio incompleto,
porque o índice do "o" final estaria no 12, mas o
Python para antes dele.

**Os dois pontos `:`** funcionam como marcador de
início/fim:

```python
frase[:5]    # do início (0) até o 5
frase[15:]   # do 15 até o final da string
```

**Pulando caracteres no fatiamento:**
```python
frase[2:7:2]   # do 2 ao 7, pulando de 2 em 2
frase[9::3]    # do 9 até o final, pulando de 3 em 3
```

O terceiro número depois dos dois pontos é o "passo"
— de quanto em quanto ele avança.

---

## Métodos de análise

**len() — comprimento da string**
```python
len(frase)   # 21 caracteres em 'Curso em video'
```

`len` vem de *length*.

**count() — contar ocorrências**
```python
frase.count('o')   # conta 3 "o" na frase
```

Também dá pra combinar com fatiamento:
```python
frase.count('o', 0, 13)   # conta só entre a posição 0 e 13
```

**find() — encontrar posição**
```python
frase.find('deo')   # retorna a posição 11
frase.find('android')   # retorna -1, porque não existe
```

Quando não encontra, o `find` retorna `-1` como sinal
de que a busca falhou.

**in — verificar se existe**
```python
'Curso' in frase   # True ou False
```

---

## Métodos de transformação

```python
frase.replace('Python', 'Android')   # substitui uma palavra por outra
frase.upper()      # tudo maiúsculo
frase.lower()      # tudo minúsculo
frase.capitalize() # só a primeira letra da frase maiúscula
frase.title()      # primeira letra de cada palavra maiúscula
frase.strip()      # remove espaços extras do início e fim
frase.rstrip()     # remove espaço só da direita (right)
frase.lstrip()     # remove espaço só da esquerda (left)
```

---

## Divisão e junção

**split() — dividir a frase em pedaços**
```python
frase.split()
```

Divide a string em uma lista, separando por espaço.
Cada pedaço vira um item novo com sua própria contagem
de posição resetada.

**join() — juntar de volta**
```python
'-'.join(frase)
```

Junta os pedaços novamente, mas usando o caractere
informado no lugar do espaço — nesse caso um hífen.
Se quiser manter espaço normal, é só colocar um espaço
dentro das aspas.

**Strings com três aspas**
```python
print("""texto grande
que pode ocupar
várias linhas""")
```

Permite escrever textos longos, inclusive com quebra
de linha, sem precisar concatenar tudo.

---

## Combinando métodos

```python
frase.count('O')            # não encontra nada (só tem minúsculo)
frase.upper().count('O')    # encontra 3, porque primeiro deixou tudo maiúsculo
```

Dá pra encadear métodos — o resultado de um vira a
entrada do próximo.

---

## Acessando itens de uma lista dividida

```python
frase = 'Curso em Vídeo Python'
dividido = frase.split()
print(dividido[0])       # 'Curso'
print(dividido[2][3])    # letra 3 da palavra 'Vídeo' → 'e'
```

Dá pra combinar índice de lista com índice de string —
primeiro pega a palavra, depois pega a letra dentro dela.

---

## Exercícios de hoje

**Analisando um nome digitado**
```python
nome = input('Digite seu nome: ')
print(f'{nome.upper()}')
print(f'{nome.lower()}')
divido = nome.split()
replace = nome.replace(" ", "")
print(nome.replace(" ", ""))
print(len(replace))
print(divido[0])
print(len(divido[0]))
```

---

**Separando unidade, dezena, centena e milhar — versão 1**
```python
num = int(input('Digite um numero: '))
num = str(num)
print(f'Analisando o numero {num}')
print(f'unidade: {num[3]}')
print(f'dezena: {num[2]}')
print(f'centana: {num[1]}')
print(f'milhar: {num[0]}')
```

Aqui converti o número para string pra poder acessar
cada dígito pelo índice — mas isso só funciona se o
número tiver exatamente 4 dígitos.

**Versão alternativa — matemática, sem depender do tamanho**
```python
num = int(input('Digite um numero: '))
u = num // 1 % 10
d = num // 10 % 10
c = num // 100 % 10
m = num // 1000 % 10
print(f'Analisando o numero {num}')
print(f'unidade: {u}')
print(f'dezena: {d}')
print(f'centana: {c}')
print(f'milhar: {m}')
```

Essa versão é mais correta porque usa divisão inteira
`//` e resto `%` pra extrair cada dígito, funcionando
independente de quantos dígitos o número tiver.

---

**Verificando se a cidade começa com "SANTO"**
```python
cid = str(input('Em que cidade você nasceu? ')).strip()
print(cid[:5].upper() == 'SANTO')
```

---

**Verificando se o nome contém "silva"**
```python
nome = str(input('qual seu nome? ')).strip()
print(f'Seu nome tem Silva? {"silva" in nome.lower()}')
```

---

**Contando e localizando a letra A numa frase**
```python
frase = str(input('Digite uma frase:')).upper().strip()
print(f'A letra A aparece {frase.count("A")}')
print(f'A primeira letra A apareceu na posição {frase.find("A")+1}')
print(f'A última letra A apareceu na posição {frase.rfind("A")+1}')
```

O `+1` é porque a posição real do Python começa do 0,
mas pra mostrar pra pessoa fica mais natural contar
a partir do 1.

---

**Separando primeiro e último nome**
```python
n = str(input('Digite seu nome completo: ')).strip()
nome = n.split()
print('Muito prazer em te conhecer!')
print(f'Seu primeiro nome é: {nome[0]}')
print(f'Seu ultimo nome é {nome[len(nome)-1]}')
```

`len(nome)-1` pega a última posição da lista, porque
a contagem sempre começa do 0 — então se a lista tem
3 itens, o último está na posição 2, não na 3.
