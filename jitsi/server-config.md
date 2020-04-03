# Recommendations for Jitsi Server Settings

## jitsi-meet/config.js

Disable Peer to Peer Mode.
Switching between server mode (3+ clients) and p2p (2 clients) mode often causes problems.

```
p2p = {
    enabled = false,

    ...
```

Limit Resolution:

```
constraints: {
    video: {
        aspectRatio: 16 / 9,
        height: {
            ideal: 480,
            max: 480,
            min: 240
        }
    }
}
```

Every participant after the 8th will start with muted video:

```
startVideoMuted: 8,
```


## jitsi-meet/interface_config.js

Disable Background Blur which can consume a lot of CPU time:

```
DISABLE_VIDEO_BACKGROUND = true;
```
## Docker

This repository contains the necessary tools to run a Jitsi Meet stack on Docker using Docker Compose:

https://github.com/jitsi/docker-jitsi-meet

The deployment can be configured by modifying `.env`.

* Set `PUBLIC_URL` and `DOCKER_HOST_ADDRESS` (public IPv4)
* Use a reverse proxy like Nginx in front of jitsi-web with Letsencrypt and set `DISABLE_HTTPS=1`
* allow access to ports 10000/udp and 4443/tcp from the outside

JVB logs IP addresses of users by default in some messages with log level INFO. Log level can be changed with:

```
sed -i 's/\.level=INFO/.level=WARNING/g' ~/.jitsi-meet-cfg/jvb/logging.properties
docker-compose restart jvb
```

XXX: customize docker image instead?


## Infrastructure

### Virtual Servers

* Disable power saving (e.g. in BIOS set power management to "performance")
* dedicated and pinned vCPUs
* use non-generic CPU models (e.g. Skylake+)
