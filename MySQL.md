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
You can't change the name of databases. You have to dump and reload the data into a new database     
`DROP TABLE states;`  
`EXIT` leave MySQL  


## Create backup using mysqldump
1. Add mysql.exe to system path: `set path=C:\Program Files\MySQL\MySQL Server 5.7\bin` (one time set, use your directory of mysql.exe)
2. Try to create a test dump: `mysqldump -u root -p backup_test > testdump.sql`. "-u" is your user name and "-p" is the name of the database. The user has to have at least SELECT priviledge. Default direcotory of the dump file is C:\Users\username
3. Restore the data: `mysql -u root -p backup_test < testdump.sql`
4. A more complicated command. You could choose to put the password in if it's a secured server. The file name will  be the data of today. Name multiple databases you want to backup.  

    ```
    mysqldump.exe --user=root --password  --host=localhost --port=3306 --result-file="backup.%date:~10,4%%date:~4,2%%date:~7,2%.%time:~0,2%%time:~3,2%.sql" --default-character-set=utf8 --single-transaction=TRUE --databases "backup_test"
    ```
    `--all-databases`  
    
5. 34
