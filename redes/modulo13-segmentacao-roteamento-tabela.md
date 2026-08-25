# Redes — Módulo 13: Segmentação, Roteamento e Tabela de Roteamento

## Por que dividir uma rede grande

Três motivos principais para uma empresa segmentar
a rede:

**1. Limitar o broadcast**
Muitos dispositivos na mesma rede recebendo broadcast
constantemente prejudica o desempenho de toda a rede.

**2. Segurança**
Separar departamentos evita acessos indevidos. Exemplo:
- Vendas não deveria acessar servidores da Contabilidade
- Contabilidade não deveria acessar os mecanismos de
  controle da rede

**3. Localização geográfica**
Se um departamento muda de prédio ou andar, a rede
original pode não conseguir atender bem aquela nova
localização — então faz sentido dividir a infraestrutura
em redes menores e independentes.

## O roteador como separador de redes

Quando o roteador é inserido, cada interface dele
se conecta a uma rede diferente:

Rede A → interface | Roteador | interface ← Rede B


Com isso o roteador separa duas coisas:
- Redes IP
- Domínios de broadcast

## Domínio de broadcast

Domínio de broadcast é a área que ouve um broadcast.

Sem roteador, todos os dispositivos estão no mesmo
domínio:

PC1 ─┐
PC2 ─┤
PC3 ─┼── Switch
PC4 ─┤
PC5 ─┘


Um broadcast se propaga pelo switch para todos.

Com o roteador no meio, ficamos com dois domínios
separados — o broadcast de um lado não atravessa
para o outro:

PC1 ─┐ ┌─ PC4
PC2 ─┼── Switch ── Roteador ──┤
PC3 ─┘ └─ PC5


## Roteamento

Roteamento é o processo de identificar o melhor
caminho até um destino.

Quando o pacote chega no roteador:
1. O roteador desencapsula o quadro Ethernet
2. Analisa o IP de destino
3. Consulta a tabela de roteamento para escolher
   a melhor saída
4. Cria um novo quadro Ethernet para o próximo trecho

O IP continua sendo encaminhado em direção ao destino,
mas o quadro Ethernet é recriado a cada enlace.

## Tabela de roteamento

Armazena informações sobre redes conhecidas e o melhor
caminho para alcançá-las.

Estrutura básica:

| Tipo | Rede de destino | Interface de saída |
|------|-----------------|--------------------|
| C    | 192.168.1.0/24  | Fa0/0              |
| C    | 10.0.0.0/8      | Fa0/1              |

- **Tipo** → tipo de conexão
- **Rede** → rede de destino
- **Interface** → porta usada para encaminhar

**C = Connected** — rede diretamente conectada
ao roteador.

A tabela pode ser preenchida:
- **Dinamicamente** → por outros roteadores (protocolos
  de roteamento dinâmico)
- **Manualmente** → por um administrador de rede

Se não houver rota conhecida para o destino, o
roteador descarta o pacote.

## Rota padrão e gateway padrão

**Rota padrão** — caminho usado quando o roteador
não tem uma rota específica para aquela rede de destino.

**Gateway padrão** — o endereço IP da interface do
roteador conectada à mesma rede local do host. Para
descobrir o MAC do gateway, o host usa ARP.

## Resumo do fluxo completo

**HOST:**
- Decide se o destino está na mesma rede ou não
- Mesma rede → envia direto usando o MAC do destino
- Rede remota → envia ao gateway usando o MAC do roteador

**ROTEADOR:**
- Recebe o pacote
- Consulta a tabela de roteamento pelo IP de destino
- Escolhe a interface de saída correta

IP destino = destino final (não muda)
MAC destino = próximo dispositivo no enlace atual (muda a cada salto)
