# Docker / MySQL - Execute statement or script
## Execute single statement
```bash
db_exec(){
  statement="${1}"
  docker-compose exec -T mysql sh -c "exec mysql -uroot -hlocalhost -p\"\${MYSQL_ROOT_PASSWORD}\" -e \"${statement}\" \"\${MYSQL_DATABASE}\""
}
```

Example: `db_exec 'SELECT * FROM user;'`


## Execute script
```bash
db_exec_script(){
  pathToScript="${1}"
  docker-compose exec -T mysql sh -c "exec mysql -uroot -hlocalhost -p\"\${MYSQL_ROOT_PASSWORD}\" -D\"\${MYSQL_DATABASE}\"" < "$
{pathToScript}"
}
```

Example: `db_exec_script backups/2019-01-01.sql`