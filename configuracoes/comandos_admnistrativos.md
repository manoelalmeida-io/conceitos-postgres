# Comandos administrativos

## Ubuntu

* **`pg_lsclusters`** -- lista todos os clusters PostgreSQL
* **`pg_createcluster <version> <cluster name>`** -- Cria um novo cluster PostgreSQL
* **`pg_dropcluster <version> <cluster>`** -- Apaga um cluster PostgreSQL
* **`pg_ctlcluster <version> <cluster> <action>`** -- Start, Stop, Status, Restart de clusters PostgreSQL

## CentOS

### `systemctl <action> <cluster>`
### Exemplos: 
* **`systemctl start postgresql-11`** -- Inicia o cluster PostgreSQL
* **`systemctl status postgresql-11`** -- Mostra o status do cluster PostgreSQL
* **`systemctl stop postgresql-11`** -- Para o cluster PostgreSQL
* **`systemctl restart postgresql-11`** -- Reinicia o cluster PostgreSQL

## Windows

No windows o serviço do PostgreSQL pode ser admnistrado através dos Serviços. Para abrir os serviços do windows utilize o atalho `ctrl + r` e escreva o comando `services.msc` dentro da caixa de texto e execute o comando. Procure o serviço do PostgreSQL e clique com o botão direito do mouse no serviço.

## Admnistração através dos binários do PostgreSQL

* **createdb** -- Cria um banco de dados no cluster
* **createuser** -- Cria um usuário
* **dropdb** -- Apaga um banco de dados
* **dropuser** -- Apaga um usuário
* **initdb** -- Cria um cluster
* **pg_ctl** -- Start, Stop, Restart, Status do banco de dados
* **pg_basebackup** -- Inicia um backup do banco de dados
* **pg_dump / pg_dumpall** -- Extrair informações do banco de dados
* **pg_restore** -- Restaurar arquivos de dump e dumpall
* **psql** -- Entrar no banco de dados pelo sistema operacional
* **reindexdb** -- Utilitário para reconstruir índices do banco de dados
* **vacuumdb** -- Utilitário para limpar um banco de dados