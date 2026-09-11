# Cisco Introduction to Cybersecurity — Módulo 2: Defesas, Criptografia e Privacidade

## As 4 primeiras defesas básicas

```
Firewall           → controla o tráfego de rede que pode entrar/sair
Antivírus/antispyware → tenta detectar e remover software malicioso
Atualização (patch) → corrige vulnerabilidades conhecidas
Senha               → impede acesso direto ao dispositivo/conta
```

São defesas diferentes — um firewall não substitui
antivírus, e antivírus não corrige vulnerabilidade do
sistema operacional. Cada uma cobre uma frente distinta.

O firewall analisa o tráfego de rede e aplica regras
sobre quem pode entrar e sair, protegendo contra acesso
não autorizado.

O antivírus procura software malicioso examinando
arquivos, processos e comportamentos associados a
malware — pode verificar o computador e e-mails
recebidos.

O patch é necessário porque, quando um atacante descobre
uma vulnerabilidade, o patch corrige o problema assim
que descoberto, impedindo que o atacante continue
explorando.

## Por que criptografar dados

Se alguém rouba meu notebook, sem criptografia consegue
acessar o armazenamento com arquivos legíveis. Com
criptografia, o conteúdo fica inutilizável sem a chave
de acesso.

## IoT — o problema combinado

```
1. Recebe poucas atualizações
2. Software potencialmente vulnerável
3. Está conectado à rede
```

Exemplo: uma câmera vulnerável é comprometida, e como
está dentro da minha rede, o atacante tenta alcançar
outros dispositivos a partir dela. Por isso é recomendado
colocar dispositivos IoT numa rede isolada.

## Wi-Fi — mitos e boas práticas

Esconder o SSID não é segurança de verdade — só esconde
o nome da rede. Se o atacante conseguir acesso de outra
forma, o resultado é o mesmo. O que realmente protege
é autenticação + criptografia da rede.

Recomendado: alterar SSID/senha padrão e habilitar WPA2.

## KRACK — vulnerabilidade mesmo com WPA2

Mesmo uma rede com WPA2 pode ter falha no processo de
negociação das chaves. O atacante explora uma falha na
reinstalação da chave:

```
Roteador ↔ dispositivo → processo de estabelecimento
da chave → atacante interfere → possibilidade de
comprometer a comunicação
```

Isso mostra que ter criptografia não torna o sistema
automaticamente invulnerável.

## Criptografia — conceito

Transforma informação num formato que pessoas não
autorizadas não conseguem ler.

```
Senha 123456        → plaintext (texto claro)
8fA#91xL@2...        → ciphertext (texto cifrado)
```

```
PLAINTEXT → (+ chave) → CIFRAGEM → CIPHERTEXT →
(+ chave correta) → DECIFRAGEM → PLAINTEXT
```

A chave é fundamental — sem ela, o atacante não
consegue reverter o ciphertext de forma viável.

**Importante:** criptografia não impede interceptação.
O que ela faz é tornar o que foi capturado ilegível —
e ainda assim existem maneiras de contornar isso.

---

## Termos de Serviço (ToS)

É um contrato que vincula legalmente as regras entre
você, o provedor e outros usuários do serviço:

```
Você aceita os termos → Provedor → regras do relacionamento
```

Não é uma página informativa qualquer — é um contrato
real. "Concordo com os Termos de Serviço" não deveria
ser um botão apertado sem pensar.

**Três documentos diferentes:**

- **Política de uso de dados** — como a empresa armazena, usa e compartilha seus dados
- **Configurações de privacidade** — quem pode ver seus dados (público, amigos, autorizados)
- **Política de segurança** — como a empresa protege as informações que tem sobre você

**Transferível** — a licença pode passar pra outra entidade em certas circunstâncias.

**Sublicenciável** — a empresa pode conceder a terceiros direitos que ela própria recebeu. Ela não necessariamente guarda sua foto — ela recebe direitos jurídicos de utilização definidos pelo contrato.

**Isenta de royalties** — a empresa não precisa te pagar pelo uso da licença concedida:
```
Você concede licença → empresa utiliza → não paga royalties
```

Sem alterar as configurações padrão, qualquer pessoa
pode ver informações e acessar seu perfil.

**Checklist de proteção básica:**
```
Ler os Termos de Serviço
Configurar a privacidade
Limitar quem pode visualizar o conteúdo
Verificar a política de segurança
Utilizar senhas fortes
```

---

## Cinco mecanismos de proteção da privacidade

```
1. Autenticação de dois fatores (2FA)
2. OAuth
3. Compartilhamento consciente de informações
4. Reconhecimento de engenharia social/phishing
5. Privacidade no navegador e no e-mail
```

### 1. 2FA

Sem 2FA, o atacante só precisa da senha. O sistema
não diferencia usuário real de atacante.

Com 2FA, depois do login o sistema pede algo adicional
que só o usuário tem — código, celular, biometria:

```
Senha roubada → atacante tenta entrar → servidor pede
segundo fator → atacante não possui → acesso bloqueado
```

Mas 2FA não é invulnerável — phishing, engenharia
social e malware já capturam esses dados também:

```
2FA              → dificulta roubo de credenciais
Phishing         → tenta fazer você entregar as credenciais
Malware          → pode capturar/interferir no processo
Engenharia social → manipula a pessoa diretamente
```

### 2. OAuth

*Open Authorization* — o aplicativo obtém autorização
sem precisar conhecer sua senha do provedor.

### 3. Compartilhamento social e agregação de informações

Cada informação isolada parece inofensiva. O problema
aparece quando são combinadas — princípio da
**agregação de informações**:

```
LinkedIn      → empresa + cargo
Instagram     → nome + foto
Facebook      → aniversário + amigos
Site empresa  → gerente + estrutura da empresa
```

Separadamente têm pouco valor. Juntas formam um perfil
extremamente detalhado, usável pra engenharia social.

### 4/5. Navegação privada e fingerprinting

Modo privado/incógnito não torna anônimo — é só uma
ferramenta pra não deixar rastros locais (cookies,
histórico). Ao fechar a sessão, esses dados somem —
útil principalmente quando outra pessoa usa o mesmo
dispositivo depois.

**Fingerprinting** — mesmo sem cookies, outras
características identificam o navegador/dispositivo:

```
navegador + sistema operacional + resolução + idiomas
+ fontes + características do ambiente = "impressão
digital" do navegador
```

Privacidade não depende de um único mecanismo.

### Gerenciador de senhas

Cada serviço deveria ter senha diferente. O gerenciador
cria e armazena senhas de forma protegida/criptografada,
com geração aleatória de credenciais únicas — evita
precisar lembrar cada senha manualmente.
