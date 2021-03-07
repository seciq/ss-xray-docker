# ss-xray

Docker image for shadowsocks-rust server with build-in xray-plugin

## Environment Variables

| Variable | Default value | Description |
|-|-|-|
| HOST | `mydomain.me` | Hostname for server |
| SERVER_ADDR | `0.0.0.0:1080` | Local address to listen on |
| PASSWORD | `password` | Shadowsocks password |
| METHOD | `chacha20-ietf-poly1305` | Encryption method |
| OBFS_PLUGIN | `xray-plugin` | Shadowsocks obfuscation plugin |
| OBFS_OPTS | `server` | Options for obfuscation plugins |
| ARGS | | Additional arguments for Shadowsocks |

## Usage example

### Server configuration

#### Prerequisites

* [docker](https://docs.docker.com/get-docker/)
* [docker-compose](https://docs.docker.com/compose/install/)

Here is one-click example with [Traefik](https://traefik.io/) router with automatic https certificate generation.

[docker-compose.yml](./example/docker-compose.yml)

Please change domain, path and secrets for your needs and make sure that DNS was propagated for your domain, otherwise ssl certificate generation will be fail.

```bash
docker create network traefik
docker-compose up -d
```

### Client configuration

*Clients available for all modern platforms and should be similar for all of that*

*Here is json configration for shadowsocks-libev client for linux/macos:*

```
{
  "server": "mydomain.me",
  "server_port": 443,
  "local_port": 1080,
  "password": "password",
  "method": "chacha20-ietf-poly1305",
  "plugin": "/usr/local/bin/xray-plugin",
  "fast_open": true,
  "mode": "tcp_only",
  "no_delay": true,
  "plugin_opts": "path=/xray;mux=8;host=mydomain.me;tls"
}
```

