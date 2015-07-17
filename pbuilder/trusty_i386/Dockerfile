FROM ubuntu:trusty
MAINTAINER Adam Sutton <dev@adamsutton.me.uk>

ENV _clean="rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*"
ENV _apt_clean="eval apt-get clean && $_clean"
ENV _apt_update="apt-get update -qq"
ENV _apt_install="apt-get install -qqy"

RUN $_apt_update && $_apt_install build-essential git   && $_apt_clean
RUN $_apt_update && $_apt_install debhelper             && $_apt_clean
RUN $_apt_update && $_apt_install pkg-config            && $_apt_clean
RUN $_apt_update && $_apt_install python                && $_apt_clean
RUN $_apt_update && $_apt_install wget curl             && $_apt_clean

RUN $_apt_update && %_apt_install libc6-dev-i386        && $_apt_clean

RUN mkdir /build /out

RUN cd /build\
  && git clone https://github.com/tvheadend/tvheadend.git tvheadend\
  && cd tvheadend\
  && ARCH=i386 CFLAGS=-m32 ../configure\
  && make

VOLUME /build
