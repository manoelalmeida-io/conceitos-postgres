# O que é o arquivo pg_hba.conf?

## Definição
> Arquivo responsável pelo controle de authenticação dos usuários no servidor PostgreSQL.

O formato pode ser:
```
local      database  user  auth-method  [auth-options]
host       database  user  address  auth-method [auth-options]     
hostssl    database  user  address  auth-method  [auth-options]
hostnossl  database  user  address  auth-method  [auth-options]
host       database  user  IP-address  IP-mask  address  auth-method
hostssl    database  user  IP-address  IP-mask  address  auth-method
hostnossl  database  user  IP-address  IP-mask  address  auth-method
```

## Métodos de autenticação
* **TRUST** (conexão sem requisição de senha)
* **REJECT** (rejeitar conexões)
* **MD5** (criptografia md5)
* **PASSWORD** (senha sem criptografia)
* **GSS** (generic security service application program interface)
* **SSPI** (security support provider interface - somente para windows)
* **KRB5** (kerberos V5)
* **IDENT** (utiliza o usuário do sistema operacional do cliente via ident server)
* **PEER** (utiliza o usuário do sistema operacional do cliente)
* **LDAP** (ldap server)
* **RADIUS** (radius server)
* **CERT** (autenticação via certificado ssl do cliente)
* **PAM** (pluggable authentication modules)

### Exemplo:
```
# TYPE  DATABASE    USER     ADDRESS         METHOD
host    all         all      127.0.0.1/32    md5
```