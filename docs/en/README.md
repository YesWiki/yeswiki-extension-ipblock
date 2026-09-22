# ipblock extension

Blocks editing from the IP addresses of selected countries, or from specific
addresses.

Reading stays open: only write access is refused.

## Configuration

In `wakka.config.php`, or through the cog wheel then Site management, "conf. file" tab.

| Key | Format | Purpose |
|---|---|---|
| `ipblock_blocked_countries` | array of 2-letter country codes | countries whose IPs may not edit |
| `ipblock_blocked_ips` | array of IP addresses | specific addresses to refuse |

```php
'ipblock_blocked_countries' => ['ID', 'MY'],
'ipblock_blocked_ips' => ['203.0.113.7', '198.51.100.22'],
```

## How matching works

The extension carries its own database of address ranges per country, hence its size:
by far the largest extension repository, around 60,000 lines of PHP. No external
service is queried, so nothing leaks, but the database ages with the repository and is
only as fresh as the last commit.

## Word of caution

Blocking works on the IP the server sees. Behind a proxy or a CDN that IP is the
proxy's for everyone: make sure the web server passes the real address through before
relying on this filter.
