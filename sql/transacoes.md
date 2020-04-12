# Transações

## Definição
Conceito fundamental de todos os sistemas de bancos de dados.\
Conceito de múltiplas etapas/códigos reunidos em apenas 1 transação, onde o resultado precisa ser **tudo ou nada**.

## Exemplo:
```sql
UPDATE conta SET valor = valor - 100.00
  WHERE nome = 'Alice';

UPDATE conta SET valor = valor + 100.00
  WHERE nome = 'Bob';
```

```sql
BEGIN;

  UPDATE conta SET valor = valor - 100.00
    WHERE nome = 'Alice';

  UPDATE conta SET valor = valor + 100.00
    WHERE nome = 'Bob';

COMMIT;
```

```sql
BEGIN;

  UPDATE conta SET valor = valor - 100.00
    WHERE nome = 'Alice';

SAVEPOINT my_savepoint;

  UPDATE conta SET valor = valor + 100.00
    WHERE nome = 'Bob';
  -- oops ... não é para o Bob, é para o Wally!!!

ROLLBACK TO my_savepoint;

  UPDATE conta SET valor = valor + 100.00
      WHERE nome = 'Wally';

COMMIT;
```