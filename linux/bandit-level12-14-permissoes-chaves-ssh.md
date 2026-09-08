# Bandit — Level 12 ao 14: Permissões, Chaves SSH e SCP

## Level 12 — identificando e descompactando arquivos

| Comando | O que faz | Quando usar |
|---------|-----------|-------------|
| `mktemp -d` | Cria diretório temporário único | No início, pra ter um lugar limpo |
| `cp` | Copia arquivos | Pra trazer o data.txt original |
| `mv` | Move ou renomeia | Pra mudar extensão (.bin → .gz) |
| `file` | Mostra o tipo do arquivo | SEMPRE antes de descompactar |
| `xxd -r` | Converte hexdump pra binário | Primeiro passo, com `>` |
| `gzip -d` | Descompacta .gz | Quando `file` disser gzip compressed |
| `bzip2 -d` | Descompacta .bz2 | Quando `file` disser bzip2 compressed |
| `tar -xvf` | Extrai .tar | Quando `file` disser POSIX tar archive |
| `cat` | Mostra conteúdo | No final, quando for ASCII text |

```bash
xxd -r data.txt > data.bin
```

- `xxd -r data.txt` → lê o hexadecimal presente no arquivo
- `>` → redireciona a saída
- `data.bin` → cria (ou sobrescreve) o arquivo com os
  bytes binários resultantes

---

## Level 13 — chmod e permissões

**chmod = change mode** — altera as permissões de um
arquivo.

As permissões são divididas em três grupos:

```
600
│││
││└── outros
│└─── grupo
└──── proprietário
```

Cada número representa uma soma de permissões:
```
r = 4 (read)
w = 2 (write)
x = 1 (execute)
```

`600` = `4+2` = **rw-** para o proprietário, e **---**
(nada) para grupo e outros. Ou seja: só o proprietário
pode ler e escrever.

### Lendo o resultado do ls -l

```bash
ls -l ~/Documentos/sshkey.private
```

```
-rw-------
│ │  │  │
│ │  │  └── outros
│ │  └───── grupo
│ └──────── proprietário
└────────── tipo do arquivo
```

Nesse caso: `rw-` (leitura+escrita) pro dono, `---`
(nada) pro grupo e outros.

### Erro "0664 are too open"

```
owner  → rw-
group  → rw-
other  → r--
```

Isso significa que outras pessoas conseguem **ler**
a chave privada. O SSH considera isso inseguro e
simplesmente **ignora** a chave — recusa usá-la até
a permissão ser corrigida.

---

## Conectando com chave privada

```bash
ssh -i ~/Documentos/sshkey.private bandit14@bandit.labs.overthewire.org -p 2220
```

- `ssh` → programa usado pra estabelecer conexão SSH
- `-i` → "use este arquivo como identidade/chave privada"
- `-p` → "conecte usando a porta TCP 2220"

## Level 14 — SCP

**scp** permite copiar arquivos através de uma conexão
SSH:

```
scp origem destino

origem → servidor:/caminho/arquivo
destino → computador local
```

```
SSH → conexão/interação com o servidor
SCP → transferência de arquivos entre máquinas
```

## Autenticação por chave

O SSH não precisa necessariamente de senha — pode
usar par de chaves:

```
chave privada + chave pública → autenticação
```

A chave privada nunca deve ficar acessível pra outros
usuários — por isso `chmod 600` é a configuração
padrão pra proteger uma chave privada.
