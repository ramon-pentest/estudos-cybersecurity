# Redes — Módulo 9: IPv6

## Por que o IPv6 existe

O IPv4 possui 32 bits, o que gera um espaço de
aproximadamente 4,3 bilhões de combinações teóricas.

Parece muito, mas hoje temos computadores, celulares,
TVs, câmeras, sensores, dispositivos IoT, dispositivos
médicos e muito mais conectados à internet.

O **IPv6 usa 128 bits**, o que aumenta drasticamente
o espaço de endereçamento disponível — praticamente
inesgotável para uso prático.

## O que prolongou a vida do IPv4

O **NAT** foi o principal fator que prolongou a vida
do IPv4 — ele permite que vários dispositivos internos
compartilhem um ou poucos endereços públicos.

Porém o NAT tem limitações reais:
- Adiciona latência
- Cria problemas para determinadas aplicações
- Limita a comunicação ponto a ponto

## Por que IPv4 e IPv6 coexistem

Substituir o IPv4 completamente exigiria que toda a
infraestrutura existente fosse capaz de trabalhar com
o novo protocolo — o que é inviável de fazer de uma
vez só, especialmente considerando dispositivos e
sistemas antigos ainda em operação.

Por isso os dois protocolos passaram a coexistir, e
existem três mecanismos principais para isso:

### 1. Pilha dupla (Dual Stack)

Um dispositivo possui IPv4 e IPv6 ao mesmo tempo e
sabe trabalhar com ambos:

IPv4: 192.168.1.10
IPv6: 2001:db8::10


### 2. Tunelamento

O IPv6 viaja através de uma infraestrutura IPv4.
O pacote IPv6 é encapsulado dentro de um pacote IPv4:

[ Cabeçalho IPv4 ]
[ Pacote IPv6 ]


A rede IPv4 intermediária transporta o pacote olhando
apenas para o cabeçalho IPv4 externo. No destino, o
encapsulamento é removido e o pacote IPv6 original
continua seu caminho normalmente.

### 3. Conversão — NAT64

Funciona como uma tradução entre os dois protocolos:

Rede IPv6 → NAT64 → Rede IPv4


## Estrutura do endereço IPv6

O IPv6 usa 128 bits divididos em **oito hextetos**
em formato hexadecimal, separados por dois pontos:

2001:0db8:0000:0000:0000:0000:0000:0010


### Regras de compressão

Para facilitar a leitura, existem duas regras de
compressão:

**1. Remover zeros à esquerda dentro de cada hexteto:**

0db8 → db8
0000 → 0


**2. Substituir sequências contínuas de hextetos
zerados por `::`**

2001:db8:0:0:0:0:0:10
→ 2001:db8::10


O `::` só pode ser usado **uma única vez** no endereço
— caso contrário seria impossível saber quantos blocos
foram omitidos.

### Como expandir um endereço comprimido

Para expandir de volta ao formato completo, conta-se
quantos hextetos estão visíveis e completa-se até
chegar em 8 blocos, preenchendo os zeros omitidos
onde está o `::`.

Exemplo:

2001:db8::10

Hextetos visíveis: 2001, db8, 10 = 3 hextetos
Faltam: 8 - 3 = 5 hextetos de zeros

Expandido:
2001:0db8:0000:0000:0000:0000:0000:0010
