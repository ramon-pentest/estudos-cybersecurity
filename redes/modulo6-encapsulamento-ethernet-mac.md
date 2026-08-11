# Redes — Módulo 6: Encapsulamento, Ethernet e MAC

## Encapsulamento

Quando uma aplicação envia dados, esses dados vão sendo
"embrulhados" com informações necessárias em cada etapa
da comunicação.

Visão simplificada:

Dados da aplicação → TCP → IP → Ethernet → bits


Exemplo real ao acessar um site:

HTTP → TCP → IP → Ethernet → cabo/Wi-Fi


## Ethernet e a NIC

Ethernet é a tecnologia/protocolo de comunicação de rede
local. Para participar dessa comunicação, o dispositivo
precisa de uma **NIC** (interface de rede) — que funciona
como a ponte entre os dados e a rede física.

Um notebook pode ter mais de uma NIC:

NIC Wi-Fi → MAC: AA:BB:CC:11:22:33
NIC Ethernet → MAC: DD:EE:FF:44:55:66


O endereço **MAC pertence à interface de rede**, não ao
computador como um todo.

## O quadro Ethernet

O quadro Ethernet funciona como um envelope — carrega as
informações necessárias para a entrega, parecido com uma
carta: destino, origem, tipo de conteúdo, os dados em si,
e uma verificação de erro.

Estrutura de encapsulamento (Ethernet por fora, IP dentro,
TCP dentro do IP, dados da aplicação no centro):

Ethernet
→ IP
→ TCP
→ Dados da aplicação


## Preamble e Start Frame Delimiter (SFD)

**Preamble** — sincroniza o transmissor e o receptor antes
da comunicação começar de verdade. É como duas pessoas no
rádio precisando estar sincronizadas para se entender.

**SFD (Start Frame Delimiter)** — indica onde o quadro
realmente começa, depois da sincronização do Preamble.

Preamble → sincronização
SFD → agora começa o frame de verdade


## Destination MAC e Source MAC

**Destination MAC** — indica qual interface de rede deve
receber aquele quadro dentro da rede local.

Exemplo com dois notebooks conectados no mesmo switch:

Notebook A (MAC: AA:AA:AA) ←→ Switch ←→ Notebook B (MAC: BB:BB:BB)


Se o quadro tem `Destination: BB:BB:BB`, o switch usa esse
endereço para decidir por qual porta encaminhar o quadro.

**Source MAC** — indica de qual interface o quadro se
originou.

Source MAC: AA:AA:AA
Destination MAC: BB:BB:BB


É basicamente "de quem → para quem" dentro do contexto
da Ethernet.

## MAC não é a mesma coisa que IP

Isso é essencial entender:

- **IP** é usado para comunicação entre redes diferentes —
  é o que leva o pacote até um servidor no Japão, por exemplo
- **MAC** está relacionado só à comunicação dentro da rede
  local — muda a cada trecho do caminho

Notebook → Roteador → ISP → ...

O IP de origem/destino continua o mesmo (lógico)
O MAC muda a cada trecho (físico/local)


No trecho Notebook → Roteador, o quadro Ethernet tem um
par de MACs. Depois que o roteador encaminha para outra
rede, um novo quadro Ethernet é criado com outros MACs
para aquele próximo trecho.

## Type / Length

Esse campo pode significar duas coisas dependendo do
contexto:

- **Length** — informa quantos bytes existem nos dados
- **Type** — informa que tipo de protocolo está dentro
  daquele quadro (por exemplo, IPv4 ou IPv6)

Isso permite que a Ethernet saiba qual protocolo deve
assumir o processamento da próxima parte.

## Data e FCS

**Data** — é o pacote propriamente dito, carregado dentro
do quadro.

**FCS (Frame Check Sequence)** — campo de verificação de
erro. O dispositivo receptor confere se o quadro chegou
corretamente; se a verificação não bater, significa que
houve corrupção durante a transmissão.

Envia → [Quadro] → cabo → interferência/problema →
FCS detecta se chegou corrompido ou não


## A camada de acesso e a tabela MAC

Cenário: um roteador, um switch e quatro notebooks (A, B,
C, D) conectados na mesma LAN. O notebook A quer falar
com o D — mas como o switch sabe em qual porta está o D?

É isso que a **tabela MAC** resolve.

Cada dispositivo tem um endereço MAC de 48 bits, geralmente
representado assim: `00:1A:2B:3C:4D:5E`

O switch trabalha na **camada 2** (Ethernet/MAC) — ele não
está interessado no IP, só no MAC de destino do quadro.

## Como o switch aprende (MAC Address Learning)

O switch observa o **MAC de origem** de cada quadro que
recebe e registra por qual porta aquele MAC chegou:
Tabela MAC
MAC Porta

AA-AA Fa01


Isso é chamado de **MAC Address Learning** — o switch
aprende observando a origem, não o destino.

## Unknown Unicast Flooding

Se o switch procura o MAC de destino na tabela e não
encontra (tabela vazia ou endereço desconhecido), ele
envia o quadro por todas as portas, exceto a porta de
onde recebeu — isso é o **Unknown Unicast Flooding**.

Cada dispositivo que recebe o quadro verifica se o MAC
de destino bate com o seu próprio:

Quadro chega em H2 (MAC: BB-BB) → destino é DD-DD → descarta
Quadro chega em H3 (MAC: CC-CC) → destino é DD-DD → descarta
Quadro chega em H4 (MAC: DD-DD) → destino é DD-DD → aceita


Com a resposta de H4, o switch aprende o novo registro:
Tabela MAC
MAC Porta

AA-AA Fa01
DD-DD Fa04


Da próxima vez que precisar mandar de AA-AA para DD-DD,
o switch já sabe exatamente para qual porta encaminhar —
sem precisar mandar para todas de novo.

## A tabela MAC como um mapa
Tabela MAC
MAC Porta

AA-AA Fa01
BB-BB Fa02
CC-CC Fa03
DD-DD Fa04


Com essa tabela montada, o switch toma decisões rápidas
sobre para onde encaminhar cada quadro.

## Os registros não são permanentes

O switch não guarda essa tabela para sempre — os registros
costumam expirar em torno de 5 minutos, e depois são
resetados, obrigando o switch a reaprender.

## Resumo — onde cada coisa vive

MAC de origem/destino → dentro do quadro
Tabela MAC → dentro do switch
