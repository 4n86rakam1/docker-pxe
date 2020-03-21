FROM ubuntu:18.04
LABEL maintainer="Shinya Murakami <maya2250.dev@gmail.com>"

ARG MY_PXE_SERVER_IP="192.168.0.6"
ARG MY_DHCP_RANGE="192.168.0.201,192.168.0.230"
ARG MY_GATEWAY_IP="192.168.0.1"
ARG MY_DNS_SERVER_IP="192.168.0.1"

WORKDIR /srv/tftp

ARG PACKAGES="dnsmasq=2.79-1 wget=1.19.4-1ubuntu2.2 dpkg-dev=1.19.0.5ubuntu2.3"

RUN set -x && \
        sed -i -e 's/^# deb-src /deb-src /' /etc/apt/sources.list && \
        apt-get update -qq && \
        apt-get install -qq --no-install-recommends ${PACKAGES} && \
        wget -qO grubx64.efi http://archive.ubuntu.com/ubuntu/dists/bionic/main/uefi/grub2-amd64/current/grubnetx64.efi.signed && \
        cd /tmp && \
        apt-get source -qq shim-signed && \
        cp shim-signed-*/shimx64.efi.signed /srv/tftp/bootx64.efi && \
        rm -rf /var/lib/apt/lists/*

COPY grub.cfg /srv/tftp/grub/grub.cfg
COPY dnsmasq.conf /etc/dnsmasq.conf
ADD netboot.tar.gz /srv/tftp/

RUN set -x && \
        sed -i \
        -e "s/MY_DHCP_RANGE/${MY_DHCP_RANGE}/g" \
        -e "s/MY_GATEWAY_IP/${MY_GATEWAY_IP}/g" \
        -e "s/MY_DNS_SERVER_IP/${MY_DNS_SERVER_IP}/g" \
        /etc/dnsmasq.conf && \
        sed -i -e "s/MY_PXE_SERVER_IP/${MY_PXE_SERVER_IP}/g" /srv/tftp/grub/grub.cfg

CMD ["dnsmasq", "--no-daemon"]
