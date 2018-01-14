# SQL-toolkit

SQL toolkit is a free tool for easier and much faster DDL(Data Definition Language) from console.
This is on MIT license.)

(This project is currently started. These are just ideas) 

## Examples

```bash
sqlt USERS(varchar(50) name, varchar(200) hash, varchar(200) salt) 
```

- Defines the table **Users** with columns: `user_id`, `user_name`, `user_hash`, `user_salt`, `user_created`, `user_modified`  
  You can configure this as:   
  1. extensive: `user_id`, `user_name`, `user_hash`, `user_salt`, `user_created`, `user_modified`  
  2. unextensive: `user_id`, `user_name`, `user_hash`, `user_salt`  

```javascript
sqlt USERS(*,varchar(50) birthday not null)
```

- Adds column `user_birthday` to the table

```javascript
sqlt USERS(*,date birthday not null)
```
- Redefines column `user_birthday` with date type 

```javascript
sqlt USERS < ARTICLES(varchar(100) name!, text text)
```
- Defines table Articles with columns: `article_id`, `user_id`, `article_created`, `article_modified`
- `user_id` can be null, and it is forigen key to `Users.user_id`
  -  ON DELETE do nothing
  -  ON MODIFY do nothing

## Guide

### basics
- `TABLE_NAME` is basically uppercase and transformed to `TableName`
if there is at least one non-uppercase character then no conversion will be done  
- **parameters** strictly follows the `TABLE_NAME`:  
  - `USERS(text name)`    
    - text is the type 
    - and name is the parameter  
- you can add **multiple parameters**, seperated by comma (,):
  - `USERS(text name, int experience)`
- you can add **default parameter:**
  - `USERS(text name, int experience = 1 )`
  
### restrictions
- not null
  - you can use `not null` or `required` or just simply `!` mark
- USER(varchar(50) name!)
  - any order you want:
  - `USER(varchar(50) !name)`
  - `USER(!varchar(50) name)`
- for **value check** constraints you simply write `CHECK(here the sql code)`
  - `USER(varchar(50) name, int experience = 1 CHECK(< 4) ) `
  - you can also use in lower case mode: `check(< 4)`
  - you can define separately
  - `USER(varchar(50) name, int experience = 1, CHECK( experience < 4 and name = LOWER(name) ) ) `
  - if you don't want you dont need to write brackets, but must be at the end of the parameter
  - `USER(varchar(50) name CHECK = LOWER(name), int experience = 1, CHECK experience < 4  ) `

### joins 
To define foreign keys:

| join    |   meaning                                            |  
|---------|------------------------------------------------------|  
| `A < B` |  means one row of `A` can have multiple rows of `B`  |  
| `A > B` |  means one row of `B` can have multiple rows of `A`  |  
| `A = B` |  means one row of `A` can have only one row of `B`   |  
| `A ~ B` |  means `A < B` and `A > B`                           |  


All of the joins can labelled with a `!` mark to ensure can't be e.g :
| example |   meaning                                                                                     |   
|---------|-----------------------------------------------------------------------------------------------|
|`A <! B` | means every row of `A` must have at least one row of `B`                                      |  
|`A !< B` | means every row of `B` must have parent (not required to sign because irrelevant to be null ) |  
|`A !<! B`| the combination of two                                                                        |  

joins can have attributes like 
`A ~(date approved_on = CURDATE()) B`

	
## Configure
to generate sql-toolkit-config.json , write:
```bash
	$> sqlt config
    alternatives:
    configure
    -config
    -configure
    --cofig
    --configure
```
You will have to setup the hostname,username,password  
You can modify style. Currently:  
- {singular_table_name}_{column_name} // from `name` produces: user_name
- available variables:
  - `{TableName}` for TABLE_NAME to TableName
  - `{TableNameSingular}` e.g. USERS to User
  - `{tablename}` for TABLE_NAME to tablename
  - `{tablenamesingular}` e.g. USERS to user
  - `{table_name}` for TABLE_NAME to table_name
  - `{table_name_singular}` e.g. TABLE_NAMES to table_name
  - `{ColumnName}` for the written column name (there is no conversion)

## DQL integration 
there is not really DQL(Data Query Language) but you can the basics:
```bash
sqlt list USERS~ARTICLES where user_id=2
#extracted to: SELECT * FROM Users NATURAL JOIN Users_Articles_Connections NATURAL JOIN Articles
```

## Installation
	will be avalaible on npm 
  
