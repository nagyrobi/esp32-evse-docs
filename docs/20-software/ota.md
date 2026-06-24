---
title: OTA updates
---

# OTA updates

The firmware can update itself over the network ("over-the-air"). There are two
independent mechanisms:

- **Channel update (pull)** — the device fetches a small descriptor from a
  remote *channel*, compares versions, and if they differ downloads and flashes
  the firmware over HTTPS.
- **Image upload (push)** — you send a firmware `.bin` straight to the device as
  the body of an HTTP request.

Both write to a spare application slot and only switch over once the image is
complete and valid, so a failed or interrupted update leaves the running
firmware intact. The very first installation (a blank chip) is done over USB
with the [browser web installer](https://dzurikmiroslav.github.io/esp32-evse-docs/installer/), not OTA.

## How it works

The partition table reserves two application slots, `app0` (`ota_0`) and `app1`
(`ota_1`) of 1856 KB each, plus an `otadata` partition that records which slot
boots. An update always writes to the slot that is **not** currently running.
When the image passes validation, `otadata` is flipped to the new slot and the
device restarts into it; if anything fails, the old slot is untouched and stays
the boot target. The restart is scheduled a moment after the HTTP response is
sent, so the client still receives the result.

!!! note
    All HTTPS transfers verify the server certificate against the built-in
    certificate bundle, so the channel descriptor and the firmware binary must be
    served over HTTPS with a publicly trusted certificate.

## Update channels

Channels are declared in [`board.yaml`](board-config-schema.md#ota) under
`ota.channels` — one to three entries, each with a `name` and a `path` (the URL
of the channel's descriptor):

```yaml
ota:
  channels:
    - name: stable
      path: https://dzurikmiroslav.github.io/esp32-evse/ota/stable/esp32.json
    - name: testing
      path: https://dzurikmiroslav.github.io/esp32-evse/ota/testing/esp32.json
```

The descriptor path differs per chip family (`esp32.json`, `esp32s2.json`, …),
which is how the right build is matched to the hardware.

The **selected** channel is stored in NVS; if none has been chosen, the first
channel in `board.yaml` is the default. 

### Channel descriptor format

The file each channel points at is a small JSON object with two string fields:

```json
{
  "version": "v2.2.0",
  "path": "https://dzurikmiroslav.github.io/esp32-evse/ota/stable/esp32-evse.bin"
}
```

| Field | Meaning |
| ----- | ------- |
| `version` | The firmware version string offered by this channel |
| `path` | Absolute HTTPS URL of the firmware image to flash |

If you self-host a channel, serve a descriptor in this shape and point a
`board.yaml` channel `path` at it.

## When OTA is not enough

OTA only replaces the application image. Some releases also change things outside
the app slot — the **partition table**, or the **`board.yaml` format**. Those
cannot be delivered by OTA and require a **full flash over USB** with the
[web installer](https://dzurikmiroslav.github.io/esp32-evse/web-installer), after
which the `board.yaml` may need to be recreated in the new format. The release
notes call this out when it applies, so check them before a major version jump.

!!! note
    Because a full flash rewrites the LittleFS `usr` partition, back up your
    `board.yaml` and any [Lua scripts](Lua.md) first (for example over
    [WebDAV](rest-api.md#related-webdav-file-access)).

## See also

- [Board configuration schema → `ota`](board-config-schema.md#ota) — defining channels
- [Web installer](https://dzurikmiroslav.github.io/esp32-evse/web-installer) — initial install and full reflash

