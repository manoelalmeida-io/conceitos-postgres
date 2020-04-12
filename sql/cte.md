# CTE (Commom Table Expression)

## Definição
Forma auxiliar de organizar "statements", ou seja, blocos de códigos, para consultas muito grandes, gerando tabelas temporárias e criando relacionamentos entre elas.

Dentro dos statements podem ter SELECTs, INSERTs, UPDATEs ou DELETEs.

```sql
WITH [nome1] AS (
  SELECT (campos,)
  FROM tabela_A
  [WHERE]
), [nome2] AS (
  SELECT (campos,)
  FROM tabela_B
  [WHERE]
)
SELECT [nome1].(campo,), [nome2].(campos,)
FROM [nome1]
JOIN [nome2]
```