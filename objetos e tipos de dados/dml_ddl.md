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