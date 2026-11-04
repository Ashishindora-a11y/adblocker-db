# adblocker-db

Aggregated **ad- and tracking-server database** for the
[adblockker](https://github.com/Ashishindora-a11y) project. It merges 25
public filter lists into one deduplicated, subdomain-collapsed set of domains,
rebuilt automatically every day.

> **503,565 blocked domains** &middot; built 2026-11-04T05:57:00.925Z &middot;
> checksum `c8e26e6feeb001ad`

This is a data repository. The extension and the command-line tools that consume
it live in the main project.

## Files

| File | What it is |
| --- | --- |
| [`database/blocklist/domains.txt`](https://raw.githubusercontent.com/Ashishindora-a11y/adblocker-db/main/database/blocklist/domains.txt) | The canonical list: one domain per line, each covering its subdomains. |
| [`database/blocklist/meta.json`](https://raw.githubusercontent.com/Ashishindora-a11y/adblocker-db/main/database/blocklist/meta.json) | Build metadata, per-source counts, and the checksum. |
| [`database/allowlist.txt`](https://raw.githubusercontent.com/Ashishindora-a11y/adblocker-db/main/database/allowlist.txt) | Domains never blocked (sign-in, payment, CAPTCHA, critical CDNs). |
| [`database/exports/hosts.txt`](https://raw.githubusercontent.com/Ashishindora-a11y/adblocker-db/main/database/exports/hosts.txt) | Same data as a `hosts` file (`0.0.0.0 domain`). |
| [`database/exports/dnsmasq.conf`](https://raw.githubusercontent.com/Ashishindora-a11y/adblocker-db/main/database/exports/dnsmasq.conf) | Same data as a dnsmasq configuration. |
| [`database/exports/adblockker.txt`](https://raw.githubusercontent.com/Ashishindora-a11y/adblocker-db/main/database/exports/adblockker.txt) | Same data in Adblock Plus syntax, for uBlock Origin / AdGuard. |
| [`database/community/discovered.txt`](https://raw.githubusercontent.com/Ashishindora-a11y/adblocker-db/main/database/community/discovered.txt) | Domains found by the extension's heuristic detector. |

## Use it directly

**Pi-hole / AdGuard Home** — add this as a blocklist URL:

```
https://raw.githubusercontent.com/Ashishindora-a11y/adblocker-db/main/database/exports/hosts.txt
```

**uBlock Origin / AdGuard** — add a custom filter list:

```
https://raw.githubusercontent.com/Ashishindora-a11y/adblocker-db/main/database/exports/adblockker.txt
```

**dnsmasq** — drop the config in and restart:

```
https://raw.githubusercontent.com/Ashishindora-a11y/adblocker-db/main/database/exports/dnsmasq.conf
```

## Sources

Compiled from these upstream lists. Each is the work of its own maintainers,
under its own licence; this repository only aggregates them.

| Source | Category | Domains | Unique | Licence |
| --- | --- | ---: | ---: | --- |
| EasyList | ads | 46,330 | 25 | GPLv3 / CC BY-SA 3.0 |
| EasyPrivacy | tracking | 47,275 | 10,243 | GPLv3 / CC BY-SA 3.0 |
| uBlock Origin — base filters | ads | 115 | 41 | GPLv3 |
| uBlock Origin — privacy | tracking | 108 | 44 | GPLv3 |
| uBlock Origin — badware risks | malware | 3,309 | 1,939 | GPLv3 |
| uBlock Origin — resource abuse | other | 3 | 2 | GPLv3 |
| uBlock Origin — quick fixes | ads | 8 | 5 | GPLv3 |
| Peter Lowe's Ad and tracking server list | ads | 3,563 | 20 | CC BY-NC-SA 4.0 (non-commercial use only) |
| AdGuard DNS filter | ads | 187,480 | 7,567 | GPLv3 |
| AdGuard Base filter | ads | 58,716 | 25 | GPLv3 |
| AdGuard Tracking Protection filter | tracking | 118,293 | 44 | GPLv3 |
| StevenBlack unified hosts (adware + malware) | ads | 77,757 | 3,523 | MIT |
| oisd blocklist (big) | ads | 232,109 | 66,458 | Free for personal use, attribution |
| anudeepND ad servers | ads | 42,342 | 6,271 | MIT |
| MVPS hosts file | ads | 8,728 | 2 | CC BY-NC-SA 4.0 (non-commercial use only) |
| 1Hosts (Lite) | ads | 202,868 | 46,546 | GPLv3 |
| AdAway default blocklist | mobile | 6,540 | 8 | CC BY 3.0 |
| Dan Pollock's hosts file | ads | 12,971 | 15 | Non-commercial, attribution |
| Frogeye first-party trackers | tracking | 14,737 | 5,849 | MIT |
| URLhaus malware filter (malware-filter mirror) | malware | 1,905 | 540 | GPLv3 (data: CC0 from abuse.ch) |
| DandelionSprout anti-malware hosts | malware | 11,767 | 3,512 | BSD-3-Clause |
| Spam404 main blacklist | malware | 8,122 | 6,013 | CC BY-SA 4.0 |
| Phishing Army blocklist | malware | 151,406 | 46,587 | CC BY-NC-SA 4.0 |
| EasyList Cookie List | annoyances | 320 | 182 | GPLv3 / CC BY-SA 3.0 |
| AdGuard Mobile Ads filter | mobile | 959 | 0 | GPLv3 |

## How it is built

Domains are normalised to punycode, validated, and checked against the Public
Suffix List so that a public suffix (`com`, `co.uk`) can never be blocked.
Low-trust sources are quarantined until a second source confirms a domain, and
subdomains already covered by a listed parent are collapsed away. See the main
project for the aggregator and the full pipeline.

## Licence

Aggregation scripts and metadata: MIT. The domain data is redistributed under
the licences of its upstream sources, listed in the table above and in
`database/blocklist/meta.json`. Several sources are non-commercial only; respect
their terms.

---

*Generated by `adbk`. Do not edit by hand — this repository is overwritten by
the daily update job.*
