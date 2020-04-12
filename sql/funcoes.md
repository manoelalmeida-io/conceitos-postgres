# Funções

## Definição

Conjunto de código que são executados dentro de uma transação com a finalidade de facilitar a programação e obter o reaproveitamento/reutilização de código.

Existem 4 tipos de funções:
* Query language functions (funções escritas em SQL)
* Procedural language function (funções escritas em, por exemplo, PL/pgSQL ou PL/py)
* Internal functions
* C-language function

Porém, o foco aqui é falar sobre USER DEFINED FUNCTIONS.\
Funções que podem ser criasas pelo usuário.

## Linguagens

* SQL
* PL/PGSQL
* PL/PY
* PL/PHP
* PL/RUBY
* PL/Java
* PL/Lua
* ...

## Idepotência

```sql
CREATE OR REPLACE FUNCTION [nome da função]
```
* Mesmo nome
* Mesmo tipo de retorno
* Mesmo número de parâmetros/argumentos

## Returns

* Tipo de retorno (data type)
  * INTEGER
  * CHAR / VARCHAR
  * BOOLEAN
  * ROW
  * TABLE
  * JSON

## Segurança

* SECURITY
  * INVOKER
  * DEFINER

## Comportamento

* **IMMUTABLE**\
Não pode alterar o banco de dados.\
Funções que garantem o mesmo resultado para os mesmos argumentos/parâmetros da função. Evitar a utilização de selects, pois tabelas podem sofres alterações.
* **STABLE**\
Não pode alterar o banco de dados.\
Funções que garantem o mesmo resultado para os mesmos argumentos/parâmetros da função. Trabalha melhor com tipos de current_timestamp e outros tipos variáveis. Podem conter selects.
* **VOLATILLE**\
Comportamento padrão. Aceita todos os cenários.

## Segurança e Boas Práticas

* **CALLED ON PULL INPUT**\
Padrão.\
Se qualquer um dos parâmetros/argumentos for NULL, a função será executada.
* **RETURNS NULL ON NULL INPUT**
Se qualquer um dos parâmetros/argumentos for NULL, a função retornará NULL

* **SECURITY INVOKER**\
Padrão.\
A função é executada com as permissões de quem executa.

* **SECURITY DEFINER**\
A função é executada com as permissões de quem criou a função.

## Recursos

* **COST**\
Custo/row em unidades de CPU

* **ROWS**\
Número estimado de linhas que será analisada pelo banner

## SQL Functions

Não é possível utilizar **TRANSAÇÕES**

```sql
CREATE OR REPLACE FUNCTION fc_somar (INTEGER, INTEGER)
RETURNS INTEGER
LANGUAGE SQL
AS $$
  SELECT $1 + $2;
$$;
```

```sql
CREATE OR REPLACE FUNCTION fc_somar (num1 INTEGER, num2 INTEGER)
RETURNS INTEGER
LANGUAGE SQL
AS $$
  SELECT num1 + num2;
$$;
```

```sql
CREATE OR REPLACE FUNCTION fc_banco_add(p_numero INTEGER, p_nome VARCHAR, p_ativo BOOLEAN)
RETURNS TABLE (numero INTEGER, nome VARCHAR)
RETURNS NULL ON NULL INPUT
LANGUAGE SQL
AS $$
  INSERT INTO banco (numero, nome, ativo)
  VALUES (p_numero, p_nome, p_ativo);

  SELECT numero, nome
  FROM banco
  WHERE numero = p_numero;
$$;
```

## PL/PGSQL Function

```sql
CREATE OR REPLACE FUNCTION banco_add(p_numero INTEGER, p_nome VARCHAR, p_ativo BOOLEAN)
RETURNS BOOLEAN
LANGUAGE PLPGSQL
AS $$
DECLARE variavel_id INTEGER;
BEGIN
  SELECT INTO variavel_id, numero FROM banco WHERE nome = p_nome;

  IF variavel_id IS NULL THEN
    INSERT INTO banco (numero, nome, ativo) VALUES (p_numero, p_nome, p_ativo);
  ELSE
    RETURN FALSE;
  END IF;

  SELECT INTO variavel_id, numero FROM BANCO WHERE nome = p_nome;

  IF variavel_id IS NULL THEN
    RETURN FALSE;
  ELSE
    RETURN TRUE;
  END IF;

END; $$;

SELECT banco_add(13, 'Banco azarado', true);
```