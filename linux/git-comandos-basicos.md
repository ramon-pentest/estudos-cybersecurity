# Git — Comandos Básicos

## Branches

Branches são como "raízes" ou canais diferentes dentro
de um repositório. Geralmente existe um principal,
chamado `main` ou `master`, mas dá pra criar um canal
separado pra testar coisas sem afetar esse principal.

## Clonando e explorando o histórico

```bash
git clone
```
Baixa todo um repositório pra máquina local.

```bash
git log
```
Mostra o histórico de commits — cada commit é um
"salvamento" de mudanças, com autor, data e mensagem.

```bash
git log --all
```
Inclui todos os commits de todos os branches, não só
do que está ativo no momento.

```bash
git show
```
Mostra o conteúdo detalhado de um commit específico,
identificado pelo hash — um hexadecimal de uns 35-40
caracteres, único pra cada commit.

## Listando e navegando entre branches

```bash
git branch -a
```
Lista todos os branches, incluindo os criados pra
teste — o `-a` mostra tudo, não só o principal.

```bash
git switch <nome-branch>
```
Troca os arquivos locais pra ver o que existe naquele
branch específico — dá pra descobrir, por exemplo, a
existência de um branch `dev` e o que foi mexido nele.

## Vendo tudo de uma vez

```bash
git reflog
```
Mostra o histórico de todas as ações feitas localmente
no repositório (checkouts, commits, etc), incluindo
coisas que não aparecem no `git log` normal.

```bash
git show --all
```
Mostra todas as informações de todas as referências,
branches e tags de uma vez — em vez de procurar
manualmente em cada branch um por um.

## Preparando e salvando mudanças

```bash
git add <arquivo>
```
Prepara um arquivo pra entrar no próximo commit — isso
é chamado de "staging", a área de preparação antes do
salvamento definitivo.

```bash
git add -f
```
Sobrepõe qualquer aviso do `.gitignore`, adicionando o
arquivo mesmo estando na lista de ignorados.

```bash
git commit -m "mensagem"
```
Salva as mudanças preparadas como um novo commit, com
uma mensagem descritiva explicando o que mudou.

## Enviando pro repositório remoto

```bash
git push origin master
```
Envia os commits locais pro repositório remoto.

```
origin → nome padrão que o Git dá ao repositório de
         onde foi clonado
master → branch de destino do push
```
