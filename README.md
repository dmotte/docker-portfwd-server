# docker-portfwd-server

[![GitHub main workflow](https://img.shields.io/github/actions/workflow/status/dmotte/docker-portfwd-server/main.yml?branch=main&logo=github&label=main&style=flat-square)](https://github.com/dmotte/docker-portfwd-server/actions)
[![Docker Pulls](https://img.shields.io/docker/pulls/dmotte/portfwd-server?logo=docker&style=flat-square)](https://hub.docker.com/r/dmotte/portfwd-server)

This is a :whale: **Docker image** containing an **OpenSSH server** that can be used for **local port forwarding** only.

If you want a **rootless** version of this image, check out [dmotte/docker-portfwd-server-rootless](https://github.com/dmotte/docker-portfwd-server-rootless).

> :package: This image is also on **Docker Hub** as [`dmotte/portfwd-server`](https://hub.docker.com/r/dmotte/portfwd-server) and runs on **several architectures** (e.g. amd64, arm64, ...). To see the full list of supported platforms, please refer to the [`.github/workflows/main.yml`](.github/workflows/main.yml) file. If you need an architecture which is currently unsupported, feel free to open an issue.

## Usage

The first things you need are **host keys** for the OpenSSH server and an **SSH key pair** for the client to be able to connect. See the usage example of [dmotte/docker-portmap-server](https://github.com/dmotte/docker-portmap-server) for how to get them.

In general, the use of this image is very similar to [dmotte/docker-portmap-server-rootless](https://github.com/dmotte/docker-portmap-server-rootless).

Example:

```bash
docker run -it --rm \
    -v "$PWD/hostkeys:/ssh-host-keys" \
    -v "$PWD/myclientkey.pub:/ssh-client-keys/myuser/myclientkey.pub:ro" \
    -p2222:22 \
    dmotte/portfwd-server myuser:10.0.2.15:8080
```

See [dmotte/docker-portmap-server](https://github.com/dmotte/docker-portmap-server) for further details on usage; it's very similar to this one.

For a more complex example, refer to the [`docker-compose.yml`](docker-compose.yml) file.

### Environment variables

List of supported **environment variables**:

| Variable             | Required         | Description                                                      |
| -------------------- | ---------------- | ---------------------------------------------------------------- |
| `KEEPALIVE_INTERVAL` | No (default: 30) | Value for the `ClientAliveInterval` option of the OpenSSH server |

## Development

If you want to contribute to this project, you can use the following one-liner to **rebuild the image** and bring up the **Docker-Compose stack** every time you make a change to the code:

```bash
docker-compose down && docker-compose up --build
```
