# Anotaçẽs gerais sobre SQL

- [O que é SQL](#o-que-é-sql)
- [Geral](#geral)
- [Tables](#tables)
- [Queries](#queries)
- [Joins](#joins)
- [Transactions](#transactions)


## O que é SQL
- **SQL** significa *structure query language*, é uma linguagem de programação usada em bancos de dados.
- **SQL** é um padrão usado para comunição com bancos relacionais (RDBMS).
- **RDBMS** significa *relational database management system*. *RDBMS* são dialetos criados por empresas que fazem o uso do padrão definido no **SQL**.
  - *PL/SQL (procedural language/SQL)* desenvolvido pela Oracle.
  - *Transact-SQL ou T-SQL* desenvolvido pela Microsoft para o Microsoft SQL Server.
  - *PL/pgSQL (procedural language/postgreSQL* criado por PostgreSQL.
  - *MySQL* comprado e mantido atualmente pela Oracle.


## Geral
- Os *dados* são armazedos no banco de dados em tabelas. *Tabelas* basicamente são coleções de dados relanionados.
- Toda *tabela(table)* é composta por *campos*, chamados de *fields*, que é uma *coluna* para armazenas uma informação específica.
- Dentro da *tabela* cada entrada de dado é representada por uma *linha(row)*.
  <details>
    <summary>Ex:</summary>

    |  Id   |   Name  |  Age  |  Salary  |   City   |    Country    |
    | :---: | :------ | :---: | :------: | :------- | :------------ |
    | 1     | Jhon    | 50    | 250.00   | New York | USA           |
    | 2     | Ana     | 24    | 4000.00  | Tokyo    | Japan         |
    | 3     | Peter   | 31    | 1200.45  | London   | England       |
  </details>
- No exemplo acima temos representado 6 *colunas(column)* com diferentes valores em cada *row*.
- Em casos onde não temos valores para o *field*, represantamos a falta de valor como **NULL**, ou seja, um *field* com valor em branco é um *field* *NULL*.
- Comentários em **sql** são feitos com dois traços, `--` ou `/* */`.
- **SQL** possui vários comandos, cada comando geralmente é finalizado com *;*, indicando o fim do comando.
- Comandos **SQL** pode ser divididos em 4 categorias: *DML*, *DQL*, *DML* e *DCL*.
  - *DDL – Data Definition Language*.
    - Consiste nos *comandos SQL* usados para definir o *schema*, usado para criar, modificar e deletar a estrutura do banco de dados.
    - `CREATE` usado para criar *database*, *table*, *index*, *triggers*, *function*, *views* e *store procedure*.
      - `CREATE DATABASE database_name;`
      - `CREATE TABLE table_name (column1 data_type, column2 data_type, ...);`
      - `CREATE INDEX index_name on table_name (column1, column2, ...);`
    - `DROP` deleta objetos do *database*.
      - `DROP TABLE table_name;`
      - `DROP DATABASE database_name;`
    - `ALTER` altera estrutura do *database*.
      - `ALTER TABLE table_name ADD COLUMN column_name data_type;`
      - `ALTER TABLE table_name DROP COLUMN column_name;`
      - `ALTER TABLE table_name ADD INDEX index_name [index_type];`
      - `ALTER TABLE table_name DROP INDEX index_name;`
      - `ALTER TABLE table_name RENAME COLUMN old_column_name to new_column_name;`
    - `TRUNCATE` remove todos o dados da tabela.
      - `TRUNCATE TABLE table_name;`
    - `COMMENT` adicina comentários no dicionário de dados.
      - `COMMENT 'comment text' ON TABLE table_name;`
    - `RENAME` renomeia objetos existentes no *database*.
      - `RENAME TABLE old_name TO new_table_name;`
  - *DQL – Data Query Language*
    - São comandos usados para fazer busca de dados no *database*.
    - `SELECT` é usado para buscar dados do *database*.
      - `SELECT column1, column2, ... FROM table_name WHERE condition;`
  - *DML – Data Manipulation Language*
    - Usado para realizar manipulação dos dados presentes no *database*.
    - `INSERT` insere dados na tabela.
      - `INSERT INTO table_name (column1, column2, ...) VALUES (value1, value2, ...);`
      - `INSERT INTO table_name VALUES (value1, value2, ...);`
    - `UPDATE` faz uma operação de atualização de dados existentes na tabela.
      - `UPDATE table_name SET column1 = value1, column2 = value2 WHERE condition;`
    - `DELETE` faz a remoção de dado presente na tabela.
      - `DELETE FROM table_name WHERE condition;`
  - *DCL – Data Control Language*
    - Incluem comandos para gerenciar permissões, como permitir um usuário acessar o banco ou remover a permissão de um usuário existente.
    - `GRANT` adiciona novos privilégios ao usuário.
      - `GRANT privilege_type [(column_list)] ON [object_type] object_name TO user [WITH GRANT OPTION];`
    - `REVOKE` remove  privilégios de um usuário.
      - `REVOKE [GRANT OPTION FOR] privilege_type [(column_list)] ON [object_type] object_name FROM user [CASCADE];`
- *Constraints* são regras usadas em colunas ou tabelas.
  - `NOT NULL` garante que uma *column* não pode ter valores nulos.
  - `DEFAULT` insere um valor padrão em caso de nenhum valor especificado para a *column*.
  - `UNIQUE` o campo da *column* deve ser único.
  - `PRIMARY KEY` usado para identificar *row*.
  - `FOREIGN KEY` usado para identificar *row* em outra tabela.
  - `CHECK` garante que o valor da *column* satisfaz a condição especificada.
  - `INDEX` usado para criar e buscar dados de uma forma mais eficaz.
- *Operadores* são palavras ou símbolos reservados para realizar comparações ou operações aritiméticas.
  - Exemplos de operadores aritiméticos:
    - `+` soma.
    - `-` subtração.
    - `*` multiplicação.
    - `/` divisão.
    - `%` módulo.
  - Exemplos de operadores de comparação:
    - `=` igual.
    - `!=` diferente.
    - `>` maior que.
    - `<` menor que.
    - `>=` maior igual.
    - `<=` menor igual.
  - Exemplos de operadores lógicos:
    - `ALL` *true* se todas as comparações forem *true*.
    - `AND` *true* se todas as comparações separadas por `AND` forem *true*.
    - `OR` *true* se uma das comparações separadas por `OR` forem *true*.
    - `BETWEEN` *true* se o operando estiver no range usado na comparação.
    - `IN` *true* se o operando for igual a um item da lista informada.
    - `LIKE` *true* se o operando corresponder ao padrão informado.
    - `NOT` reverte o valor de qualquer operador booleano.

## Tables
- Aqui entraremos mais afundo em como fazer operações em **tables**.
- Para criar uma tabela, usamos o comando `CREATE`.
  <details>
    <summary>Ex:</summary>

    ```sql
    CREATE TABLE CUSTOMERS(
      ID      INT NOT NULL,
      NAME    VARCHAR(20) NOT NULL,
      AGE     INT NOT NULL,
      SALARY  DECIMAL(18, 2),
      PRIMARY KEY (ID)
    );
    ```
    |  ID   |   NAME  |  AGE  |  SALARY   |
    | :---: | :------ | :---: | :------:  |

  </details>
- Podemos verificar uma tabela que já existente usando o comando, `DESC table_name;`, irá mostrar a estrutura da tabela com as colunas, tipos de dados e constraints se existir.
- Se temos uma situação que queremos criar uma tabela, porém ela já existe, usando o exemplo mostrado acima, irá ocorrer um erro. Para não ocorrer erros, podemos alterar o comando para: `CREATE TABLE IF NOT EXISTS`.
- Para listar todas as tabelas do database, usar `SHOW TABLES;`.
- Para remover tabela, `DROP TABLE table_name;` ou `DROP TABLE IF EXISTS table_name;`.
- Para remover todos os dados de uma tabela de uma vez, usar `TRUNCATE TABLE table_name;`. Não aceita condição `WHERE`.
- Para remover dados da tabela usando uma condição `WHERE`, usar `DELETE FROM table_name WHERE condition;`. Podendo ser usado sem `WHERE`, irá remover todos as linhas.

## Queries
- Como já mencionado anteriormente, para fazer *queries* usamos o comando `SELECT`.
- Podemos adicionar cláusulas `WHERE` em nossas *queries*. `SELECT * FROM table_name WHERE condition;`.
  - `SELECT * FROM CUSTOMERS WHERE AGE >= 18;`.
  - `SELECT * FROM CUSTOMERS WHERE SALARY BETWEEN 1800 AND 2500;`.
  - `SELECT * FROM CUSTOMERS WHERE SALARY >= 18 AND SALARY <= 25;`.
  - `SELECT * FROM CUSTOMERS WHERE AGE IN (18, 19, 20);`.
  - `SELECT * FROM CUSTOMERS WHERE AGE NOT 18;`.
- Podemos ordenar de forma crescente ou decrescente os dados por colunas:
  - `SELECT * FROM table_name WHERE condition ORDER BY column_name ASC;` sendo esta opção por padrão, não precisando informar `ASC`.
  - `SELECT * FROM table_name WHERE condition ORDER BY column_name DESC;`
- Usamos `DISTINCT` para remover apenas da *query* valores duplicados, informando quais colunas queremos fazer esse filtro:
  - `SELECT DISTINCT column1, column2, ... FROM table_name;`.
- Temos funções de agregação usadas em *queries*:
  - **AVG** retorna a média dos itens avaliados: `SELECT AVG(AGE) FROM CUSTOMERS;`. Irá retornar a idade média da coluna *AGE* da tabela.
  - **COUNT** retorna a quantidade dos itens avaliados: `SELECT COUNT(*) FROM CUSTOMERS;`. Irá retornar a quantidade de linhas da tabela.
  - **MAX** retorna o valor máximo para dos itens avaliados. `SELECT MAX(AGE) FROM CUSTOMERS;`. Irá retornar a maior idade encontrada.
  - **MIN** retorna o valor mínimo para dos itens avaliados. `SELECT MIN(AGE) FROM CUSTOMERS;`. Irá retornar a menor idade encontrada.
  - **SUM** retorna a soma dos valores para os itens avaliados. `SELECT SUM(SALARY) FROM CUSTOMERS;`. Irá retorna a soma de todos os salários.
- Podemos usar a condicional **SQL CASE**, para tomadas de decisão, para retornar valores baseado na condição criada. Usado geralmente para criar uma nova coluna de acordo com os valores e a condição.
  <details>
    <summary>Ex:</summary>

    ```sql
    SELECT 
      NAME,
      SALARY,
      CASE
        WHEN SALARY < 3000 THEN 'Low'
        WHEN SALARY >= 3000 AND SALARY <= 5000 THEN 'Average'
        WHEN SALARY > 5000 THEN 'High'
      END as EVALUATION
    FROM
      CUSTOMERS;
    ```

  </details>

## Joins
- **JOINS** são cláusulas usadas para combinar dados de duas ou mais *tabelas*. Usando as **chaves estrangeiras(foreign keys)** para combinar os campos das tabelas.
- A *sintaxe* básica para o uso de **JOIN** é a seguinte: `SELECT * FROM table1 JOIN table2;`.
  <details>
    <summary>Ex:</summary>

    ```sql
    CREATE TABLE CUSTOMERS(
      ID      INT NOT NULL,
      NAME    VARCHAR(20) NOT NULL,
      AGE     INT NOT NULL,
      SALARY  DECIMAL(18, 2),
      PRIMARY KEY (ID)
    );

    INSERT INTO CUSTOMERS VALUES
    (1, 'Ramesh', 32, 2000.00 ),
    (2, 'Khilan', 25, 1500.00 ),
    (3, 'Kaushik', 23, 2000.00 ),
    (4, 'Chaitali', 25, 6500.00 ),
    (5, 'Muffy', 24, 10000.00 );

    CREATE TABLE ORDERS (
      ORDER_ID INT NOT NULL,
      DATE VARCHAR (20) NOT NULL,
      CUSTOMER_ID INT NOT NULL,
      AMOUNT DECIMAL (18, 2)
    );

    INSERT INTO ORDERS VALUES 
    (102, '2009-10-08 00:00:00', 3, 3000.00),
    (100, '2009-10-08 00:00:00', 3, 1500.00),
    (101, '2009-11-20 00:00:00', 2, 1560.00),
    (103, '2008-05-20 00:00:00', 4, 2060.00);

    SELECT ID, NAME, AGE, AMOUNT 
    FROM CUSTOMERS 
    JOIN ORDERS 
    ON CUSTOMERS.ID = ORDERS.CUSTOMER_ID;
    ```

  </details>
- **SQL** permite vários tipos de **JOINS**, com base no tipo que queremos que essa junção seja feita.
  - **INNER JOIN** é quando buscamos os dados na intersecção de duas tabelas, faz a junção apenas se existirem nas duas tabelas.
  - **LEFT JOIN** retorna tudo que está na tabela da esquerda.
  - **RIGHT JOIN** retorna tudo que está na tabela da direita.

## Transactions
- **TRANSACTIONS** são usados para gerenciar e executar operações com o intuito de manter a consistência e integridade dos dados.
- Podemos iniciar e finalizar uma *transaction*, sendo finalizada com um *commit* ou *rollback*.
- Alguns dos beneficios são:
  - Controlar a execução de operações e prevenir conflitos.
  - Garantir a integridade dos dados, mesmo com operações de falhar durante a transação.
  - Permitir a recuperação de um erro mantendo a consistência do banco de dados.
- **Transactions** aderem ao principio ACID.
  - *Atomicity(atomicidade)* garante que todas as operaçẽos dentro de uma transação são completadas ou nenhuma delas. Se uma operação falha, toda a transação sofre o rollback, desfazendo todas as mudanças anteriores dentro da transação.
  - *Consistency(consistência)* garante que todo o banco de dados permanceça consistente após a execução da transação.
  - *Isolation(isolamento)* ao iniciar uma transação, ela fica invisível de outras transações que ocorrem de forma concorrente, previnindo conflitos entre múltiplas transações.
  - *Durability(durabilidade)* quando uma transação finaliza com *commit*, seus efeitos serão adicionados a base mesmo que ocorra erros após isso.
- Para iniciar uma transaction, usar o comando: `BEGIN TRANSACTION;` ou `START TRANSACTION;`.
- Para fazer o commit de uma transaction, usar o comando: `COMMIT;`.
  - O comando `COMMIT` é usado para salvar permanentemente os dados que sofrearam alteração durante a transação no banco de dados.
- Para fazer o rollback, usar o comando: `ROLLBACK;`
  - O comando `ROLLBACK` é usado para cancelar qualquer mudança feita durante a transação.