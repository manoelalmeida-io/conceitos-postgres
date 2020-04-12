# Views

## Definição
Views são visões\
São "camadas" para as tabelas\
São "alias" para uma ou mais queries\
Aceitam comandos de **SELECT, INSERT, UPDATE, DELETE**

```sql
CREATE [ OR REPLACE ] [ TEMP | TEMPORARY] [ RECURSIVE ] VIEW name [ ( column_name [,...] ) ]
  [ WITH ( view_option_name [= view_option_value] [, ...]) ]
  AS query
  [ WITH [ CASCADED | LOCAL ] CHECK OPTION ]
```

## INSERT, UPDATE, DELETE

```sql
CREATE OR REPLACE VIEW vw_bancos AS (
  SELECT numero, nome, ativo
  FROM banco
);
```

```sql
SELECT numero, nome, ativo
FROM vw_bancos;
```

* Funcionam apenas para VIEWs com apenas uma tabela

```sql
INSERT INTO vw_bancos (numero, nome, ativo) VALUES (100, 'Banco CEM', true);

UPDATE vw_bancos SET nome = 'Banco 100' WHERE numero = 100;

DELETE FROM vw_bancos WHERE numero = 100;
```

## TEMPORARY
```sql
CREATE OR REPLACE TEMPORARY VIEW vw_bancos AS (
  SELECT numero, nome, ativo
  FROM banco
);

SELECT numero, nome, ativo FROM vw_bancos;
```

VIEW presente apenas na sessão do usuário.\
Se você se desconectar e conectar novamente, a VIEW não estará disponível.

## RECURSIVE
```sql
CREATE OR REPLACE RECURSIVE VIEW (nome_da_view) (campos_da_view) AS (
  SELECT base
  UNION ALL
  SELECT campos
  FROM tabela_base
  JOIN (nome_da_view)
);
```

* Obrigatório a existência dos campos da VIEW
* UNION ALL

```sql
CREATE TABLE IF NOT EXISTS funcionarios (
  id SERIAL NOT NULL,
  nome VARCHAR(50),
  gerente INTEGER,
  PRIMARY KEY (id),
  FOREIGN KEY (gerente) REFERENCES funcionario (id)
)
```
```sql
INSERT INTO funcionarios (nome, gerente) VALUES ('Ancelmo', null);
INSERT INTO funcionarios (nome, gerente) VALUES ('Beatriz', 1);
INSERT INTO funcionarios (nome, gerente) VALUES ('Magno', 1);
INSERT INTO funcionarios (nome, gerente) VALUES ('Cremilda', 2);
INSERT INTO funcionarios (nome, gerente) VALUES ('Wagner', 4);
```

```sql
CREATE OR REPLACE RECURSIVE VIEW vw_funcionarios(id, gerente, funcionario) AS (
  SELECT id, gerente, nome
  FROM funcionarios
  WHERE gerente IS NULL
  UNION ALL
  SELECT funcionarios.id, funcionarios.gerente, fundionarios.nome
  FROM funcionarios
  JOIN vw_funcionarios ON vw_funcionarios.id = funcionario.gerente
);

SELECT id, gerente, funcionario FROM vw_funcionarios;
```

```sql
CREATE OR REPLACE RECURSIVE VIEW vw_funcionarios(id, gerente, funcionario) AS (
  SELECT id, CAST('' AS VARCHAR(50)) AS gerente, nome
  FROM funcionarios
  WHERE gerente IS NULL
  UNION ALL
  SELECT funcionarios.id, gerentes.nome, funcionarios.nome
  FROM funcionarios
  JOIN vw_funcionarios ON vw_funcionarios.id = funcionarios.gerente
  JOIN funcionarios gerentes ON gerentes.id = vw_funcionarios.id 
);

SELECT id, gerente, funcionario FROM vw_funcionarios;
```

## WITH OPTIONS
```sql
CREATE OR REPLACE VIEW vw_banco AS (
  SELECT numero, nome, ativo
  FROM banco
);

INSERT INTO vw_banco (numero, nome, ativo) VALUES (100, 'Banco CEM', false); -- OK
```

```sql
CREATE OR REPLACE VIEW vw_banco AS (
  SELECT numero, nome, ativo
  FROM banco
  WHERE ativo IS TRUE
) WITH LOCAL CHECK OPTION;

INSERT INTO vw_banco (numero, nome, ativo) VALUES (100, 'Banco CEM', false); -- ERRO
```