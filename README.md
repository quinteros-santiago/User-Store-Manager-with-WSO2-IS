# WSO2-User-Store-Manager

This repository contains the necessary scripts and configuration for setting up a MySQL database to work with the WSO2 User Store Manager.

## Setting Up the Database

A Docker container is used to host a MySQL database which is used by the WSO2 User Store Manager. The Docker container runs MySQL, and a database called `CUSTOM_USERSTORE` is created with a table named `COLABORADORES`.

Here's an example command to start the MySQL Docker container:
```bash
docker run --name WSO2-User-Store-Manager -p 3306:3306 -e MYSQL_ROOT_PASSWORD=my-secret-pw -d mysql:tag
```

The database and table are created using the following SQL script:

```sql
CREATE DATABASE CUSTOM_USERSTORE;
USE CUSTOM_USERSTORE;
CREATE TABLE COLABORADORES(
    ID int(4) AUTO_INCREMENT,
    USERNAME VARCHAR (100),
    SENHA VARCHAR (100),
    NOME varchar(30) NOT NULL,
    SOBRENOME varchar(30) NOT NULL,
    EMAIL varchar(50),
    PRIMARY KEY (ID)
);
```

We then populate the `COLABORADORES` table with sample data using `INSERT` SQL statements.

```sql
INSERT INTO COLABORADORES (ID, USERNAME, SENHA, NOME, SOBRENOME, EMAIL) VALUES (1, 'usuario0', 'password2022', 'Usuario0', 'Usuario0', 'usuario0@test.com');
INSERT INTO COLABORADORES (ID, USERNAME, SENHA, NOME, SOBRENOME, EMAIL) VALUES (2, 'usuario1', 'password2022', 'Usuario1', 'Usuario1', 'usuario1@test.com');
INSERT INTO COLABORADORES (ID, USERNAME, SENHA, NOME, SOBRENOME, EMAIL) VALUES (3, 'usuario2', 'password2022', 'Usuario2', 'Usuario2', 'usuario2@test.com');
INSERT INTO COLABORADORES (ID, USERNAME, SENHA, NOME, SOBRENOME, EMAIL) VALUES (4, 'usuario3', 'password2022', 'Usuario3', 'Usuario3', 'usuario3@test.com');
INSERT INTO COLABORADORES (ID, USERNAME, SENHA, NOME, SOBRENOME, EMAIL) VALUES (5, 'usuario4', 'password2022', 'Usuario4', 'Usuario4', 'usuario4@test.com');
INSERT INTO COLABORADORES (ID, USERNAME, SENHA, NOME, SOBRENOME, EMAIL) VALUES (6, 'usuario5', 'password2022', 'Usuario5', 'Usuario5', 'usuario5@test.com');
INSERT INTO COLABORADORES (ID, USERNAME, SENHA, NOME, SOBRENOME, EMAIL) VALUES (7, 'usuario6', 'password2022', 'Usuario6', 'Usuario6', 'usuario6@test.com');
INSERT INTO COLABORADORES (ID, USERNAME, SENHA, NOME, SOBRENOME, EMAIL) VALUES (8, 'usuario7', 'password2022', 'Usuario7', 'Usuario7', 'usuario7@test.com');
INSERT INTO COLABORADORES (ID, USERNAME, SENHA, NOME, SOBRENOME, EMAIL) VALUES (9, 'usuario8', 'password2022', 'Usuario8', 'Usuario8', 'usuario8@test.com');
```

## User Creation and Access Control

To ensure data security, we create a MySQL user that has only `SELECT` (read) permissions on the `COLABORADORES` table. This user is used by the WSO2 User Store Manager to read data from the database, ensuring that it cannot modify the data.

The user is created and granted permissions with the following SQL commands:

```sql
CREATE USER 'reader'@'%' IDENTIFIED BY 'password';
GRANT SELECT ON CUSTOM_USERSTORE.COLABORADORES TO 'reader'@'%';
FLUSH PRIVILEGES;
```

Please replace `'reader'` and `'password'` with your actual username and password.
