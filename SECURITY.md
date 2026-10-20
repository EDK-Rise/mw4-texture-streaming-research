# Security

This is a hobby research project with no hosted service. The parts that deserve care are the ones that change your system: the hosts-file editor
(`tools/ccshosts.py`, run elevated only for that step) and the local proxy, which listens on loopback only.

If you find a problem in them (for example a way to make the hosts editor change lines outside its marked block, or the proxy reachable from another machine),
please report it privately through GitHub's *Report a vulnerability* button on this repository rather than in a public issue.

Not in scope: vulnerabilities in the game, its servers or its anti-cheat. Please report those to the vendor.
