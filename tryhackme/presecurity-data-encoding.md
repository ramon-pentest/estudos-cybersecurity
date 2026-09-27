# TryHackMe — Pre-Security: Data Encoding

## Como o computador vira caractere

No computador, tudo é número. Pra esse número virar
caractere na tela existe o **encoding** (codificação).

```
65 = A
66 = B
67 = C
```

Se o computador encontra o número 65, ele sabe que deve
mostrar "A". O computador não guarda literalmente uma
"letra A" na memória — guarda dados numéricos em bits,
e o encoding é o acordo de como interpretar isso.

```
A → número → bits → memória
memória → bits → número → encoding → A
```

## Representation vs Encoding — a diferença

**Representation** é como o dado existe fisicamente:
```
01000001 (isso são só bits)
```

**Encoding** é o acordo sobre o que aquele número
significa:
```
01000001 → 65 → A (em ASCII)
```

A representação diz como o dado tá armazenado. O
encoding diz como interpretar esse dado.

**Isso explica aquele "Ã§ â€™" que às vezes aparece
num arquivo** — o problema não está necessariamente nos
dados em si, é o programa interpretando os bytes usando
um encoding diferente do que foi usado pra salvar.

## ASCII

Criado em 1963, usa 7 bits originalmente:
```
2⁷ = 128 códigos possíveis (0 até 127)
```

Cobre letras, números, pontuação e alguns caracteres de
controle.

**ASCII não é o "número universal do caractere"** — é
só uma tabela de correspondência que o padrão ASCII
específico define.

```
65 → A       66 → B       67 → C
```

Em hexadecimal a sequência fica organizada direitinho:
```
A = 41    Z = 5A
a = 61    z = 7A
```

Como a sequência é organizada, saber que `a = 61` já
permite deduzir que `b = 62`, `c = 63`, `d = 64`, e
assim por diante.

## Números também são caracteres em ASCII

```
'0' → 48
'1' → 49
'2' → 50
...
'9' → 57
```

Isso é diferente do número em si — `'5'` (o caractere,
entre aspas) não é o mesmo que `5` (o valor numérico).
Em ASCII, o caractere `'5'` tem o código 53.

Então quando escrevo a string `"123"`, o computador
representa três caracteres separados (`'1'`, `'2'`,
`'3'`), não o número 123 diretamente.

## Exemplo prático — "TryHackMe" em hexadecimal ASCII

```
T→54  r→72  y→79  H→48  a→61  c→63  k→6B  M→4D  e→65
```

Esses hexadecimais são só uma forma conveniente de
enxergar os bytes reais:
```
54 → 01010100 → 84 decimal → T
```

## Caracteres de controle

O `\n` (quebra de linha, quando aperto Enter) também é
um código:
```
00001010 = 0A (hex) = newline
```

Nem tudo num arquivo precisa ser uma letra visível —
existem esses caracteres de controle representados
também.

## O problema do ASCII — só cobria inglês

ASCII representa A-Z, a-z, 0-9, pontuação e controles
— mas não dava conta de `ç ã ñ Ω あ ب 😊`.

## ISO-8859 — tentativa regional que deu errado

Usar 8 bits em vez de 7 dá 256 possibilidades (mais 128
posições além do ASCII original) — mas ainda não é
suficiente pra todos os idiomas. Surgiram vários
padrões regionais diferentes:
```
ISO-8859-1 → Western European
ISO-8859-2 → Central/Eastern European
```

O problema: se um arquivo é salvo com ISO-8859-1 mas
aberto interpretando como ISO-8859-2, o mesmo conjunto
de bytes vira caractere errado — essa é a origem do
"gibberish" (texto embaralhado sem sentido).

## Unicode — a solução universal

Ao invés de cada região ter sua própria tabela, Unicode
cria um identificador único pra cada caractere do
mundo, chamado **code point**:

```
U+0041 → A
U+03A9 → Ω
U+3042 → あ
U+1F525 → 🔥
```

**Unicode é diferente de UTF-8:**
```
Unicode  → define QUAIS são os caracteres e seus code points
UTF-8    → define COMO esses code points viram bytes
```

```
Unicode: U+0041 → UTF-8: 41
```

## UTF-8 — o mais usado na web

Usa entre 1 e 4 bytes, dependendo do caractere:
```
ASCII (A-Z, 0-9)  → 1 byte (compatível direto com ASCII)
Caracteres complexos (Ω) → mais bytes
Emojis (🔥)        → até 4 bytes
```

A vantagem é não gastar 4 bytes em tudo — só gasta mais
quando o caractere realmente precisa.

## UTF-16

Usa 2 ou 4 bytes. Caracteres comuns cabem em 2 bytes;
alguns fora dessa faixa (como emojis) precisam de dois
blocos de 16 bits, totalizando 4 bytes.

Exemplo — o emoji 🔥 em UTF-16:
```
U+D83D U+DD25 (dois code units de 16 bits)
```

## UTF-32 — o mais simples, mas gasta mais

Cada code point recebe sempre 4 bytes, sem variação:
```
A  → U+00000041
🔥 → U+0001F525
```

Vantagem: simplicidade. Desvantagem: gasta 4 bytes até
pra caracteres simples que caberiam em menos.

## Resumo dos três

```
UTF-8  → variável, 1 a 4 bytes (mais eficiente, mais usado)
UTF-16 → 2 ou 4 bytes
UTF-32 → sempre 4 bytes (mais simples, menos eficiente)
```
