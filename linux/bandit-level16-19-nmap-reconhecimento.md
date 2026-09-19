# Bandit — Level 16 ao 19: Nmap e Ferramentas de Reconhecimento

## nmap — descobrindo o que está exposto

O `nmap` serve pra olhar uma máquina de fora e
descobrir quais portas estão abertas e quais serviços
estão disponíveis.

Exemplo de portas comuns:
```
22   → ssh
80   → http
443  → https
3306 → mySQL
```

```bash
nmap alvo.com
```

Retorna algo como:
```
22/tcp open ssh
80/tcp open http
443/tcp open https
```

**Buscando portas específicas:**
```bash
nmap -p 31000-32000 localhost
```
Busca só as portas dentro desse intervalo.

**Descobrindo o que está rodando na porta:**
```bash
nmap -sV alvo.com
```
Mostra a versão do serviço, não só se está aberto:
```
80/tcp open http Apache httpd 2.4.x
```

**Investigação agressiva:**
```bash
nmap -A alvo.com
```
Tenta coletar versões, sistema operacional, scripts de
enumeração e outras informações do alvo de uma vez.

## ss — o que a máquina está escutando por dentro

```bash
ss -tlnp
```

Diferente do nmap (que olha de fora), esse comando
roda dentro da máquina e mostra o que ela está
escutando:
```
Listen
0.0.0.0:22
0.0.0.0:80
127.0.0.1:3306
```

## nc — conversando manualmente com uma porta

Depois que o nmap acha uma porta aberta (ex: `80/tcp
open http`), pra conversar com ela manualmente:

```bash
nc alvo.com 80
```

Isso cria uma conexão TCP e permite enviar dados
manualmente. Dá pra mandar uma requisição HTTP na mão:

```
GET / HTTP/1.1
Host: alvo.com
```

E analisar a resposta que volta.

## ncat — versão mais moderna do netcat

Suporta SSL/TLS, proxies, autenticação e diferentes
tipos de conexão — recursos que o `nc` tradicional não
tem.

## telnet — acesso remoto sem criptografia

```bash
telnet alvo.com 80
```

Tem o mesmo propósito do SSH (acesso remoto), mas
transmite tudo sem criptografia — perigoso, porque
alguém pode observar o tráfego facilmente.

## socat — mais completo que o nc

Faz conexão com uma variedade maior de endpoints:
```
Aplicação A → TCP → Socat → SSL → Servidor B
```

## openssl s_client — conectando em portas TLS

Se uma porta como 443 está aberta mas esperando TLS,
um `nc` simples é recusado. Pra estabelecer o handshake
criptográfico:

```bash
openssl s_client -connect alvo.com:443
```

O `s_client` atua como cliente TLS, observando:
```
Certificado
Handshake
Versão TLS
Informações criptográficas
Resposta do servidor
```

**Fluxo típico de investigação:**
```
nmap → descubro que 443 está aberta
openssl s_client → descubro como o TLS está configurado
HTTP → depois posso conversar com o serviço protegido
```

## ssh — acesso remoto com criptografia

Diferente do telnet, o SSH fornece acesso remoto com
criptografia e autenticação:

```bash
ssh usuario@alvo.com -p 2222
```

Com chave privada:
```bash
ssh -i chave_privada usuario@alvo.com
```

**Executando comando direto, sem shell interativo:**
```bash
ssh usuario@alvo.com "comando"
```

Isso executa o comando assim que loga — mesmo que a
sessão seja configurada pra desconectar logo após a
autenticação (como aconteceu em alguns levels do
Bandit), o comando roda e retorna resultado antes de
desconectar. Exemplo:
```bash
ssh usuario@alvo.com cat readme
```

## diff — comparando dois arquivos

```bash
diff config.old config.new
```

Mostra o que mudou entre dois arquivos.

## comm — comparando linhas entre conjuntos

Princípio parecido com o `diff`, mas em vez de comparar
o conteúdo linha a linha, o `comm` descobre quais
linhas pertencem exclusivamente a cada arquivo e quais
são comuns aos dois.
