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

```SQL
SELECT 
  *
FROM ethereum.core.fact_event_logs
WHERE block_timestamp > '2022-06-03 02:27:42.000'
QUALIFY ROW_NUMBER() OVER (PARTITION BY origin_from_address ORDER BY block_timestamp) = 1
LIMIT 100
```
> Anyone have a sample query where you look at the first transaction of a wallet after a specific tx/event?
> for the value of block_timestamp you guys can just find out what's the timestamp for the tx that you want. you can change the = 1 to whatever number you want to include nth tx after event. change to < n to include all tx below n

```SQL
select * from table(flatten(input => parse_json('{"a":1, "b":[77,88]}'), path => 'b')) f;
select 
		  		block_timestamp, tx_hash, origin_function_signature, voter, to_address, tx_fee, gas_price, gas_used,
		      size, index, value, regexp_count(value, '0', 1) as zeros, len(value) as hex_size, this
from table t, table(FLATTEN(input => t.segmented_data)) f order by tx_hash, index
```
https://docs.snowflake.com/en/sql-reference/functions/flatten.html

```SQL
time_series as (
  	select -1 + row_number() over(order by 0) as i, start_date + i as date 
  	from (select '2022-07-07'::date start_date, current_date() end_date)
      join table(generator(rowcount => 10000 )) x
      qualify i < 1 + end_date - start_date
  )
```
