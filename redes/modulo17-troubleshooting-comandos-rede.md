# Redes — Módulo 17: Troubleshooting e Comandos de Rede

## O problema

Imagine que você tenta acessar um site e não consegue.
O objetivo é descobrir onde está o problema:
- No meu PC?
- Na rede local?
- No caminho até a internet?
- No DNS?
- No próprio serviço?

Existem comandos que ajudam a localizar cada um
desses pontos.

## IPconfig

Mostra como o PC está configurado:

ipconfig → IPv4, máscara de sub-rede, gateway padrão
ipconfig /all → muito mais detalhes: MAC, IPv4, IPv6,
servidor DHCP, servidores DNS,
informações da concessão DHCP


Outros usos:

ipconfig /release → libera a configuração DHCP atual
ipconfig /renew → solicita uma nova configuração ao DHCP


## Ping

Confirma se a rede consegue chegar ao destino usando
**ICMP echo request** e esperando um **ICMP reply**.

É possível pingar diretamente pelo IP ou pelo nome
do host. No segundo caso, há um passo adicional onde
o DNS descobre o IP antes de fazer o ping.

### Como interpretar os resultados

Ping no gateway falha
→ problema na rede local ou na configuração do próprio host

Ping no gateway funciona, mas ping no destino externo falha
→ problema mais adiante no caminho (fora da rede local)

Ping no nome do destino falha
→ grande probabilidade de ser problema de DNS

Ping funciona, mas o serviço (HTTP/HTTPS) não
→ a rede está ok, mas o servidor pode estar parado


**Atenção:** nem sempre ping falhando significa rede
quebrada — firewalls frequentemente bloqueiam ICMP.
O servidor pode estar funcionando perfeitamente e
aceitando HTTP/HTTPS, mas bloqueando ping.

### Variações do comando

ping -t 10.10.10.1 → pinga continuamente até interromper
útil para observar quedas intermitentes

ping -n 10 10.10.10.1 → envia 10 requisições em vez do padrão (4)

ping -l 1000 10.10.10.1 → envia pacote com tamanho específico de dados


## Netstat

Mostra com quem o PC está conectado — as conexões
TCP ativas:

Proto Local Address Foreign Address
TCP 192.168.1.124:3158 207.138.126.152:http


- **Local Address** → IP do PC local + porta local
- **Foreign Address** → IP remoto + porta remota
- **Established** → conexão ativa

netstat -n → mostra números de porta em vez dos nomes
(ex: 80 em vez de "http")


## Tracert (traceroute)

Mostra quais roteadores o tráfego está passando
no caminho até o destino — útil para identificar
onde exatamente o pacote está parando.

tracert 8.8.8.8


Cada linha representa um salto (hop) — um roteador
pelo qual o pacote passou. Se travar num salto
específico, é sinal de que o problema está naquele
ponto do caminho.

## Nslookup

Confere se o DNS consegue resolver um nome:

nslookup www.google.com


Retorna o IP associado ao nome consultado. Útil
para confirmar se o problema de acesso é de DNS
ou de outra coisa.

## Resumo dos comandos

| Comando | Para que serve |
|---------|----------------|
| `ipconfig` | Ver configuração de rede do PC |
| `ipconfig /all` | Ver todos os detalhes (MAC, DHCP, DNS) |
| `ipconfig /release` | Liberar configuração DHCP |
| `ipconfig /renew` | Renovar configuração DHCP |
| `ping` | Testar conectividade com um destino |
| `netstat` | Ver conexões TCP ativas |
| `netstat -n` | Ver conexões com números de porta |
| `tracert` | Ver roteadores no caminho até o destino |
| `nslookup` | Verificar resolução de nomes DNS |
