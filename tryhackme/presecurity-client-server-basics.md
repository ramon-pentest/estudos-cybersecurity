# TryHackMe — Pre-Security: How Websites Work

## Modelo Client-Server (analogia da pizza)

| Elemento real | Elemento computacional |
|---------------|--------------------------|
| Alice (quem quer a pizza) | Client — quem inicia o pedido/requisição |
| Bob (leva o pedido até Luigi's) | Protocol — define como a comunicação acontece |
| Luigi's Pizza | Server — quem responde ao pedido |
| O pedido ("pizza de pepperoni") | Request |
| A pizza entregue (ou erro "não tem pepperoni") | Response |
| Porta específica pra cada serviço (retirada/salão/delivery) | Port |
| GPS traduzindo nome → localização | DNS — traduz nome do site → endereço IP |

**Regra chave:** o client é sempre quem inicia a
requisição. O server nunca "liga" primeiro.

## Protocol — o que ele define

Um protocolo é o "idioma e regras" combinados entre
client e server:

```
Quais comandos existem (ex: GET)
Como a requisição é estruturada (ordem, formato)
Qual sintaxe é usada
Qual resposta corresponde a qual tipo de pedido
Qual resposta dar quando o pedido é inválido/malformado
```

## Port

Identifica qual serviço específico rodando num server o
client quer acessar. Um mesmo server pode rodar múltiplos
serviços simultaneamente, cada um numa porta diferente
(analogia: porta A = retirada, porta B = salão, porta C
= delivery — mesmo restaurante, entradas diferentes).

## DNS (Domain Name Service)

Traduz o nome de um recurso (nome de um site) pra sua
localização real — o endereço IP. Funciona como GPS:
você sabe o nome do destino, o DNS resolve isso pra
coordenadas que o sistema consegue de fato usar pra
chegar lá.

## HTTP(S) na prática

**HTTP é stateless** — cada requisição é processada de
forma independente, o server não guarda memória de
requisições anteriores por padrão.

Aplicações modernas simulam "memória" (statefulness)
na camada de aplicação usando sessão/cookie/token — é
por isso que você continua logado entre páginas, mesmo
o protocolo em si não lembrando de nada sozinho.

Sem esse mecanismo, seria necessário autenticar de novo
a cada requisição nova.

## Os 9 métodos HTTP (definidos nas RFCs)

```
GET, POST, PUT, DELETE, PATCH, HEAD, OPTIONS, CONNECT, TRACE
```

### GET em detalhe

Usado pra retrieval (buscar/recuperar) um recurso do
server. Ex: `GET https://tryhackme.com/index.php` busca
a homepage.

O browser monta essa requisição automaticamente nos
bastidores quando você digita uma URL — você não escreve
o GET manualmente.

## Campos observados numa requisição (via DevTools → Network)

```
Scheme   → protocolo usado (HTTP ou HTTPS)
Host     → nome do host de onde o recurso é pedido
Filename → qual arquivo foi requisitado (/ geralmente = index.html)
Address  → IP onde o site está hospedado
           (127.0.0.1 = hospedado na própria máquina local)
Status   → se a requisição teve sucesso (200 OK = sucesso)
```

## Estrutura da resposta

Toda resposta tem duas partes:

```
Response header → metadados sobre a resposta
Response body   → o conteúdo em si (ex: o HTML da página)
```
