# Dockerfiles Definitions

This repository stores Dockerfiles definitions for different containers types. The next list describes the kind of images that can be obtained with each dockerfile in this repository

* centos: Generate a docker image for Centos 6 SO, enabled with some basic services
* !!No more for now!!

## Centos (/centos/Dockerfile)

This dockerfile generates a Centos 6 docker image enabled with SSH, SAMBA and X11 forwarding. The SSH  service is configured to allow root access and X11 forwarding, on the other hand, the SAMBA service shares the `/tmp` directory (as `MyShare` unit) with no authentication. 
* To generate it, just run: `docker build -rm -t [image-name] [dockerfiles-repo-path]/centos/`
* To start it, just run: `docker run -d -p 1022:22 -p 138:138/udp -p 139:139 -p 445:445 -p 445:445/udp -h centos-base --name centos-base [image.name]`


