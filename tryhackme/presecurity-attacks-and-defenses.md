# TryHackMe — Pre-Security: Attacks and Defenses

## The CIA Triad

Além de definir as três propriedades (confidencialidade,
integridade e disponibilidade), a sala ensina a usar a tríade
pra analisar um incidente:

```
Credenciais expostas                   → confidencialidade afetada
Alguém altera uma transferência
bancária ou uma nota sem autorização   → problema de integridade
Serviço fora do ar, ou dados que
não dá pra acessar                     → problema de disponibilidade
```

Uma mesma situação pode afetar mais de uma propriedade. Na
hora de analisar um incidente as perguntas são: os dados
foram expostos? Foram alterados? O sistema ou serviço ficou
indisponível?

## Cryptography Basics

Criptografia protege dados enquanto estão guardados ou sendo
transmitidos. O **algoritmo** é o conjunto de regras usado pra
cifrar e decifrar, e a **chave** é o valor secreto que controla
o processo. A segurança tem que depender da proteção da
chave, não de esconder o algoritmo.

### Simétrica

A mesma chave cifra e decifra. É rápida e boa pra grandes
quantidades de dados, mas surge um problema: como entregar a
chave pro destinatário sem alguém interceptar?

**Cifra de César** — exemplo didático: cada letra é deslocada
um número fixo de posições. Com chave 3, `HELLO` vira `KHOOR`,
e pra decifrar as letras voltam três posições. Não serve pra
proteger dado real: um computador testa as poucas
possibilidades em segundos.

### Assimétrica

Usa um par de chaves: a **pública**, que pode ser
compartilhada, e a **privada**, que fica secreta. Uma mensagem
cifrada com a chave pública do Bob só pode ser decifrada pela
chave privada dele.

Isso resolve o problema de distribuir uma chave secreta antes
da comunicação. Mas ainda precisa confirmar que a chave pública
é mesmo do servidor esperado — quem faz essa associação são os
**certificados digitais**, assinados por autoridades
certificadoras confiáveis.

### Como o HTTPS junta as duas

```
Início da conexão → o navegador valida o certificado e usa
                    criptografia assimétrica pra estabelecer
                    um segredo compartilhado
Resto da sessão   → criptografia simétrica, que é mais rápida
                    pra proteger o volume de dados
```

## Become a Hacker

Segurança ofensiva é testar sistemas de forma **autorizada**
pra achar falhas antes de um invasor real. O teste tem escopo
definido: quais sistemas podem ser avaliados e quais ações são
permitidas.

**Red teaming** simula um adversário pra avaliar tanto os
sistemas quanto a capacidade da organização de detectar e
responder.

Fluxo da sala, numa loja fictícia:

1. **Enumeração** — procurar páginas que não aparecem na
   navegação normal. Dá pra testar URLs na mão, ou usar o
   **Gobuster**, que automatiza a busca com uma wordlist e
   analisa os códigos de resposta do servidor (mesma ideia do
   dirb que usei antes).
2. **Autenticação** — encontrar uma página de login não
   significa que a aplicação foi comprometida. O risco cresce
   quando a descoberta se combina com outra fraqueza, como
   senha previsível. A sala testa isso na mão e com o
   **Hydra**, que automatiza tentativas a partir de uma lista
   de senhas.
3. **Encadeamento** — descobrir a página → testar a
   autenticação → ver o que uma conta acessível permite fazer.
   Senhas, páginas administrativas e dados de usuários abrem
   novas possibilidades.

Tudo isso aconteceu no laboratório, dentro de escopo
autorizado. Numa avaliação profissional é preciso permissão
explícita e respeitar os limites combinados.

## Become a Defender

Segurança defensiva é proteger sistemas e dados, perceber
atividade suspeita e limitar o impacto de incidentes. Pra
defender um ambiente, primeiro é preciso saber o que existe
nele: dispositivos de usuários, servidores, aplicações,
redes, firewalls, serviços externos.

A sala usa a analogia de uma cidade:
```
Casas e prédios                              → os sistemas
Câmeras e patrulhas                          → visibilidade
Tentativas repetidas de login, IPs incomuns  → sinais suspeitos
Firewall                                     → portão que controla o tráfego
```

**Etapas do trabalho defensivo:**
```
Prevenção           → reduzir a chance de um ataque funcionar
                      (atualizações, antivírus, regras de firewall)
Detecção            → identificar atividade suspeita (logs,
                      alertas, monitoramento)
Mitigação           → limitar os danos (bloquear tráfego,
                      isolar um sistema)
Análise             → examinar logs e evidências pra entender
                      o que aconteceu
Resposta e melhoria → recuperar os sistemas e reduzir a chance
                      de acontecer de novo
```

A defesa também precisa pensar na sequência do ataque: um
anexo malicioso compromete o computador de um funcionário →
credenciais roubadas dão acesso ao e-mail → esse acesso leva a
dados mais sensíveis. Cada etapa é uma chance de prevenir ou
detectar.

Nem todo sistema tem o mesmo risco: a prioridade é identificar
os mais importantes e o que aconteceria se fossem
comprometidos. As defesas precisam acompanhar as mudanças do
ambiente e dos métodos dos atacantes.
