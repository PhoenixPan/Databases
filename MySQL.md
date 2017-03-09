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
    mysqldump.exe --user=root --password='pwd'  --host=localhost --port=3306 --result-file=C:\User\pan\backup.%date:~10,4%%date:~4,2%%date:~7,2%.%time:~0,2%%time:~3,2%.sql" --default-character-set=utf8 --single-transaction=TRUE "mydatabase"
    ```
    `--databases "db1" "db2"`  
    `--all-databases`  
    
5. Make this a routine task using Windows Task Scheduler

### Encrypt the password for mysqldump
1. Find cnf location by typing `mysql --help` in cmd

    ```
    Default options are read from the following files in the given order:
    C:\Windows\my.ini C:\Windows\my.cnf C:\my.ini C:\my.cnf C:\Program Files\MySQL\M
    ySQL Server 5.7\my.ini C:\Program Files\MySQL\MySQL Server 5.7\my.cnf
    ```
2. Create the my.cnf file in one of these locations and put in your password as

    ```
    [mysqldump]
    user=username
    password='pwd'
    ```
3. Now you should be able to log in without -p parameter
    
### Complete batch code
To complete the backup process, we need some lines of code with batch to help us zip and relocate the .sql files.  

    ```
    :: Set path for mysqldump if not specified
    set path=C:\Program Files\MySQL\MySQL Server 5.7\bin

    :: Where the sqldump files are and where the zipped sql files should go
    set DUMPDIR=M:\sqldump
    set ZIPDIR=M:\sqlzips

    :: Export all databases to the dump folder
    mysqldump.exe --user=root --password=1538  --host=localhost --port=3306 
    --result-file=%DUMPDIR%\backup.%date:~10,4%%date:~4,2%%date:~7,2%.%time:~0,2%%time:~3,2%.sql 
    --default-character-set=utf8 --single-transaction=TRUE --all-databases

    :: Find the most recent dump file
    FOR /F "delims=" %%I IN ('DIR "%DUMPDIR%\*.sql" /B /O:D') DO SET NewestFile=%%I
    echo %NewestFile%

    :: Set path for 7z if not specified
    set path=C:\Program Files\7-Zip

    :: Truncate the file name and zip it up
    set ZipName=%NewestFile:~0,-4%
    7z a %ZIPDIR%\%ZipName%.7z %DUMPDIR%\%NewestFile%
    ```
