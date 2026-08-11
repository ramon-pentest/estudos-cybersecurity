# Redes — Módulo 4: Protocolos, TCP/IP e Modelo OSI

## O que é um protocolo

Protocolo é o conjunto de regras que define como dois
dispositivos vão se comunicar. Todo protocolo precisa
definir 6 coisas:

### 1. Formato da mensagem
Como a mensagem deve ser estruturada — parecido com
preencher um formulário:
`[REMETENTE] [DESTINO] [TIPO] [DADOS]`

### 2. Tamanho da mensagem
Mensagens grandes demais podem precisar ser divididas
em partes menores para serem transmitidas.

### 3. Temporização
Define quando e em que ritmo a comunicação acontece —
quando enviar, quando esperar resposta, quanto tempo
esperar, e quando considerar que algo falhou.

Exemplo de fluxo coordenado:

A envia → B recebe → B responde → A continua


Exemplo quando não há resposta:

A envia → B não responde → A espera → A tenta de novo


### 4. Codificação
A mensagem precisa ser convertida em bits para viajar
pelo meio físico:

Mensagem → codificação → bits/sinais → rede →
bits/sinais → decodificação → mensagem


Cada meio físico representa os bits de um jeito:
- Cabo de cobre → sinais elétricos
- Fibra óptica → pulsos de luz
- Wi-Fi → ondas de rádio

**Codificação não é criptografia.** Codificação transforma
a informação para que possa ser transmitida. Criptografia
transforma a informação para que pessoas não autorizadas
não consigam entender.

### 5. Encapsulamento
Adiciona informações de controle aos dados para que a
rede saiba como tratar e entregar aquilo — origem, destino,
dados. Conforme a mensagem passa pelas camadas, mais
informações de controle vão sendo adicionadas.

### 6. Padrão da mensagem
Algumas comunicações exigem confirmação de recebimento,
outras não:

Com confirmação: A pergunta "recebeu?" → B responde "sim"
Sem confirmação: A envia → termina, sem resposta de B


## DHCP — endereçamento automático

O DHCP fornece automaticamente:
- Meu IP
- Minha rede
- Gateway padrão
- DNS

**Gateway** é o próximo ponto de saída para alcançar
outra rede — geralmente o roteador. Se o notebook percebe
que o destino não está na rede local, manda o pacote
para o gateway.

## DNS — tradução de nomes

Quando digito `www.example.com`, o computador não pode
usar esse nome diretamente como destino — precisa
descobrir o IP correspondente através do DNS:

www.example.com → DNS → 203.0.113.x


DNS resolve nomes para endereços IP.

## IP e TCP — endereçamento e confiabilidade

**IP** leva os pacotes ao destino, mas não garante a
entrega — é como enviar uma carta com endereço certo,
mas sem garantia de que vai chegar.

**TCP** garante confiabilidade — detecta se algum pacote
não chegou e trabalha para retransmitir.

IP → leva os pacotes ao destino
TCP → garante que a comunicação seja confiável


## Padrões e organizações da internet

Dispositivos diferentes (notebook Dell, roteador TP-Link,
roteador Cisco, servidor Linux, servidor Windows) conseguem
conversar porque seguem os mesmos padrões e protocolos.

Organizações responsáveis por esses padrões:

IEEE, IETF, IANA, ICANN, ITU, TIA


**RFC (Request for Comments)** — documentos que
formalizam padrões, especificações e propostas
relacionadas à internet.

## A pilha de protocolos

Ethernet → IP → TCP → HTTP


- **Ethernet** → cuida da comunicação dentro da rede local
- **IP** → endereça o pacote e leva da origem ao destino
  entre redes diferentes
- **TCP** → torna a comunicação confiável (controle de
  sequência e retransmissão)
- **HTTP** → protocolo da camada de aplicação usado na
  comunicação web

## Modelo TCP/IP — resumo por camada

| Camada | Ideia principal |
|--------|-----------------|
| Aplicação | Serviços usados pelas aplicações (ex: HTTP) |
| Transporte | Comunicação entre dispositivos (ex: TCP) |
| Internet | Endereçamento e encaminhamento (ex: IP) |
| Acesso à rede | Hardware e meio físico (ex: Ethernet, Wi-Fi) |

## OSI vs TCP/IP

**OSI** é um modelo de referência — divide a comunicação
em 7 camadas para facilitar entendimento e diagnóstico.

**TCP/IP** é um modelo de protocolo — está diretamente
ligado à suíte de protocolos TCP/IP usada na prática.

Comparação entre os dois modelos:

OSI TCP/IP
7 Aplicação ┐
6 Apresentação ┼──→ Aplicação (HTTP)
5 Sessão ┘
4 Transporte ──→ Transporte (TCP)
3 Rede ──→ Internet (IP)
2 Enlace ┐
1 Física ┴──→ Acesso à Rede (Ethernet/Wi-Fi)


## Tipos de mídia física

| Mídia | Como transmite | Ponto importante para segurança |
|-------|-----------------|----------------------------------|
| Cobre (UTP) | Impulsos elétricos | Sofre interferência eletromagnética, fisicamente acessível |
| Coaxial | Sinal elétrico | Usado em TV a cabo, possui blindagem |
| Fibra óptica | Pulsos de luz | Não sofre interferência eletromagnética, permite longas distâncias |
| Wireless | Ondas eletromagnéticas | Se propaga pelo ambiente — alcance e exposição física importam |
