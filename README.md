# ProtoCloack2

High-performance Stratum v1 mining proxy with an encrypted client/server
tunnel. Public releases are binary-only; source code is not published.

## Quick Links

- Releases (download binaries): <https://github.com/qianfan75/ProtoCloack2/releases>
- Install: [INSTALL.md](INSTALL.md)
- Configuration: [CONFIG.md](CONFIG.md)
- Changelog: [CHANGELOG.md](CHANGELOG.md)
- Security policy: [SECURITY.md](SECURITY.md)
- License: [LICENSE](LICENSE)

## Components

- `server`: proxy engine, web UI, pool management, statistics, service fee and
  optional operator user fee scheduling.
- `client`: lightweight encrypted tunnel endpoint for forwarding local miner
  traffic to a ProtoCloack2 server.

## Security

The web UI is reachable from the host's network interfaces immediately after
installation. The only built-in protection at that point is the generated web
credential printed by the installer and stored in
`/root/.protocloack2-bootstrap-secrets`.

You are expected to restrict access by IP, VPN, firewall, security group, or an
authenticated reverse proxy before exposing this host to untrusted networks.
