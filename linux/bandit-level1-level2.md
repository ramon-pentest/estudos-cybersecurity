# Bandit — Level 1 e Level 2

## Level 1 — Arquivo com nome especial (hífen)

O desafio era ler um arquivo chamado `-` (hífen).
O problema é que o Linux interpreta `-` como uma opção
de comando, não como nome de arquivo.

A solução foi indicar o caminho completo:
`cat ./-`

O `./` diz pro Linux: "estou falando de um arquivo
aqui na pasta atual", aí ele para de interpretar
o hífen como opção.

## Level 2 — Arquivo com espaços no nome

O desafio era ler um arquivo com espaços no nome.
O problema é que o Linux interpreta cada espaço
como separação entre argumentos diferentes.

Três formas de resolver:

Usando aspas — tudo entre aspas vira um argumento só:
`cat "spaces in this filename"`

Usando barra invertida antes de cada espaço:
`cat spaces\ in\ this\ filename`

Usando `--` antes do nome para o Linux parar de
interpretar o que vem depois como opção:
`cat -- "spaces in this filename"`

## Variações do comando ls que aprendi

| Comando | O que faz |
|---------|-----------|
| `ls` | Lista os arquivos da pasta |
| `ls -l` | Lista em formato detalhado |
| `ls -a` | Lista incluindo arquivos ocultos |
| `ls -la` | Detalhado e com arquivos ocultos |
| `ls -1` | Lista um arquivo por linha |

## O que aprendi sobre opções de comando

Todo comando Linux segue essa estrutura:
`comando -opção argumento`

O `-` antes de uma letra indica que é uma opção,
não um arquivo. Por isso arquivos que começam com
`-` precisam de tratamento especial.
