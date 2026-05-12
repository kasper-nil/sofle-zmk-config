# split-keyboards

Personal ZMK config repo for the split keyboards I own. `main` is a keyboard-agnostic template; each keyboard lives on its own branch.

## Branches

| Branch | Keyboard | Notes |
|--------|----------|-------|
| `main` | _(template)_ | Skeleton config, no shield wired up. Branch off this when adding a new keyboard. |
| `sofle` | Sofle v2 | nice_nano_v2 + nice!view, Norwegian locale, 5 layers (base, mac, special L/R, function) |
| `lily58` | Lily58 | nice_nano_v2 + nice!view, Norwegian locale |

## How to flash

1. Pick the branch for your keyboard.
2. GitHub Actions builds firmware on every push — grab the `firmware` artifact from the latest run.
3. Drop the `.uf2` files onto each half in bootloader mode.

## Adding a new keyboard

```sh
git checkout main
git checkout -b <keyboard-name>
```

Then edit on the new branch:

- `config/<keyboard>.conf` — feature flags (display, studio, RGB, encoders, …)
- `config/<keyboard>.keymap` — layers and bindings
- `build.yaml` — board + shield matrix consumed by the GH Actions matrix build
- `config/west.yml` — extra ZMK modules (locales, displays, etc.)

Push the branch. Actions builds firmware.

## Keeping branches in sync with main

When the template changes (e.g. new ZMK revision in `west.yml`, workflow tweaks), rebase or merge `main` into each keyboard branch.
