---
title: Installation
nav_order: 2
---

# Installation

## Requirements

- Paper or Folia **1.21.11** or newer
- Java **21** or newer
- A copy of NuRobots downloaded from your BuiltByBit account

## Optional plugins

NuRobots works on its own. These plugins add extra features when they're installed:

| Plugin | What it adds |
| --- | --- |
| Vault + an economy plugin | Robot prices, upgrade and skill costs, repairs with money, auto sell |
| WorldGuard | Region protection and the `nurobots-place` and `nurobots-work` flags |
| PlaceholderAPI | `%nurobots_...%` placeholders, and PlaceholderAPI placeholders inside NuRobots text |
| MiniPlaceholders (3.x) | `<nurobots_...>` tags, and MiniPlaceholders tags inside NuRobots text |
| Nexo, Oraxen, ItemsAdder | Custom items in loot, menus, equipment and robot items |
| ModelEngine (R4) | Custom 3D robot models with animations |
| MythicMobs (5.x) | MythicMobs mobs as robot bodies |

## Steps

1. Stop your server.
2. Put `NuRobots-<version>.jar` in your `plugins` folder.
3. Start the server. NuRobots creates `plugins/NuRobots/` with `config.yml`, `robots.yml`, `menus.yml` and `messages.yml`.
4. Look at the console. NuRobots lists any config problems it found and how it handled them.
5. Give yourself a robot with `/nurobots give <your name> miner` and right click a block to place it.

## Updating

1. Replace the old jar with the new one and restart.
2. New settings are added to `config.yml`, `messages.yml` and `menus.yml` automatically. Your own changes are kept.
3. `robots.yml` is never changed for you, so your robot types stay exactly as you wrote them. Compare it against the default in the jar if you want new options.

If `messages.yml` or `menus.yml` come from a version before the current layout, NuRobots moves them to `plugins/NuRobots/backups/` and creates fresh ones. The console tells you when that happens, so you can copy your text changes across.

## Files

| File | What it's for |
| --- | --- |
| `config.yml` | General settings, database, Redis, sell prices, integrations |
| `robots.yml` | Robot types and skills |
| `menus.yml` | Every menu layout |
| `messages.yml` | Every chat message |
| `nurobots.db` | Robot storage when using SQLite |
| `backups/` | Old config files and imports |

Run `/nurobots reload` after editing any of these.
