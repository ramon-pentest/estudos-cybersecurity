# TryHackMe — Pre-Security: Virtualisation Basics

## O problema antes da virtualização

Existia uma regra antiga: **um server = uma aplicação**. Cada
serviço (site, banco de dados, e-mail, app interno) tinha a
sua própria máquina física. Isso trazia problemas:

```
Custo alto       → além do hardware: eletricidade, refrigeração,
                   manutenção, espaço no data center
Baixa utilização → muitos servers ficavam em 5–20% de uso,
                   desperdiçando CPU, memória e storage
Deploy lento     → configurar um server físico novo levava
                   dias ou semanas
Difícil escalar  → se uma aplicação precisava de mais recursos
                   de repente, muitas vezes era preciso
                   comprar outro server inteiro
```

## A ideia da virtualização

E se várias aplicações pudessem dividir o mesmo server físico
com segurança? Pra isso entra uma camada chamada
**hypervisor**, que age como um árbitro e permite que cada
computador virtual se comporte de forma independente, como se
fosse uma máquina física.

**Analogia do prédio:** uma pessoa morando sozinha num prédio
de 10 andares usa só um andar mas paga o prédio inteiro
(eletricidade, limpeza, água, segurança) — é o server físico
rodando uma única aplicação. Dividindo o prédio em
apartamentos, cada um com sua porta e privacidade mas
dividindo a estrutura, tudo fica mais barato e eficiente.

```
O prédio         → o server físico
Os apartamentos  → as VMs (lab machines)
Os moradores     → aplicações ou sistemas operacionais
O gerente        → o hypervisor
```

Cada VM age como um sistema independente, com seu próprio SO,
apps e configurações, mesmo dividindo o mesmo hardware.

## Hypervisor

É a tecnologia central da virtualização — o software que cria
e gerencia as VMs.

- Divide um computador físico em vários virtuais
- Dá pra cada VM sua fatia de CPU, memória e storage
- Mantém tudo isolado e seguro
- Gerencia o ciclo de vida das VMs (start, stop, pause, clone,
  delete)

```
Type 1 → roda direto no hardware físico
         rápido e eficiente
         uso: servidores de produção, bancos de dados, data centers

Type 2 → roda dentro de um sistema operacional já existente
         mais fácil de instalar
         uso: aprendizado, testes, rodar o Kali Linux, testar
         arquivos maliciosos
         exemplos: VirtualBox, VMware Workstation
```

**Cuidado ao testar malware numa VM:** garantir que a máquina
host não seja infectada pelo que está sendo testado na guest.
Abordagens: usar um SO diferente entre guest e host, ou isolar
a guest pra ela não se comunicar com o host.

## VM (lab machine)

Computador virtual criado pelo hypervisor. Se comporta como
máquina real: tem CPU, RAM, storage e rede virtuais, roda
qualquer sistema operacional e é totalmente isolada das
outras — se uma quebra, as outras continuam funcionando.

## Container

Ambiente leve e isolado que roda uma única aplicação com tudo
que ela precisa pra funcionar. A diferença chave pra VM: o
container **não traz um SO inteiro** — compartilha o kernel do
sistema host.

```
+ inicia quase instantaneamente
+ usa menos recursos que uma VM completa
+ empacota a aplicação com as dependências (bibliotecas,
  ferramentas, versões)
+ isolado de outros containers
+ roda de forma consistente em qualquer máquina
- precisa ser do mesmo tipo do host (não roda container
  Windows numa máquina Linux)
```

**Docker** é a plataforma open-source mais comum pra simplificar
build, deploy e execução de aplicações com containers.

```
VM         = apartamento (máxima separação e flexibilidade)
Container  = quarto dentro do apartamento (leve, ideal pra
             deploy rápido e escalável)
```

## Lab prático — AutoGalo

Cenário: fico responsável pelo ambiente virtual da empresa
AutoGalo usando uma aplicação chamada Virtualization Manager.
A tela principal tem três áreas: Summary (visão geral),
Lab Machines (detalhes de cada VM com ações disponíveis) e
Hosts (uso e performance de cada server físico).

**Problema no e-mail:** todo mundo parou de receber. Na seção
Lab Machines, a VM Mail-SERVER estava em estado de Error.
Reiniciei pelo botão de restart e voltou a funcionar.

**Criando uma VM** pro site do time de marketing:
```
Name       → Marketing-VM
CPU Cores  → 4
Memory     → 8 GB
Disk Size  → 100 GB
```

**Análise de uso de hardware:**
```
HV-PROD-01   → ainda tinha capacidade pra hospedar mais VMs
HV-PROD-02   → quase em 100% da capacidade (precisaria ser reportado)
HV-BACKUP-01 → desconectado, sem hospedar nenhuma VM
```

## Benefícios da virtualização

Economia de custo, melhor uso de recursos, teste seguro pra
cybersecurity, deploy mais rápido, flexibilidade,
portabilidade, escalabilidade e gerenciamento centralizado.
