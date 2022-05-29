# Snowflake SQL Cheat Sheet
``` SQL
LEFT JOIN
```
> The `LEFT JOIN` keyword returns all records from the left table (table1), and the matching records from the right table (table2). The result is 0 records from the right side, if there is no match.

``` SQL
UNION
```
> The UNION operator is used to combine the result-set of two or more SELECT statements.
> * Every SELECT statement within UNION must have the same number of columns
> * The columns must also have similar data types
> * The columns in every SELECT statement must also be in the same order

``` SQL
IFF( <condition> , <expr1> , <expr2> )
```
> Single-level if-then-else expression. Similar to CASE, but only allows a single condition.

``` SQL
listagg()
```
> | a | 
> 
> | b | -> | a, b, c |
> 
> | c |
```
``` SQL
object_keys()
```
>  extract keys from dictionary and parse them in array
``` SQL
TRY_PARSE_JSON()
```
> parse the string that contain string as json (try_xxx = if work execute else give null)

``` SQL
max()
```
> | a    | null | null |
> 
> | null |  b   | null | -> | a | b | c |
> 
> | null | null |  c   |