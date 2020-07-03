This docker image is based on ubuntu 18.04.
It includes Qt LTS 5.12.9

To build this image, install docker on your machine, then in a terminal:

$ docker built -t trapta_ubuntu:1.1 .

Onced built, the image is kept in the docker storage space, but you can save the image:
$ docker save trapta_ubuntu:1.1 | gzip > trapta_ubuntu_1.1.tar.gz
Later, you can load it like this:
$ docker load < trapta_ubuntu_1.1.tar.gz
