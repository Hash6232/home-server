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

### SFTP - [Documentation](https://web.archive.org/web/20241114203204/https://www.turnkeylinux.org/docs/set-up-sftp-chroot-jail)

Add an user to a dedicated SFTP group

```sh
# Add a dedicated group for SFTP access
groupadd sftpusers
# Add your main user to the sftpusers group..
usermod -aG sftpusers my-user
usermod -s /usr/sbin/nologin my-user
# ..or optionally create a new user with no login access
useradd -G sftpusers -s /usr/sbin/nologin friend-user
# and set a password for SFTP only access
passwd friend-user
```

Configure their SFTP jail

```sh
# Create the user's sftp root
mkdir -p /home/username/files
# Change ownership to root for sftp jail to work
chown root:root /home/username
# Make sure the user has access to the new root
chown username:username /home/username/files
# And that nobody but them can access to it
chmod 700 /home/username/files
# Finally set the new root as home directory
usermod -d /home/username/files username
```

Replace the following default line in `/etc/ssh/sshd_config`

```
# From this
Subsystem       sftp    /usr/lib/openssh/sftp-server
# to this
Subsystem       sftp    internal-sftp
```

Use the config files in the `ssh` directory in this repository as template

```sh
# Finally restart the SSH server to load the new configuration
systemctl restart sshd
```

### Samba - [Documentation](https://wiki.debian.org/Samba/ServerSimple)

Optionally add a samba share for easy access on Windows clients

```sh
# Create a companion samba user with the same name as your user
smbpasswd -a username
```

Append a new samba share to `/etc/samba/smb.conf`
```conf
[anameofyourchoice]
   read only = no
   path = /home/username/files
   guest ok = no
   valid user = username
```
Restart samba with `systemctl restart smbd` and access the directory with `\\server-ip\anameofyourchoice`.

## DDNS and Wireguard

TODO