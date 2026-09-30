---
title: Commands
nav_order: 5
---

# Commands

## Player commands

| Command | Description | Permission |
| --- | --- | --- |
| `/robots` | Open the robot menu | `nurobots.use` |
| `/robots manage` | List your robots | `nurobots.use` |
| `/robots shop` | Open the robot shop | `nurobots.shop` |
| `/nurobots stats` | Server wide robot stats | `nurobots.stats` |
| `/nurobots version` | Version, storage, hooks and licence info | `nurobots.version` |

`/robot` works the same as `/robots`.

## Admin commands

`/nr` works the same as `/nurobots`.

| Command | Description | Permission |
| --- | --- | --- |
| `/nurobots` or `/nurobots help` | List commands | `nurobots.use` |
| `/nurobots reload` | Reload every config file | `nurobots.admin.reload` |
| `/nurobots give <player> <type> [level] [amount]` | Give robot items | `nurobots.admin.give` |
| `/nurobots remove <player> <id>` | Delete one of a player's robots | `nurobots.admin.remove` |
| `/nurobots reset <player>` | Delete every placed robot a player owns | `nurobots.admin.reset` |
| `/nurobots view [radius]` | List robots near you | `nurobots.admin.view` |
| `/nurobots robots <player>` | Open a player's robot list. From console it prints them instead. | `nurobots.admin.robots` |
| `/nurobots export <file>` | Upload a config file to pastes.dev | `nurobots.admin.export` |
| `/nurobots import <file> <link>` | Load a config file from a pastes.dev link | `nurobots.admin.import` |
| `/nurobots effects` | List every skill effect you can use in `robots.yml` | `nurobots.admin.debug` |
| `/nurobots debug` | Toggle debug output and list config problems | `nurobots.admin.debug` |

`<file>` is `config`, `messages`, `robots` or `menus`.

Robot ids appear in `/nurobots view`, `/nurobots robots` and robot menus.

## Examples

```
/nurobots give Steve miner
/nurobots give Steve farmer 5 2
/nurobots remove Steve 42
/nurobots view 32
/nurobots export robots
/nurobots import robots https://pastes.dev/aBcD1234
```
