---
title: Permissions
nav_order: 6
---

# Permissions

## Players

Everyone has these by default.

| Permission | Allows |
| --- | --- |
| `nurobots.use` | Opening `/robots` |
| `nurobots.place` | Placing robots |
| `nurobots.shop` | Buying robots from the shop |
| `nurobots.upgrade` | Upgrading robots |
| `nurobots.skills` | Buying skills |
| `nurobots.fuel` | Refuelling robots |
| `nurobots.trust` | Trusting other players |
| `nurobots.filter` | Editing item filters |
| `nurobots.autosell` | Turning auto sell on and off |
| `nurobots.stats` | `/nurobots stats` |
| `nurobots.version` | `/nurobots version` |

## Extras

| Permission | Default | Allows |
| --- | --- | --- |
| `nurobots.rename.color` | op | Colours and formatting in robot names |
| `nurobots.admin.free` | nobody | Buying and upgrading without paying |

## Admins

| Permission | Allows |
| --- | --- |
| `nurobots.admin.reload` | `/nurobots reload` |
| `nurobots.admin.give` | `/nurobots give` |
| `nurobots.admin.remove` | `/nurobots remove` |
| `nurobots.admin.reset` | `/nurobots reset` |
| `nurobots.admin.view` | `/nurobots view` |
| `nurobots.admin.robots` | `/nurobots robots` |
| `nurobots.admin.export` | `/nurobots export` |
| `nurobots.admin.import` | `/nurobots import` |
| `nurobots.admin.debug` | `/nurobots debug` and `/nurobots effects` |
| `nurobots.admin.bypass` | Ignore robot limits and placement rules, and open or manage anyone's robots |
| `nurobots.admin` | Every admin permission above |
| `nurobots.*` | Everything |

## Robot limits

How many robots a player can have placed at once:

| Permission | Limit |
| --- | --- |
| none | `default-max-robots` from `config.yml` (3) |
| `nurobots.limit.<number>` | That number, for example `nurobots.limit.10`. The highest one a player has wins. |
| `nurobots.limit.unlimited` | No limit |

Robot types can also have their own per player limit with `placement.max-per-player`.

## Type and skill permissions

Set `permission:` on a robot type or skill in `robots.yml` to lock it behind any permission you like, for example `nurobots.type.hunter`. Players without it see locked types in the shop but can't buy or place them.
