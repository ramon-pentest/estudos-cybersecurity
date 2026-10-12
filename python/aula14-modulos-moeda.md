# Python — Aula 14: Módulos e Moedas

## Cálculos com módulo de moeda

```python
from utilidadesCeV import moeda

preco = float(input('Digite o preço: R$ '))
print(f'A metade de {preco} é {moeda.metade(preco)}')
print(f'O dobro de {preco} é {moeda.dobro(preco)}')
print(f'Aumentando 10%, temos {moeda.aumentar(preco, 10)}')
print(f'Reduzindo 10%, temos {moeda.diminuir(preco, 10)}')
```

`import` permite usar código de outro módulo. A notação `moeda.metade()` indica a função `metade` que está dentro do módulo `moeda`.

---

## Exibindo valores formatados

```python
from utilidadesCeV import moeda

preco = float(input('Digite o preço: R$ '))
print(f'A metade de {moeda.moeda(preco)} é {moeda.metade(preco, True)}')
print(f'O dobro de {moeda.moeda(preco)} é {moeda.dobro(preco, True)}')
print(f'Aumentando 10%, temos {moeda.aumentar(preco, 10, True)}')
print(f'Reduzindo 10%, temos {moeda.diminuir(preco, 10, True)}')
```

---

## Escolhendo o formato do resultado

```python
from utilidadesCeV import moeda

preco = float(input('Digite o preço: R$ '))
formatar = str(input('Exibir os resultados formatados como moeda? [S/N] ')).strip().upper() == 'S'

print(f'A metade de {moeda.moeda(preco)} é {moeda.metade(preco, formatar)}')
print(f'O dobro de {moeda.moeda(preco)} é {moeda.dobro(preco, formatar)}')
print(f'Aumentando 10%, temos {moeda.aumentar(preco, 10, formatar)}')
print(f'Reduzindo 10%, temos {moeda.diminuir(preco, 10, formatar)}')
```

---

## Resumo de valores

```python
from utilidadesCeV import moeda

preco = float(input('Digite o preço: R$ '))
taxa_aumento = float(input('Taxa de aumento (%): '))
taxa_reducao = float(input('Taxa de redução (%): '))
moeda.resumo(preco, taxa_aumento, taxa_reducao)
```

---

## Criando o pacote `utilidadesCeV`

O pacote reúne os módulos em uma pasta chamada `utilidadesCeV`. O módulo `moeda.py` concentra operações e formatação, e `dados.py` valida a entrada monetária.

```text
utilidadesCeV/
    __init__.py
    moeda.py
    dados.py
```

### Módulo `utilidadesCeV/moeda.py`

```python
def moeda(valor):
    valor_formatado = f'{valor:,.2f}'
    valor_formatado = valor_formatado.replace(',', 'X').replace('.', ',').replace('X', '.')
    return f'R$ {valor_formatado}'


def aumentar(preco, taxa, formato=False):
    resultado = preco + (preco * taxa / 100)
    return moeda(resultado) if formato else resultado


def diminuir(preco, taxa, formato=False):
    resultado = preco - (preco * taxa / 100)
    return moeda(resultado) if formato else resultado


def dobro(preco, formato=False):
    resultado = preco * 2
    return moeda(resultado) if formato else resultado


def metade(preco, formato=False):
    resultado = preco / 2
    return moeda(resultado) if formato else resultado


def resumo(preco, taxa_aumento=10, taxa_reducao=5):
    print('-' * 40)
    print(f'{"RESUMO DO VALOR":^40}')
    print('-' * 40)
    print(f'Preço analisado: {moeda(preco):>25}')
    print(f'Dobro do preço: {moeda(dobro(preco)):>26}')
    print(f'Metade do preço: {moeda(metade(preco)):>24}')
    print(f'{taxa_aumento}% de aumento: {moeda(aumentar(preco, taxa_aumento)):>24}')
    print(f'{taxa_reducao}% de redução: {moeda(diminuir(preco, taxa_reducao)):>24}')
    print('-' * 40)
```

O valor padrão `formato=False` mantém o resultado numérico quando o parâmetro não é informado. A expressão condicional em cada função retorna o número ou o texto formatado. `replace()` troca um trecho de texto por outro.

---

## Usando os módulos do pacote

```python
from utilidadesCeV import dados, moeda

preco = float(input('Digite o preço: R$ '))
print(f'Valor informado: {moeda.moeda(preco)}')
print(f'Metade: {moeda.metade(preco, True)}')
print(f'Dobro: {moeda.dobro(preco, True)}')
print(f'Aumentando 10%: {moeda.aumentar(preco, 10, True)}')
print(f'Reduzindo 10%: {moeda.diminuir(preco, 10, True)}')
print(f'Validação de valor monetário: {dados.leiaDinheiro("Digite outro valor: R$ ")}')
```

### Módulo `utilidadesCeV/dados.py`

```python
import re


def leiaDinheiro(mensagem):
    while True:
        entrada = str(input(mensagem)).strip()
        entrada = re.sub(r'^R\$\s*', '', entrada, flags=re.IGNORECASE)
        entrada = entrada.replace(' ', '')

        inteiro = r'[+-]?\d+'
        decimal_brasileiro = r'[+-]?\d+,\d{1,2}'
        milhar_brasileiro = r'[+-]?\d{1,3}(?:\.\d{3})+(?:,\d{1,2})?'
        decimal_ponto = r'[+-]?\d+\.\d{1,2}'

        if re.fullmatch(milhar_brasileiro, entrada):
            valor = entrada.replace('.', '').replace(',', '.')
            return float(valor)
        if re.fullmatch(decimal_brasileiro, entrada):
            return float(entrada.replace(',', '.'))
        if re.fullmatch(decimal_ponto, entrada):
            return float(entrada)
        if re.fullmatch(inteiro, entrada):
            return float(entrada)

        print(f'\033[31mErro: "{entrada}" não é um valor monetário válido.\033[m')
```

`re` oferece ferramentas de expressão regular. `re.fullmatch()` só aceita a entrada quando todo o texto combina com o formato esperado; por isso valores com letras ou separadores fora do lugar são rejeitados.

---

## Resumo com entrada validada

```python
from utilidadesCeV import dados, moeda

preco = dados.leiaDinheiro('Digite o preço: R$ ')
taxa_aumento = dados.leiaDinheiro('Taxa de aumento (%): ')
taxa_reducao = dados.leiaDinheiro('Taxa de redução (%): ')
moeda.resumo(preco, taxa_aumento, taxa_reducao)
```
