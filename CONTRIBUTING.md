# Contributing

Thanks for looking. A few ground rules, mostly to keep the project on the right side of the line it has drawn for itself:

- **Never attach game files**, chunk lists (`*_cdn.xpak`), cache files, mirror contents, decoded textures or screenshots that show them. If a capture is needed to
  explain a bug, describe it or trim it to the lines that matter.
- The tools stay on the data and network path. Pull requests that patch or hook the game, read its memory, touch drivers or anti-cheat, or get around licensing or
  login will be closed.
- Be considerate to the CDN: no change should raise the default request rate or connection count, or remove the User-Agent or the back-off on 429/503.
- Standard library only. If you really need a dependency, open an issue first.
- Run `python -m unittest discover -s tools/tests` before sending a change. The tests use fake chunk lists and a fake CDN on localhost, never the real game or
  server.
- Python 3.10+, Windows paths and behaviour first. Linux/Wine reports are interesting but not supported yet.

Useful reports: another PC where the IPv6-only lookup shows up (or does not), which Windows version and ISP type, and what the Doctor tab says.
