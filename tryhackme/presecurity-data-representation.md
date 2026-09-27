# TryHackMe — Pre-Security: Data Representation

## Por que o computador usa binário

A gente usa decimal naturalmente (base 10): 0 1 2 3 4
5 6 7 8 9. O computador trabalha só com dois estados:
0 e 1 — binário (base 2).

Pensando numa lâmpada: desligada = 0, ligada = 1. Um
bit é justamente um desses dois estados.

## Quanto mais bits, mais possibilidades

```
1 bit  → 2 possibilidades
2 bits → 4 possibilidades
3 bits → 8 possibilidades
4 bits → 16 possibilidades
8 bits → 256 possibilidades
```

A fórmula é: **possibilidades = 2 elevado ao número de
bits**. Por isso 8 bits dá 256 (2⁸).

## Aplicando isso em cores (RGB)

Com 3 bits (um pra cada cor: R, G, B), cada canal é só
ligado ou desligado — 8 combinações possíveis:

```
000 = Preto      101 = Magenta
001 = Azul       110 = Amarelo
010 = Verde      111 = Branco
100 = Vermelho   011 = Ciano
```

Exemplo: R=1, G=0, B=1 dá Magenta.

## Adicionando intensidade

Ao invés de só ligado/desligado, cada canal pode ter
256 níveis de intensidade (0 = nenhum, 255 = máximo).

Com 3 canais de 256 possibilidades cada:
```
256 × 256 × 256 = 16.777.216 combinações
```

16 milhões de cores possíveis — isso que dá aquela
variedade toda que vemos na tela.

```
256 possibilidades = 8 bits = 1 byte
```

Cada canal (R, G, B) ocupa 1 byte — total de 3 bytes
(24 bits) pra representar uma cor completa.

## Por que usamos hexadecimal

Ler `10100011` direto em binário é difícil. Por isso
usamos hexadecimal — base 16, com os símbolos:
```
0 1 2 3 4 5 6 7 8 9 A B C D E F
```
Onde A=10, B=11, C=12, D=13, E=14, F=15.

O truque é que **1 dígito hexadecimal = exatamente 4
bits**, porque 4 bits dá 16 possibilidades (2⁴), que
é exatamente a quantidade de símbolos do hexadecimal.

```
0 = 0000    6 = 0110    D = 1101
1 = 0001    7 = 0111    E = 1110
2 = 0010    8 = 1000    F = 1111
3 = 0011    A = 1010
4 = 0100    B = 1011
5 = 0101    C = 1100
```

## Aplicando na cor hexadecimal

Cada cor tem 24 bits total (8 por canal). Como cada
hexadecimal representa 4 bits: `24 ÷ 4 = 6` dígitos
hexadecimais — por isso códigos de cor tipo `#A3EA2A`
sempre têm 6 caracteres.

```
#A3EA2A
A3 → Vermelho (R)
EA → Verde (G)
2A → Azul (B)
```

Cada par de dígitos hex = 1 byte = 1 canal de cor.

Convertendo pra binário:
```
A3 = 1010 0011
EA = 1110 1010
2A = 0010 1010
```

Hexadecimal não é "outra cor" — é só uma forma mais
compacta de escrever os mesmos bits.

## A matemática por trás da conversão

No decimal, cada posição representa uma potência de 10:
```
213 = 2×10² + 1×10¹ + 3×10⁰
```

No binário é a mesma lógica, só que com base 2:
```
1001
1  0  0  1
↓  ↓  ↓  ↓
8  4  2  1  (potências de 2: 2³ 2² 2¹ 2⁰)

1×8 + 0×4 + 0×2 + 1×1 = 9

Então: 1001₂ = 9₁₀
```

Cada bit "seleciona" ou não aquela potência na soma.

Mais um exemplo:
```
1101
8 4 2 1
1 1 0 1
8 + 4 + 1 = 13

1101₂ = 13₁₀
```

E convertendo direto pra hexadecimal:
```
1111₂ = 15₁₀ = F₁₆
1010₂ = 10₁₀ = A₁₆
```

É por essa correspondência direta (4 bits = 1 hex) que
converter entre binário e hexadecimal é tão mais fácil
do que converter entre binário e decimal.

`FF` em hexadecimal = `1111 1111` em binário — o valor
máximo que 1 byte consegue representar.
