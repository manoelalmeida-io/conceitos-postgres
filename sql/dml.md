# DML - CRUD

## SELECT
```sql
SELECT (campos) FROM tabela [condições];
```

### EXEMPLO:
```sql
SELECT numero, nome FROM banco;
SELECT numero, nome FROM banco WHERE ativo IS TRUE;
SELECT nome FROM cliente WHERE email LIKE '%gmail.com';

SELECT numero FROM agencia
  WHERE banco_numero IN (SELECT numero FROM banco WHERE nome LIKE '%Bradesco%');
```

## SELECT - Condição (WHERE / AND / OR)

WHERE (coluna/condição):
* =
* \> / >=
* < / <=
* <> / !=
* LIKE
* ILIKE
* IN

Primeira condição sempre **WHERE.**\
Demais condições, **AND** ou **OR.**

## SELECT - Idepotência
```sql
SELECT (campos, ...)
FROM tabela1
WHERE EXISTS (
  SELECT (campo, ...)
  FROM tabela2
  WHERE campo1 = valor1
  [AND/OR campoN = valorN]
)
```
Não é uma boa prática.\
Melhor prática utilizar LEFT JOIN.

## INSERT
```sql
INSERT (campos da tabela,) VALUES (valores,);
INSERT (campos da tabela,) SELECT (valores,);
```

## INSERT - Idepotência
```sql
INSERT INTO agencia (banco_numero, numero, nome) VALUES (341, 'Centro da cidade');

INSERT INTO agencia (banco_numero, numero, nome)
SELECT 341, 1, 'Centro da cidade'
WHERE NOT EXISTS (SELECT banco_numero, numero, nome FROM agencia WHERE banco_numero = 341 AND numero = 1 AND nome = 'Centro da cidade');
```

### ON CONFLICT
```sql
INSERT INTO agencia (banco_numero, numero, nome) VALUES (341, 1, 'Centro da cidade') ON CONFLICT (banco_numero, numero) DO NOTHING;
```

## UPDATE
```sql
UPDATE (tabela) SET campo1 = novo_valor WHERE (condição);
```

## DELETE
```sql
DELETE FROM (tabela) WHERE (condição);
```