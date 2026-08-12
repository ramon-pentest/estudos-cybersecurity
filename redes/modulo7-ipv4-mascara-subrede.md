# Redes — Módulo 7: IPv4, Máscara de Sub-rede

## O que é o endereço IPv4

O endereço IPv4 é composto por 32 bits. O computador
representa assim:

11010001101001011100100000000001


Para ficar legível para humanos, esse número foi abreviado
em formato decimal:

209.165.200.1


## Como a conversão funciona

Os 32 bits são agrupados em quatro grupos de 8 bits cada.
Cada grupo de 8 bits é chamado de **octeto**.

11010001 . 10100101 . 11001000 . 00000001
8 bits 8 bits 8 bits 8 bits


Cada octeto é convertido para decimal separadamente:

11010001 → 209
10100101 → 165
11001000 → 200
00000001 → 1


Resultado final: `209.165.200.1`

Ou seja: **IPv4 = 32 bits = quatro octetos de 8 bits.**

## Origem e destino num pacote

Todo pacote enviado pela internet carrega um IP de origem
e um IP de destino:

Origem: 192.168.200.8 → Dados → Destino: 192.168.5.100


## MAC vs IP — a distinção essencial

**Endereço MAC** — identifica uma interface de rede dentro
da comunicação Ethernet (rede local).

Exemplo: AA:BB:CC:11:22:33


**Endereço IP** — identifica logicamente um dispositivo
dentro de uma rede IP (pode atravessar redes diferentes).

Exemplo: 192.168.1.20


Resumindo:

MAC → "Qual interface Ethernet?"
IP → "Qual endereço/rede IP?"


O switch olha principalmente para o MAC (usando a tabela
MAC para decidir a porta). Já o IP é o que determina para
qual rede o pacote precisa ir.

## O IP indica também a rede, não só o dispositivo

O IP não representa apenas um dispositivo isolado — ele
também mostra em qual rede esse dispositivo está.

Exemplo com três redes diferentes numa empresa:

Rede 1 — Gerenciamento → 192.168.1.x
Rede 2 — Contabilidade → 192.168.2.x
Rede 3 — Vendas → 192.168.3.x


Dentro da rede de Vendas:

PC 1 → 192.168.3.10
PC 2 → 192.168.3.20
PC 3 → 192.168.3.30


Os três compartilham o mesmo prefixo `192.168.3` (a rede)
e são diferenciados pelo último número (o host):

192.168.3 → REDE
.10 → HOST


## Por que separar rede e host

Imagine uma empresa com 200 computadores, todos na rede
`192.168.1.0`. É muito mais eficiente o roteador tratar
todos os pacotes como pertencentes à mesma rede
`192.168.1.0`, do que precisar de uma regra separada
para cada um dos 200 hosts individualmente.

## Máscara de sub-rede

A máscara de sub-rede é o que permite saber qual parte do
IP representa a rede e qual parte representa o host.

Exemplo:

IP: 192.168.5.11
Máscara: 255.255.255.0


A máscara `255.255.255.0` indica que os três primeiros
octetos (`255.255.255`) representam a **rede**, e o último
octeto (`0`) representa o **host**:

Rede: 192.168.5
Host: 11


**Importante:** isso não é uma regra fixa universal — outras
máscaras dividem o IP em pontos diferentes, dependendo de
como a rede foi configurada.

## Quando usar Switch/MAC e quando usar Roteador/IP

Quando dois dispositivos estão na **mesma rede**, a
comunicação usa Switch, Ethernet e endereço MAC.

Quando a comunicação precisa ir para uma **rede diferente**,
entra o Roteador — ele é responsável por encaminhar o
pacote para fora da rede local, até o destino correto.
