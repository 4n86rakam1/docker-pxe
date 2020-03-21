![Build docker image](https://github.com/maya2250/docker-pxe/workflows/Build%20docker%20image/badge.svg?branch=master)

# docker-pxe
## Spec

- PXE Server: docker-compose on host machine
  - NOTE: Release ports; 67/udp, 69/udp
- PXE Client: Ubuntu 18.04(bionic) server
- Support UEFI Secure Boot

## Usage

1. Download netboot.tar.gz archive into hdpc directory

   ``` bash
     curl -sSLo dhcp/netboot.tar.gz http://archive.ubuntu.com/ubuntu/dists/bionic-updates/main/installer-amd64/current/images/netboot/netboot.tar.gz
   ```

1. `docker-compose up -d`

# References
- [UEFI/PXE-netboot-install - Ubuntu Wiki](https://wiki.ubuntu.com/UEFI/PXE-netboot-install)
- [UEFI/SecureBoot/PXE-IPv6 - Ubuntu Wiki](https://wiki.ubuntu.com/UEFI/SecureBoot/PXE-IPv6)
