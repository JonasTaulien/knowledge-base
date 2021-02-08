# Docker - `ENTRYPOINT` vs. `CMD`
When both `ENTRYPOINT` and `CMD` are provided in array (`EXAMPLE ["a", "b"]`), rather than shell-form (`EXAMPLE a b`):  
Then Docker runs this on container startup: 
```shell
<Value of ENTRYPOINT> <Value of CMD>
```

[Source on docs.docker.com](https://docs.docker.com/engine/reference/builder/#understand-how-cmd-and-entrypoint-interact)

## `ENTRYPOINT`
In a Dockerfile `ENTRYPOINT` overrides the default value of `/bin/sh -c`.

```Dockerfile
ENTRYPOINT ["executable", "param1", "param2"]
```

[Documentation on docs.docker.com](https://docs.docker.com/engine/reference/builder/#entrypoint)
## `CMD`
`CMD` is empty by default.

```Dockerfile
CMD ["param3", "param4"]
```

Or to override it when starting the container:
```shell
docker run -i -t <image-name> param3 param4
```

[Documentation on docs.docker.com](https://docs.docker.com/engine/reference/builder/#cmd)

## Source
[Source on stackoverflow.com](https://stackoverflow.com/a/34245657)
