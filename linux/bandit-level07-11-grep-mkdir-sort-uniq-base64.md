# Bandit — Level 7 ao 11: Novos Comandos

## Level 7 — Grep

O arquivo `data.txt` tinha diversas palavras desconexas
que pareciam ser senhas, com nomes aleatórios antes delas.
Usei `pwd` para saber onde estava, `ls -la` para ver os
arquivos do diretório, e `cat` para tentar ler — mas o
arquivo era grande demais para achar a senha assim.

Me lembrei do `grep` e usei:

```bash
grep millionth data.txt
```

O `grep` procura por uma palavra ou padrão dentro de um
arquivo e retorna só as linhas que contêm aquilo. Muito
mais eficiente do que ler o arquivo inteiro.

---

## Comandos novos — manipulação de arquivos e diretórios

**mkdir — criar diretório**
```bash
mkdir teste
```

Cria uma pasta chamada `teste` no diretório atual.

Para criar pastas dentro de pastas de uma vez:
```bash
mkdir -p "Download/Documentos/Fotos"
```

O `-p` cria toda a estrutura de uma vez, sem precisar
fazer manualmente pasta por pasta.

**ls -R — listar recursivamente**
```bash
ls -R
```

Lista todos os arquivos e pastas, incluindo o conteúdo
de subpastas. Muito útil quando a estrutura tem vários
níveis.

**touch — criar arquivo**
```bash
touch arquivo.txt
```

**rmdir — apagar diretório**
```bash
rmdir pasta
```

**rm — apagar arquivo**
```bash
rm arquivo.txt
```

**nano — criar ou editar arquivo**
```bash
nano teste.py
```

Abre o editor de texto no terminal. Útil para criar
scripts diretamente pelo terminal.

---

## Level 8 — Sort e Uniq

O arquivo `data.txt` tinha muitas linhas repetidas e
a senha era a única linha que aparecia só uma vez.

**sort — organizar linhas**
```bash
sort data.txt
```

Organiza todas as linhas em ordem alfabética.

**uniq — identificar repetições**
```bash
sort data.txt | uniq
```

O `uniq` identifica linhas duplicadas — mas só funciona
corretamente se o arquivo estiver ordenado, por isso
uso o `sort` antes com o pipe `|`.

Variação importante:
```bash
sort data.txt | uniq -u
```

O `-u` retorna somente as linhas que aparecem uma única
vez — sem nenhuma repetição. Foi exatamente isso que
usei para encontrar a senha.

---

## Level 9 — Strings

```bash
strings data.txt
```

Lê um arquivo e extrai sequências de caracteres legíveis
dentro dele — útil quando o arquivo é binário ou tem
muita coisa ilegível misturada com o conteúdo que
realmente importa.

---

## Level 10 — Base64

O Base64 codifica ou decodifica dados:

**Codificar:**
```bash
base64 arquivo.txt
```

**Decodificar:**
```bash
base64 -d arquivo.txt
```

É útil porque permite representar qualquer tipo de dado
(inclusive binário) usando apenas caracteres de texto.
Por isso é muito usado em transferência de e-mails,
URLs, tokens de autenticação e armazenamento de dados
em JSON ou XML sem corromper o conteúdo.

Em segurança, base64 aparece bastante em tokens JWT,
dados de autenticação e payloads de ataques
