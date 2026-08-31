# Redes — Módulo 15: Servidores, DNS, HTTP e FTP

## O que é um servidor

Um servidor é um host que executa software capaz de
fornecer informações ou serviços para outros hosts.

Meu PC → solicita algo → Servidor
Meu PC ← recebe página ← Servidor


O PC é o **cliente** porque está solicitando.
O outro computador é o **servidor** porque está
oferecendo o serviço.

Um servidor pode ser cliente e servidor ao mesmo
tempo, dependendo da comunicação. Além disso, um
único servidor pode executar vários serviços
simultaneamente (e-mail, web, arquivos, etc.).

## O que acontece quando acesso um site

**Etapa 1 — DNS:**
O navegador tem o nome `www.learnip.com`, mas a rede
precisa trabalhar com endereços IP.

Cliente → "Qual é o IP de www.learnip.com?" → DNS
DNS → "172.16.10.50" → Cliente


O cliente agora sabe que `www.learnip.com` é o IP
`172.16.10.50`. Isso é necessário porque os dispositivos
de rede usam endereços IP para encaminhar pacotes,
não nomes de domínio.

**Etapa 2 — TCP:**
O cliente sabe o IP do servidor. Para estabelecer a
comunicação precisa do TCP na porta 80:

Cliente: 192.168.10.15:5507
Servidor: 172.16.10.50:80


Isso é um socket. Quando o servidor responde, olha
o IP e a porta de destino e sabe que deve entregar
ao serviço web que está escutando naquela porta.

**Visão completa:**

Você digita: www.cisco.com
↓
DNS → "Qual é o IP?"
↓
endereço IP
↓
conexão TCP → porta 80
↓
HTTP request
↓
SERVIDOR WEB
↓
HTML (código da página)
↓
NAVEGADOR interpreta o HTML
↓
PÁGINA WEB visível


## Hierarquia URI, URL e URN

**URI (Uniform Resource Identifier)**
Sequência de caracteres usada para identificar um
recurso — é o conceito mais amplo.

**URL (Uniform Resource Locator)**
Identifica onde o recurso está localizado na rede:

https://www.example.com/author/book.html#page155

https:// → esquema/protocolo
www.example.com → host
/author/book.html → caminho/recurso
#page155 → fragmento (parte específica do recurso)


**URN (Uniform Resource Name)**
Identifica o recurso dentro de um namespace, sem
depender de uma localização ou protocolo da mesma
forma que uma URL.

## HTTP e HTML — não são a mesma coisa

**HTTP (Hypertext Transfer Protocol)**
É o protocolo de comunicação — define as regras
usadas para o cliente e o servidor trocarem
informações. Determina como cliente e servidor
conversam.

**HTML (Hypertext Markup Language)**
É a linguagem usada para representar o conteúdo
e a estrutura da página web. É o código que o
navegador interpreta para construir a página visual.

```html
<h1>Olá</h1>
<p>Bem-vindo ao site.</p>
```

O navegador interpreta esse código e apresenta
visualmente para o usuário.

HTTP → como a informação é transferida
HTML → a informação/código que descreve a página


O servidor não envia a página visual — envia o
código. O navegador recebe esse código e o interpreta.
Quando abrimos o código-fonte de uma página, estamos
vendo o HTML que foi baixado/entregue ao cliente.

## HTTP vs HTTPS

O HTTP não é seguro — as informações transmitidas
podem ser interceptadas porque o HTTP tradicional
não fornece proteção criptográfica.

HTTP → Porta 80 → não criptografado
HTTPS → Porta 443 → criptografado


## FTP — File Transfer Protocol

Permite que um cliente se conecte a um servidor para
transferir e gerenciar arquivos:

- Download de arquivos
- Upload de arquivos
- Excluir arquivos
- Renomear arquivos

Cliente FTP (ex: FileZilla)
↓ FTP
Servidor FTP


### O FTP usa duas conexões separadas

Porta 21 → Controle (comandos: deletar, renomear, pedir arquivo)
Porta 20 → Dados (o arquivo em si: relatorio.pdf, imagem.jpg)


O motivo de existir duas conexões é separar os
comandos que controlam a sessão dos dados que estão
sendo transferidos.

Exemplo de download do `relatorio.pdf`:

Cliente → TCP/21 → Servidor: "Quero baixar relatorio.pdf"
Cliente ← TCP/20 ← Servidor: [relatorio.pdf]


## Tabela de serviços e protocolos

| Serviço | Protocolo | Para que serve |
|---------|-----------|----------------|
| DNS | DNS | Converte nomes em endereços IP |
| Acesso remoto | SSH | Acesso remoto seguro a servidores |
| Envio de e-mail | SMTP | Envia e-mails |
| Recebimento de e-mail | POP3/IMAP | Recupera e-mails do servidor |
| Configuração de rede | DHCP | Configura IP automaticamente |
| Web | HTTP | Solicita e transfere páginas web |
| Transferência de arquivos | FTP | Transfere arquivos entre sistemas |
