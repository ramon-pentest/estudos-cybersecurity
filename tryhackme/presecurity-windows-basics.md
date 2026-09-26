# TryHackMe — Pre-Security: Windows Basics

## Equivalências entre Linux e CMD

| Linux | CMD | Função |
|-------|-----|--------|
| `pwd` | `cd` (sem argumento) | Mostra diretório atual |
| `ls` | `dir` | Lista arquivos e pastas |
| `find` | `dir /s` | Procura arquivo em subpastas |
| `cat` | `type` | Mostra conteúdo de arquivo |

## Navegação

```
cd Documents  → entra na pasta Documents
cd ..         → volta pra pasta pai
```

## Listagem e itens ocultos

```
dir /a → inclui itens marcados como ocultos
```

**Hidden** significa que o item está escondido, não
necessariamente que é secreto — esse atributo não
protege nem criptografa o arquivo.

## Procurando um arquivo pelo nome

```
dir /s task_brief.txt
```

Procura no diretório atual e em todas as subpastas.
Caminho encontrado, por exemplo:
```
C:\Users\Administrator\Documents\task_brief.txt
```

No Windows as pastas ficam organizadas a partir de uma
unidade (`C:`), depois `Users`, nome do usuário, e
`Documents`.

## Lendo o conteúdo

```
type task_brief.txt
```

## Identificação de usuário e máquina

```
whoami   → identifica o usuário (existe também no Linux)
hostname → identifica o nome do computador
```

## Informações do sistema

```
systeminfo
```

Destaques importantes: `OS Name`, `OS Version`,
`System Type`. No Linux, `uname -a` cumpre função
parecida, mas os dois comandos não mostram exatamente
o mesmo conjunto de informações.

## Configuração de rede

```
ipconfig
```

Atenção a dois campos:
```
IPv4 Address     → identifica a interface na rede IP
Default Gateway  → próximo ponto pra onde a máquina
                    envia tráfego de outras redes
                    (geralmente o roteador)
```

## A ideia central da sala

Fazer perguntas à máquina: onde estou, o que existe
aqui, onde está determinado arquivo, quem está usando
o computador, que sistema está instalado, como está
conectado à rede. Cada sistema operacional tem seus
próprios comandos pra responder essas perguntas — mas
a lógica de investigação é a mesma.
