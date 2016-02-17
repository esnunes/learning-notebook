Title: Docker

# Docker

## How to set docker0 ip address?

```bash
DOCKER_OPTS="--bip=172.17.42.1/16"
```

## Saving memory / CPU

Docker spawns a `docker-proxy` application whenever you run a docker container.
The application is responsible to proxy ports between the host machine and
the container. I'm not sure when but newer versions of Linux Kernel support
a special network flag that makes `docker-proxy` obsolete.

In order to save memory and CPU you must run docker daemon setting the flag
`--userland-proxy=false`.

```bash
DOCKER_OPTS="--userland-proxy=false"
```
