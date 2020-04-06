# Database, Schemas e Objetos

## Database
É o banco de dados.

Grupo de schemas e seus objetos, como tabelas, types, views, funções, entre outros. Seus schemas e objetos não podem ser compartilhados entre si. Cada database é separado um do outro compartilhado apenas usuários/roles e configurações do cluster PostgreSQL.

## Schemas
É um grupo de objetos, como tabelas, types, views, funções, entre outros. É possível relacionar objetos entre diversos schemas. Por exemplo: schema public e schema curso podem ter tabelas com o mesmo nome (teste por exemplo) relacionando-se entre si.

## Objetos
São as tabelas, views, funções, types, sequences, entre outros, pertencentes aos seus schemas.

## Comandos

### Database
Criando um banco de dados
```sql
CREATE DATABASE name
  [ [ WITH ] [ OWNER [=] user_name ]
      [ TEMPLATE [=] template ]
      [ ENCODING [=] encoding ]
      [ LC_COLLATE [=] lc_collate ]
      [ LC_CTYPE [=] lc_ctype ]
      [ TABLESPACE [=] tablespace_name ]
      [ ALLOW_CONNECTIONS [=] allowconn ]
      [ CONNECTION LIMIT [=] connlimit ]
      [ IS_TEMPLATE [=] istemplate ] ]
```

Alterando um banco de dados
```sql
ALTER DATABASE name RENAME TO new_name;
ALTER DATABASE name OWNER TO { new_owner | CURRENT_USER | SESSION_USER };
ALTER DATABASE name SET TABLESPACE new_tablespace;
```

Deletando um banco de dados
```sql
DROP DATABASE name;
```

### Schema
Criando um Schema
```sql
CREATE SCHEMA schema_name [ AUTHORIZATION role_specification];
```

Alterando um Schema
```sql
ALTER SCHEMA name RENAME TO new_name;
ALTER SCHEMA name OWNER TO { new_owner | CURRENT_USER | SESSION_USER };
```

Deletando um Schema
```sql
DROP SCHEMA name;
```

#### Melhores práticas
Verificar existência do Schema ao realizar uma operação no banco de dados.
```sql
CREATE SCHEMA IF NOT EXISTS schema_name [ AUTHORIZATION role_specification];
DROP SCHEMA IF EXISTS name;
```