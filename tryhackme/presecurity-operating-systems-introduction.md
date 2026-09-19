# TryHackMe — Pre-Security: Operating Systems Introduction

## O cenário da sala

Um amigo te deu um computador antigo, dizendo só que
"costumava rodar bem", sem lembrar de mais detalhes.
Antes de decidir se você vai fazer upgrade, formatar,
vender ou transformar em projeto, é preciso investigar
exatamente o que a máquina tem — é essa a investigação
que guia a sala toda.

## O que é um sistema operacional

O OS é o software central que coordena tudo que
acontece num computador. Fica entre o usuário, as
aplicações e o hardware físico, agindo como um
"gerente invisível" que mantém a máquina rodando como
um sistema unificado.

```
Hardware físico → Sistema Operacional → Aplicações → Usuário
```

## Analogia com aeroporto

```
Hardware (CPU, RAM, storage) → pistas, aviões, radar,
                                a infraestrutura física

Aplicações (browser, jogo)   → companhias aéreas e
                                passageiros, tentando
                                decolar, pousar, pedir serviços

Sistema Operacional          → controle de tráfego aéreo —
                                agenda recursos, gerencia
                                tráfego, resolve conflitos,
                                garante segurança
```

Sem o OS, cada aplicação precisaria de controle direto
sobre CPU, memória, arquivos, dispositivos e segurança
— gerando conflito rapidamente. O OS resolve isso
agindo como organizador central.

## Camadas de privilégio

Partes diferentes do sistema operam em níveis de
permissão diferentes — separação intencional pra
prevenir conflitos e problemas de segurança.

**Kernel space** — núcleo privilegiado e travado do OS.
É onde o kernel (parte do OS que gerencia hardware e
recursos diretamente) roda. Acesso irrestrito a CPU,
memória, storage e todo o hardware.

**User space** — onde aplicações padrão rodam.
Aplicações aqui são impedidas de acessar hardware
diretamente. Sempre que precisam abrir um arquivo,
tocar um som ou conectar no Wi-Fi, fazem uma **system
call**, pedindo pro kernel agir em nome delas.

**Continuando a analogia do aeroporto:** kernel space
é a torre de controle, área estritamente segura onde
só controladores confiáveis trabalham. Aplicações em
user space são as companhias aéreas e passageiros no
chão — não podem entrar na torre, só "chamar por
rádio" (system calls) pedindo pra torre executar algo
com segurança.

Essa separação é o que mantém o OS confiável: uma app
com bug não consegue derrubar o sistema inteiro.

## Responsabilidades centrais do OS

**Process Management** — cria, agenda, prioriza e
termina programas rodando. O OS decide quanto tempo de
CPU cada processo recebe, fazendo o multitasking
parecer contínuo. Ex: abrir várias apps sem travar.

**Memory Management** — aloca RAM pra processos,
protege a memória de uma app das outras, recupera
memória quando apps fecham. Quando a RAM fica baixa, o
OS usa memória virtual pra manter o sistema estável.

**File System Management** — organiza arquivos em
diretórios, lida com nomeação, paths, permissões,
metadados. Ex: criar pasta, salvar foto, definir
arquivo como "somente leitura".

**User Management** — lida com múltiplas contas,
autenticação e permissões que determinam quem acessa
o quê.

**Device Management** — carrega drivers e fornece uma
interface universal (hardware abstraction layer),
permitindo que apps digam "imprima isso" sem se
preocupar com o hardware específico.

## Segurança do OS

Antes de qualquer antivírus ou firewall, o próprio OS
já aplica proteções em segundo plano:

```
Authentication    → verifica quem você é (senha, biometria)
Permissions       → controla o que cada usuário/app pode
                     ler, escrever ou executar
Isolation         → mantém cada processo em sua própria
                     "caixa" protegida (kernel/user space)
System Protection → protege arquivos e configurações
                     críticas contra mudanças não autorizadas
```

## Interfaces de interação

**GUI (Graphical User Interface)** — representação
gráfica de tudo (ícones, janelas, menus). Analogia:
usar um app de navegação tocando no ícone do lugar,
sem precisar digitar.

**CLI (Command-Line Interface)** — você digita
comandos baseados em texto. Mais precisão, controle e
velocidade pra tarefas avançadas, mas exige
familiaridade com os comandos. Analogia: digitar as
coordenadas GPS exatas — direto e preciso, mas só se
você souber a informação certa pra digitar.

## Tipos de sistema operacional

```
Desktop      → computadores pessoais, trabalho, jogos.
                Interface gráfica rica, multitarefa
Server       → hospedagem web, databases, back-end.
                Sem GUI, uptime máximo, multiusuário
Mobile       → smartphones e tablets. Touch, eficiente
                em energia, apps em sandbox
Embedded     → eletrodomésticos, carros, IoT, roteadores.
                Footprint minúsculo, hardware limitado
Virtual/Cloud → lab machines, containers, instâncias
                cloud. Leve, escalável, deploy rápido
```

## Famílias reais de sistemas operacionais

**Desktop:**
```
Windows → mais usado em PCs pessoais
macOS   → OS da Apple, integração com ecossistema
Linux   → família de distribuições open-source
          (Ubuntu, Debian, Fedora)
```

**Server:**
```
Windows Server → redes grandes, data centers, corporativo
Linux          → maioria dos web servers, robustez open-source
Unix           → grandes empresas, finanças, governo
```

**Mobile:**
```
Android → OS mobile mais usado
iOS     → OS da Apple pra iPhone/iPad
```

**Embedded e IoT:**
```
Embedded Linux → especializado em dispositivos com função dedicada
Real-Time OS   → tempo de resposta garantido (controles
                  de aeronave, ex: FreeRTOS, VxWorks)
```

**Virtual e Cloud:**
```
Cloud/VM              → data centers massivos
Container-optimized   → alternativa leve a VMs
```

Cada ambiente valoriza capacidades diferentes — não
existe um único OS perfeito pra toda situação, e sim
um ecossistema inteiro de opções.

## Lab prático — investigando o computador do amigo

Máquina rodando Ubuntu MATE. Usando "About This
Computer" (System Monitor):

```
Versão do Ubuntu MATE  → 1.26.2
Memória alocada         → 1.9 GiB
Tipo do /dev/root        → ext4
```

Investigando o diretório Home:
```
3 diretórios de usuário existentes
```

Navegando até o diretório de um usuário (Alex) →
Documents → note.txt continha a flag:
```
THM{new_pc_for_free!}
```

## Glossário

```
Operating System (OS) → software central que gerencia
                         hardware, apps e recursos do sistema
Kernel space          → área privilegiada com acesso
                         direto ao hardware
User space            → área com permissões limitadas,
                         por segurança e estabilidade
GUI                   → interface visual, interação por
                         clique/toque
CLI                   → interface de texto, comandos precisos
```
