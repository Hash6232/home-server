# SSHD

I allowed root login to configure the entirety of my system from SSH after the first installation. I am well aware of the security implications, I do not plan on using a normal user for maintenance tasks and in fact I force them into their SFTP jail because this is a media server first and foremost.

## sshd_config.d

New SFTP configuration files are stored in the `/etc/ssh/sshd_config.d/` directory.

The configuration files in this directory will allow sftp access to:
- `/srv/docker` for the `docker` system user for maintenance/update reasons.
- `/home/<username>/files` for all the users in the `sftpusers` group.