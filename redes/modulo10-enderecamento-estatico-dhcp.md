# Redes — Módulo 10: Endereçamento Estático e DHCP

## Endereçamento estático vs dinâmico

Um dispositivo recebe as informações necessárias para
participar da rede de forma **manual (estático)** ou
**automática (DHCP)**.

## Endereçamento estático

As informações são configuradas manualmente no
dispositivo e ficam fixas:

IP: 192.168.1.10
Máscara: 255.255.255.0
Gateway: 192.168.1.1


O dispositivo sempre será encontrado no mesmo endereço.
O problema é que se o endereço mudar repentinamente
(de `192.168.1.10` para `192.168.1.87`, por exemplo),
tudo que dependia do endereço antigo pode deixar de
encontrá-lo.

Por isso faz sentido usar IP estático em dispositivos
que precisam ser sempre localizados no mesmo lugar:

- Servidores
- Impressoras
- Roteadores
- Switches gerenciáveis

## DHCP — Dynamic Host Configuration Protocol

Configurar manualmente 500 computadores numa empresa —
com IP, máscara e gateway em cada um — seria inviável.
É aí que o DHCP entra.

Ele distribui automaticamente as configurações de rede
para cada dispositivo que se conecta.

### O IP alugado — Lease

O IP distribuído pelo DHCP não é permanente — ele tem
um período de validade chamado de **Lease** (concessão
ou aluguel). Quando esse período expira, o IP pode ser
atribuído temporariamente a outro dispositivo,
formando um ciclo.

### Onde o DHCP roda

O DHCP não precisa estar num servidor físico dedicado:

- Em **empresas** → normalmente há um servidor com
  software DHCP fornecendo configurações aos clientes
- Em **casa** → o próprio roteador costuma fazer isso

### Pool de endereços

O DHCP possui um **pool de endereços** — uma tabela
de IPs disponíveis para distribuir:

Pool DHCP:
192.168.1.100
192.168.1.101
192.168.1.102
192.168.1.103
...


## O processo DORA

O processo de obtenção de IP via DHCP segue quatro
etapas:

Discover → Offer → Request → ACK


### 1. Discover

Um PC se conecta à rede sem ter IP. O problema: como
ele conversa com o servidor DHCP se nem sabe o endereço
dele?

A solução é o **broadcast** — o PC envia um
**DHCP Discover** pela rede pedindo uma configuração IP.

O switch recebe o broadcast e propaga dentro do domínio
de broadcast. Todos os dispositivos recebem, mas só
quem tem a função DHCP responde.

### 2. Offer

O servidor DHCP olha o pool de endereços disponíveis
e oferece uma configuração ao PC:

IP: 192.168.1.100
Máscara: 255.255.255.0
Gateway: 192.168.1.1


### 3. Request

O PC aceita a oferta e envia uma mensagem confirmando
que quer aquela configuração.

### 4. ACK (Acknowledgment)

O servidor confirma ao cliente que aquela configuração
foi aceita e registrada. A partir daí o PC pode usar
o IP na rede.

## O que o DHCP distribui

Além do endereço IP, o DHCP também informa:

- Máscara de sub-rede
- Gateway padrão
- Informações de DNS
