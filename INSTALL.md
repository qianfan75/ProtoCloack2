# Install

## Requirements

- Linux amd64 or arm64
- systemd
- root privileges for installation
- `htpasswd` from `apache2-utils` / `httpd-tools`, or Python with the `bcrypt`
  module, so the installer can generate a bcrypt web password hash

## Download

Asset names are version-less, so the GitHub `releases/latest/download/`
redirect always points at the most recent published release:

```bash
wget https://github.com/qianfan75/ProtoCloack2/releases/latest/download/protocloack2-linux-amd64.tar.gz
wget https://github.com/qianfan75/ProtoCloack2/releases/latest/download/SHA256SUMS
sha256sum -c SHA256SUMS
```

Use `protocloack2-linux-arm64.tar.gz` on ARM servers. To pin a specific
version, replace `latest` with a tag (e.g. `v0.1.0`) and adjust both URLs
accordingly. Available tags: <https://github.com/qianfan75/ProtoCloack2/releases>.

## Install Server

```bash
tar xzf protocloack2-linux-amd64.tar.gz
cd protocloack2-linux-amd64
sudo ./install.sh server
```

The installer creates `/opt/protocloack2`, writes a minimal config when needed,
installs the systemd unit, starts the service, and writes bootstrap credentials
to:

```text
/root/.protocloack2-bootstrap-secrets
```

Save those credentials to a password manager and remove the file when you no
longer need it.

## Install Client

```bash
tar xzf protocloack2-linux-amd64.tar.gz
cd protocloack2-linux-amd64
sudo ./install.sh client
```

(Same archive as for the server — both binaries ship in one bundle.)

Client mode installs the encrypted tunnel client service and creates a tunnel
token if one is missing.

## Security

The web UI is reachable from the host's network interfaces immediately after
installation. The only built-in protection is the generated credential.

You are expected to restrict access by IP, VPN, or firewall before exposing
this host to untrusted networks. Do not assume the web UI is loopback-only.
