[MiraDB](https://miradb.com/docs/) an object database is a light-weight database management system in which information is represented in the form of objects as used in javascript programming.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
    *   [2.1 terminal](#terminal)
    *   [2.2 Query Guide](#Query_Guide)
        *   [2.2.1 UNIQUE](#UNIQUE)
        *   [2.2.2 SELECT](#SELECT)
        *   [2.2.3 UPDATE](#UPDATE)
        *   [2.2.4 ADD](#ADD)
        *   [2.2.5 RENAME](#RENAME)
        *   [2.2.6 DELETE](#DELETE)
        *   [2.2.7 CREATE](#CREATE)
        *   [2.2.8 DROP](#DROP)
        *   [2.2.9 LIST](#LIST)

## Installation

[Install](/index.php/Install "Install") the [miradb](https://aur.archlinux.org/packages/miradb/) package. The installation default directory `/usr/bin/miradb`

## Usage

	you need to first switching to the (root) user before start miradb.

```
 `$ su root` 

```

	register bash command (one-time):

```
 $ sh /usr/bin/miradb/service

```

### terminal

	specific commands to [ start | stop | restart | status ]

```
 $ miradb start

```

### Query Guide

	MiraQuery is a standard regular expression for storing, manipulating and retrieving data in databases. Our Querie tutorial will teach you how to use let's beginning.

#### UNIQUE

	returns a dataset that contains only one observation for each unique combination of values for the strings in A specified in column.

 `query`  `UNIQUE COLUMN <COLUMN_NAME> TABLE <TABLE_NAME>;`  `example usage` 
```
    db.query("UNIQUE COLUMN pass TABLE user",function(data,err){ 
      console.log(data); 
    });

```

#### SELECT

	the returned all the columns from the table

 `query`  `SELECT TABLE <TABLE_NAME>;` 

	the returned the number of rows

 `query`  `SELECT TABLE <TABLE_NAME> COUNT;` 

	the returned selected columns in the table

 `query`  `SELECT TABLE <TABLE_NAME> COLUMN [COLUMN_NAME];` 

	the returned specify the number of records range (start-end) **LIMIT [1,5]**

 `query`  `SELECT TABLE <TABLE_NAME> LIMIT [START_NUMBER,END_NUMBER];` 

	finds rows that contain a specific string value in a column.

 `query`  `SELECT TABLE <TABLE_NAME> COLUMN [COLUMN_NAME] FIND ["SEARCH_STRING"];` 

	used in search for similar string of in a column

 `query`  `SELECT TABLE <TABLE_NAME> COLUMN [COLUMN_NAME] FIND ["SEARCH_STRING"] LIKE;`  `example usage` 
```
    db.query("SELECT TABLE user;",function(data,err){ 
      console.log(data); 
    });

```

#### UPDATE

	used to modify the existing records in a table.

 `query`  `UPDATE ROW <TABLE_NAME> COLUMN [COLUMN_NAME] VALUE [STRING] FIND [COLUMN_NAME,"STRING"];`  `example usage` 
```
    db.query("UPDATE ROW user COLUMN ["user","pass","mail"] VALUE ["olivia","3333","olivia@example.com"] FIND ["user","mason"];",function(data,err){ 
        console.log(data); 
    });

```

#### ADD

	insert new record in a data table.

 `query`  `ADD ROW  COLUMN [COLUMN_NAME] VALUE [STRING];` 

	create new column in a data table.

 `query`  `ADD COLUMN [COLUMN_NAME] TABLE <TABLE_NAME>;`  `example usage` 
```
    db.query("ADD ROW COLUMN ["user","pass","mail"] VALUE ["arvin","6666","arvin@example.com"];",function(data,err){ 
      console.log(data); 
    });

```

#### RENAME

	not ready yet

#### DELETE

	not ready yet

#### CREATE

	not ready yet

#### DROP

	not ready yet

#### LIST

	not ready yet