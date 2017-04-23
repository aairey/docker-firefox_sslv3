# docker-firefox_sslv3

Docker image which runs a Firefox version that still supports the deprecated protocol SSLv3.

Very handy to access those few legacy web applications that can't be updated for whatever reason.

## Tags

* `latest`: same as `debian`
* `debian`: built on `debian:8`
* `centos`: built on `centos:7`

## Prerequisites

### Docker host setup

First on your linux docker host, you must enable the container to use the X Server:

```bash
xhost local:root
```

#### SELinux
If your docker host is SELinux enabled (for example Fedora/CentOS are by default), there is a SELinux Policy included which you can import on your system.

This policy allows containers to connect to the X11 Unix Socket.

To import it:
```bash
semodule -i mypol.pp
```

## Using

Then run the containter as follows:

```bash
docker run -ti --rm -e DISPLAY=$DISPLAY -v /tmp/.X11-unix:/tmp/.X11-unix:z  aairey/firefox-sslv3
```
And a Firefox v33 should pop up.

To browse to a website directly from the CLI:

```bash
docker run -ti --rm -e DISPLAY=$DISPLAY -v /tmp/.X11-unix:/tmp/.X11-unix:z  aairey/firefox-sslv3 https://www.howsmyssl.com/
```

## Building

Simple:

```bash
docker build -t aairey/firefox-sslv3 .
```

