### Dump database to file (format used in eZ Publish/Platform DemoBundle)

```bash
/usr/local/mysql/bin/mysqldump -u %username% --skip-add-drop-table --no-create-info --no-create-db --extended-insert=FALSE %database_name% > %filename.sql%
```

### Login to shell

```bash
mysql -u %username% -p
```

### Change password for database

```sql
SET PASSWORD FOR %username%@%hostname% = PASSWORD('%new_password%');

# reset root password:

SET PASSWORD FOR root@localhost = PASSWORD('');
```

### Import sql file from shell

```sql
use %database%
source %filename%;
```

### Reset auto-increment value

```sql
ALTER TABLE %table_name% AUTO_INCREMENT=%value%
```

### Truncate table that has FK constraints applied on it

```sql
SET FOREIGN_KEY_CHECKS = 0;
TRUNCATE %table_name%;
SET FOREIGN_KEY_CHECKS = 1;
```
