# On-demand texture streaming never connects on IPv4-only PCs

| | |
|---|---|
| Product | Modern Warfare (cod26) PC client, single-player campaign, engine 13.1 |
| Area | streaming / networking |
| Severity | major for the people it hits: only the lowest texture tier is ever used |
| Status | reproduced on one machine; I'd like a second independent repro |

## Summary

The texture streamer tries to fetch higher-resolution texture pieces from `cod-assets.cdn.callofduty.com` while you play. On a PC with no IPv6 connectivity it
looks the name up, gets an answer, and then never opens a TCP connection. The streaming cache stays empty and every surface keeps the textures that ship with the
game, whatever the texture quality and "on-demand texture streaming" settings say.

## Environment

Windows (64-bit), 12 GB GPU, ordinary IPv4-only home internet (no global IPv6 address), 2560x1440.

## How to reproduce

1. Set texture quality to the highest value and on-demand texture streaming to its best setting.
2. Load a campaign mission and play for five minutes or more.
3. In parallel, capture DNS lookups (Windows *DNS-Client/Operational* log, or ETW) and packets (`pktmon start --capture --comp nics`, then `pktmon etl2txt -v 2`;
   the text output is UTF-16).
4. Look for the CDN name: you will see bursts of lookups, answers of the form `::ffff:a.b.c.d`, and **no SYN packets to port 80 or 443** from the game.
5. The `xpak_cache` folder stays empty.

## Evidence

- The lookup asks for IPv6 only (`getaddrinfo` with `AF_INET6` and the V4-mapped flag). The answer is an IPv4 address written as `::ffff:a.b.c.d`.
- A Windows IPv6 socket has `IPV6_V6ONLY` switched on by default, and with it on, `connect()` to a `::ffff:` address fails with WinError 10049. No packet leaves the
  machine. With `IPV6_V6ONLY` turned off the same connect works.
- Control experiment: a hosts entry `::1 cod-assets.cdn.callofduty.com` plus a loopback proxy that forwards over IPv4. The unmodified game connected within a few
  minutes and filled its cache (3,197 requests, about 1.5 GB in the first half hour).

## Expected and actual

Expected: fall back to IPv4 (or use a dual-stack socket) and download. Actual: nothing is sent, no error is shown, textures stay low.

## Workaround

This toolkit: a marked hosts-file entry (loopback for the CDN name) and a local forwarding proxy. See the README and [USAGE.md](USAGE.md).
