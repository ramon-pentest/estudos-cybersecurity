# Bandit — Level 0 para Level 1

## O que era pra fazer

Conectar no servidor do Bandit via SSH e encontrar
a senha armazenada num arquivo chamado `readme`
no diretório pessoal.

## Como resolvi

Conectei usando o comando:
`ssh bandit0@bandit.labs.overthewire.org -p 2220`

Depois listei os arquivos com `ls` e vi o arquivo `readme`.
Usei `cat readme` para ler o conteúdo e a senha estava lá.

## Comandos que aprendi nesse level

| Comando | O que faz |
|---------|-----------|
| `ls` | Lista os arquivos da pasta atual |
| `cat` | Lê e mostra o conteúdo de um arquivo |
| `cd` | Muda de pasta |
| `pwd` | Mostra o caminho completo de onde você está |
| `file` | Mostra o tipo do arquivo |
| `find` | Procura arquivo pelo nome |
| `du` | Mostra o tamanho do arquivo |
| `man` | Abre o manual de qualquer comando |
| `ssh` | Conecta em servidores remotos |

## Símbolos importantes do Linux

| Símbolo | Significado |
|---------|-------------|
| `.` | Diretório atual |
| `..` | Pasta anterior |
| `/` | Separa pastas no caminho |
| `~` | Pasta pessoal (home) |
| `$` | Terminal esperando um comando |
| `@` | Indica usuário no computador |

## Dicas para pesquisar comandos

- `man [comando]` → manual completo, sair com `q`
- `[comando] --help` → explicação resumida
- `apropos [palavra]` → acha comandos relacionados ao tema
- `compgen -c` → lista todos os comandos do sistema
## Encontrando arquivos ocultos

O `find` consegue encontrar arquivos ocultos — o `ls`
sozinho não mostra. No Linux, qualquer arquivo que
começa com `.` é considerado oculto.

## Navegação rápida

`/tmp` funciona como um atalho — parecido com um botão
de "voltar" para uma pasta específica do sistema.

## O curinga `*`

O `*` representa "todos os arquivos da pasta atual".
file -- * → mostra o tipo de todos os arquivos da pasta
du -- * → mostra o tamanho de todos os arquivos da pasta


## Find com filtros específicos

O `find` pode buscar por características exatas do
arquivo, combinando várias condições:

find -type f -size 1033c ! -executable

- `-type f` → procura por arquivos (não pastas)
- `-size 1033c` → tamanho exato de 1033 bytes (o `c`
  indica que a unidade é bytes)
- `-executable` → o arquivo é executável
- `! -executable` → o `!` nega a condição, ou seja,
  procura por arquivo que NÃO é executável
