# Docker / MySQL - Initialize
## Problem
Every time the container gets created we want to setup the database by creating tables or inserting test data.

## Solution
In your docker-compose, add the following:
```yaml
services:
  myql:
    volumes:
    - ./my-initailization-scripts:/docker-entrypoint-initdb.d:ro
```

This will execute all `.sql`-files in alphabetical order.
In combination with using a '.gitignore'-file with the following content:
```.gitignore
/my-initailization-scripts/test-*.sql
```
that is a nice setup with which every developer can setup his/her database with own data (`test-users.sql` etc.).

[Source](https://hub.docker.com/_/mysql#initializing-a-fresh-instance)