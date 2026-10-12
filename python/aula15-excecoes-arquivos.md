# Python — Aula 15: Exceções, Rede e Arquivos

## Leitura de inteiros e números reais

```python
import math


def leiaInt(mensagem):
    while True:
        entrada = str(input(mensagem)).strip()
        try:
            return int(entrada)
        except ValueError:
            print('\033[31mErro! Digite um número inteiro válido.\033[m')


def leiaFloat(mensagem):
    while True:
        entrada = str(input(mensagem)).strip().replace(',', '.')
        try:
            valor = float(entrada)
            if not math.isfinite(valor):
                raise ValueError
            return valor
        except ValueError:
            print('\033[31mErro! Digite um número real válido.\033[m')


numero_inteiro = leiaInt('Digite um número inteiro: ')
numero_real = leiaFloat('Digite um número real: ')
print(f'Você digitou o inteiro {numero_inteiro} e o real {numero_real}.')
```

`except ValueError` captura falhas de conversão e permite pedir novamente. `math.isfinite()` rejeita `inf` e `nan`, que podem ser convertidos para `float`, mas não são números reais finitos. `replace(',', '.')` permite usar vírgula como separador decimal.

---

## Teste de acessibilidade de um site

```python
from urllib.error import HTTPError, URLError
from urllib.request import Request, urlopen


def verificar_site(url='https://www.pudim.com.br', timeout=5):
    requisicao = Request(url, headers={'User-Agent': 'Mozilla/5.0'})
    try:
        with urlopen(requisicao, timeout=timeout) as resposta:
            print(f'O site {url} está acessível (HTTP {resposta.status}).')
            return True
    except HTTPError as erro:
        print(f'O site {url} respondeu com HTTP {erro.code}; o servidor está acessível.')
        return True
    except (URLError, TimeoutError, OSError) as erro:
        print(f'Não foi possível acessar {url}: {erro}')
        return False


if __name__ == '__main__':
    verificar_site()
```

`Request` monta a requisição e `urlopen()` tenta acessar o endereço. `timeout` limita o tempo de espera. `HTTPError` indica que o servidor respondeu com um código HTTP de erro; `URLError` pode indicar falha de conexão. O bloco `with` fecha a resposta ao terminar.

---

## Sistema de cadastro modularizado

### Estrutura dos arquivos

```text
utilidadesCadastro/
    __init__.py
    arquivo.py
    interface.py
exercicio115.py
```

### Módulo `utilidadesCadastro/arquivo.py`

```python
import csv
from pathlib import Path


CAMINHO_ARQUIVO = Path(__file__).with_name('pessoas.csv')


def arquivoExiste():
    return CAMINHO_ARQUIVO.is_file()


def criarArquivo():
    with CAMINHO_ARQUIVO.open('a', encoding='utf-8', newline=''):
        pass


def lerArquivo():
    pessoas = []
    with CAMINHO_ARQUIVO.open('r', encoding='utf-8', newline='') as arquivo:
        for nome, idade in csv.reader(arquivo):
            pessoas.append((nome, int(idade)))
    return pessoas


def cadastrar(nome, idade):
    with CAMINHO_ARQUIVO.open('a', encoding='utf-8', newline='') as arquivo:
        csv.writer(arquivo).writerow([nome, idade])
```

`Path` representa caminhos de arquivos. `with` abre o arquivo e garante que seja fechado ao terminar o bloco. O modo `'a'` acrescenta registros sem apagar os anteriores, e `csv.writer()` organiza os campos em linhas separadas por vírgulas.

---

### Módulo `utilidadesCadastro/interface.py`

```python
def cabecalho(texto):
    print('-' * 40)
    print(f'{texto:^40}')
    print('-' * 40)


def leiaInt(mensagem):
    while True:
        try:
            return int(input(mensagem))
        except ValueError:
            print('\033[31mErro! Digite uma opção numérica válida.\033[m')


def menu():
    cabecalho('MENU PRINCIPAL')
    print('1 - Ver pessoas cadastradas')
    print('2 - Cadastrar nova pessoa')
    print('3 - Sair do sistema')
    print('-' * 40)
    return leiaInt('Sua opção: ')
```

---

### Programa principal `exercicio115.py`

```python
from utilidadesCadastro import arquivo, interface


def main():
    try:
        if not arquivo.arquivoExiste():
            arquivo.criarArquivo()
            print('Arquivo de cadastro criado.')

        while True:
            opcao = interface.menu()
            if opcao == 1:
                interface.cabecalho('PESSOAS CADASTRADAS')
                pessoas = arquivo.lerArquivo()
                if not pessoas:
                    print('Nenhuma pessoa cadastrada.')
                else:
                    for nome, idade in pessoas:
                        print(f'{nome:<30}{idade:>3} anos')
            elif opcao == 2:
                interface.cabecalho('NOVO CADASTRO')
                nome = input('Nome: ').strip()
                while not nome:
                    print('O nome não pode ficar vazio.')
                    nome = input('Nome: ').strip()
                idade = interface.leiaInt('Idade: ')
                while idade < 0:
                    print('A idade não pode ser negativa.')
                    idade = interface.leiaInt('Idade: ')
                arquivo.cadastrar(nome, idade)
                print(f'Cadastro de {nome} salvo com sucesso.')
            elif opcao == 3:
                print('Até logo!')
                break
            else:
                print('Opção inválida. Escolha 1, 2 ou 3.')
    except OSError as erro:
        print(f'Erro ao acessar o arquivo de cadastro: {erro}')


if __name__ == '__main__':
    main()
```

`csv.reader()` lê os registros e `csv.writer().writerow()` grava uma pessoa por linha. O teste `if __name__ == '__main__'` executa `main()` quando esse arquivo é iniciado diretamente, mas não quando é importado. `OSError` trata problemas de leitura e gravação de arquivos.
