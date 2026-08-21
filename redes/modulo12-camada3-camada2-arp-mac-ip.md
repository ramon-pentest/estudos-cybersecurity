# Redes — Módulo 12: Camadas IP e MAC, ARP e Comunicação

## O papel de cada camada

Camada 3 — IP → para onde o pacote vai ir
Camada 2 — MAC → para quem vai entregar naquele trecho


## Comunicação local — destino na mesma rede

O PC olha para o IP de destino e faz um AND com a
máscara de sub-rede para descobrir se estão na mesma
rede.

Exemplo:

IP origem: 192.168.10.10
IP destino: 192.168.10.11
Máscara: 255.255.255.0


Resultado: ambos pertencem à mesma rede — o roteador
não é necessário.

O PC então usa o **ARP** para descobrir o MAC do
dispositivo destino, faz o broadcast, e o PC2 responde
com seu MAC `55:55:55`.

O quadro fica:

IP origem: 192.168.10.10
IP destino: 192.168.10.11
MAC origem: aa:aa:aa
MAC destino: 55:55:55


**Quando o destino está na mesma rede:**

MAC destino = MAC do dispositivo final


## Comunicação remota — destino em outra rede

Agora o PC (`192.168.10.10`) quer entregar para um IP
remoto (`10.1.1.10`). Ele percebe que não estão na
mesma rede e manda o pacote direto para o **gateway
padrão** (porta de saída da rede).

O PC usa ARP para descobrir o MAC do roteador
(interface `192.168.10.1`) — o roteador responde com
seu MAC `bb:bb:bb`.

O quadro fica:

Camada IP:
IP origem: 192.168.10.10
IP destino: 10.1.1.10 ← destino final, não muda

Camada MAC:
MAC origem: aa:aa:aa
MAC destino: bb:bb:bb ← MAC do gateway local


**Quando o destino está fora da LAN:**

IP destino = dispositivo final remoto (não muda)
MAC destino = gateway local (muda a cada salto)


## O que o roteador faz no caminho

O switch só faz o trabalho de entregar o quadro do
PC até o roteador.

Quando o quadro chega no roteador, ele remove o
cabeçalho Ethernet (os MACs) e olha somente para o
IP destino. Ao identificar para onde precisa enviar,
cria um novo quadro com os MACs do próximo trecho:

Interface roteador 1 → MAC origem: cc:cc:cc
Interface roteador 2 → MAC destino: dd:dd:dd


O IP continua o mesmo:

Origem: 192.168.10.10
Destino: 10.1.1.10


## Resumo — o que muda e o que não muda

O IP quase nunca muda ao longo do caminho. O MAC
muda a cada salto:

PC → R1: aa → bb
R1 → R2: cc → dd
R2 → PC2: ee → 55


## Broadcast Ethernet

Um broadcast Ethernet é um quadro cujo MAC de destino
é `FF:FF:FF:FF:FF:FF` — esse é o MAC de broadcast.

- **Switch** → floda todas as portas exceto a porta
  de entrada
- **Roteador** → recebe o broadcast mas não encaminha
  para outras redes

## ARP — como funciona

O ARP é o processo que descobre o MAC de um dispositivo
na mesma rede usando o IP como referência.

O processo:
1. O PC faz um broadcast perguntando quem tem o IP
   que ele está procurando
2. O dispositivo com aquele IP responde com seu MAC
3. A partir daí o processo passa a ser individual,
   pois o MAC fica registrado na **tabela ARP**

## Endereço físico vs endereço lógico

**Endereço físico (MAC)** — usado para comunicação
de NIC para NIC dentro da mesma rede Ethernet.

**Endereço lógico (IP)** — usado para enviar o pacote
do dispositivo de origem até o dispositivo de destino
final, independente de quantas redes intermediárias
existam.

O IP de destino pode estar na mesma rede que a origem
ou em uma rede completamente remota.
