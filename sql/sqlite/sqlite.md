## summary

Useful SQL commands for sqlite dbms

## comments
`--comments`

`/*comments*/`

## database version
`select sqlite_version()`

## database contents
`select tbl_name from sqlite_master where type='table' and tbl_name not like 'sqlite_%'`

`select sql from sqlite_master where type!='meta' and sql not null and name='table_name'` 

## boolean check
`select sql from sqlite_master where type!='meta' and sql not null and name='table_name'`

`and (select LENGTH(tbl_name) from sqlite_master where type='table' and tbl_name not like 'sqlite_%' limit 1 offset 0)=table_name_length_number`
  

