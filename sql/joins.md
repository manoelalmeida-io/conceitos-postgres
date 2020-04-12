# JOINs

## JOIN (INNER)
```sql
SELECT tabela_1.campos, tabela_2.campos
FROM tabela_1
JOIN tabela_2
  ON tabela_1.campo = tabela_2.campo
```

### Resultado:
| ID | NOME |
|---|---|
| 1 | Genivaldo |
| 2 | Emengarda |
| 3 | Hercules |

| ID | TBL1_ID | VALOR |
|---|---|---|
| 1 | 1 | R$ 10,00 |
| 2 | 1 | R$ 15,00 |
| 3 | 3 | R$ 50,00 |

| TBL_1 | TBL_2 |
|---|---|
| Genivaldo | R$ 10,00 |
| Genivaldo | R$ 15,00 |
| Hercules | R$ 50,00 |

## LEFT JOIN(OUTER)
```sql
SELECT tabela_1.campos, tabela_2.campos
FROM tabela_1
LEFT JOIN tabela_2
  ON tabela_1.campo = tabela_2.campo
```

### Resultado:
| ID | NOME |
|---|---|
| 1 | Genivaldo |
| 2 | Emengarda |
| 3 | Hercules |

| ID | TBL1_ID | VALOR |
|---|---|---|
| 1 | 1 | R$ 10,00 |
| 2 | 1 | R$ 15,00 |
| 3 | 3 | R$ 50,00 |

| TBL_1 | TBL_2 |
|---|---|
| Genivaldo | R$ 10,00 |
| Genivaldo | R$ 15,00 |
| Emengarda |---|
| Hercules | R$ 50,00 |

## RIGHT JOIN(OUTER)
```sql
SELECT tabela_1.campos, tabela_2.campos
FROM tabela_1
RIGHT JOIN tabela_2
  ON tabela_1.campo = tabela_2.campo
```
### Resultado:

| ID | PRODUTO |
|---|---|
| 1 | Camiseta Polo |
| 2 | Calça Jeans |
| 3 | Saia Longa |

| ID | TAMANHO |
|---|---|
| 1 | P |
| 2 | M |
| 3 | G |

| TBL_1 | TBL_2 |
|---|---|
| 1 | 2 |
| 1 | 3 |
| 2 | 2 |

| TBL_1 | TBL_2 |
|---|---|
| Camiseta Polo | M |
| Camiseta Poli | G |
| Calça Jeans | M |
| --- | P |

## FULL JOIN
```sql
SELECT tabela_1.campos, tabela_2.campos
FROM tabela_1
FULL JOIN tabela_2
  ON tabela_1.campo = tabela_2.campo
```

### Resultado:

| ID | PRODUTO |
|---|---|
| 1 | Camiseta Polo |
| 2 | Calça Jeans |
| 3 | Saia Longa |

| ID | TAMANHO |
|---|---|
| 1 | P |
| 2 | M |
| 3 | G |

| TBL_1 | TBL_2 |
|---|---|
| 1 | 2 |
| 1 | 3 |
| 2 | 2 |

| TBL_1 | TBL_2 |
|---|---|
| Camiseta Polo | M |
| Camiseta Poli | G |
| Calça Jeans | M |
| Saia Longa | --- |
| --- | P |

## CROSS JOIN
Todos os dados de uma tabela serão cruzados com todos os dados da tabela referenciada no CROSS JOIN criando uma matriz.

```sql
SELECT tabela_1.campos, tabela_2.campos
FROM tabela_1
CROSS JOIN tabela_2
```

### Resultado:

| ID | NOME |
|---|---|
| 1 | José Colméia |
| 2 | Airton Senna |

| ID | VALOR |
|---|---|
| 1 | R$ 10,00 |
| 2 | R$ 15,00 |
| 3 | R$ 25,00 |

| TBL1 = ID | TBL1 = NOME | TBL2 = ID | TBL2 = VALOR |
|---|---|---|---|
| 1 | José Colméia | 1 | R$ 10,00 |
| 1 | José Colméia | 2 | R$ 15,00 |
| 1 | José Colméia | 3 | R$ 25,00 |
| 2 | Airton Senna | 1 | R$ 10,00 |
| 2 | Airton Senna | 2 | R$ 15,00 |
| 2 | Airton Senna | 3 | R$ 25,00 |