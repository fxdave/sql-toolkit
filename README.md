# SQL-toolkit

SQL toolkit is a free tool for easier DDL(Data Definition Language) from console.
This is on MIT license.

(This project is currently started. These are just ideas) 

## Examples
```sql
	USERS(varchar(50) name, varchar(200) hash, varchar(200) salt) 
```

- Defines the table **Users** with columns: `user_id`, `user_name`, `user_hash`, `user_salt`, `user_created`, `user_modified`  
  You can configure this as:   
  1. extensive: `user_id`, `user_name`, `user_hash`, `user_salt`, `user_created`, `user_modified`  
  2. unextensive: `user_id`, `user_name`, `user_hash`, `user_salt`  

```sql	
USERS(*,varchar(50) birthday not null)
```

- Adds column `user_birthday` to the table

```sql
USER(*,date birthday not null)
```
- Redefines column `user_birthday` with date type 

```sql
USER<ARTICLES(varchar(100) name!, text text)
```
- Defines table Articles with columns: `article_id`, `user_id`, `article_created`, `article_modified`
- `user_id` can be null, and it is forigen key to `Users.user_id`
  -  ON DELETE do nothing
  -  ON MODIFY do nothing

## Guide

### joins 
	
	A < B  means one row of A can have multiple rows of B 
	A > B  means one row of B can have multiple rows of A
	A = B  means one row of A can have only one row of B
	A ~ B  means A < B and A > B 
	
	all of the joins can labelled with a "!" mark for restriction e.g : 
		A <! B means every row of A must have at least one row of B
		A !< B means every row of B must have parent (not required to sign (this is default))
		A !<! B the combination of two

	joins can have attributes like 
	A ~(date approved_on) B
		
	
## Configure

You can modify style. Currently:
- {singular_table_name}_{column_name} // from `name` produces: user_name
- alternatives: 
  - `{singular_table_name}{Column_name}`  //produces: `userName`  
  - `{table_name}{Column_name}` // produces: `usersName`  
  - `_{column_name}` // produces: `_name`
  - etc..  
  
  