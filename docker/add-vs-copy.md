# Docker - ADD vs. COPY
In a Dockerfile you can use both `ADD` and `COPY` to insert files into the image beeing build.

## Use `COPY`!
It is best practice to use `COPY` as a default because `ADD` has more functionality build on top of just copying files.

> Although `ADD` and `COPY` are functionally similar, generally speaking, `COPY` is preferred. 
> That’s because it’s more transparent than `ADD`. `COPY` only supports the basic copying of local files 
> into the container, while `ADD` has some features (like local-only tar extraction and remote URL support) 
> that are not immediately obvious. Consequently, the best use for `ADD` is local tar file auto-extraction 
> into the image, as in `ADD rootfs.tar.xz /`.

[Source on docs.docker.com](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/#add-or-copy)
