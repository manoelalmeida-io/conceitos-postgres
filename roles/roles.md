# Conceitos users/roles/groups

## Definição
> Roles (Papéis ou funções), users (usuários) e grupos de usuário são "contas", perfis de atuação em um banco de dados, que possuem permissões em comum ou específicas.

Nas versões anteriores do PostgreSQL, usuários e roles tinham comportamentos diferentes.

Atualmente, roles e users são alias.

É possível que roles pertençam a outras roles.

Exemplo:

* **Administradores**: acesso ilimitado dentro do banco
* **Professores**: escrever em apenas 2 tabelas e leitura em todas as tabelas
  * **Daniel**: herda as permissões da role **professores**
  * **Robert**: herda as permissões da role **professores**
* **Alunos**: apenas ler as tabelas
  * **Gumercindo**: herda as permissões da role **alunos**

## Administração

```sql
CREATE ROLE name [[WITH] option [...]]
```

As opções podem ser:

```sql
SUPERUSER | NOSUPERUSER -- Role tem permissão de super usuário
CREATEDB | NOCREATEDB -- Role pode criar um novo banco de dados
CREATEROLE | NOCREATEROLE -- Role pode criar novas roles
INHERIT | NOINHERIT -- Role herda caracteristicas de outras roles
LOGIN | NOLOGIN -- Role pode se conectar no banco de dados
REPLICATION | NOREPLICATION -- Role pode fazer backup ou replicação
BYPASSRLS | NOBYPASSRLS -- Bypass row-level security
CONNECTION LIMIT connlimit -- Limite dentro do banco de dados
[ ENCRYPTED ] PASSWORD 'password' | PASSWORD NULL -- Senha da role
VALID UNTIL 'timestamp' -- Até que data a role tem acesso ao banco de dados
IN ROLE role_name [,...]-- Pertence a role definida
IN GROUP role_name [,...] -- Pertence a role definida
ROLE role_name [,...] -- A role definida pertence a nova role
ADMIN role_name [,...] -- Tem acessos administrativos dentro da role
USER role_name [,...] -- Deprecated
SYSID uid [,...] -- Deprecated
```

Exemplo: 
```sql
CREATE ROLE admnistradores
  CREATEDB
  CREATEROLE
  INHERIT
  NOLOGIN
  REPLICATION
  BYPASSRLS
  CONNECTION LIMIT 1;

CREATE ROLE professores
  NOCREATEDB
  NOCREATEROLE
  INHERIT
  NOLOGIN
  NOBYPASSRLS
  CONNECTION LIMIT 10;

CREATE ROLE alunos
  NOCREATEDB
  NOCREATEROLE
  INHERIT
  NOLOGIN
  NOBYPASSRLS
  CONNECTION LIMIT 90;
```

## Associação entre roles
Quando uma role assume as permissões de outra role.
Necessário a opção `INHERIT`

No momento de criação da role:
* `IN ROLE` (passa a pertencer a role informada)
* `ROLE` (a role informada passa a pertencer a nova role)

Ou após a criação da role
* `GRANT [role a ser concedida] TO [role a assumir as permissões]`

Exemplo:
```sql
CREATE ROLE professores
  NOCREATEDB
  NOCREATEROLE
  INHERIT
  NOLOGIN
  NOBYPASSRLS
  CONNECTION LIMIT -1;

CREATE ROLE daniel
  LOGIN
  CONNECTION LIMIT 1
  PASSWORD '123'
  IN ROLE professores;

-- Role daniel passa a assumir as permissões da role professores

CREATE ROLE daniel
  LOGIN
  CONNECTION LIMIT 1
  PASSWORD '123'
  ROLE professores;

-- Role professores passa a fazer parte da role daniel assumindo suas permissões

CREATE ROLE daniel
  LOGIN
  CONNECTION LIMIT 1
  PASSWORD '123';

GRANT professores TO daniel;
```

## Desassociar membros entre roles

Caso precise desassociar um membro de uma role, quando um usuário deixar não pertencer ao quadro de professores por exemplo.

Utilize o comando:  `REVOKE [role que será revogada] FROM [role que terá suas permissões revogadas]`

Exemplo:

```sql
REVOKE professores FROM daniel;
```

## Alterando uma role
```sql
ALTER ROLE role_specification [WITH] option [...]
```

As opções podem ser:
```sql
SUPERUSER | NOSUPERUSER -- Role tem permissão de super usuário
CREATEDB | NOCREATEDB -- Role pode criar um novo banco de dados
CREATEROLE | NOCREATEROLE -- Role pode criar novas roles
INHERIT | NOINHERIT -- Role herda caracteristicas de outras roles
LOGIN | NOLOGIN -- Role pode se conectar no banco de dados
REPLICATION | NOREPLICATION -- Role pode fazer backup ou replicação
BYPASSRLS | NOBYPASSRLS -- Bypass row-level security
CONNECTION LIMIT connlimit -- Limite dentro do banco de dados
[ ENCRYPTED ] PASSWORD 'password' | PASSWORD NULL -- Senha da role
VALID UNTIL 'timestamp' -- Até que data a role tem acesso ao banco de dados
```

## Excluindo uma role
```sql
DROP ROLE role_specification;
```