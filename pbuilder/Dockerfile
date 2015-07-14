FROM ubuntu-debootstrap:14.04
MAINTAINER Adam Sutton <dev@adamsutton.me.uk>

ENV _clean="rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*"
ENV _apt_clean="eval apt-get clean && $_clean"

RUN apt-get update -qq && apt-get install -qqy build-essential git pbuilder\
  && $_apt_clean

RUN apt-get update -qq && apt-get install -qqy debhelper && $_apt_clean

RUN apt-get update -qq && apt-get install -qqy ubuntu-dev-tools && $_apt_clean

RUN cap-add=SYS_ADMIN pbuilder-dist trusty i386 create


RUN mkdir /build /out \
  && git clone https://github.com/tvheadend/tvheadend.git /build/tvheadend\
  && cd /build/tvheadend\
  && sed -i "s/-sgpg -pgpg//" ./support/pbuilder
  && TVH_BUILD="trusty:i386" ./support/pbuilder
