FROM alpine:3.11.3
MAINTAINER Shinya Murakami <maya2250.dev@gmail.com>

ARG PXE_SERVER_IP="192.168.0.6"
ARG DHCP_RANGE="192.168.0.201,192.168.0.230"

RUN set -x && \
        apk add --quiet dnsmasq

COPY dnsmasq.conf /etc/dnsmasq.conf
COPY grub.cfg /srv/tftp/grub/grub.cfg
COPY grubnetx64.efi.signed /srv/tftp/grubnetx64.efi.signed
COPY netboot.tar.gz /tmp/netboot.tar.gz

RUN set -x && \
        tar zxf /tmp/netboot.tar.gz -C /srv/tftp && \
        sed -i -e "s/DHCP_RANGE/${DHCP_RANGE}/g" /etc/dnsmasq.conf && \
        sed -i -e "s/PXE_SERVER_IP/${PXE_SERVER_IP}/g" /srv/tftp/grub/grub.cfg

CMD ["dnsmasq", "--no-daemon"]
