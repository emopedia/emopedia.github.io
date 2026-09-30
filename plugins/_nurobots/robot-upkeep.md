---
title: Robot Upkeep
parent: Configuration
nav_order: 3
---

# Robot Upkeep

Fuel, durability, experience, auto sell and placement rules are all optional and set per robot type in `robots.yml`. Leave a section out to turn that system off for the type.

## fuel

The robot burns fuel every cycle.

```yaml
fuel:
  enabled: true
  consumed-per-cycle: 1
  starting-fuel: 50
  idle-when-empty: true
  accept-any-burnable: true
  burnable-units-per-item: 4
  items:
    COAL: 8
    COAL_BLOCK: 80
    LAVA_BUCKET: 100
```

| Key | Default | Description |
| --- | --- | --- |
| `consumed-per-cycle` | `1` | Fuel used per cycle |
| `starting-fuel` | `0` | Fuel a new robot comes with |
| `idle-when-empty` | `true` | Stop when empty. When `false`, the gauge is just for show. |
| `items` | | Fuel items and how many units each is worth. A plain list counts each item as 1. |
| `accept-any-burnable` | `true` | Also accept anything a furnace burns |
| `burnable-units-per-item` | `1` | Units for those extra furnace fuels |

The tank size is `max-fuel` on each [level](../robot-types/#levels). Lava buckets give the bucket back.

Players refuel from the robot menu, which pulls fuel from their inventory, or by right clicking the robot with fuel in hand.

## durability

The robot wears down as it works and needs repairing.

```yaml
durability:
  enabled: true
  loss-per-cycle: 1
  loss-per-block: 0.5
  on-break: stop
  warn-owner: true
  warn-below: 0.2
  repair-cost-per-point: 5
  repair-items:
    IRON_INGOT: 50
    IRON_BLOCK: 500
```

| Key | Default | Description |
| --- | --- | --- |
| `loss-per-cycle` | `1` | Wear per cycle |
| `loss-per-block` | `0` | Extra wear for each block broken or mob hit |
| `on-break` | `stop` | `stop` waits for a repair, `drop-item` pops the robot off as an item, `destroy` deletes it |
| `warn-owner` | `true` | Message the owner when it's wearing out |
| `warn-below` | `0.25` | When to warn, as a fraction of full |
| `repair-cost-per-point` | `0` | Money per missing point |
| `full-repair-cost` | `0` | A flat price for a full repair instead |
| `repair-items` | | Items that repair, and how many points each gives |

Maximum durability is `max-durability` on each [level](../robot-types/#levels). If both money settings are `0`, the robot can only be repaired with items.

## experience

Robots earn XP as they work.

```yaml
experience:
  enabled: true
  per-cycle: 2
  per-item: 0.5
  per-block: 0
  auto-level: false
  announce-level-up: true
  keep-overflow: true
```

| Key | Default | Description |
| --- | --- | --- |
| `per-cycle` | `1` | XP every cycle |
| `per-item` | `0` | XP for each item produced |
| `per-block` | `0` | XP for each block broken or mob hit |
| `auto-level` | `true` | `true`: level up for free when the bar fills. `false`: a full bar unlocks the paid upgrade. |
| `announce-level-up` | `true` | Tell the owner |
| `keep-overflow` | `false` | Carry spare XP into the next level |

Loot entries can also give XP with `experience:`. The XP needed per level is `experience-required` on each [level](../robot-types/#levels).

## auto-sell

With Vault installed, owners can have output sold the moment it's made.

```yaml
auto-sell:
  allowed: true
  default: false
  permission: ""
  price-multiplier: 1.0
  tax-rate: 0.05
  sell-unpriced-items: false
  prices:
    DIAMOND: 60.0
```

| Key | Default | Description |
| --- | --- | --- |
| `allowed` | `true` | Whether this type can auto sell at all |
| `default` | `false` | New robots start with auto sell on |
| `permission` | | Extra permission needed to turn it on |
| `price-multiplier` | `1.0` | Multiplies every price |
| `tax-rate` | `0` | Fraction taken off, for example `0.05` is 5% |
| `sell-unpriced-items` | `false` | Sell items with no price at `auto-sell.default-price` from `config.yml` |
| `prices` | | Prices just for this type |

Where a price comes from, first match wins:
1. `prices` on the robot type
2. `sell-price` on the loot entry
3. `auto-sell.prices` in `config.yml`
4. `auto-sell.default-price`, only if `sell-unpriced-items` is on

Items without a price go to storage as normal.

## placement

Limits where a type can be placed. Players with `nurobots.admin.bypass` ignore these.

```yaml
placement:
  worlds:
    - world
    - resource_world
  biomes:
    mode: blacklist
    entries:
      - minecraft:deep_dark
  ground-blocks:
    - "#minecraft:dirt"
    - farmland
  min-y: -64
  max-y: 320
  min-distance-between: 3
  max-per-chunk: 2
  max-per-player: 5
  allow-in-liquid: false
  require-solid-ground: true
```

| Key | Description |
| --- | --- |
| `worlds`, `biomes`, `ground-blocks` | A list is a whitelist. Use `mode` and `entries` for a blacklist. |
| `min-y`, `max-y` | Height limits |
| `min-distance-between` | Blocks between robots of this type |
| `max-per-chunk` | Robots of this type per chunk |
| `max-per-player` | Robots of this type one player can place, on top of their overall limit |
| `allow-in-liquid` | Allow placing in water or lava |
| `require-solid-ground` | The block below must be solid |
