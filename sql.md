# Anotaçẽs gerais sobre SQL

- [O que é SQL](#o-que-é-sql)
- [Geral](#geral)


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
    | 3     | Peter   | 31    | 1200.45  | London   | Englang       |
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
      - `CREATE INDEX index_name on table_name (column1);`
    - `DROP` deleta objetos do *database*.
      - `DROP TABLE table_name;`
      - `DROP DATABASE database_name;`
    - `ALTER` altera estrutura do *database*.
      - `ALTER TABLE table_name ADD COLUMN column_name data_type;`
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
      - `DELETE FROM table_name WHERE condition`
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