# Dockerfile to create a container with a Firefox version that still supports SSLv3
# https://github.com/aairey/docker-firefox_sslv3
FROM centos:7

MAINTAINER aairey <airey.andy+docker@gmail.com>

# Dependencies tar, curl, glibc, libstdc++ already statisfied
RUN yum update -y && yum install -y bzip2 pango gtk2 libXt dbus-x11 alsa-lib libcanberra-gtk2 dejavu-lgc-sans-fonts
RUN yum clean all

RUN useradd -m firefox
USER firefox
WORKDIR /home/firefox

# Download and unpack Firefox version before v34 (disabled SSLv3)
RUN curl -sQL https://ftp.mozilla.org/pub/firefox/releases/33.1.1/linux-x86_64/en-GB/firefox-33.1.1.tar.bz2 | tar xvj 

ENTRYPOINT ["/home/firefox/firefox/firefox","-setDefaultBrowser"]
CMD ["https://www.ssllabs.com/ssltest/viewMyClient.html"]

