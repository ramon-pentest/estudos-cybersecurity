# Redes — Módulo 8: Unicast, Broadcast, Multicast, IPv4 e Segmentação

## Tipos de comunicação

### Unicast
Um dispositivo se comunica com outro dispositivo específico.

PC A → PC B (1 para 1)

Quando acesso um servidor web, isso já é uma comunicação
Unicast — meu computador envia dados para um destino
específico e recebe dados daquele mesmo destino.

### Broadcast
O dispositivo envia para todos que estão dentro do
domínio de broadcast.

Qualquer dispositivo dentro da mesma rede recebe o envio.

- **Switch** → recebe o broadcast e encaminha para todas
  as portas, exceto a porta de onde recebeu
- **Roteador** → recebe o broadcast, mas não encaminha
  para outra rede por padrão — funciona como barreira
  do domínio de broadcast

O broadcast precisa ser limitado porque enviar para todos
a todo momento comprometeria o desempenho da rede e dos
dispositivos.

### Multicast
O dispositivo envia para um grupo específico — somente
os membros daquele grupo recebem e processam a mensagem.

No IPv4, os endereços multicast ficam entre:

224.0.0.0 → 239.255.255.255


## Tipos de endereço IPv4

O IPv4 se divide em duas categorias principais:

**IP Público** → pode ser roteado pela internet

**IP Privado** → usado dentro de redes internas,
não é roteado diretamente pela internet

### Os três blocos privados (RFC 1918)

10.0.0.0/8 → Privado
172.16.0.0/12 → Privado (172.16.0.0 até 172.31.255.255)
192.168.0.0/16 → Privado


Atenção: não é qualquer `172.x.x.x` que é privado —
só o intervalo de `172.16.0.0` até `172.31.255.255`.
Da mesma forma, `192.168.x.x` é privado, mas
`192.100.x.x` não é.

### Por que IPs privados existem

Sem eles, cada dispositivo dentro de uma rede local
precisaria ter um IP público exclusivo — o que seria
inviável.

Em casa, por exemplo:

Notebook → 192.168.1.10
Celular → 192.168.1.11
TV → 192.168.1.12
Console → 192.168.1.13


Outra pessoa em outra casa pode usar exatamente os
mesmos endereços sem problema — são duas redes
independentes, como numerações internas separadas.

### NAT — quando o IP privado precisa sair para a internet

Quando preciso acessar um site, meu IP de origem é privado
e não pode ser usado diretamente na internet. O NAT faz
a tradução:

192.168.1.20 → NAT → 200.x.x.x → Internet


Quando a resposta volta, o NAT consegue relacioná-la
ao dispositivo interno que fez a solicitação.

## Endereços especiais

**Loopback — 127.0.0.1**
Significa "eu mesmo". Ao fazer `ping 127.0.0.1`, o
computador confirma se a própria interface de rede
está funcionando — o tráfego volta para o próprio
dispositivo.

**APIPA — 169.254.x.x**
Se um dispositivo entra numa rede e não recebe um IP
via DHCP, o Windows atribui automaticamente um endereço
`169.254.x.x` como algo provisório. Isso é chamado de
APIPA ou link-local.

## Quem distribui os IPs públicos

IPs públicos precisam ser globalmente únicos para
funcionar na internet global. A hierarquia de distribuição é:

IANA → RIR → ISP → Organização/Cliente


A **IANA** administra o espaço global de endereços.
Ela distribui blocos para os **RIRs**, que administram
regiões do mundo. Para a América Latina existe o
**LACNIC**:

LACNIC → ISP → Cliente


## CIDR — breve contexto histórico

O sistema antigo dividia o IPv4 em classes fixas, o que
desperdiçava muitos endereços. Por isso hoje é usado
o endereçamento sem classe, chamado de CIDR.

## Segmentação de rede

A ideia central é simples: uma rede grande pode ser
dividida em redes menores para controlar quem está
junto, reduzir tráfego desnecessário e limitar o
alcance de determinados eventos.

### Domínio de broadcast e o problema do tamanho

Quando um PC precisa descobrir o MAC de um determinado
IP, ele usa o **ARP** — que envia um broadcast para
toda a rede. O switch passa esse broadcast para todos
os dispositivos, exceto a porta de onde recebeu.

O roteador funciona como barreira — o broadcast da
Rede 1 não atravessa para a Rede 2. Isso cria a
separação de domínios de broadcast.

O problema: todos os dispositivos da rede precisam
receber e processar esse tráfego de broadcast, o que
gera desperdício de recursos e afeta o desempenho.

### Como a segmentação resolve isso

Dividindo a rede em sub-redes menores:

172.16.0.0/16 → 172.16.0.0/24 (LAN 1)
172.16.1.0/24 (LAN 2)


Com 400 dispositivos, por exemplo:
- LAN 1 → 200 dispositivos
- LAN 2 → 200 dispositivos

O broadcast da LAN 1 não chega na LAN 2 e vice-versa.

O `/16` foi mudado para `/24` porque estamos usando
bits que antes pertenciam à parte de hosts para
diferenciar sub-redes — ou seja, mais bits para
identificar a rede, menos bits disponíveis para hosts.

### Exemplo de rede segmentada por função

Administração → 10.0.1.0/24
RH → 10.0.3.0/24
Contabilidade → 10.0.4.0/24


## Distinção importante — ARP vs Broadcast IPv4

**ARP** → mecanismo de Camada 2, usa um quadro
Ethernet broadcast para descobrir o MAC correspondente
a um IPv4.

**255.255.255.255** → endereço IPv4 de broadcast,
portanto estamos falando da Camada 3.

São conceitos relacionados mas em camadas diferentes.
