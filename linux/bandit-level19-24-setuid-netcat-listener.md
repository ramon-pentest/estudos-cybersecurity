# Bandit — Level 20: Setuid e Netcat como Listener

## bandit20-do — comando setuid

`./bandit20-do` é um bit setuid — basicamente um
comando configurado pelo root onde, ao executar aquele
comando específico, eu passo a "ser" um usuário
específico e posso ler as informações dele, já que
tecnicamente sou ele durante a execução. Mas eu não
continuo sendo ele depois que o comando termina.

```bash
./bandit20-do cat /etc/bandit_pass/bandit20
```

Durante esse comando eu sou o bandit20 e leio o que
está no arquivo dele — mas assim que o comando termina
e retorna a informação, volto a ser o bandit19.

## nc -lvp — netcat como servidor (listener)

Esse uso do netcat tem flags diferentes do que já
tinha visto antes:

```
-l → listen (escutar). Faz o oposto do uso normal do
     netcat — ao invés de SE CONECTAR em algo, ele
     VIRA o servidor esperando alguém se conectar
-v → verbose (detalhado). Faz o nc imprimir mensagens
     extras tipo "Conexão recebida de tal IP", em vez
     de ficar em silêncio — útil pra confirmar
     visualmente quando alguém conecta
-p → port (porta). Especifica em qual porta o servidor
     vai escutar
```

Juntando tudo:
```bash
nc -lvp 12345
```
"Netcat, escute na porta 12345 e me avise com detalhes
quando algo conectar."

## Combinando com echo e pipe

```bash
echo SENHA | nc -lvp 12345
```

O `echo` gera o texto e manda pelo pipe como entrada.
Assim que alguém conecta na porta 12345, o nc já tem o
texto pronto pra transmitir de volta pra quem conectou.

## & — rodando em segundo plano

O `&` permite que o shell rode um comando em segundo
plano. Sem ele, o shell espera aquele comando terminar
antes de aceitar o próximo — com ele, dá pra executar
outros comandos em paralelo sem esperar.

## Verificando se a porta está livre

```bash
ss -tln | grep :12345
```

```
ss -tln:
  -t → mostra só conexões TCP (UDP fica de fora)
  -l → modo listening (esperando conexão)
  -n → numeric — mostra o número da porta direto,
       em vez de tentar traduzir pro nome do serviço
       conhecido (mostra "80" em vez de "http")

grep :12345 → filtra a saída do ss pra mostrar só a
              linha que contém essa porta específica
              (formato tipo "0.0.0.0:12345"), evitando
              precisar olhar a lista inteira manualmente
```

O contexto de usar `ss` + `grep` junto é confirmar que
ninguém mais está usando aquela porta no servidor antes
de tentar abrir o listener nela.
