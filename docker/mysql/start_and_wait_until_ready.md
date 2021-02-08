# Docker / MySQL - Start and wait until ready
## Problem
When automating docker-setups you often want to execute a next step only after the MySQL-database
is ready.

## Solution
Precondition: Have function `db_exec <statement>` from 
[Docker / MySQL - Execute statement or script](execute_statement_or_script.md) available.

The following bash-function returns only after the database is ready:
```bash
db_start(){
  docker-compose up --detach mysql
  success=$?

  if [[ "${success}" = 0 ]]; then
      for i in {30..0}; do
          if db_exec 'SELECT 1;' &> /dev/null; then
              break
          fi
          echo 'MySQL init process in progress...'
          sleep 1
      done

      if [[ "$i" = 0 ]]; then
          echo >&2 'MySQL init process failed.'
          return 1
      else
          return 0
      fi
  else
      return "${success}"
  fi
}
```

[Source](https://github.com/docker-library/mysql/blob/master/8.0/docker-entrypoint.sh#L127)
