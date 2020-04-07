# DML e DDL

## DML
Data Manipulation Language\
Linguagem de manipulação de dados
INSERT, UPDATE, DELETE, **SELECT**\
\* O select, alguns consideram como DML, outros como DQL, que significa data query language, ou linguagem de consulta de dados.

## DDL
Data Definition Language\
Linguagem de definição de dados\
CREATE, ALTER, DROP

### CREATE / ALTER / DROP
```sql
CREATE [objeto] [nome do objeto] [opções];
ALTER [objeto] [nome do objeto] [opções];
DROP [objeto] [nome do objeto] [opções];
```

```sql
CREATE DATABASE dadosbancarios;
ALTER DATABASE dadosbancarios OWNER TO diretoria;
DROP DATABASE dadosbancarios;
```

```sql
CREATE SCHEMA IF NOT EXISTS bancos;
ALTER SCHEMA bancos OWNER TO diretoria;
DROP SCHEMA IF EXISTS bancos;
```

### CREATE / ALTER / DROP
```sql
CREATE TABLE [IF NOT EXISTS] [nome da tabela] (
  [nome do campo] [tipo] [regras] [opções],
  [nome do campo] [tipo] [regras] [opções],
  [nome do campo] [tipo] [regras] [opções]
);
```

```sql
ALTER TABLE [nome da tabela] [opcoes];
```

```sql
DROP TABLE [nome da tabela];
```

#### Exemplo:

```sql
CREATE TABLE IF NOT EXISTS banco (
  codigo INTEGER PRIMARY KEY,
  nome VARCHAR(50) NOT NULL,
  data_criacao TIMESTAMP NOT NULL DEFAULT NOW()
);
```

```sql
CREATE TABLE IF NOT EXISTS banco (
  codigo INTEGER,
  nome VARCHAR(50) NOT NULL,
  data_criacao TIMESTAMP NOT NULL DEFAULT NOW(),
  PRIMARY KEY (codigo)
);
```

```sql
ALTER TABLE banco ADD COLUMN tem_poupanca BOOLEAN;
```

```sql
DROP TABLE IF EXISTS banco;
```

### INSERT
```sql
INSERT INTO banco (codigo, nome, data_criacao) VALUES (100, 'Banco do Brasil', now());
```

```sql
INSERT INTO banco (codigo, nome, data_criacao) SELECT 100, 'Banco do Brasil', now();
```

### UPDATE
```sql
UPDATE [nome da tarefa] SET 
[campo1] = [novo valor do campo1],
[campo2] = [novo valor do campo2],
...
[WHERE + condições];
```

**ATENÇÃO: muito cuidado com os updates. Sempre utilize-os com condição**

#### Exemplos:
```sql
UPDATE banco SET codigo = 500 WHERE codigo = 100;
```

```sql
UPDATE banco SET data_criacao = now() WHERE data_criacao IS NULL;
```

### DELETE
```sql
DELETE FROM [nome_da_tabela] [WHERE + condicoes];
```

**ATENÇÃO: muito cuidado com os deletes. Sempre utilize-os com condição**

#### Exemplos:
```sql
DELETE FROM banco WHERE codigo = 512;
```

```sql
DELETE FROM banco WHERE nome = 'Conta Digital';
```

### SELECT
```sql
SELECT [campos da tabela] FROM [nome da tabela] [WHERE + condições];
```

**DICAS DE BOAS PRATICAS: Evite sempre que puder o SELECT \***

#### Exemplos:

```sql
SELECT codigo, nome FROM banco;
```

```sql
SELECT codigo, nome FROM banco WHERE data_criacao > '2019-10-15 15:00:00';
```