# TryHackMe — Pre-Security: Network Fundamentals

## Intro to Networking

Rede é um conjunto de dispositivos conectados que conseguem
se comunicar. Pode ser só dois computadores ou bilhões de
dispositivos — computadores, celulares, câmeras, semáforos,
sensores. É parecido com uma rede de transporte ou de
energia, só que quem participa são dispositivos trocando
dados seguindo regras.

A Internet é uma **rede de redes**: redes privadas menores
se conectam através de redes públicas e formam a estrutura
que liga dispositivos no mundo todo.

- A **ARPANET**, do fim dos anos 1960, foi uma das precursoras
  da Internet
- A **World Wide Web** foi criada por Tim Berners-Lee
- Internet e Web não são a mesma coisa: a Internet conecta
  redes e dispositivos, e a Web é um dos serviços que rodam
  em cima dela

**MAC spoofing** — o endereço MAC pode ser falsificado. Uma
rede que confia só no MAC pra decidir quem entra pode ser
enganada.

## Intro to LAN

### Topologias

Topologia é a forma como os dispositivos de uma rede são
organizados.

```
Star (estrela)
→ todos ligados a um ponto central, normalmente um switch
+ fácil adicionar equipamentos
+ falha num cabo afeta só aquele dispositivo
- se o equipamento central parar, quem está ligado nele
  perde a comunicação

Bus (barramento)
→ vários dispositivos compartilhando um cabo principal
+ barata e simples de montar
- o cabo central vira gargalo
- se ele falhar, a rede inteira pode parar
- difícil descobrir a origem de um problema

Ring (anel)
→ dispositivos formam um circuito e os dados passam de um
  pro outro até chegar no destino
+ pode reduzir colisões
- uma falha no caminho pode interromper a comunicação
```

### Hub x switch

O hub repete os dados pra todas as portas, o que gera mais
tráfego. O switch aprende em qual porta cada MAC está e
encaminha o quadro só pro destino certo.

### Sub-redes

Dividir uma rede maior em redes menores ajuda na
organização, reduz o alcance do tráfego local e permite
separar grupos — por exemplo, funcionários e visitantes
no Wi-Fi.

Três endereços aparecem nesse contexto:

```
Endereço de rede  → identifica a própria sub-rede
Endereço de host  → identifica um dispositivo dentro dela
Gateway padrão    → o roteador usado pra chegar em outras redes
```

Em redes domésticas o gateway costuma ser `.1` ou `.254`,
mas pode variar.

### ARP

Depois que o dispositivo descobre o MAC de um IP (request em
broadcast, reply de quem tem aquele IP), o resultado fica
guardado no **cache ARP** pra consultas futuras — assim não
precisa perguntar de novo toda vez.

## OSI Model

O OSI divide a comunicação em 7 camadas. É um modelo de
referência: serve pra entender o que acontece numa
comunicação e pra localizar onde está um problema.

Quando os dados descem pelas camadas, cada uma acrescenta as
informações necessárias pra próxima etapa (encapsulamento).
No destino, isso é removido em ordem inversa.

```
7 Application  → serviços usados pelas aplicações (HTTP, DNS, SMTP)
6 Presentation → representação, conversão e formatação dos dados;
                 a criptografia costuma ser explicada aqui
5 Session      → inicia, mantém e encerra sessões entre aplicações
4 Transport    → comunicação entre aplicações; TCP e UDP, com portas
3 Network      → endereçamento IP e roteamento entre redes (roteadores)
2 Data Link    → comunicação local com quadros e MAC (a NIC participa)
1 Physical     → meios físicos e sinais que carregam os bits
```

Resumindo a separação de responsabilidades: o IP indica o
destino lógico, o MAC entrega no enlace local e a porta diz
qual serviço deve receber os dados.

## Packets & Frames

Dados grandes são divididos em partes menores pra atravessar
a rede. Na camada 3 essa unidade é o **pacote** (com as
informações IP). Na camada 2 o pacote vai dentro de um
**quadro** (com os MACs daquele trecho).

Analogia da carta: o conteúdo é o pacote e o envelope, com os
endereços usados naquele trecho, é o quadro.

**Campos do pacote IP que ajudam a controlar a entrega:**
```
TTL                  → limita quantos saltos o pacote pode dar
Checksum             → permite verificar se certos dados foram corrompidos
Source Address       → IP de origem
Destination Address  → IP de destino
```

### TCP — three-way handshake

O TCP é orientado à conexão. Antes de trocar dados, cliente e
servidor estabelecem a conexão:

```
SYN → SYN/ACK → ACK
```

O SYN inicia, o SYN/ACK confirma e responde, o ACK completa.
Só depois os dados são enviados.

O TCP usa números de sequência e confirmações pra manter a
ordem e detectar perdas, retransmitindo se precisar — fica
confiável, mas com mais processamento, então pode ser mais
lento que o UDP.

```
FIN → encerra a conexão de forma normal
RST → interrompe a conexão de forma abrupta
```

O UDP não estabelece conexão contínua nem confirma a entrega
do mesmo jeito. É mais simples e rápido, mas os dados podem
chegar fora de ordem ou nem chegar — usado quando a
velocidade importa e a aplicação tolera perdas, como voz e
vídeo em tempo real.

### Portas

Vão de 0 a 65535. Algumas portas padrão:
```
21   → FTP
22   → SSH
80   → HTTP
443  → HTTPS
445  → SMB
3389 → RDP
```

O serviço pode usar outra porta, mas o cliente precisa saber
qual. Uma conexão envolve IP e porta de origem e IP e porta
de destino.

## Extending Your Network

### Port forwarding e firewall

**Port forwarding** é configurado no roteador e encaminha o
tráfego que chega numa porta pública pra um dispositivo e uma
porta específicos dentro da rede privada. Assim um servidor
que só podia ser acessado localmente fica acessível de fora.

Não é a mesma coisa que firewall: o encaminhamento define
**pra onde** o tráfego vai, o firewall decide **se** ele pode
passar.

Um firewall pode avaliar origem, destino, porta e protocolo.
```
Stateful   → considera o estado da conexão inteira
Stateless  → aplica as regras a cada pacote individualmente
```

### VPN

Cria um túnel protegido entre dispositivos ou redes em locais
diferentes, que passam a se comunicar como se fossem uma rede
privada, e ajuda a proteger o tráfego contra interceptação.

```
PPP   → fornece autenticação e criptografia, mas não
        transporta o tráfego pelas redes sozinho
PPTP  → permite o tráfego atravessar redes, mas é antigo e fraco
IPsec → protege as comunicações usando o protocolo IP
```

### Equipamentos

Roteadores encaminham pacotes entre redes. Switches conectam
dispositivos e encaminham tráfego local por MAC. Um switch
de camada 2 trabalha com quadros; um de camada 3 também
encaminha tráfego entre redes usando IP.

**VLANs** separam virtualmente dispositivos que usam a mesma
infraestrutura física. Exemplo: os computadores de Vendas e
Contabilidade podem estar nos mesmos switches mas em redes
diferentes.
