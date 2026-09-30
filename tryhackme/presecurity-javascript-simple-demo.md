# TryHackMe — Pre-Security: JavaScript Simple Demo

## Onde o JavaScript roda

JavaScript pode rodar de duas formas:
```
Navegador  → client-side, roda no PC do usuário
Node.js    → server-side, roda fora do navegador
```

## let vs const

`let` guarda um valor que pode ser alterado depois:
```javascript
let tries = 0;
let guess = 0;
```

`const` não pode ser reatribuída depois de criada — usei
pro número secreto do jogo, que precisa ser escolhido
uma única vez e permanecer igual durante toda a partida:
```javascript
const secret = Math.floor(Math.random() * 20) + 1;
```

## Gerando o número secreto

```
Math.random()          → produz decimal entre 0 e 1 (ex: 0.372)
Math.random() * 20      → amplia pra faixa 0 até 20 (ex: 7.44)
Math.floor(7.44)        → remove a parte decimal, arredondando
                           pra baixo (fica 0 a 19)
+ 1                      → transforma em 1 a 20
```

Resultado: número inteiro entre 1 e 20, incluindo os
dois extremos.

## Mostrando algo na tela

```
Python:     print('Hello')
JavaScript: console.log('Hello');
```

## Pegando o palpite do usuário

```javascript
const text = await rl.question("Take a guess: ");
guess = parseInt(text, 10);
```

O que o usuário digita chega como **texto**, não número
— se digitar "15", o programa lê isso como string.

`parseInt(text, 10)` pega esse texto e interpreta como
número inteiro na base 10 (decimal). O `10` indica
especificamente qual base numérica usar.

## Configurando a entrada no terminal

```javascript
import * as readline from "node:readline/promises";
import {stdin as input, stdout as output} from "node:process";
const rl = readline.createInterface({input, output});
```

O Node.js não foi feito principalmente pra ficar parado
esperando digitação no terminal, então é preciso criar
um canal entre o programa e o terminal:

```
Teclado → stdin → readline → programa JS → stdout → Tela

stdin     = entrada (normalmente teclado)
stdout    = saída (normalmente terminal)
readline  = ferramenta pra trabalhar com entrada de texto
rl        = objeto/interface criado pra conversar com o terminal
```

`rl.question(...)` significa: "use essa interface pra
fazer uma pergunta e esperar uma resposta."

## await — esperando a resposta

```javascript
const text = await rl.question("take a guess: ");
```

O `await` faz o programa esperar a resposta antes de
continuar a execução:
```
Pergunta → Espera → usuário digita → recebe resposta → continua
```

Sem essa espera, o programa poderia continuar executando
antes do usuário responder.

## try/finally — limpeza de recursos

```javascript
try {
  // código
} finally {
  rl.close();
}
```

A interface criada com `readline.createInterface()`
precisa ser fechada quando termina. O `finally` garante
que essa limpeza aconteça depois da tentativa de
executar o código — como abrir um microfone, usar, e
fechar depois.

## Incrementando

```javascript
tries = tries + 1;
```

Forma abreviada:
```javascript
tries += 1;
```

## Condicionais do jogo

```javascript
if (guess < 1 || guess > 20) {
    console.log("That number is out of range. Try again.");
} else if (guess < secret) {
    console.log("Too low, try again.");
} else if (guess > secret) {
    console.log("Too high, try again.");
} else {
    console.log("You got it in", tries, "tries!");
}
```

`||` significa **OR**. `if (guess < 1 || guess > 20)`
lê-se: "se guess for menor que 1 OU maior que 20..."

Exemplo: `guess = 35`
```
35 < 1  → falso
35 > 20 → verdadeiro
falso || verdadeiro = verdadeiro
```
Resultado: número fora da faixa.

## Como o programa sabe que acertou, sem usar ==

A sequência de `else if` vai eliminando possibilidades:
```
else if (guess < secret)   → não é menor
else if (guess > secret)   → não é maior
else                        → só sobra: é igual
```

Exemplo: `secret = 10, guess = 10`
```
10 < 10 → falso
10 > 10 → falso
```
Logo, cai no `else` — acertou.

## Operadores de comparação

```
=   → atribuição
===  → comparação de igualdade estrita
!==  → comparação de desigualdade estrita
```

## O loop while do jogo

```javascript
while (guess !== secret) {
```

"Enquanto o palpite não for igual ao segredo, continue
repetindo."

Exemplo:
```
secret = 14, guess = 10
10 !== 14 → true → repete

guess = 14
14 !== 14 → false → loop para
```

## Por que guess começa em 0

```javascript
let guess = 0;
while (guess !== secret)
```

O segredo está sempre entre 1 e 20 — como `guess`
começa em 0, ele nunca é igual ao segredo de cara,
então:
```
0 !== secret → sempre true no início → o loop começa
```

É uma decisão de lógica pra garantir que o programa
entre no loop na primeira execução.
