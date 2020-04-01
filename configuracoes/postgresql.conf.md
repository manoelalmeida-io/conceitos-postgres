# O que é o arquivo postgresql.conf?

## Definição
> Arquivo onde estão definidas e armazenadas todas as configurações do servidor PostgreSQL. Alguns parâmetros só podem ser alterados com uma reinicialização do banco de dados. A view pq_settings, acessada por dentro do banco de dados, guarda todas as configurações atuais.

## postgresql.conf
Ao acessar a view pg_settings, é possível visualizar todas as configurações atuais.

```postgresql
SELECT name, setting FROM pg_settings
```

Ou é possível usar o commando `SHOW [parâmetro]`. Ex:
```postgresql
SHOW ALL -- Mostra os valores de todos os parâmetros de configuração.
```

## Localização do arquivo postgresql.conf
Por padrão, encontra-se dentro do diretório PGDATA definido no momento da inicialização do cluster de banco de dados.

* Linux: `/var/lib/pgsql/[versão]/data` 
* Windows: `C:\Program Files\PostgreSQL\[versão]\data`

No sistema operacional Ubuntu, se o PostgreSQL foi instalado a partir do repositório oficial, o local do arquivo postgresql.conf será diferente do diretório de dados. `/etc/postgresql/[versão]/[nome do cluster]/postgresql.conf`

## Configurações de conexão
* **LISTEN_ADRESSES** --
Endereço(s) TCP/IP das interfaces que o servidor PostgreSQL vai escutar/liberar conexões.
* **PORT** -- A porta TCP que o servidor PostgreSQL vai ouvir. O padrão é 5432.
* **MAX_CONNECTIONS** -- Número máximo de conexões simultâneas no servidor PostgreSQL.
* **SUPERUSER_RESERVED_CONNECTIONS** -- Número de conexões (slots) reservadas para conexões ao banco de dados de super usuários.

## Configurações de autenticação
* **AUTHENTICATION_TIMEOUT** -- Tempo máximo em segundos para o cliente conseguir uma conexão com o servidor.
* **PASSWORD_ENCRYPTION** -- Algoritmo de criptografia das senhas dos novos usuários criados no banco de dados.
* **SSL** -- Habilita a conexão criptografada por SSL (Somente de o PostgreSQL foi compilado com suporte SSL).

## Configurações de memória
* **SHARED_BUFFERS** -- Tamanho da memória compartilhada do servidor PostgreSQL para cache/buffer de tabelas, índices e demais relações.
* **WORK_MEM** -- Tamanho de memória para operações de agrupamentos e ordenação (ORDER BY, DISTINCT, MERGE JOINS).
* MAINTENANCE_WORK_MEM -- Tamanho da memória para operações como VACUUMM, INDEX, ALTER TABLE.

