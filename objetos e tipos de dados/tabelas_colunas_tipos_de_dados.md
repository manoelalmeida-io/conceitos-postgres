# Tabelas, Colunas e Tipos de dados

## Definição
Conjunto de dados dispostos em colunas e linhas diferentes a um objetivo comum.\
As colunas são consideradas como "campos da tabela", como atributos da tabela.\
As linhas de uma tabela são chamadas também de tuplas, e é onde estão contidos os valores, os dados.

## Exemplo:

TABELA = automovel\
COLUNA 1 = tipo (carro, moto, avião, helicóptero)\
COLUNA 2 = ano_fabricacao (2010, 2011, 2020)\
COLUNA 3 = capacidade_pessoas (1, 2, 350)\
COLUNA 4 = fabricante (Honda, Avianca, Yamaha)

TABELA = produto\
COLUNA 1 = código serial do produto\
COLUNA 2 = tipo (vestuário, eletrônico, beleza)\
COLUNA 3 = preco (24.50, 5.99, 10.00)

### Tabela produto:
| NOME | MARCA | TAMANHO | COR |
|---|---|---|---|
| Camisa | Hering | GG | Branca |
| Calça | Levis | 46 | Preta |

## Primary Key / Chave Primária / PK
No conceito de modelo de dados relacional e obedecendo as regras de normalização, uma PK é um conjunto de um ou mais campos que nunca se repetem em uma tabela e que seus valores garantem a integridade do dado único e a utilização do mesmo como referência para o relacionamento entre demais tabelas.

* Não pode haver duas ocorrência de uma mesma entidade com o mesmo conteúdo na PK.
* A chave primária não pode ser composta por atributo opcional, ou seja, atributo que aceite nulo.
* Os atributos identificadores devem ser o conjunto mínimo que pode identificar cada instância de uma entidade.
* Não devem ser usadas chaves externas.
* Não deve conter informação volátil.

### Tabela produto:
| NOME | MARCA | TAMANHO | COR |
|---|---|---|---|
| Camisa | Hering | GG | Branca |
| Calça | Levis | 46 | Preta |
| Camisa | Hering | M | Branca

PK = nome + marca + tamanho

## Foreign Key / Chave Estrangeira / FK
Campo, ou conjunto de campos que são referências de chaves primárias de outras tabelas ou da mesma tabela.\
Sua principal função é garantir a integridade referencial entre tabelas.

### Exemplo:

#### Cliente
| CPF | NOME | TELEFONE | 
|---|---|---|
| 23433244567 | Ermelino Carlos | 83977863122 |
| 29555467899 | Arlinda da Graça | 15988900122 |
| 27335445017 | Gumercindo Orlando | 11988000900 |

#### Produto
| NUMERO_SERIE | NOME | VALOR |
|---|---|---|
| 10001 | Camiseta | R$ 59,90 |
| 10005 | Calça Jeans | R$ 99,90 |
| 10099 | Relógio de Ouro | R$ 1515,90 |

#### Pedido
| NUMERO | CLIENTE_CPF | PRODUTO_NUMERO_SERIE | VALOR | DESCONTO |
|---|---|---|---|---|
| 18015 | 23433244567 | 10001 | R$ 59,90 | |
| 18015 | 23433244567 | 10005 | R$ 99,90 | R$ 10,00 |
| 18016 | 27335445017 | 10099 | R$ 1515,00 | 

PK = numero + cliente_cpf + produto_numero_serie

## Tipos de dados

* **Numeric Types**
* Monetary Types
* **Character Types**
* Binary Data Types
* **Date/Time Types**
* **Boolean Type**
* Enumerated Types
* Geometric Types
* Network Address Types
* Bit String Types
* Text Search Types
* UUID Type
* XML Type
* JSON Types
* Array
* Composite Types
* Range Types
* Domain Types
* Object Identifier Types
* pg_lsn Type
* Pseudo Types

### Numéricos
| Name | Storage Size | Description | Range |
|---|---|---|---|
| smallint | 2 bytes | small-range integer | -32768 to +32767 |
| integer | 4 bytes | typical choice for integer | -2147483648 to -2147483647 |
| bigint | 8 bytes | large-range integer | -9223372036854775808 to +9223372036854775807 |
| decimal | variable | user-specified precision, exact | up to 131072 digits before the decimal point; up to 16383 digits after decimal point |
| numeric | variable | user-specified precision, exact | up to 131072 digits before the decimal point; up to 16383 digits after decimal point |
| real | 4 bytes | variable-precision, inexact | 6 decimal digit precision |
| double precision | 8 bytes | variable-precision, inexact | 15 decimal digit precision |
| smallserial | 2 bytes | small autoincrementing integer | 1 to 32767 |
| serial | 4 bytes | autoincrementing integer | 1 to 2147483647 |
| bigserial | 8 bytes | large autoincrementing integer | 1 to 9223372036854775807 |

### Caracteres
| Name | Description |
|---|---|
| character varying(n), varchar(n) | variable-length with limit |
| character(n), char(n) | fixed-length, blank padded |
| text | variable unlimited length |

### Datas
| Name | Storage Size | Description | Low Value | High Value | Resolution |
|---|---|---|---|---|---|
| timestamp [ (p) ] [ without time zone ] | 8 bytes | both date and time (no time zone) | 4713 BC | 294276 AD | 1 microsecond |
| timestamp [ (p) ] with time zone | 8 bytes | both date and time, with time zone | 4713 BC | 294276 AD | 1 microsecond |
| date | 4 bytes | date (no time of day) | 4713 BC | 5874897 AD | 1 day |
| time [ (p) ] [ without time zone ] | 8 bytes | time of day (no date) | 00:00:00 | 24:00:00 | 1 microsencond |
| time [ (p) ] with time zone | 12 bytes | time of day (no date), with timezone | 00:00:00+1459 | 00:00:00-1459 | 1 microsencond |
| interval [ fields ] [ (p) ] | 16 bytes | time interval | -178000000 years | 178000000 years | 1 microsencond |

### Booleanos
| Name | Storage Size | Description |
|---|---|---|
| boolean | 1 byte | state of true or false |