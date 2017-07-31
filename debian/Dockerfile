# Dockerfile to create a container with a Firefox version that still supports SSLv3
# https://github.com/aairey/docker-firefox_sslv3
FROM debian:8

MAINTAINER aairey <airey.andy+docker@gmail.com>

# Build-time metadata as defined at http://label-schema.org
ARG BUILD_DATE
ARG VCS_REF
ARG VERSION=debian

LABEL org.label-schema.build-date=$BUILD_DATE \
      org.label-schema.name="firefox_sslv3" \
      org.label-schema.description="Run Firefox with legacy SSLv3 support in Docker" \
      org.label-schema.url="https://www.firefox.org/" \
      org.label-schema.vcs-ref=$VCS_REF \
      org.label-schema.vcs-url="https://github.com/aairey/docker-firefox_sslv3" \
      org.label-schema.vendor="None" \
      org.label-schema.version=$VERSION \
      org.label-schema.schema-version="1.0"

# Set noninteractive during build to statisfy APT
ARG DEBIAN_FRONTEND=noninteractive

# Dependencies tar, curl, glibc, libstdc++ already statisfied
RUN apt-get update && \
    apt-get install -y --no-install-recommends apt-utils && \
    apt-get upgrade -y
# Took dependenies from iceweasel here and added libcanberra-gtk-module
RUN apt-get install -y \
    bzip2 ca-certificates curl dbus dconf-gsettings-backend dconf-service \
    dictionaries-common emacsen-common firefox-esr fontconfig fontconfig-config \
    fonts-dejavu-core glib-networking glib-networking-common \
    glib-networking-services gsettings-desktop-schemas gstreamer1.0-libav \
    gstreamer1.0-plugins-base gstreamer1.0-plugins-good gstreamer1.0-x \
    hicolor-icon-theme hunspell-en-us i965-va-driver iceweasel iso-codes \
    krb5-locales libaa1 libalgorithm-c3-perl libarchive-extract-perl libasound2 \
    libasound2-data libatk1.0-0 libatk1.0-data libavahi-client3 \
    libavahi-common-data libavahi-common3 libavc1394-0 libavcodec56 \
    libavformat56 libavresample2 libavutil54 libbsd0 libcaca0 libcairo-gobject2 \
    libcairo2 libcap-ng0 libcdparanoia0 libcgi-fast-perl libcgi-pm-perl \
    libclass-c3-perl libclass-c3-xs-perl libcpan-meta-perl libcups2 libcurl3 \
    libdata-optlist-perl libdata-section-perl libdatrie1 libdbus-1-3 \
    libdbus-glib-1-2 libdconf1 libdrm-intel1 libdrm-nouveau2 libdrm-radeon1 \
    libdrm2 libdv4 libedit2 libelf1 libevent-2.0-5 libexpat1 libfcgi-perl \
    libffi6 libflac8 libfontconfig1 libfreetype6 libgdbm3 libgdk-pixbuf2.0-0 \
    libgdk-pixbuf2.0-common libgl1-mesa-dri libgl1-mesa-glx libglapi-mesa \
    libglib2.0-0 libglib2.0-data libglu1-mesa libgmp10 libgnutls-deb0-28 libgpm2 \
    libgraphite2-3 libgsm1 libgssapi-krb5-2 libgstreamer-plugins-base1.0-0 \
    libgstreamer1.0-0 libgtk2.0-0 libgtk2.0-bin libgtk2.0-common libgudev-1.0-0 \
    libharfbuzz0b libhogweed2 libhunspell-1.3-0 libice6 libidn11 libiec61883-0 \
    libjack-jackd2-0 libjasper1 libjbig0 libjpeg62-turbo libk5crypto3 \
    libkeyutils1 libkrb5-3 libkrb5support0 libldap-2.4-2 libllvm3.5 \
    liblog-message-perl liblog-message-simple-perl libmodule-build-perl \
    libmodule-pluggable-perl libmodule-signature-perl libmp3lame0 \
    libmro-compat-perl libnettle4 libogg0 libopenjpeg5 libopus0 liborc-0.4-0 \
    libp11-kit0 libpackage-constants-perl libpango-1.0-0 libpangocairo-1.0-0 \
    libpangoft2-1.0-0 libparams-util-perl libpciaccess0 libpixman-1-0 libpng12-0 \
    libpod-latex-perl libpod-readme-perl libproxy1 libraw1394-11 \
    libregexp-common-perl librtmp1 libsamplerate0 libsasl2-2 libsasl2-modules \
    libsasl2-modules-db libschroedinger-1.0-0 libshout3 libsm6 \
    libsoftware-license-perl libsoup2.4-1 libspeex1 libsqlite3-0 libssh2-1 \
    libssl1.0.0 libstartup-notification0 libsub-exporter-perl \
    libsub-install-perl libtag1-vanilla libtag1c2a libtasn1-6 libterm-ui-perl \
    libtext-soundex-perl libtext-template-perl libthai-data libthai0 libtheora0 \
    libtiff5 libtxc-dxtn-s2tc0 libv4l-0 libv4lconvert0 libva1 libvdpau1 \
    libvisual-0.4-0 libvisual-0.4-plugins libvorbis0a libvorbisenc2 libvpx1 \
    libwavpack1 libx11-6 libx11-data libx11-xcb1 libx264-142 libxau6 \
    libxcb-dri2-0 libxcb-dri3-0 libxcb-glx0 libxcb-present0 libxcb-render0 \
    libxcb-shm0 libxcb-sync1 libxcb-util0 libxcb1 libxcomposite1 libxcursor1 \
    libxdamage1 libxdmcp6 libxext6 libxfixes3 libxi6 libxinerama1 libxml2 \
    libxrandr2 libxrender1 libxshmfence1 libxt6 libxv1 libxvidcore4 libxxf86vm1 \
    openssl perl perl-modules rename sgml-base shared-mime-info strace ucf \
    va-driver-all vdpau-va-driver x11-common xdg-user-dirs xml-core \
    libcanberra-gtk-module
RUN apt-get clean

RUN useradd -m firefox
USER firefox
WORKDIR /home/firefox

# Download and unpack Firefox version before v34 (disabled SSLv3)
RUN curl -sQL https://ftp.mozilla.org/pub/firefox/releases/33.1.1/linux-x86_64/en-GB/firefox-33.1.1.tar.bz2 | tar xvj 

ENTRYPOINT ["/home/firefox/firefox/firefox","-setDefaultBrowser"]
CMD ["https://www.ssllabs.com/ssltest/viewMyClient.html"]

