
## [How to get IP address of running docker container]

If you don't want to map ports from your host to the container you can access directly to the docker range ip for the container. This range is by default only accessed from your host. You can check your container network data doing:

```bash
docker inspect <containerNameOrId>
```

Probably is better to filter:

``` bash
docker inspect <containerNameOrId> | grep '"IPAddress"' | head -n 1
```

Usually, the default docker ip range is `172.17.0.0/16`. Your host should be `172.17.0.1` and your first container should be `172.17.0.2` if everything is normal and you didn't specify any special network options.

**EDIT** Another more elegant way using docker features instead of "bash tricking":

``` bash
docker inspect -f "{{ .NetworkSettings.IPAddress }}" <containerNameOrId>
```

**EDIT2** For modern docker engines, now it is this way (thanks to the commenters!):

``` bash
docker inspect -f '{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' <containerNameOrId>
```