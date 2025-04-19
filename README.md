# Home Server Setup
This repository will roughly show the setup process I used for my own home server and its main configuration files.

## Purpose
- Media server
- Self-hosting hub
- Wireguard server
- Ad blocker

## Specs
- Lenovo ThinkCentre M710q - 4GB RAM - 1TB APPLE HDD HTS541
- Intel(R) Celeron(R) CPU G3900T @ 2.60GHz - x86_64
- Debian GNU/Linux 12 (bookworm)

## Toolkit
- **SSH**: A secure protocol for encrypted remote login and data transfer.
- **Samba**: A file sharing service tailored for Windows clients.
- **[ranger](https://github.com/ranger/ranger)**: A VIM-inspired filemanager for the console.
- **[Docker](https://docs.docker.com/engine/install/debian/#install-using-the-repository)**: A containerization platform for services deployment.

## Services
- **[Caddy](https://caddyserver.com/)**: A reverse-proxy to pair each service to my local TLD.
- **[Pihole](https://pi-hole.net/)**: A network-level ad blocker and DNS proxy for my local TLD.
- **[Wireguard](https://www.wireguard.com/)**: A fast, secure, and modern VPN to expose my services.
- **[DuckDNS](https://www.duckdns.org/)**: A free dynamic DNS hosted on AWS.
- **[qBittorrent](https://www.qbittorrent.org/)**: A cross-platform and features rich torrent client.
- **[Flexget](https://flexget.com/)**: A smart automation tool to download seasonal anime.
- **[Autobrr](https://autobrr.com/)**: A tool to farm private trackers and "climb the ladder".
- **[Prowlarr](https://prowlarr.com/)**: An indexer manager for both torrents and usenet.

## Disclaimer
This repository is tailored to my personal setup. There is no guarantee this is going to be a drop-in replacement for your own server.