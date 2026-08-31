# Redes — Módulo 14: TCP, UDP, Portas e Sockets

## TCP e UDP

TCP e UDP são dois protocolos da Camada de Transporte
(Camada 4) que resolvem o problema de entregar dados
entre aplicações. A diferença principal é:

- **UDP** → velocidade e simplicidade, sem garantir
  entrega ou ordem
- **TCP** → confiabilidade, confirmando recebimento
  e organizando os dados

## O problema das múltiplas aplicações

Quando o PC tem várias coisas abertas ao mesmo tempo
que requerem internet (navegador, Discord, jogo, DNS,
e-mail), o IP consegue identificar qual dispositivo
deve receber o pacote — mas surge outro problema:

**Qual aplicação dentro daquele dispositivo deve
receber os dados?**

É aqui que as portas entram:

```
Navegador → Porta 80/443
DNS       → Porta 53
E-mail    → Porta 25/110
```

IP = identifica o dispositivo
Porta = identifica a aplicação/serviço naquele dispositivo


TCP e UDP trabalham nessa camada de transporte usando
números de porta para fazer essa diferenciação.

## Segmentos

Quando os dados são grandes demais para ser enviados
como uma única unidade, a camada de transporte os
divide em unidades menores. No caso do TCP, essas
unidades são chamadas de **segmentos**.

Dados grandes → Camada de Transporte →
[Segmento 1] [Segmento 2] [Segmento 3] [Segmento 4] → Rede


Cada segmento recebe informações de transporte:
- Porta de origem
- Porta de destino

## Porta de origem e porta de destino

Exemplo: o PC usa a porta de origem `5105` e quer
acessar o DNS na porta `53`:

IP: 192.168.1.10
Porta: 5105
↓
DNS Server
Porta: 53


As portas permitem identificar a comunicação entre
aplicações e serviços.

## Confiabilidade — a principal diferença entre TCP e UDP

**UDP — sem garantia de entrega:**

Pacote 1 → chegou
Pacote 2 → chegou
Pacote 3 → perdeu
Pacote 4 → chegou
Pacote 5 → chegou


O UDP não tenta recuperar o pacote 3. Em uma ligação
de voz em tempo real, por exemplo, se um pequeno
pedaço da transmissão for perdido, a pessoa escuta
algo como "Oi, ... bem?" em vez de "Oi, tudo bem?".
É imperfeito, mas a conversa continua.

Se o UDP ficasse parando para tentar recuperar o
pacote perdido, isso introduziria um atraso grande
que prejudicaria muito mais do que simplesmente perder
um pacote e manter o fluxo.

**TCP — com confirmação de recebimento:**

Pacote enviado → ACK (recebi)
Pacote enviado → ACK (não recebi) → retransmite


O TCP usa o **ACK (acknowledgment/reconhecimento)**
para confirmar cada entrega. O UDP não faz isso.

## Overhead

Overhead é o custo adicional necessário para controlar
a comunicação. No TCP:

A → Dados
B → ACK
C → Dados
D → ACK


Isso adiciona tráfego e processamento. O UDP é mais
simples justamente porque não carrega esse conjunto
de mecanismos de confiabilidade.

**Quando o UDP é mais utilizado:**
- Streaming
- Comunicação em tempo real
- Voz sobre IP

Se velocidade e continuidade são mais importantes do
que garantir cada pacote individual, o UDP pode ser
mais apropriado.

## TCP em detalhes

O TCP foi criado para situações onde perder dados é
inaceitável — como uma transferência bancária. Se
alguns pacotes contendo informações importantes
fossem perdidos, não dá pra simplesmente ignorar.

### Números de sequência

Imagine que três segmentos foram enviados mas chegam
fora de ordem:

Enviado: Segmento 1 → Segmento 2 → Segmento 3
Chegou: Segmento 2 → Segmento 1 → Segmento 3


Os números de sequência permitem que o destino saiba
a ordem correta e reorganize os dados antes de
entregá-los à aplicação.

### Mecanismo Window

O TCP não precisa esperar o ACK de cada segmento
individualmente — isso seria muito lento. Em vez
disso, ele pode enviar vários segmentos antes de
receber uma confirmação:

1 → 2 → 3 → 4 → 5 → 6 → 7 → 8 → ACK


O tamanho da janela (window) se adapta à qualidade
da rede:

Rede confiável → [1 2 3 4 5 6 7 8 9 10...]
Rede problemática → [1 2 3] → aguarda ACK


Assim o TCP reduz a quantidade enviada de uma vez
quando a conexão está ruim, evitando que muitos
segmentos sejam perdidos ao mesmo tempo.

## Portas — analogia do prédio

IP = endereço do prédio
Porta = sala específica dentro do prédio


Exemplo:

192.168.1.7:80 → host 192.168.1.7, serviço na porta 80 (HTTP)
192.168.1.7:21 → mesmo host, mas serviço na porta 21 (FTP)


## Portas de origem e destino numa comunicação

Comunicação Web:
Origem: 192.168.1.5:1099
Destino: 192.168.1.7:80

Comunicação FTP (simultânea):
Origem: 192.168.1.5:1305
Destino: 192.168.1.7:21


O PC usa porta de origem aleatória porque podem
acontecer várias comunicações ao mesmo tempo. Assim
o computador consegue diferenciar cada uma delas.

Quando o servidor responde, ele inverte as portas:

Origem: 192.168.1.7:80
Destino: 192.168.1.5:1099


Isso garante que a resposta seja entregue à aplicação
correta no cliente.

## Socket

O **socket** é a combinação de IP + Porta:

Socket cliente: 192.168.1.5:1099
Socket servidor: 192.168.1.7:80


Ambos juntos formam um **par de sockets** que identifica
aquela comunicação específica de forma única.

## Portas conhecidas — as mais importantes para pentest

| Porta | Protocolo | Serviço |
|------:|-----------|---------|
| 21 | TCP | FTP |
| 22 | TCP | SSH |
| 23 | TCP | Telnet |
| 25 | TCP | SMTP |
| 53 | TCP/UDP | DNS |
| 67 | UDP | DHCP servidor |
| 68 | UDP | DHCP cliente |
| 80 | TCP | HTTP |
| 110 | TCP | POP3 |
| 143 | TCP | IMAP |
| 443 | TCP | HTTPS |

## Faixas de portas

0 – 1023 → portas conhecidas (serviços padrão)
1024 – 49151 → portas registradas (aplicações específicas)
49152 – 65535 → portas privadas/dinâmicas (usadas como origem)


A porta de origem aleatória (como a 1099 dos exemplos)
funciona como um identificador de retorno — ela diz
ao servidor para onde mandar a resposta.

## Comando netstat

Permite visualizar as conexões TCP ativas no computador:

Proto Local Address Foreign Address
TCP 192.168.1.124:3158 207.138.126.152:http


- **Local Address** → IP do PC local + porta local
- **Foreign Address** → IP remoto + porta remota
- **Established** → conexão TCP estabelecida

O comando `netstat -n` mostra os números de porta
em vez dos nomes dos serviços (ex: `80` em vez de `http`).
