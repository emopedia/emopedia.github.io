---
title: Robot Types
parent: Configuration
nav_order: 2
---

# Robot Types

Robot types live under `robots:` in `robots.yml`. The key is the type's id, used in commands and placeholders. Ids aren't case sensitive.

Each type has these sections:
- **General settings:** name, item and shop
- **Work:** what the robot does
- **Loot:** what it produces
- **Levels:** how it improves
- **Upkeep:** fuel, durability, experience, auto sell and placement rules, covered on [Robot Upkeep](../robot-upkeep/)
- **Appearance:** covered on [Appearance](../appearance/)
- **Skills:** covered on [Skills](../skills/)

## A full example

```yaml
robots:
  miner:
    display-name: "<aqua><bold>Miner"
    description:
      - "<gray>Digs up stone, coal and ores"
      - "<gray>even while you're offline."
    material: PLAYER_HEAD
    head-texture: "eyJ0ZXh0dXJlcy..."
    permission: ""
    shop:
      enabled: true
      order: 1
    work:
      mode: virtual
      cycle-time: 20s
    loot-table:
      - item: COBBLESTONE
        weight: 40
        amount: 1-3
      - item: DIAMOND
        weight: 2
    skills:
      - overclock
      - fortune
    levels:
      1:
        cost: 1000
        upgrade-cost: 2500
        speed: 1.0
        efficiency: 1.0
        storage: 128
      2:
        cost: 2500
        upgrade-cost: 0
        speed: 1.2
        efficiency: 1.15
        storage: 256
```

## General settings

| Key | Description |
| --- | --- |
| `display-name` | Name shown everywhere |
| `description` | One line or a list of lines |
| `material` | The item used for the robot item and menu icon |
| `head-texture` | A base64 skin texture, used when `material` is `PLAYER_HEAD` |
| `custom-item-id` | Use a Nexo, Oraxen or ItemsAdder item as the robot item instead |
| `permission` | Permission needed to buy or place this type. Leave empty for everyone. |
| `skills` | Ids of the skills this type can learn |

### shop

| Key | Default | Description |
| --- | --- | --- |
| `enabled` | `true` | Show this type in the shop |
| `order` | `0` | Lower numbers come first |
| `slot` | `-1` | A fixed slot on the first shop page. `-1` places it automatically. |

The shop price is the `cost` of level 1.

## work

This decides what the robot actually does.

| Key | Default | Description |
| --- | --- | --- |
| `mode` | `virtual` | `virtual` or `physical` |
| `task` | `none` | What a physical robot does: `mine`, `farm`, `chop`, `fish`, `hunt`, `ranch`, `collect` or `none` |
| `cycle-time` | `30s` | Time between work cycles at speed 1 |
| `rolls-per-cycle` | `1` | Loot table rolls per cycle (1 to 64) |
| `work-offline` | `true` | Keep working while the owner is offline |
| `require-chunk-loaded` | `false` (`true` for physical) | Only work while the robot's chunk is loaded |
| `max-catch-up` | `24h` | For virtual robots: how much time spent offline or unloaded is made up when the server starts |
| `max-catch-up-cycles` | `240` | Most cycles one catch-up can give. `0` turns catch-up off. |
| `drop-on-ground` | `false` | Drop output on the ground instead of storing it |

### Virtual robots

Virtual robots roll their loot table every cycle. They never touch the world, so they:
- are cheap to run
- can't grief anything
- keep working in unloaded chunks and while the server is off, up to `max-catch-up`

### Physical robots

Physical robots really work the area around them, but only while their chunk is loaded. Each block and mob is checked against WorldGuard before it's touched.

Settings every physical task uses:

| Key | Default | Description |
| --- | --- | --- |
| `radius` | `3` | How far out the robot works, in blocks (up to 16) |
| `vertical-radius` | same as `radius` | How far up and down it works |
| `max-targets-per-cycle` | `8` | Blocks, crops, mobs or items handled per cycle |
| `blocks` | everything | Which blocks it may touch. A list is a whitelist. Use `mode: whitelist` or `mode: blacklist` with `entries:` for more control. |
| `mobs` | everything | Which mobs a hunter or rancher may touch. Same format as `blocks`. |
| `use-vanilla-drops` | `true` | Collect the real drops. When off, the loot table is rolled instead. |
| `check-protection-per-block` | `true` | Check WorldGuard for every block, not just the robot's own spot |
| `break-effects` | `true` | Show break particles and sounds |
| `allow-protected-blocks` | `false` | Let the robot break chests, spawners, beds, signs and other blocks that are normally off limits. Almost never a good idea. |

#### mine

Breaks blocks from the top of its area down.

| Key | Default | Description |
| --- | --- | --- |
| `regenerate.enabled` | `false` | Put broken blocks back after a delay |
| `regenerate.delay` | `1m` | How long before a block comes back |

Blocks that need a better tool are skipped unless the robot has the `tool_tier` skill effect.

#### farm

Harvests fully grown crops, sugar cane, cactus, bamboo, melons, pumpkins, sweet berries, nether wart and cocoa.

| Key | Default | Description |
| --- | --- | --- |
| `replant` | `true` | Replant crops, using one seed from the drops |
| `till-soil` | `false` | Turn dirt and grass with air above it into farmland |
| `bone-meal` | `false` | Grow crops that aren't ready yet |

#### chop

Fells a whole tree at a time by following connected logs.

| Key | Default | Description |
| --- | --- | --- |
| `tree-feller-limit` | `64` | Most blocks taken from one tree |
| `include-leaves` | `false` | Also break the leaves, for saplings and apples |
| `replant-saplings` | `true` | Plant a matching sapling where the tree stood |

`max-targets-per-cycle` is how many trees it fells per cycle.

#### fish

Needs water within `radius`. Rolls the vanilla fishing loot when it can, otherwise the robot's loot table. It shows as "Can't work here" when there's no water.

#### hunt

Hits mobs around it and keeps the drops of anything it kills.

| Key | Default | Description |
| --- | --- | --- |
| `damage-per-hit` | `6` | Damage per hit |
| `hostile-only` | `true` | Only attack hostile mobs |
| `ignore-named-mobs` | `true` | Leave mobs with name tags alone |
| `ignore-tamed-mobs` | `true` | Leave pets alone |

Players, armour stands and other robots are never attacked.

#### ranch

Shears sheep and collects eggs from chickens and scutes from armadillos, without hurting them.

| Key | Default | Description |
| --- | --- | --- |
| `ranch-cooldown` | `5m` | How long before the same animal can be used again |

#### collect

Picks up items lying on the ground, and stops when storage is full.

## Loot

`loot-table` is what a virtual robot produces each roll. A physical robot uses it when `use-vanilla-drops` is off, or for the `none` task.

One entry is picked per roll, weighted by `weight`.

```yaml
loot-table:
  - COD:40:1
  - INK_SAC:6:1-3
  - item: DIAMOND
    weight: 2
    amount: 1-2
    chance: 0.5
    experience: 10
    sell-price: 60
  - item: ENCHANTED_BOOK
    weight: 1
    enchantments:
      MENDING: 1
  - item: nexo:ruby
    weight: 3
```

The short form is `ITEM:weight:amount`.

| Key | Default | Description |
| --- | --- | --- |
| `item` | | Item name or custom item id |
| `weight` | `1` | How likely this entry is compared to the others |
| `chance` | `1.0` | Once picked, the chance it actually drops |
| `amount` | `1` | A number or a range like `1-3`. You can also use `min-amount` and `max-amount`. |
| `amount-per-level` | `0` | Extra items for every robot level above 1 |
| `experience` | `0` | Robot XP when this drops |
| `sell-price` | | Auto sell price for this item, winning over `config.yml` |
| `name`, `lore` | | Custom name and lore |
| `enchantments` | | Map of enchantment to level. Books get stored enchantments. |
| `custom-model-data` | | Custom model data |
| `glow` | `false` | Enchanted shine |
| `unbreakable`, `hide-flags` | `false` | Item flags |

### level-loot

Changes the table as the robot levels up. `add` adds to the table, `replace` swaps it out. Each change carries on to higher levels.

```yaml
level-loot:
  5:
    entries:
      - item: REDSTONE
        weight: 8
        amount: 2-5
  8:
    mode: replace
    entries:
      - item: ANCIENT_DEBRIS
        weight: 1
```

## Levels

| Key | Description |
| --- | --- |
| `cost` | Price to buy the robot at this level. The shop uses level 1. |
| `upgrade-cost` | Price to go from this level to the next |
| `speed` | Work speed. `2.0` works twice as often. |
| `efficiency` | Output multiplier. `1.5` produces 50% more. |
| `storage` | How many items the robot can hold |
| `max-fuel` | Fuel tank size, when fuel is on |
| `max-durability` | Durability, when durability is on |
| `experience-required` | XP needed to reach the next level, when experience is on |

If you skip a level, it copies the one below it.

### Generated levels

A type with no `levels:` section gets levels built from `defaults:` at the top of `robots.yml`:

```yaml
defaults:
  max-level: 10
  base-cost: 2500
  cost-growth: 1.8
  base-speed: 1.0
  speed-per-level: 0.15
  base-efficiency: 1.0
  efficiency-per-level: 0.15
  base-storage: 128
  storage-per-level: 128
  base-max-fuel: 200
  fuel-per-level: 50
  base-max-durability: 500
  durability-per-level: 100
  base-experience-required: 100
  experience-growth: 1.6
```

Each level's cost is the last one times `cost-growth`. XP needed is multiplied by `experience-growth` each level.
