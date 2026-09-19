# TryHackMe — Pre-Security: Cloud Computing Fundamentals

## O problema que a cloud resolve

Imagina que você tem uma ideia de app pra ajudar
estudantes a praticar cybersecurity, e hospeda ela no
seu próprio computador, no seu país. O que fazer quando
usuários de outras partes do mundo sentem lag ao
acessar? E se muitos estudantes conectarem ao mesmo
tempo, ou seu computador for desligado? Esses limites
dificultam o crescimento do app.

A cloud resolve exatamente esses problemas. Ela é
construída em cima de tecnologias que já vimos antes —
virtualização e containers — que permitem rodar muitas
aplicações eficientemente numa infraestrutura
compartilhada, criando e mudando ambientes rapidamente
quando necessário.

## Como os servers evoluíram até a cloud

Cloud computing não apareceu do nada — é resultado de
anos de mudanças em como servers eram usados e
gerenciados. Em cada etapa, empresas buscavam reduzir
custo, usar recursos com mais eficiência e tornar suas
aplicações mais fáceis de rodar e escalar.

## Benefícios e características da cloud

```
Scalability          → escalar pra cima ou pra baixo
                        conforme a necessidade muda
On-demand self-service → criar ou remover server/storage
                          instantaneamente, sem esperar hardware
Pay only for what you use → cobrança por uso, não custo fixo
Security              → provedores protegem a infraestrutura
                         com medidas fortes
High availability     → app continua rodando mesmo se
                         parte do sistema falhar
Global access          → acessível por usuários em
                         qualquer lugar do mundo
```

## Tipos de deployment de cloud

**Public Cloud** — usado por startups, websites, apps
globais. Acessível pela internet, compartilhado entre
várias pessoas/empresas. Barato, fácil de escalar, sem
gerenciamento de infraestrutura próprio. É o tipo mais
comum, preferível pra quase todo caso de uso.

**Private Cloud** — usado por bancos, saúde, governo.
Construída só pra uma empresa, com mais controle,
customização e compliance pra dados sensíveis.

**Hybrid Cloud** — mistura de public e private,
trabalhando juntas. Usado por e-commerce, por exemplo,
que precisa manter dados sensíveis privados mas ainda
escalar publicamente em picos de demanda.

## Modelos de serviço de cloud

**IaaS (Infrastructure as a Service)** — você aluga
recursos básicos (servers virtuais, storage, rede).
Você gerencia o SO e a aplicação; o provedor gerencia
o hardware físico. Cybersecurity geralmente usa esse
modelo, porque precisa de acesso total ao SO pra
instalar ferramentas, configurar o sistema e simular
ataques/defesas com segurança.

**PaaS (Platform as a Service)** — o provedor gerencia
infraestrutura e SO. Você foca só em construir, fazer
deploy e rodar sua aplicação, sem se preocupar com
servers.

**SaaS (Software as a Service)** — você usa uma
aplicação completa pela internet. O provedor gerencia
tudo, você só acessa via browser ou app. Exemplos:
Gmail, Zoom.

**Analogia rápida:** os três modelos são como formas
diferentes de alugar um lugar pra morar — desde alugar
só a estrutura básica (IaaS) até morar num lugar
totalmente mobiliado e gerenciado (SaaS).

## Principais fornecedores

```
AWS (Amazon)     → líder de mercado, oferta mais extensa
Microsoft Azure  → forte em enterprise e hybrid cloud
Google Cloud     → conhecido por data analytics, AI e ML
Alibaba Cloud    → grande player na Ásia
IBM Cloud        → foco em hybrid cloud e soluções AI
Oracle Cloud     → foco em enterprise e databases
```

**Exemplos de uso real:**
- Netflix roda a plataforma inteira na AWS pra escalar
  globalmente
- Spotify usa cloud pra lidar com milhões de
  músicas/usuários
- Instagram depende da cloud pra armazenar
  fotos/vídeos em massa
- Lojas online usam cloud pra aguentar picos de
  tráfego (Black Friday) sem comprar infraestrutura
  permanente

## Terminologia AWS usada no lab

**EC2 (Elastic Compute Cloud)** — representa um
computador virtual na cloud. Tem CPU e memória, roda
aplicações. Cada instância EC2 adicionada é um
computador a mais no ambiente.

**Instance Type** (ex: t2, t3, m5) — descreve o quão
potente é o computador virtual. Instância maior = mais
poder + custo mais alto. Instância menor = menor poder
+ custo mais baixo.

## Lab prático

O exercício simulava criar um ambiente IaaS na AWS pra
hospedar uma app de treino de cybersecurity — alinhado
ao modelo IaaS, já que cybersecurity geralmente precisa
de acesso total ao SO.

**Passos:**
1. Escolha de região (localização geográfica dos recursos)
2. Criação de 3 instâncias EC2:
```
   Application-interface → t3.micro
   study-machine-1       → m5.large
   study-machine-2       → m5.large
```
3. Seção de Billing mostra custo por instância e total
4. Parar instâncias sem uso ativo (as duas study-machine,
   já que ainda não havia usuários na plataforma) reduz
   custo imediatamente — demonstra na prática o
   benefício do "pay only what you use"

## Glossário

```
Public Cloud  → serviços acessados pela internet,
                compartilhados entre várias pessoas/empresas
Private Cloud → cloud construída só pra uma empresa
Hybrid Cloud  → mistura de public e private
IaaS          → aluga peças básicas de computador (servers, storage)
PaaS          → ambiente pronto pra construir/rodar apps
SaaS          → software usado online sem instalar nada
EC2           → computadores da AWS que você usa e
                redimensiona conforme necessário
```
