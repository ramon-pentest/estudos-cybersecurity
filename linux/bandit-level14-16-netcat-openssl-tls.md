# Bandit — Level 14 ao 16: Netcat, OpenSSL e TLS Handshake

## Level 14 — nc (netcat)

```bash
nc localhost 30000
```

O `nc` é diferente do SSH — ele permite estabelecer
conexões TCP e UDP e enviar/receber dados diretamente.
O SSH tenta fazer login numa conta; o `nc` já permite
conversar diretamente com um serviço de rede, sem
autenticação de usuário.

## echo

Exibe texto, strings ou o valor de variáveis na saída
padrão:

```bash
echo "senha para acesso do localhost" | nc localhost 30000
```

Essa senha já seria enviada automaticamente pro
localhost assim que a conexão fosse estabelecida.

## Level 15/16 — printf, openssl e s_client

```bash
printf '%s\n' 'SENHA_ATUAL' | openssl s_client -connect localhost:30001
```

- **printf** + `'%s\n'` + texto → imprime o texto seguido de uma quebra de linha
- **openssl** → conjunto de ferramentas relacionadas a criptografia e protocolos seguros
- **s_client** → cliente capaz de estabelecer conexões TLS/SSL pra testes e diagnóstico
- **-connect** → indica endereço e porta de destino (ex: `-connect localhost:31790`)
- **`|` (pipe)** → envia a saída do comando à esquerda como entrada do comando à direita
- **-quiet** → suprime informações de certificado/handshake, mostrando só os dados trocados após a conexão

## TLS Handshake

Antes de transmitir dados normais, cliente e servidor
negociam os parâmetros da conexão segura — esse processo
é o **handshake**:

```
Cliente                              Servidor
   │──── ClientHello ─────────────────>│
   │<─── parâmetros/certificado ───────│
   │──── negociação de chaves ─────────>│
   │<──── conexão estabelecida ────────│
   │──── dados protegidos ─────────────>│
```

Não é preciso executar manualmente cada etapa — o
`openssl s_client` faz essa negociação por si só.
