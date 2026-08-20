# Redes — Módulo 11: Comunicação Local e Remota, ARP e NAT

## Como o PC decide se o destino é local ou remoto

O PC usa a **máscara de sub-rede** para descobrir se
o destino está na mesma rede ou em outra rede.

## Comunicação local — destino na mesma rede

Se o destino estiver na mesma rede, o PC percebe que
o outro dispositivo está no mesmo domínio. Então:

1. O PC usa o **ARP** para descobrir o MAC do PC2
2. O **switch** faz a comunicação entre os dois
3. Os dispositivos se encontram diretamente

## Comunicação remota — destino fora da rede

Se o PC quiser acessar um IP externo (como `8.8.8.8`):

1. O PC percebe que o destino está fora da rede local
2. O switch faz a comunicação do PC até o roteador
3. O roteador encaminha o tráfego para a internet

Para isso funcionar, o PC precisa enviar o quadro ao
roteador local. Como eles estão na mesma rede e domínio
de broadcast, o PC usa o **ARP** para descobrir o
MAC do gateway (roteador).

O resultado fica assim:

IP Destino: o IP externo que o PC quer acessar (ex: 8.8.8.8)
MAC Destino: MAC do gateway local (roteador), descoberto via ARP


O roteador recebe o quadro, vê que o destino é externo
e encaminha para a internet.

## NAT — tradução de endereços

O NAT traduz endereços IP privados em endereços IP
públicos quando o tráfego sai para a internet, e faz
a tradução inversa quando a resposta retorna.

IP privado → NAT → IP público → Internet
Internet → NAT → IP privado → dispositivo interno


## Por que existem diferentes faixas de rede privada

Organizações diferentes precisam de redes privadas de
tamanhos diferentes. As três faixas privadas existem
justamente para isso:

**192.168.0.0/16 com sub-rede /24**
A mais comum em redes domésticas e pequenas.
Com /24, sobram 8 bits para hosts:

2⁸ = 256 endereços
254 disponíveis para hosts (descontando rede e broadcast)


**172.16.0.0/12**
Faixa privada maior — adequada para organizações
médias que precisam de mais endereços.

**10.0.0.0/8**
A maior das três — adequada para organizações que
precisam de uma quantidade muito grande de endereços
privados internos.

Isso não significa que uma faixa seja melhor que a
outra — é somente uma questão de quanto espaço de
endereçamento a organização precisa.
