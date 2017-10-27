FROM ubuntu:xenial
MAINTAINER pablor

# setting this as to avoid getting error:
#   debconf: unable to initialize frontend: Dialog
# see http://github.com/phusion/baseimage-docker/issues/58
ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update && \
    apt-get install apt-utils isc-dhcp-server -y

COPY dhcpd.conf.sample /etc/dhcp/dhcpd.conf
RUN touch /var/lib/dhcp/dhcpd.leases

EXPOSE 67/UDP
ENTRYPOINT ["/usr/sbin/dhcpd"]
CMD ["-f", "-4", "-cf", "/etc/dhcp/dhcpd.conf"]
