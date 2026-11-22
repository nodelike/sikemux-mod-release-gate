# Release gate

A [Sikemux](https://sikemux.com) mod for checklists that must be all ticked before something ships. You and your agents share them: an agent ticks a check once it has proved it, and says how in the check's note.

## Install

Open `sikemux://install-mod?repo=nodelike/sikemux-mod-release-gate`, or install it from [sikemux.com/mods](https://sikemux.com/mods). It installs as `sikemux-mod-release-gate`.

## What it does

- Keep several gates, such as a release, a pull request or a launch. Start one empty or from a template.
- Tick checks and see who ticked each one and when.
- The tab's badge shows how many checks are done, and says ready once all of them are.
- Archive a gate after it ships.

## Permissions

It reads nothing from Sikemux and writes nothing outside its own data, so it never asks you to allow anything.

## Data

`gates`:

| Field | Type | |
| --- | --- | --- |
| `name` | string, up to 80 | required |
| `archived` | boolean | |

`checks`:

| Field | Type | |
| --- | --- | --- |
| `gate` | the gate's id | required |
| `text` | string, up to 300 | required |
| `done` | boolean | required |
| `note` | string, up to 300 | |
| `order` | number | |

## For agents

Find the open checks:

```json
mod_read { "mod": "sikemux-mod-release-gate", "collection": "checks" }
```

Tick one you have proved, by the id `mod_read` gave it:

```json
mod_write {
  "mod": "sikemux-mod-release-gate",
  "writes": [{
    "collection": "checks",
    "id": "g-mhx2k1-0",
    "patch": { "done": true, "note": "CI green on 7960ab7" }
  }]
}
```

## License

MIT
