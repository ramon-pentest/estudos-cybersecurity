# Redes — Módulo 2: Largura de Banda e Infraestrutura

## Largura de banda, throughput e latência

**Largura de banda** é a capacidade máxima do canal —
. Medida em:
- Kbps — milhares de bits por segundo
- Mbps — milhões de bits por segundo
- Gbps — bilhões de bits por segundo

**Throughput** é quanto realmente passou pelo canal —
os litros que saíram da torneira por minuto.

**Latência** é o tempo que os dados demoram para
sair daqui e chegar lá — quanto tempo até sair
a primeira gota depois de abrir a torneira.

Se a largura de banda é 100 Mbps e o throughput
está em 100 Mbps, a rede fica lenta porque não
sobra espaço para mais dados. Se o throughput
for 20 Mbps, tem espaço sobrando.

## Clientes, servidores e hosts

**Host** é qualquer dispositivo conectado na rede
que pode enviar ou receber informações.

**Cliente** é quem faz o pedido.

**Servidor** é quem responde o pedido.

O software instalado determina se o dispositivo
vai agir como cliente ou servidor.

**Redes P2P** — todos podem pedir e todos podem
entregar ao mesmo tempo. Mais barato, mas os
computadores ficam mais sobrecarregados.

## Infraestrutura de rede

São todos os dispositivos que fazem a rede funcionar:

**Dispositivos finais (hosts):**
notebook, computador, celular, tablet, impressora, smart TV

**Intermediários — os que guiam o caminho:**

| Dispositivo | Função |
|-------------|--------|
| Switch | Organiza a comunicação dentro da mesma rede |
| Roteador | Conecta redes diferentes entre si |
| Firewall | Filtra e protege o tráfego |
| Access Point | Distribui o Wi-Fi |

Forma simples de lembrar:
- Switch = dentro de casa
- Roteador = fora de casa

## Caminho de um dado até o YouTube
Notebook → Wi-Fi → Roteador → Provedor →
Internet → Servidor do YouTube

Em detalhes com infraestrutura física:

PC → Wi-Fi → Roteador → Fibra óptica →
Provedor → Cabos submarinos → Outro país →
Servidor do YouTube
## ISP e Backbone

**ISP** é a empresa que vende acesso à internet.
No Brasil: Vivo, Claro, TIM, OI, Algar.
Vários ISPs se conectam entre si para que dados
cheguem de um país ao outro.

**Backbone** é a grande estrada principal da internet —
feita principalmente de fibra óptica, com a maioria
dos cabos passando pelo fundo do oceano.

## Tipos de conexão

| Tipo | Característica |
|------|----------------|
| Fibra óptica | Mais rápida e estável |
| Cabo coaxial | Cabo da TV |
| DSL | Linha telefônica antiga |
| Satélite | Mais lento e caro |
| 4G/5G | Celular via torre |

## MODEM e Roteador

**MODEM** traduz o sinal do ISP para a rede doméstica.
**Roteador** distribui a conexão para os dispositivos.

Caminho completo:
ISP → MODEM → Roteador → PC

Nunca conectar o cabo do MODEM direto no PC —
ficaria sem proteção de firewall e roteador,
exposto diretamente à internet.

Hoje em dia MODEM e Roteador geralmente
vêm num aparelho só.
