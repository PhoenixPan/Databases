# MySQL


## Basic commands
`SHOW DATABASES;`  
`CREATE DATABASE test;`  
`USE test[;]`  
```
CREATE TABLE states (
    id INT NOT NULL PRIMARY KEY AUTO_INCREMENT, 
    state CHAR(25), 
    population INT(9)
);
```
`SHOW TABLES` display all tables in this database  
`DESCRIBE states`
`INSERT INTO states (id, state, population) VALUES (NULL, 'Alaska', '731449'), (NULL, 'Arizona', '6553255'), (NULL, 'Arkansas', '2949131');` insert multiple entries at a time  
`SELECT * FROM states;`  
`DELETE FROM states WHERE id > 3;`  
`ALTER TABLE states DROP population;` remove a column   
`ALTER TABLE states ADD population INT(9);` add a column  
`ALTER TABLE states MODIFY population INT(10);` change column data type  
`ALTER TABLE states CHANGE state state_name CHAR(25)` change column name  
You can't change the name of databases  
`DROP TABLE states;`  
`EXIT` leave MySQL  
