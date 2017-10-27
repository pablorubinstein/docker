FROM ubuntu:xenial
MAINTAINER pablor

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update && \
    apt-get install apt-utils python -y

RUN mkdir -p /www/esxi
COPY unattended.ks.sample /www/esxi/unattended.ks
WORKDIR /www

EXPOSE 8000/TCP 
ENTRYPOINT ["/usr/bin/python"]
CMD ["-m", "SimpleHTTPServer"]
