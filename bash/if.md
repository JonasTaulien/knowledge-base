# Bash - If
## Basics
Executes the `block1` if `command1` returns `0`.
Else if `command2` returns `0`, `block2` gets executed. 
Otherwise `block3`:
```bash
if command1; then
    block1
elif command2; then
    block2
else
    block3
fi
```

Executes the block if the command returns anything else than `0`:
```bash
if ! command; then
    block
fi
```

Or short if the block is just one command:
```bash
command || block
```

## File exists?
```bash
if [ -f filePath ]; then
    block
fi

# File not exists?
if [ ! -f filePath ]; then
    block
fi
```

## File contains (multiline) String?
```
if [[ $(<"${filePath}") = *"${string}"* ]]; then
    block
fi
```

## Software installed?
```bash
if which "${software}" > /dev/null; then
    block
fi
```

## Predicates on numbers
```
if (( $someNumber > 10 )); then
    block
fi
```
* `>=`
* `==`
* `<=`
* `<`
