# kiwi-ltsp docker image

This is the Dockerfile for creating Docker image for [KIWI-LTSP][] project, the
openSUSE's integration work to it's upstream [LTSP][] project in order to take
advantage of many awesome features from the [KIWI][] Image System.

## Building

Move to the folder containing the Dockerfile and do:

```
docker build -t kiwi-ltsp
```

## Runing

To run docker in a container you need to mount cgroup file system volume, and
also extended privilege needs to be gave out to container.

```
docker run --name ltsp-server --rm --privileged -d --net=host -ti -e 'container=docker' -v /sys/fs/cgroup:/sys/fs/cgroup:ro kiwi-ltsp
```

It is recommended to have a look on [KIWI-LTSP network configuration][] to
grasp some idea of concerned network interface to be used by KIWI-LTSP if you
don't specify any. Or you can force it to go with your favorite through editing
the  _/etc/sysconfig/kiwi-ltsp_ config file. For example this will set to use
_eth1_ in your host network to serve DHCP requests.

```
docker exec ltsp-server sh -c 'echo DHCP_IFACES=eth1 >> /etc/sysconfig/kiwi-ltsp'
```

To setup and run the server, execute `kiwi-ltsp -c` in the container. 

```
docker exec -ti ltsp-server sh -c 'kiwi-ltsp -c'
```

[KIWI-LTSP]: https://en.opensuse.org/Portal:KIWI-LTSP
[LTSP]: https://ltsp.org/
[KIWI]: https://opensuse.github.io/kiwi/
[KIWI-LTSP network configuration]: https://en.opensuse.org/SDB:KIWI-LTSP_network_configuration
