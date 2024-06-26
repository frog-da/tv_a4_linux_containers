# Container

# **Intro**

Setting up an isolated container based on a Docker image filesystem (which is by default `[busybox](https://hub.docker.com/_/busybox)`) is the goal of the work.

The article [Linux containers in a few lines of code](https://zserge.com/posts/containers/) served as the foundation for the container source code.

## **Features**

- Filesystem, processes and network interfaces isolated from the host system.
- The filesystem is persistent and stored as `.img` file (ext4)

## How to

### tl;dr

```sh
sudo make rootfs
sudo make compile
sudo make run
```

### I can do read

Use the `sudo` for every `make` command.

[`Makefile`](./Makefile) is configured to create `rootfs.img` file from `busybox` image, change if needed.

- `make rootfs`
  
  Create new `rootfs.img` file. This file has to exist for the container to run.

- `make compile`
  
  Compile the container source, creating `./container` file

- `make run`
  
  This runs two actions one after another:

  - `make shell`

    Runs `/bin/sh` in the container.

  - `make restore`

    Restore `procfs`, remove `rootfs.img` mount and loop.