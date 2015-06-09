---
layout: default
title: MySQL
---

## Dump database to file: ##

`/usr/local/mysql-5.6.22-osx10.8-x86_64/bin/mysqldump -u %username% --skip-add-drop-table --no-create-info --no-create-db %database_name% > %filename.sql%`

## Login to shell: ##
`mysql -u %username% -p`

## Change password for database: ##

`SET PASSWORD FOR '%username%'@'%hostname%' = PASSWORD('%new_password%');`

## Import sql file from shell: ##

`use %database%
source %filename%;`
