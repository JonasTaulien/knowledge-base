# Bash - Exit early
Instead of writing:
```bash
   command1 \
&& command2 \
&& command3
```

one can use `set -e`:
```bash
set -e

command1
command2
command3
```
