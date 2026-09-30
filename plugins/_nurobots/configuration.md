---
title: Configuration
nav_order: 4
has_children: true
---

# Configuration

NuRobots is set up through four files in `plugins/NuRobots/`:

| File | Page |
| --- | --- |
| `config.yml` | [config.yml](../config-yml/) |
| `robots.yml` | [Robot Types](../robot-types/), [Robot Upkeep](../robot-upkeep/), [Appearance](../appearance/), [Skills](../skills/) |
| `menus.yml` and `messages.yml` | [Menus and Messages](../menus-and-messages/) |

## General rules

- **Reloading:** `/nurobots reload` applies every file without a restart. Placed robots pick up their new settings straight away.
- **Mistakes don't break anything.** If a value is wrong, NuRobots logs what it found, what it used instead and why. Run `/nurobots debug` to see the full list in game.
- **Text** uses [MiniMessage](https://docs.advntr.dev/minimessage/format.html), like `<red>`, `<gradient:#5ee7df:#39a0ed>` or `<bold>`. Old `&c` colour codes work too.
- **Durations** can be `30s`, `5m`, `1h30m`, `2d` or ticks like `600t`.
- **Items and blocks** can be a name (`diamond`), a namespaced key (`minecraft:diamond`) or, in lists, a tag (`#minecraft:logs`).
- **Custom items** use `nexo:<id>`, `oraxen:<id>` or `itemsadder:<namespace>:<id>`.
- **Sounds** can be written `BLOCK_ANVIL_USE` or `block.anvil.use`.

## Editing configs from a browser

`/nurobots export robots` uploads `robots.yml` to [pastes.dev](https://pastes.dev) and gives you a link. After editing, `/nurobots import robots <link>` loads it back. The import checks that the file is valid YAML before saving, and keeps a copy of the old file in `backups/`.
