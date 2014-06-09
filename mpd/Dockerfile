FROM ubuntu:trusty
MAINTAINER Todd Bealmear <todd@t0dd.io>

RUN apt-get update --fix-missing
RUN apt-get install -y mpd

ADD mpd.conf /etc/mpd.conf

EXPOSE 6600

CMD mpd --no-daemon --stdout -v /etc/mpd.conf
