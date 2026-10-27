# ISC2 CC — Domain 1: Security Principles

## Code of Professional Conduct

Código de conduta que membros certificados pela ISC2
devem seguir. A certificação é um privilégio que precisa
ser conquistado e mantido.

**Code of Ethics** — estabelece os princípios éticos
fundamentais exigidos dos membros. Seguir esse código é
condição pra manter a certificação.

### Os 4 princípios éticos da ISC2

1. **Protect society** — proteger a sociedade, o bem
   comum, a confiança pública e a infraestrutura.
2. **Act honorably** — agir com honra, honestidade,
   justiça, responsabilidade e dentro da lei.
3. **Provide diligent and competent service** — prestar
   serviço com dedicação, cuidado e competência aos
   clientes ou organizações atendidas, que são a
   prioridade principal.
4. **Advance and protect the profession** — promover e
   proteger a profissão de segurança da informação.

---

## Due Care vs Due Diligence

Não basta implementar medidas de segurança — é preciso
acompanhar e verificar se elas continuam funcionando.

Due Care → tomar as medidas razoáveis e prudentes
pra cumprir uma responsabilidade,
considerando todo o ciclo de vida da tarefa

Due Diligence → monitorar, controlar, gerenciar e avaliar
se essas medidas estão funcionando e
continuam necessárias


**Exemplo:** uma empresa instala um sistema de segurança
pra proteger dados.

Due Care → escolher e implementar controles adequados
Due Diligence → verificar continuamente se os controles
funcionam, acompanhar novos riscos e
corrigir falhas


### Reasonable vs Prudent

Reasonable actions → decisão com justificativa lógica,
cuidadosa e baseada nas informações
disponíveis

Prudent actions → atitude que uma pessoa com
experiência, educação e autoridade
semelhantes tomaria nas mesmas
circunstâncias


A diferença: *reasonable* foca na justificativa da
decisão que a pessoa tomou; *prudent* enfatiza o
julgamento cuidadoso diante da situação.

### O que a falta de cuidado coloca em risco

Confidencialidade e privacidade → ignorar exigências
de proteção de dados
Integridade, disponibilidade e
autenticidade → não identificar
controles necessários
ou parar de avaliar
a segurança continuamente
Integridade, autenticidade e
não repúdio → não considerar
requisitos funcionais
em processos e sistemas


Exemplos de due diligence na prática: avaliar a
segurança de fornecedores, auditar prestadores de
armazenamento externo, verificar antecedentes antes de
conceder acesso a dados.

**Sobre provas:** publicar uma política de segurança,
por si só, não basta. A organização também precisa ter
mecanismos documentados e ativos de monitoramento e
aplicação daquela política.

---

## Cybersecurity Controls: Technical, Administrative e Physical

Controles de segurança são medidas que reduzem riscos e
protegem a confidencialidade, integridade e
disponibilidade (CIA) dos sistemas e das informações.

### 1. Technical Controls (técnicos ou lógicos)

Implementados por tecnologia: hardware, software e
firmware.

Exemplos: MFA, criptografia, firewalls, logs,
monitoramento, antivírus, Secure Boot


### 2. Administrative Controls (administrativos ou gerenciais)

Estabelecem regras, diretrizes e procedimentos pra
orientar o comportamento das pessoas.

Exemplos: políticas de segurança, treinamentos
obrigatórios, procedimentos de contratação, integração
e desligamento de funcionários


### 3. Physical Controls (físicos)

Protegem pessoas, instalações e ativos físicos,
controlando o acesso e a movimentação em espaços
físicos.

Exemplos: fechaduras, crachás, câmeras, guardas,
barreiras, recepção para visitantes


### Como trabalham juntos — analogia

Empresa que armazena informações confidenciais:

Técnico → exige MFA e limita o acesso aos sistemas
conforme a função do funcionário
Administrativo → exige treinamento de segurança que
define como conceder e remover acessos
Físico → exige crachá pra entrar no prédio e
acompanhamento de visitantes


São complementares — uma pessoa pode ter acesso
autorizado ao prédio, mas não necessariamente aos dados
da empresa.

### As três funções de um controle

Preventiva → impede ou dificulta que um incidente aconteça
Detectiva → identifica atividades suspeitas ou violações
Corretiva → ajuda a conter ou corrigir um problema


Um controle pode contribuir pra mais de uma função. O
objetivo final de tudo é reduzir os riscos a um nível
aceitável pra organização e proteger confidencialidade,
integridade e disponibilidade.

---

## Leis que regulam dados pessoais — exemplos por região

**HIPAA (Estados Unidos)**
*Health Insurance Portability and Accountability Act*
Lei dos EUA que protege informações médicas de
pacientes. O descumprimento pode gerar penalidades
financeiras e criminais.

**GDPR (Europa)**
*General Data Protection Regulation*
Dá a qualquer pessoa dentro das fronteiras da UE
controle sobre quais informações pessoais as empresas
podem coletar e manter a seu respeito.

**ISO**
Organização internacional que publica padrões,
incluindo normas relacionadas à destruição segura de
dados.

---

## Lei vs Norma/Framework vs Política vs Procedimento

Lei → exigência externa, com força jurídica,
criada pelo governo
Norma/Framework → orientação externa, geralmente do
setor, sem força de lei direta (mas
pode virar exigência contratual ou de
certificação)
Política → regra interna da organização,
definindo “o quê”
Procedimento → instrução interna da organização,
definindo “como”, na prática, dia a dia


### A cadeia completa

Leis estabelecem obrigações → padrões orientam as
práticas → políticas definem diretrizes → procedimentos
orientam a execução diária.

Lei → me diz que preciso fazer algo, mas não
diz exatamente como
(ex: “proteja dados pessoais de clientes”)

Norma/Framework → dá um caminho testado de como
organizações costumam atender essa
exigência
(ex: ISO 27001, NIST — “aqui está uma
estrutura de controles que, se seguida,
tende a satisfazer esse tipo de lei”)

Política → a organização traduz essa orientação
genérica numa regra própria dela
(ex: “nossa política é: todo dado de
cliente deve ser criptografado em
repouso e em trânsito”)

Procedimento → o funcionário recebe a instrução exata
de execução daquela política
(ex: “pra criptografar um banco de
dados novo, siga esses 5 passos no
sistema X”)

---

## Apetite, tolerância e limiar de risco

Apetite de risco (Risk appetite) → a política geral:
“quanto de risco a
organização topa
correr como regra”

Tolerância a risco (Risk tolerance) → a decisão específica:
“nessa situação
pontual, até onde eu
aceito esse risco”

Limiar de risco (Risk threshold) → o ponto de corte
exato onde a
tolerância se esgota


A tolerância a risco é a aplicação prática e situacional
do apetite de risco geral da organização, e ela escala
inversamente com a gravidade e a irreversibilidade do
pior cenário possível: quanto mais recuperável a perda,
mais risco se aceita; quanto mais irreversível (vida
humana), menor a tolerância, até chegar em zero.
---

## Accountability vs Nonrepudiation

Accountability → rastreia uma ação até uma identidade
via log/trilha de auditoria. Serve
pra investigação, mas é contestável —
um log sozinho pode ser forjado, ou
a autenticação por trás dele pode ter
sido comprometida (credencial roubada,
sessão sequestrada)

Nonrepudiation → exige prova criptográfica e protegida
contra violação — mais forte do que
simplesmente “ficou registrado em
algum lugar”


A diferença central:

Accountability diz: “Aparentemente foi essa pessoa”
Nonrepudiation diz: “Está provado, de forma verificável
e resistente a contestação, que foi
essa pessoa”


Geralmente logs de aplicação web só fornecem
Accountability.

---

## ISO 27001/27002 vs CIS Controls

ISO 27001/27002 → framework de gestão: estrutura,
governança, processo de decisão.
Responde “como a organização deve se
organizar pra gerenciar segurança”
Mais abstrato, mais sobre estrutura
de responsabilidade.

CIS Controls → lista priorizada de ações práticas.
Responde “o que eu faço primeiro, na
prática, pra reduzir risco”
Mais concreto, mais sobre execução direta.


Reduzido ao essencial: **ISO é "como gerenciar", CIS é
"o que fazer"**. Uma organização frequentemente usa os
dois juntos — ISO dá a estrutura de gestão, CIS dá a
lista de ação prioritária dentro dessa estrutura.

### A família ISO 27000

27001 → terminologia
27002 → controle de segurança
27003 → orientação de implementação (o CIS Control foca
na prática, na medição de alto impacto que
organizações podem implementar pra reduzir riscos)
27005 → gerenciamento de risco


---

## Standard vs Framework vs Guideline

Standard → requisito específico, geralmente prescritivo,
que a organização adota voluntariamente ou
pra atender expectativa regulatória
(prescritivo = dizer exatamente o que fazer,
passo a passo)

Framework → abordagem estruturada pra gerenciar risco:
oferece organização, categorias, processos

Guideline → recomendação flexível, focada em como aplicar
na prática. Fica entre framework e standard —
mais prático que framework, mas menos rígido
que standard


**A diferença fundamental:** standard é prescritivo e
específico (regra exata); framework é estruturado mas
não necessariamente prescritivo no detalhe (categoria/
processo, não número exato). Standard desce ao detalhe
operacional, framework organiza em categoria mais ampla.

### A cadeia completa

Lei (obrigatório, define “o quê” em termos gerais)
↓
Standard (especifica “a regra exata” dentro de uma
categoria — ex: ISO 27002 com seu catálogo de controle
específico)
↓
Guideline (sugere “como aplicar na prática aquela regra”
— ex: OWASP Top 10 dizendo como priorizar ação contra
risco de aplicação web)
↓
Política interna da organização → Procedimento


**Por que framework vem logo depois da lei, e não
standard:** framework organiza a conversa inteira em
categorias primeiro — você precisa saber que existe uma
função "Protect" antes de saber qual standard específico
de senha aplicar dentro dela. Standard entra depois
porque ele presume que você já sabe em qual categoria
está mexendo.

NIST CSF tem exatamente 6 funções: **Govern, Identify,
Protect, Detect, Respond, Recover**.

---

## Risk Treatment

Risk treatment → a decisão do que fazer com um risco
já identificado
Residual risk → o risco que sobra depois de aplicar
controles (o risco nunca zera,
só diminui o máximo que der)
Blast radius → o alcance do dano se algo der errado


### As 4 opções de tratamento

**1. Accept** — a empresa decide não fazer nada porque o
risco em si causaria um dano insignificante, e o custo
de eliminá-lo não compensa.

**2. Avoid** — a empresa muda o processo de negócio pra
nem ter o risco. Exemplo: em vez de guardar os dados do
cartão do cliente, usa um processador de pagamento
terceirizado, onde os dados do cartão nem chegam a tocar
no sistema da empresa.

**3. Reduce** — a empresa implementa controles pra
diminuir a chance ou o impacto do risco, mas continua
tendo que lidar com ele (MFA, controle de acesso,
criptografia).

**4. Share/Transfer** — a empresa passa parte do risco
financeiro pra outra parte, geralmente via contrato. Se
o vazamento acontecer, a seguradora cobre parte do
prejuízo financeiro.

---

## Autenticação e Autorização

*"Authentication establishes identity; authorization
enforces permissions."*

SFA (Single-Factor Authentication) → um fator único usado
pra autenticar (senha,
frase secreta, PIN)

MFA (Multi-Factor Authentication) → usa 2 ou mais fatores
ao mesmo tempo (token
físico, smart card,
chave de segurança
combinados com senha,
PIN, frase secreta)


**MFA não é duas credenciais diferentes — é duas
categorias independentes.** Usar PIN junto com senha é a
mesma categoria, e um ataque de phishing, keylogger ou
vazamento de dados provavelmente já teria as duas juntas,
porque partem do mesmo princípio.

### O limite do MFA tradicional

Num caso de senha + SMS, nenhum dos dois fatores verifica
criptograficamente que a requisição veio do site
legítimo — ambos são só dados que a pessoa digita,
interceptáveis.

**FIDO2/passkey** resiste a isso porque usa
**origin-binding**: a chave só autentica se o domínio
bater exatamente com o real, então um clone visual do
site não funciona mesmo que engane a pessoa.

Existe uma exceção: um único fator resistente a phishing
(tipo uma chave de segurança FIDO2) pode proteger mais do
que MFA tradicional baseado em senha + segundo fator
fraco.

### Modelos de controle de acesso

RBAC (Role-Based Access Control) → permissão atribuída
com base no
cargo/função. Ex:
“todo analista
financeiro” tem
acesso ao sistema
de contas a pagar,
independente de
quem ocupa o cargo

ABAC (Attribute-Based Access Control) → permissão decidida
considerando vários
atributos ao mesmo
tempo: cargo, tipo
de dispositivo,
localização, horário


**Zero Trust** é, em boa parte, a resposta estrutural ao
problema que o phishing moderno criou — se a autenticação
pode ser comprometida mesmo com MFA (via sessão
sequestrada), a defesa não pode depender só do momento do
login, precisa ser contínua.

---

## Government vs Governance

Government → quem cria a lei (uma entidade específica,
externa à empresa)
Governance → como uma organização organiza sua própria
tomada de decisão internamente (um
processo que pode existir dentro de
qualquer empresa, não só no setor público)


### Organizações de padrão — resumo

ISO → internacional, pago
NIST → agência do governo dos EUA, gratuito, mas virou
padrão mundial
IETF → protocolos de comunicação entre computadores
IEEE → foca em telecomunicação, engenharia da computação
e disciplinas similares


CIS e NIST CSF são mais escolhidos por serem mais
acessíveis — frameworks ou standards mais novos, sem
tanto fundo de investimento no começo, procuram recursos
mais acessíveis. Por isso são mais usados na prática.
