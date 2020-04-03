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


## Infrastructure

### Virtual Servers

* Disable power saving (e.g. in BIOS set power management to "performance")
* dedicated and pinned vCPUs
* use non-generic CPU models (e.g. Skylake+)
