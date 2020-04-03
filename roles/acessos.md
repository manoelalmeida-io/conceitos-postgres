# Acessos (GRANT)

## Definição
> São privilégios de acesso aos objetos do banco de dados.

## Privilégios
* **table**
* column
* sequence
* **database**
* domain
* foreign data wrapper
* foreign server
* **function**
* language
* large object
* **schema**
* tablespace
* type

## Exemplos
### Database
```sql
GRANT {{ CREATE | CONNECT | TEMPORARY | TEMP } [,...] | ALL [PRIVILEGES]}
  ON DATABASE database_name [,...]
  TO role_specification [,...] [WITH GRANT OPTIONS]
```

### Schema
```sql
GRANT {{ CREATE | USAGE } [,...] | ALL [PRIVILEGES]}
  ON SCHEMA schema_name [,...]
  TO role_specification [,...] [WITH GRANT OPTIONS]
```

### Table
```sql
GRANT {{ SELECT | INSERT | UPDATE | DELETE | TRUNCATE | REFERENCES | TRIGGER } [,...] | ALL [PRIVILEGES]}
  ON {[TABLE] table_name [,...] | ALL TABLES IN SCHEMA schema_name [,...]}
  TO role_specification [,...] [WITH GRANT OPTIONS]
```

## Revoke
Retira permissões de uma role

### Database
```sql
REVOKE [GRANT OPTION FOR]
  {{ CREATE | CONNECT | TEMPORARY | TEMP }[,...] | ALL [PRIVILEGES]}
  ON DATABASE database_name[,...]
  FROM {[GROUP] role_name | PUBLIC}[,...]
  [CASCADE | RESTRICT]
```

### Schema
```sql
REVOKE [GRANT OPTION FOR]
  {{ CREATE | USAGE }[,...] | ALL [PRIVILEGES]}
  ON SCHEMA schema_name [,...]
  FROM {[GROUP] role_name | PUBLIC}[,...]
  [CASCADE | RESTRICT]
```

### Table
```sql
REVOKE [GRANT OPTION FOR]
  {{SELECT | INSERT | UPDATE | DELETE | TRUNCATE | REFERENCES | TRIGGER}
  [,..] | ALL [PRIVILEGES]}
  ON {[TABLE] table_name [,...]
    | ALL TABLE IN SCHEMA schema_name [,...]}
  FROM {[GROUP] role_name | PUBLIC}[,...]
  [CASCADE | RESTRICT]
```

### Revogando todas as permissões

```sql
REVOKE ALL ON ALL TABLE IN SCHEMA [schema] FROM [role];
REVOKE ALL ON SCHEMA [schema] FROM [role];
REVOKE ALL ON DATABASE [database] FROM [role];
```