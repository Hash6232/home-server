# qBittorrent - `https://torrent.thinkcentre.home`

Its main purpose will be downloading seasonal anime by importing anything that Flexget downloads into a watch folder and auto-managing it so that any torrent in the anime category is removed from the list (not deleted) as soon as the ratio hits value `2.0`. Its secondary purpose is to farm private tracker ratios by pairing it with autobrr but this is more of a velleity of mine.

The configuration uses the recommended values from the Deluge [documentation](https://deluge-torrent.org/userguide/bandwidthtweaking/) along with some tweaks for private trackers because some of them will refuse to connect to your client if it uses well known torrenting ports that might be blocked by ISPs.

Furthermore, in order to work seamlessly with Flexget without using any credentials, a watch directory is used. Version 5.0.4 (the latest stable at the time of writing) still won't let you further customize watch directories through the web-ui meaning that after adding a watched directory you'll have to stop the container and manually edit the `watched_folders.json` file to specify custom management rules for it:

```json
{
    "/flexget/anime": {
        "add_torrent_params": {
            "category": "anime",
            "download_limit": -1,
            "download_path": "",
            "inactive_seeding_time_limit": -2,
            "operating_mode": "AutoManaged",
            "ratio_limit": 2,
            "save_path": "/downloads/anime",
            "seeding_time_limit": -2,
            "share_limit_action": "Remove",
            "skip_checking": false,
            "ssl_certificate": "",
            "ssl_dh_params": "",
            "ssl_private_key": "",
            "tags": [
            ],
            "upload_limit": -1,
            "use_auto_tmm": false
        },
        "recursive": false
    }
}
```