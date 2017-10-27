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
ARG MY_IP
ARG MY_NETWORK
RUN sed -i "s/MY_IP/$MY_IP/g" /etc/dhcp/dhcpd.conf && \
    sed -i "s/MY_NETWORK/$MY_NETWORK/g" /etc/dhcp/dhcpd.conf

EXPOSE 67/UDP
ENTRYPOINT ["/usr/sbin/dhcpd"]
CMD ["-f", "-4", "-cf", "/etc/dhcp/dhcpd.conf"]
