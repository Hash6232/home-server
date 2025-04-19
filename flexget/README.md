# Flexget

There's nothing much to do with Flexget. It's basically just a single `.yml `file. The Flexget daemon will run based on the schedule you set and matching titles will be downloaded as `.torrent` files in the `download` path. The main reason you might want to use Flexget over a simple RSS parser is that it maintains a database and intelligently skips duplicate episodes while also keeping track of them in its history.

## Broken Scheduler in latest Flexget versions

I am currently using version `3.13.0` instead of the latest due to a [bug](https://github.com/Flexget/Flexget/issues/4338#issuecomment-2794544772) with the scheduler. At the time of writing it hasn't been fixed yet so pay attention on what version of Flexget you use if you plan on using its scheduler.

## config.yml

Here's a sample of the config file I use. No fancy configurations, authentications or tokens required. Nice and simple download of torrents and qBittorrent will take care of everything using Watch directories. In essence the config will use `anime` as template for the task `nyaa` meaning it will import the settings specified in the template below. The template will save the downloaded torrents in a specified path, will parse a list of rss inputs and will set custom settings for the `1080p` category which is a built-in Flexget category for all the results with a `1080p` tag. In my case I am using it as a surrogate of a missing built-in `default` category so that by default Flexget will only download results from `Erai-raws` and `Subsplease` and only fallback to anything else when manually required (notice the `others` category in `series`). Finally, the scheduler will execute every 30 minutes using a cron-like syntax and will run the tasks specified (using `*` will run all the tasks).

```yaml
tasks:
  nyaa:
    template: anime
    series:
      1080p:
        - "Your favorite anime"
        - "That one title: the animation"
      others:
        - "Some niche anime not ripped from CR"

templates:
  anime:
    download: /data/anime
    inputs:
      - rss: https://nyaa.si/?page=rss&c=1_2&f=0
      - rss: https://nyaa.si/?page=rss&c=1_2&f=0&u=Erai-raws
      - rss: https://nyaa.si/?page=rss&c=1_2&f=0&u=subsplease
    series:
      settings:
        1080p:
          from_group:
            - Erai-raws
            - Subsplease

schedules:
  - tasks: '*'
    schedule:
      minute: "*/30"
```