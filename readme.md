# Beszel (Agent) - Windows AMD64 Builds
### **This repository contains Windows binaries only!**

---

Beszel is a lightweight server monitoring platform that includes Docker statistics, historical data, and alert functions.

It has a friendly web interface, simple configuration, and is ready to use out of the box. It supports automatic backup, multi-user, OAuth authentication, and API access.

## Usage:

It is unfortunate gitlab requires users authenticate to pull packages from the generic package registry afaik.
Due to this requirement I did create a new user named "public_api" with an API token of ```glpat-Gtpqt1aHVdPSS11XdREm```. 
The max expiry of a personal accesss token is 1 year! 🥴 We will worry about automating that ~ later. 🙈

To pull a [release](https://gitlab.prplanit.com/precisionplanit/beszel-agent-win-amd64/-/packages) programmatically using curl:

```
curl --header "PRIVATE-TOKEN: $GITLAB_TOKEN" \
        "$GITLAB_DOMAIN/api/v4/projects/$CI_PROJECT_ID/packages/generic/beszel-agent/$CI_COMMIT_TAG/$ZIP_NAME" \
        --output $CI_COMMIT_TAG/$ZIP_NAME"
```
Where CI_COMMIT_TAG is the [release](https://gitlab.prplanit.com/precisionplanit/beszel-agent-win-amd64/-/packages) version, i.e.:
```
curl --header "PRIVATE-TOKEN: glpat-Gtpqt1aHVdPSS11XdREm" \
  -L "https://gitlab.prplanit.com/api/v4/projects/33/packages/generic/beszel-agent/v0.11.1/beszel-agent_windows_amd64-v0.11.1.zip" \
  --output beszel-agent_windows_amd64-v0.11.1.zip
```

The release binaries are available for direct download [here](https://gitlab.prplanit.com/precisionplanit/beszel-agent-win-amd64/-/packages) as well.

---

[![agent Docker Image Size](https://img.shields.io/docker/image-size/henrygd/beszel-agent/latest?logo=docker&label=agent%20image%20size)](https://hub.docker.com/r/henrygd/beszel-agent)
[![hub Docker Image Size](https://img.shields.io/docker/image-size/henrygd/beszel/latest?logo=docker&label=hub%20image%20size)](https://hub.docker.com/r/henrygd/beszel)
[![MIT license](https://img.shields.io/github/license/henrygd/beszel?color=%239944ee)](https://github.com/henrygd/beszel/blob/main/LICENSE)
[![Crowdin](https://badges.crowdin.net/beszel/localized.svg)](https://crowdin.com/project/beszel)

![Screenshot of Beszel dashboard and system page, side by side. The dashboard shows metrics from multiple connected systems, while the system page shows detailed metrics for a single system.](https://henrygd-assets.b-cdn.net/beszel/screenshot-new.png)

## Features

- **Lightweight**: Smaller and less resource-intensive than leading solutions.
- **Simple**: Easy setup with little manual configuration required.
- **Docker stats**: Tracks CPU, memory, and network usage history for each container.
- **Alerts**: Configurable alerts for CPU, memory, disk, bandwidth, temperature, and status.
- **Multi-user**: Users manage their own systems. Admins can share systems across users.
- **OAuth / OIDC**: Supports many OAuth2 providers. Password auth can be disabled.
- **Automatic backups**: Save to and restore from disk or S3-compatible storage.
<!-- - **REST API**: Use or update your data in your own scripts and applications. -->

## Architecture

Beszel consists of two main components: the **hub** and the **agent**.

- **Hub**: A web application built on [PocketBase](https://pocketbase.io/) that provides a dashboard for viewing and managing connected systems.
- **Agent**: Runs on each system you want to monitor, creating a minimal SSH server to communicate system metrics to the hub.

## Getting started

The [quick start guide](https://beszel.dev/guide/getting-started) and other documentation is available on our website, [beszel.dev](https://beszel.dev). You'll be up and running in a few minutes.

## Screenshots

![Dashboard](https://beszel.dev/image/dashboard.png)
![System page](https://beszel.dev/image/system-full.png)
![Notification Settings](https://beszel.dev/image/settings-notifications.png)

## Supported metrics

- **CPU usage** - Host system and Docker / Podman containers.
- **Memory usage** - Host system and containers. Includes swap and ZFS ARC.
- **Disk usage** - Host system. Supports multiple partitions and devices.
- **Disk I/O** - Host system. Supports multiple partitions and devices.
- **Network usage** - Host system and containers.
- **Temperature** - Host system sensors.
- **GPU usage / temperature / power draw** - Nvidia and AMD only. Must use binary agent.

## Help and discussion

Please search existing issues and discussions before opening a new one. I try my best to respond, but may not always have time to do so.

#### Bug reports and feature requests

Bug reports and detailed feature requests should be posted on [GitHub issues](https://github.com/henrygd/beszel/issues).

#### Support and general discussion

Support requests and general discussion can be posted on [GitHub discussions](https://github.com/henrygd/beszel/discussions) or the community-run [Matrix room](https://matrix.to/#/#beszel:matrix.org): `#beszel:matrix.org`.

## License

Beszel is licensed under the MIT License. See the [LICENSE](LICENSE) file for more details.
