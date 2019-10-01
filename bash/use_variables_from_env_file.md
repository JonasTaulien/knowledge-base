# Bash - Use variables from .env file
## Problem
For example in docker-compose-setups you can create a file `.env` that contains variables 
to be used in the `docker-compose.yaml`-file.

When automating using docker-compose you sometimes want to read out the variables used.

## Solution
Given file named `.env` with content:
```env
# my var
MY_VARIABLE=example
```

Executing:
```bash
set -o allexport
source .env
set +o allexport

echo "${MY_VARIABLE}"
```

outputs: `example`.

[Source](https://stackoverflow.com/a/30969768/4099380)