# Install

## First configuration

- Download, write and launch the Debian installation `.iso` however you prefer
- Partition the main drive in such a way that `/home` has the majority of space dedicated to it:
    - 500MB EFI partition
    - 10-20GB root partition
    - rest dedicated to `/home`
- Proceed until you reach Tasksel and <u>**o n l y**</u> install `SSH server` and `standard system utilities`
- Finish the installation process, reboot and login as root
- Set a static IP for your server in `/etc/network/interfaces`:
    ```
    iface enp0s31f6 inet static
    address 192.168.1.10
    netmask 255.255.255.0
    gateway 192.168.1.1
    ```
- Enable root SSH login in `/etc/ssh/sshd_config` by appending `PermitRootLogin yes` and shutdown the server
- Finish plugging what you need into your server, turn it on and login via SSH as root from a client

## Docker

TODO

## Services

TODO

## Media sharing

TODO

## DDNS and Wireguard

TODO