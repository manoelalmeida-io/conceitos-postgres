# Arquitetura e Hierarquia

## Cluster
Coleção de banco de dados que compartilham as mesmas configurações (arquivos de configuração) do PostgreSQL e do sistema operacional (porta, listen_addresses, etc).

## Banco de dados (database)
Conjunto de schemas com seus objetos/relações (tabelas, funções, views, etc).

## Schema
Conjunto de objetos/relações (tabelas, funções, views, etc).

### **Atenção**!
*Diferente de alguns bancos de dados como o MySQL que trata um schema como sendo um banco de dados o PostgreSQL pode dividir um banco de dados em diversos schemas diferentes cada um com seus objetos Ex: bd_livraria pode conter schema_livro, schema_cliente, etc* 