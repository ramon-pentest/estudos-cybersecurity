# TryHackMe — Pre-Security: Computer Types

## Os 4 tipos de computador que usamos diretamente (com teclado/tela)

| Tipo | Teclado/tela | Propósito principal |
|------|--------------|----------------------|
| Laptop | Sim | Computação portátil do dia a dia |
| Desktop | Sim | Performance sustentada, local fixo |
| Workstation | Sim | Precisão e confiabilidade pra tarefas profissionais (simulações, modelos 3D) |
| Server | Não | Fornecer serviços pra múltiplos usuários via rede |

**Laptop** sacrifica performance sustentada em troca de
portabilidade — dificuldade de resfriamento em espaço
pequeno, dependência de bateria.

**Desktop** ganha em consistência por ficar fixo, usar
energia da tomada e ter melhor refrigeração.

**Workstation** parece um desktop, mas usa componentes
especializados pra reduzir erros em cálculos longos e
complexos.

**Server** não tem tela — roda continuamente respondendo
múltiplos usuários ao mesmo tempo.

## Computadores "escondidos" em objetos do dia a dia

| Tipo | Descrição | Exemplos |
|------|-----------|----------|
| Smartphone | Computador de bolso otimizado pra bateria e conectividade | iPhone, Android |
| Tablet | Computador touch-first, tela maior | iPad, tablet de desenho |
| IoT device | Dispositivo conectado em rede, propósito único | Termostato, campainha inteligente, smartwatch |
| Embedded computer | Computador embutido dentro de outro dispositivo | Controlador de cafeteira, sensor de porta, chip de dimmer |

**Diferença chave entre IoT e Embedded: conectividade.**

IoT se conecta a uma rede pra reportar dados ou receber
comandos. Embedded pode não se conectar a nada — faz o
trabalho isolado dentro da máquina, muitas vezes por anos
sem ninguém saber que existe.

## Por que existem tipos diferentes (não um computador universal)

Todo design é um trade-off:

```
Mobilidade custa energia    → portáteis sacrificam performance sustentada
Confiabilidade custa dinheiro → servers usam redundância (fonte
                                extra, discos extras) pra evitar falha
Propósito molda tudo         → você toca um telefone, pede
                                informação a um server, um IoT
                                device trabalha quieto sem
                                demandar atenção
```

Não existe "o melhor computador" — existe a ferramenta
certa pra cada função.

## Resumo geral da sala

8 tipos de computador cobertos: laptop, desktop,
workstation, server, smartphone, tablet, IoT device,
embedded computer.

Os mais críticos nem sempre são os mais rápidos ou
chamativos — às vezes são os chips silenciosos que
mantêm portas abrindo, aviões voando, cafeteiras
funcionando.
