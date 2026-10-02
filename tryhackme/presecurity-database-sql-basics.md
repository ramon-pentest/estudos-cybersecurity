# TryHackMe — Pre-Security: Database SQL Basics

## Por que bancos de dados são úteis

A sala usa pedidos de um café como analogia. Num
caderno de papel, descobrir quantas vezes um pedido
específico apareceu pode exigir percorrer várias
páginas. Um banco de dados organiza os registros,
permitindo buscar e ordenar informações rapidamente.

## Tabelas

Os dados ficam organizados em tabelas:
```
Coluna → representa um tipo de informação (bebida, preço)
Linha  → um registro completo (um pedido do café)
```

**Duas tabelas usadas na sala:**
```
Orders → id, drink, price, time
Menu   → drink, price
```

## SQL — a linguagem de consulta

**SELECT e FROM:**
```sql
SELECT * FROM Orders;
```
`*` significa todas as colunas. `FROM` indica de qual
tabela buscar.

Pra mostrar só colunas específicas:
```sql
SELECT drink, price FROM Orders;
```

## WHERE — filtrando resultados

```sql
SELECT * FROM Orders WHERE drink = 'Coffee';
```

Mostra só os pedidos de café. Valores de texto ficam
entre aspas simples. Se não souber quais bebidas estão
cadastradas, dá pra consultar a tabela `Menu` primeiro.

## ORDER BY — organizando resultados

```sql
ORDER BY price         -- crescente (padrão)
ORDER BY price DESC    -- decrescente
```

## Combinando tudo

```sql
SELECT * FROM Orders WHERE drink = 'Coffee' ORDER BY price DESC;
```

Seleciona os pedidos de café e organiza do mais caro
pro mais barato.

## Sobre segurança

As consultas `SELECT` dessa sala só leem e mostram
dados — não alteram nada. A pergunta que a sala deixa
no final aponta pra segurança e integridade: se alguém
sem autorização conseguisse alterar ou apagar
registros, o histórico do café deixaria de ser
confiável. Isso é exatamente o tipo de cenário que SQL
Injection explora — mas de forma maliciosa, inserindo
comandos não autorizados numa consulta que deveria só
ler dados.
