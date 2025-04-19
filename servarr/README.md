# Servarr

The servarr suite will be hosted on the `servarr.thinkcentre.home` subdomain and through subdirectories thanks to Caddy.

## Autobrr - `https://servarr.thinkcentre.home/autobrr`

You'll have to edit this line in `config.toml`:
```toml
baseUrl = "/autobrr/"
```

## Prowlarr - `https://servarr.thinkcentre.home/prowlarr`

You'll have to edit this line in `config.xml`:
```xml
<Config>
    <UrlBase>/prowlarr/</UrlBase>
</Config>
```