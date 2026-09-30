---
title: Skills
parent: Configuration
nav_order: 5
---

# Skills

Skills are upgrades players buy for individual robots. They're defined under `skills:` in `robots.yml`, and each robot type lists which ones it can learn.

```yaml
skills:
  bigger_hauls:
    name: "<green>Bigger Hauls"
    description: "<gray>More items every cycle."
    icon: CHEST
    effect: yield_multiplier
    max-level: 5
    cost: 3000
    cost-multiplier: 1.8
    multiplier-per-level: 0.1
    required-robot-level: 1
    permission: ""
```

| Key | Default | Description |
| --- | --- | --- |
| `name` | | Name shown in the skills menu |
| `description` | | One line or a list |
| `icon` | `ENCHANTED_BOOK` | Menu icon |
| `effect` | `yield_multiplier` | What the skill does, from the list below |
| `max-level` | `1` | How many times it can be bought |
| `cost` | `0` | Price of level 1 |
| `cost-multiplier` | `1.0` | Each level costs this much more than the last |
| `multiplier-per-level` | `0` | Strength per level. Level 3 with `0.1` gives `0.3`. |
| `required-robot-level` | `1` | Robot level needed before it can be bought |
| `permission` | | Permission needed to buy it |

## Setting each level by hand

```yaml
skills:
  fortune:
    effect: fortune
    max-level: 3
    levels:
      1: { cost: 5000, multiplier: 1 }
      2: { cost: 15000, multiplier: 2 }
      3: { cost: 50000, multiplier: 3 }
```

## Effects

`/nurobots effects` lists every effect on your server, including ones added by other plugins.

| Effect | What the strength means |
| --- | --- |
| `yield_multiplier` | More items per cycle. `0.2` is 20% more. |
| `efficiency_multiplier` | Same as yield. Both exist so you can split them into two skills. |
| `speed_multiplier` | Faster cycles. `0.15` is 15% faster. |
| `fortune` | Fortune levels. `1` per level is like the enchantment. |
| `silk_touch` | Blocks drop themselves instead of their normal drop |
| `auto_smelt` | Smelts anything a furnace could, like raw iron into iron ingots |
| `replant` | Replants crops after harvesting |
| `double_chance` | Chance to double a whole cycle. `0.05` is 5%. |
| `rare_find` | Rare loot shows up more often |
| `extra_roll` | Extra loot rolls per cycle. `0.5` is one extra roll every other cycle. |
| `fuel_efficiency` | Burns less fuel |
| `durability_saver` | Wears out slower |
| `experience_boost` | More robot XP |
| `sell_bonus` | Auto sell pays more |
| `storage_boost` | More storage. `0.25` is 25% more. |
| `radius_boost` | Works further out. `1` is one more block. |
| `tool_tier` | Breaks blocks that need a better pickaxe. `1` is diamond, `2` is netherite. |

For `silk_touch`, `auto_smelt` and `replant`, leave `multiplier-per-level` at `0` for always on. A value between `0` and `1` makes it a chance each cycle.

Other plugins can add their own effects through the [developer API](../developer-api/).
