# layer-libnotify

The desktop notification client — the `notify-send` CLI — as a standalone
OpenCharly layer repo.

The candy installs the `libnotify` package, which provides the `notify-send`
command-line client plus the `libnotify` shared library. `notify-send` posts
desktop notifications over the D-Bus session bus to a running notification
daemon (such as `swaync`), so shell scripts and interactive users can raise
notifications.

## What it provides

| Property | Value |
|---|---|
| Layer / candy | `libnotify` |
| Binary | `/usr/bin/notify-send` |
| Dependencies | `pod-dbus` (D-Bus session bus) |
| Service / port | none |

## How to use it

Compose the layer as a nested `candy:` list inside a named box body:

```yaml
my-desktop-box:
  candy:
    base: fedora
    candy:
      - '@github.com/opencharly/layer-libnotify:v2026.240.0154'
```

The `plan:` `check:` steps assert the binary path, its owning package, and its
`--version` handshake.

## Layout

- `charly.yml` — the `libnotify:` candy entity (the `require:`, the `check:`
  assertions, and the embedded `libnotify-skill:` skill entity).
- `.github/workflows/tag-on-merge.yml` — CalVer tag + `CHANGELOG/` on merge.
- `README.md` — this user overview.

## Related

- Owning skill: `/charly-selkies:libnotify` — the `notify-send` CLI, its package,
  and the `dbus: notify` verb alternative.
- `/charly-infrastructure:dbus-layer` — the D-Bus session bus (required dependency).
- `/charly-selkies:swaync` — the notification daemon that displays the notifications.
- `/charly-image:layer` — candy authoring reference.
- [`opencharly/charly`](https://github.com/opencharly/charly) — the charly CLI and image builder
- [`opencharly/opencharly`](https://github.com/opencharly/opencharly) — the umbrella
