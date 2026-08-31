# Redes — Módulo 16: SSH, Telnet, E-mail e VoIP

## Terminal virtual — acesso remoto

O terminal virtual permite acessar um terminal sem
estar fisicamente presente no local. O **Telnet**
foi criado exatamente para esse tipo de acesso
remoto, usando a porta 23.

O problema do Telnet é que ele **não criptografa**
os dados da sessão — um atacante poderia interceptar
facilmente tudo que passa pela rede, incluindo usuário
e senha.

## SSH — Secure Shell

O SSH surgiu como alternativa segura ao Telnet.
Porta padrão: **22**

Permite:
- Acessar servidores remotamente
- Executar comandos
- Trabalhar através de uma CLI
- Administrar dispositivos pela rede

A diferença fundamental é que o SSH **criptografa
a sessão**. Um atacante pode até capturar os pacotes,
mas o conteúdo está protegido — ele não consegue
ler o que está sendo transmitido.

Meu PC: 192.168.1.10
↓ SSH (porta 22)
Servidor: 192.168.1.50


## E-mail — múltiplos protocolos

O e-mail não usa um único protocolo. Quando uma
mensagem é enviada, existem duas operações distintas:
Enviar o e-mail → SMTP
Ler/baixar o e-mail → POP3 ou IMAP4

### SMTP — Simple Mail Transfer Protocol | Porta 25

Usado para enviar e-mail — tanto do cliente para
o servidor do provedor, quanto entre servidores
de e-mail diferentes:

VOCÊ
↓ SMTP
Servidor de e-mail do seu provedor
↓ SMTP
Servidor de e-mail do destinatário
↓ IMAP4 ou POP3
DESTINATÁRIO


### POP3 — Post Office Protocol v3 | Porta 110

Recupera as mensagens do servidor e as baixa para
o cliente. Por padrão, as mensagens **não ficam
armazenadas no servidor** depois de acessadas —
são removidas de lá após o download.

### IMAP4 | Porta 143

Também recupera e-mails, mas **mantém as mensagens
no servidor**. A diferença fundamental em relação
ao POP3 é que o IMAP mantém as mensagens na caixa
de correio do servidor, a menos que o usuário as
exclua manualmente.

SMTP → enviar e-mail | Porta 25
POP3 → baixar e-mail | Porta 110
IMAP4 → acessar e manter | Porta 143


Os servidores de e-mail funcionam como uma caixa
postal intermediária — recebem, armazenam, encaminham
e permitem que os usuários recuperem suas mensagens.

## Mensagens instantâneas

Em aplicações como WhatsApp, Microsoft Teams e
Discord, ambos os clientes podem enviar e receber
simultaneamente:

Cliente + Servidor ←→ REDE ←→ Cliente + Servidor


Diferente da visão simples de:

Cliente → Servidor


Em uma conversa em tempo real, ambos estão
constantemente enviando e recebendo.

## VoIP — Voice over IP

A voz é transformada em dados digitais e transportada
pela rede em pacotes IP:

Sua voz
↓ sinal de áudio
↓ conversão para dados digitais
↓ pacotes IP
↓ Internet
↓ pacotes IP
↓ conversão em áudio
Voz do destinatário


Em vez de percorrer uma rede telefônica tradicional,
a voz é transportada pela infraestrutura IP.

Se a ligação for feita dentro do mesmo serviço de
internet (ex: WhatsApp → WhatsApp), ela fica toda
dentro desse serviço.

Se ligarmos para um telefone convencional, o VoIP
passa pela internet, sai pelo **Gateway** para o
**PSTN** (Public Switched Telephone Network — a
rede telefônica pública), e então chega ao telefone
convencional.

O gateway funciona como a ponte entre a
infraestrutura IP e a rede telefônica tradicional.
