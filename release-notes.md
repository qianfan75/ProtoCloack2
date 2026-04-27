# ProtoCloack2 v2.1.4

Binary-only release for Linux amd64 and arm64.

## Artifacts

- protocloack2-linux-amd64.tar.gz
- protocloack2-linux-arm64.tar.gz
- SHA256SUMS

Asset names are version-less so the
`https://github.com/qianfan75/ProtoCloack2/releases/latest/download/<asset>`
redirect resolves to the right file regardless of tag. The version
(v2.1.4) is recorded in the bundle's `README.txt` and in this notes file.

## Install

```bash
sha256sum -c SHA256SUMS
tar xzf protocloack2-linux-amd64.tar.gz
cd protocloack2-linux-amd64
sudo ./install.sh server
```

The installer writes bootstrap credentials to
`/root/.protocloack2-bootstrap-secrets` and prints a network-exposure
warning. Restrict Web UI access with firewall, security group, or VPN before
the host leaves a trusted network.
