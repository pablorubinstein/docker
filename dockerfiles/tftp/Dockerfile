FROM ubuntu:xenial
MAINTAINER pablor

# setting this as to avoid getting error:
#   debconf: unable to initialize frontend: Dialog
# see http://github.com/phusion/baseimage-docker/issues/58
ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update && \
    apt-get install apt-utils tftpd-hpa xorriso rename -y

COPY Vmware-ESXi-6.0.0-2494585-Custom-Cisco-6.0.0.3.iso /tmp/

WORKDIR /var/lib/tftpboot
RUN xorriso -osirrox on -indev /tmp/Vmware-ESXi-6.0.0-2494585-Custom-Cisco-6.0.0.3.iso -ecma119_map lowercase -extract / esxi && \
    find esxi -depth -exec rename 's!([^/]*\Z)!lc($1)!e' {} + -print 

RUN mkdir pxelinux.cfg
COPY pxelinux.0.sample pxelinux.0
COPY default.sample pxelinux.cfg/default
COPY boot.cfg.sample esxi/boot.cfg

RUN rm /tmp/Vmware-ESXi-6.0.0-2494585-Custom-Cisco-6.0.0.3.iso

EXPOSE 69/UDP
ENTRYPOINT ["/usr/sbin/in.tftpd"]
CMD ["-L", "-s", "/var/lib/tftpboot"]
