# Bash - Calculate absolute path
```bash
##########
# Calculates the absolute path of the parent directory of the given path.
# If the given path is relative, it is assumed, that it is relative to the current working directory
#
# @param1 A (maybe relative) path to a file or directory
# @stdout Absolute path of the parent directory of the file or directory
##########
calculate_absolute_path_of_parent_directory(){
    local path="${1}"
    echo -n "$(cd "$(dirname "${path}")" && pwd)"
}
```

## Calculate absolute path of parent directory of current script:
```bash
$(calculate_absolute_path_of_parent_directory "${BASH_SOURCE[0]}")
```
