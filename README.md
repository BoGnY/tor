# docker-tor-privoxy

[![Build Status](https://cloud.drone.io/api/badges/bogny/tor/status.svg)](https://cloud.drone.io/bogny/tor)
[![Docker Pulls](https://img.shields.io/docker/pulls/bogny/tor.svg)](https://hub.docker.com/r/bogny/tor)
[![Docker Stars](https://img.shields.io/docker/stars/bogny/tor.svg)](https://hub.docker.com/r/bogny/tor)
[![MicroBadger](https://images.microbadger.com/badges/image/bogny/tor.svg)](https://microbadger.com/images/bogny/tor)
[![Docker Automated build](https://img.shields.io/docker/automated/bogny/tor.svg)](https://hub.docker.com/r/bogny/tor)
[![License](https://images.microbadger.com/badges/license/bogny/tor.svg)](https://microbadger.com/images/bogny/tor)

## Contributing

If you find this image useful here's how you can help:

- Send a pull request with your awesome features and bug fixes
- Help users resolve their [issues](../../issues?q=is%3Aopen+is%3Aissue).

## Issues

Before reporting your issue please try updating Docker to the latest version and check if it resolves the issue. Refer to the Docker [installation guide][installation_guide] for instructions.

SELinux's users should try disabling SELinux using the command `setenforce 0` to see if it resolves the issue.

If the above recommendations do not help then [report your issue](../../issues/new) along with the following information:

- Output of the `docker vers6` and `docker info` commands
- The `docker run` command or `docker-compose.yml` used to start the image. Mask out the sensitive bits.
- Please state if you are using [Boot2Docker][boot2docker], [VirtualBox][virtualbox], etc.

# Getting started

Automated builds of the image are available on [my Docker Hub][personal_docker_hub] and is the recommended method of installation.

```bash
docker pull bogny/tor
```

Alternatively you can build the image yourself.

```bash
docker build -t 'tor' -i bogny/tor:latest
```

# Quick Start

The quickest way to get started is using [docker-compose][docker_compose_doc].

```bash
wget https://raw.githubusercontent.com/bogny/tor/master/docker-compose.yml
docker-compose up -d
```

Alternately, you can manually launch the `tor` container.

```bash
docker run --name='tor' -d -i bogny/tor:latest
```

The exposed ports are:
* `9050`: Tor proxy (SOCKS5)
* `9051`: Tor control port

Binding port 9051 are optional. Port 9051 is the control port of Tor Network. Using that you can forcefully regenerate the Tor ip. Read more about [tor_ip_renew.py][tor_ip_renew]

# Verify

How to cross-check are you getting ip from Tor or not.

### Check your IP without Tor

```bash
curl https://ipecho.net/plain
```

or

```bash
wget -qO- https://ipecho.net/plain ; echo
```

### Check with Tor

```bash
curl -v --socks5-hostname localhost:9050 https://ipecho.net/plain
```

# Maintenance

## Shell Access

For debugging and maintenance purposes you may want access the containers shell. If you are using Docker version `1.3.0` or higher you can access a running containers shell by starting `bash` using `docker exec`:

```bash
docker exec -it tor sh
```

## Debug

If the above step is not success, you have to verify the log files.

## Upgrading

To upgrade to newer releases:

- **Step 1**: Download the updated Docker image:
```bash
docker pull bogny/tor
```

- **Step 2**: Stop the currently running image:
```bash
docker stop tor
```

- **Step 3**: Remove the stopped container
```bash
docker rm -v tor
```

- **Step 4**: Start the updated image
```bash
docker run --name 'tor' -d -i bogny/tor:latest
```

# Credits

This repository is based on content and work from the following article/repository:
- https://github.com/dockage/tor-privoxy
- https://www.arulraj.net/2015/05/docker-container-for-tor-with-privoxy.html
- https://github.com/arulrajnet/torprivoxy
- https://wildcardcorp.com/blogs/tor-torify-torsocks

[installation_guide]: https://docs.docker.com/installation
[boot2docker]: https://www.boot2docker.io
[virtualbox]: https://www.virtualbox.org
[docker_compose_doc]: https://docs.docker.com/compose
[personal_docker_hub]: https://hub.docker.com/r/bogny/tor
[tor_ip_renew]: https://gist.github.com/arulrajnet/9df385cdb70d8a945686
