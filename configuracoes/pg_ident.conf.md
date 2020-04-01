# O que é o arquivo pg_ident.conf?

## Definição
> Arquivo responsável por mapear os usuários do sistema operacional com os usuários do banco de dados. Localizado no diretório de dados PGDATA de sua instalação. A opção ident deve ser utilizada no pg_hba.conf

### Exemplo:
```
# MAPNAME             SYSTEM-USERNAME          PGUSERNAME
diretoria             daniel                   pg_diretoria
comercial             tiburcio                 pg_comercial
comercial             valdeci                  pg_comercial
```