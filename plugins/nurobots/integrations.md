---
title: Integrations
nav_order: 8
---

# Integrations

Every integration is optional and turns on when its plugin is installed. `/nurobots version` shows which ones are active.

## Vault

Needs Vault and an economy plugin, such as EssentialsX or CMI. It enables:
- robot prices, upgrades and skills
- repairs with money
- auto sell and the "sell everything" button

Without an economy these are simply turned off, and anything with a price of `0` is free.

## WorldGuard

With `settings.respect-worldguard` on, players can only place robots where they can build. Physical robots only touch blocks and mobs in places their owner could build.

NuRobots also adds two region flags:

| Flag | What it does when denied |
| --- | --- |
| `nurobots-place` | Nobody can place robots in the region |
| `nurobots-work` | Physical robots won't work in the region |

```
/rg flag spawn nurobots-place deny
/rg flag market nurobots-work deny
```

## PlaceholderAPI and MiniPlaceholders

See [Placeholders](../placeholders/). MiniPlaceholders needs version 3 or newer.

## Nexo, Oraxen and ItemsAdder

Custom items can be used as:
- loot table drops: `item: nexo:ruby`
- the robot item: `custom-item-id: oraxen:miner_robot`
- equipment and display items: `main-hand: itemsadder:tools:drill`
- menu buttons: `custom-item: nexo:button_next`

Item filters and auto sell recognise custom items as well.

Ids are written `nexo:<id>`, `oraxen:<id>` or `itemsadder:<namespace>:<id>`. When an id has no prefix, NuRobots checks the plugins in the order set by `integrations.custom-items.priority`.

## ModelEngine

Needs ModelEngine R4 or newer. Give a robot type a model with idle and work animations:

```yaml
appearance:
  model-engine:
    id: robot_miner
    idle-animation: idle
    work-animation: mine
```

## MythicMobs

Needs MythicMobs 5. Use any MythicMobs mob as the robot's body:

```yaml
appearance:
  mythicmobs-id: RobotMiner
```

Its AI is turned off and it can't be hurt.

## Folia

NuRobots runs natively on Folia with no extra setup. Robot work happens on the region that owns each robot, so robots scale across regions like the rest of the server.
