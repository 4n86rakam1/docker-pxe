# docker-pxe
## Spec

- PXE Server: docker-compose on host machine
  - NOTE: Release ports; 67/udp, 69/udp, 80/tcp
- PXE Client: Ubuntu 18.04(bionic) server

## Usage

1. Download the UEFI signed grub image and netboot.tar.gz archive into hdpc directory

   ``` bash
     curl -sSLo dhcp/grubnetx64.efi.signed http://archive.ubuntu.com/ubuntu/dists/bionic/main/uefi/grub2-amd64/current/grubnetx64.efi.signed
     curl -sSLo dhcp/netboot.tar.gz http://archive.ubuntu.com/ubuntu/dists/bionic-updates/main/installer-amd64/current/images/netboot/netboot.tar.gz
   ```

2. Download iso and extract into extracted_iso directory

   ``` bash
   curl -sSLo http/ubuntu-18.04.4-server-amd64.iso http://cdimage.ubuntu.com/releases/18.04.4/release/ubuntu-18.04.4-server-amd64.iso

   sudo mount -o loop,ro ./http/ubuntu-18.04.4-server-amd64.iso /mnt
   cp -r /mnt/* ./http/extracted_iso/
   # or
   sudo mount -o loop,ro ./http/ubuntu-18.04.4-server-amd64.iso ./http/extracted_iso/
   ```

3. `docker-compose up -d`

# References
- [UEFI/PXE-netboot-install - Ubuntu Wiki](https://wiki.ubuntu.com/UEFI/PXE-netboot-install)
