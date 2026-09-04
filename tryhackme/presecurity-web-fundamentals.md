# TryHackMe — Pre-Security: Web Fundamentals

## DIRB — encontrando páginas escondidas

O `dirb` é uma ferramenta que tenta descobrir recursos
web que não estão expostos nos links da página — como
páginas de admin, diretórios internos e arquivos ocultos.

Ele faz isso usando uma wordlist, testando vários
caminhos possíveis no servidor e analisando as respostas.

```
dirb http://fakebank.thm
```

Exemplo de resultado:
```
+ http://fakebank.thm/bank-transfer  (CODE:200|SIZE:4663)
+ http://fakebank.thm/images         (CODE:301|SIZE:179)
```

---

## Códigos HTTP importantes

**200 — OK**
A requisição foi processada com sucesso. Existe uma
resposta válida para aquele recurso — vale investigar.

**301 — Moved Permanently**
O recurso existe mas está em outro lugar. No exemplo
acima, `/images` redirecionou para `/images/` —
não é necessariamente uma página interessante, mas
confirma que o diretório existe.

---

## Método GET

O GET é o método HTTP usado para pedir um recurso
ao servidor:

```
GET /login HTTP/1.1
Host: fakebank.thm
```

Quando o dirb varre o servidor, ele está basicamente
fazendo GET requests para cada caminho da wordlist
e vendo o que responde.

---

## Quatro conceitos fundamentais de segurança web

```
Enumeration      → Existe alguma coisa aqui?
Authentication   → Quem é você?
Authorization    → Você tem permissão para fazer isso?
Functionality    → O que essa aplicação permite fazer?
```
