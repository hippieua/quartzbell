# quartzbell

Data + firmware releases for a cable-continuity tester.

The device is a read-only HTTPS client of this repository. It fetches static files
— nothing here is an API, and no service backs it.

```
SCHEMA_VERSION          format version of every file below
firmware/latest.json    update manifest: version, image URL, SHA-256, signature
adapters/registry.json  connector/adapter types the device can program   (to come)
articles/index.json     cable article list                               (to come)
articles/<id>.json      one cable: its nets + the two adapter types      (to come)
```

## Firmware updates

`firmware/latest.json` names the newest release. On boot the device compares its own
version against `fw_version` (semver) and, if it is older, streams the image into its
inactive OTA slot, then checks **SHA-256 and an ECDSA P-256 signature** before that
image is allowed to boot. The public key is compiled into the firmware; the private
key is not in this repository and never will be.

So the images here are public, but not forgeable: anyone can download one, nobody
else can produce one a device will run.
