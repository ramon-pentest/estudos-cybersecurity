# TryHackMe — Pre-Security: Operating System Security

## OS entre aplicações e hardware

O sistema operacional fica entre as aplicações e o
hardware. Hardware são as partes físicas do computador
(CPU, memória, armazenamento, teclado, monitor). As
aplicações usam os recursos do hardware através do OS,
que controla esse acesso.

**Curiosidade do quiz:** entre várias opções, a que
não é sistema operacional era Thunderbird — ele é um
cliente de e-mail. AIX, Android, Chrome OS e Solaris
são sistemas operacionais reais.

## Tríade CIA

```
Confidentiality (confidencialidade) → quem pode ver as informações
Integrity (integridade)             → quem pode alterar os dados
                                        e se eles continuam corretos
Availability (disponibilidade)      → conseguir usar o sistema e
                                        os dados quando necessário
```

## Três pontos fracos exploráveis

```
1. Autenticação e senhas fracas
2. Permissões de arquivo inadequadas
3. Programas maliciosos
```

### Autenticação

Verificação de identidade, usando:
```
Algo que você sabe   → senha, PIN
Algo que você é       → impressão digital
Algo que você possui  → telefone recebendo um código
```

Senhas fáceis de adivinhar aparecem em listas comuns:
`123456`, `password`, `qwerty`, `iloveyou`, `monkey`,
`dragon`. Uma senha também pode parecer complexa mas
seguir padrão previsível de teclado, como `qwertyuiop`
ou `1q2w3e4r5t`.

No quiz, `LearnM00r` foi considerada a opção forte —
mas trocar letra por número não basta sozinho, a ideia
é ter credenciais difíceis de prever e nunca reutilizar
entre serviços.

### Permissões e least privilege

Permissões respondem a quem pode acessar cada arquivo e
o que pode fazer com ele.

**Least privilege (menor privilégio)** — conceder só
o acesso necessário pra cada usuário fazer seu trabalho.

Permissões excessivas comprometem:
```
Confidencialidade → se alguém lê o que deveria ser restrito
Integridade       → se alguém altera sem autorização
```

### Programas maliciosos

**Trojan** — parece legítimo, mas executa ações
maliciosas, permitindo que o invasor leia ou modifique
arquivos.

**Ransomware** — criptografa arquivos, impedindo uso
normal — afeta principalmente disponibilidade. Pagar o
resgate não garante recuperação dos dados.

## Laboratório prático

Acesso via SSH como `sammie` no IP `10.65.181.98`,
senha `dragon`.

Na primeira conexão, o SSH avisa que não conhece a
chave do servidor e mostra uma fingerprint — no
laboratório respondi `yes`. Numa situação real, a
fingerprint deve ser confirmada por fonte confiável
antes de aceitar.

Ao digitar senha no terminal, normalmente nenhum
caractere aparece — nem letra, ponto ou asterisco.
Isso é comportamento normal, não erro.

**Comandos usados:**
```
whoami  → confirma qual usuário está ativo
ls      → lista arquivos e pastas
cat     → mostra conteúdo de arquivo de texto
history → mostra comandos registrados pelo shell
```

## Escalada de privilégios no cenário

Outros usuários mencionados: Johnny e Linda. O desafio
pedia achar a senha de Johnny entre opções comuns.
Depois de logar como Johnny, `history` revelou que ele
tinha digitado a senha de root por engano, como se
fosse um comando.

Sequência de escalada:
```
su - root           → trocar pra conta root
cat /root/flag.txt  → ler a flag
```

Root é a conta administrativa tradicional no Linux. No
Windows existem contas equivalentes (Administrator),
mas os mecanismos não são idênticos entre os sistemas.

O laboratório demonstra o padrão clássico de escalada:
acesso como usuário comum → falha ou informação exposta
→ credencial mais poderosa → root. Isso só é válido
dentro da máquina fornecida pro laboratório — nunca
deve ser tentado em sistema sem autorização.
