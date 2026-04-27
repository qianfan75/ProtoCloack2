# Configuration

ProtoCloack2 stores runtime configuration at:

```text
/opt/protocloack2/data/config.yaml
```

## Server

Important server fields:

- `server.web_port`: web UI port, default `8080`.
- `server.web_listen`: web UI bind address. Public binary installs use
  `0.0.0.0`.
- `server.web_password_hash`: bcrypt hash for the server web UI password.
- `server.client_token`: shared secret used by encrypted clients.
- `ports`: Stratum listener definitions.
- `user_fee`: optional operator-controlled user fee configuration.

## Client

Important client fields:

- `client.token`: shared tunnel token.
- `client.web_listen`: client web UI bind address. Public binary installs use
  `0.0.0.0`.
- `client.web_port`: client web UI port. Default `8080`. The installer writes
  `8081` automatically when a server section already lives in the same
  `config.yaml` (co-installed deployments) so the two web UIs do not collide;
  set it explicitly to override.
- `client.listeners`: local listen addresses and upstream server targets.
- `client.compress`: encrypted tunnel compression toggle.

## Reloads

Most server pool and fee settings can be reloaded through the web UI or service
reload. Listener bind-address changes and binary upgrades require a service
restart.

Always keep a copy of the previous working `config.yaml` before large edits.
