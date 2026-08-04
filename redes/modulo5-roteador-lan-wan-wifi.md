# Redes — Módulo 5: Roteador, LAN, WAN e Wi-Fi

## O caminho da internet até os dispositivos

A internet de fora via cabos de fibra óptica,
são transmitidos ao WAN, que é transmitido ao modem que traduz o sinal para que o roteador faça o papel de intermediador
entre a rede local (LAN) e fora WAN. E então o roteador entrega essa internet
para notebook, celular, TV e videogame.

## Por que o roteador se chama roteador

Ele liga duas redes diferentes: a internet (rede externa)
e a rede de casa (rede local). O roteador fica no meio
das duas e faz a ponte entre elas.

## LAN e WAN

**LAN — Local Area Network**
Tudo que se conecta nas portas LAN pertence à mesma rede
local — notebook, PC, impressora, videogame. Geralmente
o roteador tem 4 entradas LAN, e todos os dispositivos
conectados nelas conversam entre si.

**WAN — porta internet**
Ligada diretamente no modem. Não faz parte da rede de
casa — representa o "lado de fora", a internet em si.

O Wi-Fi fica dentro do roteador — praticamente todo
roteador já vem com um Access Point embutido.

## Resumo dos componentes da rede doméstica

| Componente | Função |
|------------|--------|
| ISP | Empresa que fornece a internet |
| Modem | Traduz o sinal do ISP para a rede entender |
| Roteador | Distribui a internet para toda a casa |
| LAN | Portas da rede local (dispositivos de casa) |
| WAN | Porta ligada ao modem/ISP |
| Wi-Fi | Forma sem fio de entrar na mesma rede LAN |

## Frequências do Wi-Fi

**2.4 GHz** — mais alcance, mais interferência, mais lento
**5 GHz** — menos alcance, menos interferência, muito mais rápido

O Bluetooth também usa 2.4 GHz, mas como é feito para
curtas distâncias, isso não atrapalha seu funcionamento.

## O padrão do Wi-Fi

O nome oficial do Wi-Fi é **IEEE 802.11**.

Wi-Fi e IEEE não são a mesma coisa:
- **IEEE** (Instituto dos Engenheiros Eletricistas e
  Eletrônicos) cria as regras técnicas
- **Fabricantes** criam os roteadores seguindo essas regras
- **Wi-Fi Alliance** testa se as regras foram seguidas e,
  se aprovado, coloca o selo de Wi-Fi

## Gerações do Wi-Fi (do mais antigo ao mais novo)
802.11b → versão antiga, mais lenta
802.11g → melhor
802.11n → mais rápida
802.11ac → melhor ainda
802.11ax → Wi-Fi 6, muito melhor


## Redes com fio vs sem fio

**Com fio:**
- Ethernet (cabos)

**Sem fio:**
- Wi-Fi
- Bluetooth

## Ethernet e tipos de cabo

Ethernet não é o cabo em si — é o conjunto de regras
que define como a comunicação acontece usando aquele cabo.

| Cabo | Característica |
|------|-----------------|
| Par trançado (Cat5e) | Boa velocidade, 8 fios (4 pares) |
| Coaxial | Boa distância, usado por operadoras e TV a cabo |
| Fibra óptica | Excelente velocidade e excelente distância, transmite por luz |

## Broadcast e criptografia

**Broadcast** faz o nome da rede (SSID) aparecer
automaticamente na lista de redes disponíveis, sem
precisar digitar manualmente.

**Criptografia** embaralha a senha para que, se alguém
interceptar a conexão, não consiga entender o conteúdo.

## Tipos de criptografia Wi-Fi (do mais fraco ao mais forte)

WEP → antiga, fácil de burlar
WPA → melhor
WPA2 → muito bom
WPA3 → melhor ainda


## Modo da rede e compatibilidade

Se o roteador só aceita Wi-Fi 6 e um notebook antigo só
entende 802.11g, eles não conseguem se conectar.

Se o roteador tiver **modo misto (Mixed Mode)**, tanto
dispositivos antigos quanto novos conseguem se conectar
na mesma rede.

## Outros termos importantes

**DHCP** — protocolo que entrega o IP automaticamente
para os dispositivos da rede.

**Gateway** — a porta de saída da rede, onde fica o IP
que direciona o tráfego para fora da rede local.
