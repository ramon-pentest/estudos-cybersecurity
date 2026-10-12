# TryHackMe — Pre-Security: How The Web Works

## DNS in Detail

DNS (Domain Name System) traduz nomes fáceis de lembrar, como
`tryhackme.com`, pros endereços IP usados na comunicação de
rede.

### Partes de um domínio

```
admin.tryhackme.com

.com        → TLD
tryhackme   → domínio de segundo nível
admin       → subdomínio
```

Limites: cada parte (como `admin`) tem no máximo 63
caracteres, e o nome completo no máximo 253. Pode ter letras,
números e hífen, mas o hífen não pode ficar no começo nem no
fim de uma parte.

TLDs genéricos: `.com`, `.org`, `.edu`. TLDs de código de
país: `.ca`, `.uk`.

### Tipos de registro

```
A      → aponta o nome pra um IPv4
AAAA   → aponta pra um IPv6
CNAME  → aponta pra outro nome de domínio, que depois também
         precisa ser resolvido
MX     → servidores que recebem e-mail do domínio, com
         prioridade pra definir a ordem de tentativa
TXT    → texto pra várias finalidades, como verificar o
         domínio ou publicar informações de autenticação
         de e-mail
```

### Como uma consulta é resolvida

```
1. Cache local do computador
2. Servidor DNS recursivo (geralmente do ISP)
3. Servidores raiz → indicam o servidor do TLD
4. Servidor do TLD → encaminha pro autoritativo do domínio
5. Servidor autoritativo → guarda os registros oficiais e
   devolve a resposta
6. A resposta volta pelo recursivo até o computador
```

O **TTL** do registro define por quanto tempo a resposta pode
ficar em cache antes de ser consultada de novo.

## HTTP in Detail

HTTP é o protocolo que o navegador e o servidor usam pra
trocar páginas e outros recursos. HTTPS é o HTTP protegido por
criptografia — além de esconder o conteúdo da comunicação,
ajuda o navegador a confirmar a identidade do servidor.

### URL

Informa como e onde buscar um recurso. Pode ter esquema,
usuário, host, porta, caminho, parâmetros e fragmento.

```
http://site:80/blog?id=1#comments

host       → site
porta      → 80
caminho    → /blog
parâmetro  → id=1
fragmento  → #comments (aponta pra uma parte da página)
```

### Requisição e resposta

A requisição tem uma linha inicial, cabeçalhos e, quando
precisa, um corpo. A resposta tem um status, cabeçalhos e,
muitas vezes, o conteúdo pedido.

```
GET / HTTP/1.1     → o cliente pede a página inicial usando HTTP/1.1
Host: ...          → qual domínio está sendo solicitado

HTTP/1.1 200 OK    → sucesso
Content-Type       → formato do conteúdo
Content-Length     → tamanho do conteúdo
```

### Métodos

```
GET     → busca um recurso
POST    → envia dados, muitas vezes pra criar um registro ou
          mandar um formulário
PUT     → envia dados pra atualizar um recurso
DELETE  → pede a remoção de um recurso
```

### Códigos de status

```
100–199 → informam o andamento
200–299 → sucesso
300–399 → redirecionamento
400–499 → problema na requisição ou na autorização do cliente
500–599 → erro no servidor
```

```
200 → sucesso                       400 → requisição inválida
201 → recurso criado                401 → falta autenticação
301 → redirecionamento permanente   403 → acesso negado
302 → redirecionamento temporário   404 → recurso inexistente
                                    500 → erro interno
                                    503 → indisponível
```

### Cabeçalhos e cookies

```
Host             → site solicitado
User-Agent       → identifica o navegador
Content-Length   → tamanho dos dados enviados
Accept-Encoding  → formatos de compressão aceitos
Content-Type     → formato do corpo
```

O servidor pode usar `Set-Cookie` pra pedir que o navegador
guarde um cookie. Nas próximas requisições o navegador manda
esse valor no cabeçalho `Cookie`. Como o HTTP não guarda
memória das requisições anteriores sozinho, o cookie ajuda a
manter a sessão ou preferências. Muitas vezes ele guarda um
token, não a senha em si.

## How Websites Work

Uma aplicação web tem uma parte que roda no navegador (o
**frontend**) e outra que é processada no servidor (o
**backend**). O navegador pede os recursos, o servidor
processa e devolve os dados pro navegador montar a página.

```
HTML        → estrutura e conteúdo da página
CSS         → aparência
JavaScript  → interatividade, e pode alterar a página
              enquanto ela está aberta
```

O código do backend não é enviado pro navegador — o servidor
processa e devolve só o resultado. Já o HTML, CSS e JavaScript
que chegam ao navegador podem ser examinados por qualquer
usuário.

**Sensitive Data Exposure** — acontece quando informação que
devia ficar privada aparece no código-fonte enviado ao
navegador: credenciais, links escondidos, outros dados. Por
isso, numa análise autorizada, olhar o código-fonte pode
revelar coisas que a interface não mostra.

**HTML Injection** — acontece quando a aplicação mostra uma
entrada do usuário sem filtrar direito. Se o conteúdo for
interpretado como HTML, a pessoa consegue mudar a aparência ou
o comportamento da página. A entrada precisa ser tratada antes
de entrar no conteúdo exibido.

## Putting It All Together

Quando uma página é pedida, o computador precisa descobrir o
IP do servidor (o DNS resolve o nome do site). Depois o
navegador conversa com o servidor por HTTP ou HTTPS e recebe
HTML, JavaScript, CSS e imagens, que ele interpreta pra exibir
a página. Algumas partes podem depender de serviços extras:

```
Load balancer  → recebe as requisições e distribui entre vários
                 servidores, alternando (round-robin) ou mandando
                 pros menos ocupados. Também faz verificações de
                 saúde e para de mandar tráfego pra um servidor
                 que não responde direito

CDN            → distribui arquivos estáticos (imagens, CSS,
                 JavaScript) por servidores em vários lugares,
                 então o usuário recebe de um servidor mais
                 próximo e a página carrega mais rápido

Banco de dados → guarda as informações que o site precisa
                 consultar ou atualizar

WAF            → fica entre as requisições e o servidor,
                 inspecionando o tráfego e bloqueando padrões
                 considerados maliciosos. Também pode limitar
                 a quantidade de requisições recebidas
```
