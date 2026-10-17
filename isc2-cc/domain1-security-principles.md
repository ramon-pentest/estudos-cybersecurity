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
