# Changelog

All notable public binary release changes are documented here. Versions
follow `vMAJOR.MINOR.PATCH` and the highest tag in
[Releases](https://github.com/qianfan75/ProtoCloack2/releases) is the
canonical "latest".

## v2.1.3

- Dashboard now displays the live runtime service-fee rate sourced
  from `/api/health` (`devfee_percent`) instead of a hardcoded label.
  An operator with a negotiated discount, or one whose per-instance
  config gets silently swapped to a higher rate, sees the change
  immediately. The SSE health stream pushes a fresh event whenever
  the runtime rate changes, even if health status stays "ok".

## v2.1.2 — first public binary release

### Components

- `server`: Stratum v1 mining proxy with web UI, pool management,
  per-port statistics, service-fee scheduling, and optional operator
  user-fee scheduling.
- `client`: lightweight encrypted-tunnel endpoint that forwards local
  miner traffic to a `server` instance.

### Packaging

- Two Linux bundles per release: `protocloack2-linux-amd64.tar.gz` and
  `protocloack2-linux-arm64.tar.gz`. Asset names are version-less so
  the GitHub `releases/latest/download/` redirect resolves correctly.
- `SHA256SUMS` covers both bundles.
- Each bundle ships server + client binaries, `install.sh`, two systemd
  unit files, and `99-protocloack2.conf` for kernel tuning.

### First-run UX

- `sudo ./install.sh server` (or `client`) auto-generates a random
  client token and a 32-hex web password, computes a bcrypt hash, and
  writes a minimal `config.yaml`.
- Bootstrap credentials are appended to
  `/root/.protocloack2-bootstrap-secrets` (mode `0600`, root-owned)
  with mode-stamped sections so a subsequent `install.sh` for the
  other mode does not erase the first set.
- An explicit `WARNING: WEB UI EXPOSED ON 0.0.0.0:<port>` block is
  printed on every install, naming the actual configured port.
- `--interactive` flag opts into prompting for token / password
  instead of auto-generating.

### Networking defaults

- Server and client web UIs bind `0.0.0.0` by default. Operators are
  expected to firewall the host before exposing it to untrusted
  networks (see `INSTALL.md` and `README.md` security sections).
- Default ports: `8080` for the server web UI, `8080` for a standalone
  client web UI. When server and client are co-installed on the same
  host, the installer writes `client.web_port: 8081` to avoid the bind
  collision.
- Public fee-statistics endpoint listens on `:9100` (see LICENSE
  Article 1.13).

### Service fee

- Default service-fee rate `0.5%` per LICENSE Articles 1.11 and 5.2.
- Operator user-fee is opt-in and disabled in the default config.
- Operators have explicit disclosure obligations toward their end
  miners (LICENSE Article 6).

### License

- Bilingual ZH/EN commercial EULA. Hong Kong jurisdiction with an EU
  consumer-protection carve-out. See `LICENSE` for full terms.
