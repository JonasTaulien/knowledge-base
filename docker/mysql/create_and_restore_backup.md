# Docker / MySQL - Create and restore backup
## Create:
```bash
db_backup_create(){
  backupDestinationPath="${1}"
  docker-compose exec -T mysql sh -c "exec mysqldump -uroot -p\"\${MYSQL_ROOT_PASSWORD}\" \"\${MYSQL_DATABASE}\"" > "${backupDestinationPath}"
}
```

## Restore:
Precondition: Have function `db_exec_script <statement>` from 
[Docker / MySQL - Execute statement or script](execute_statement_or_script.md) available.

```bash
db_backup_restore(){
  backupPath="${1}"
  db_exec_script "${backupPath}"
}
```
