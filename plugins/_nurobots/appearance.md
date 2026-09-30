---
title: Appearance
parent: Configuration
nav_order: 4
---

# Appearance

Everything about how a robot looks goes under `appearance:` on its type in `robots.yml`.

A placed robot is made of:
- **a body**
- **an invisible hitbox**, so players can click it
- **a hologram** above it, unless turned off

None of these are saved into your world, so removing the plugin never leaves stray entities behind.

## Body types

```yaml
appearance:
  body: item_display
```

| Body | What it is |
| --- | --- |
| `item_display` | A floating item. Uses the robot item, or `item:` if set. |
| `block_display` | A floating block. Uses `block:`, or the robot's material if it's a block. |
| `armor_stand` | An armour stand that can wear armour and hold tools |
| `mob` | Any vanilla mob |
| `text_only` | Just the hologram |
| `none` | Nothing visible, only the hitbox |

If `model-engine` or `mythicmobs-id` is set and that plugin is installed, it replaces the body.

### General options

| Key | Default | Description |
| --- | --- | --- |
| `scale` | `1.0` | Size of display bodies |
| `y-offset` | `0` | Move the body up or down |
| `spin` | `true` | Slowly spin display bodies |
| `spin-speed` | `45` | Degrees per second |
| `glow` | `false` | Glowing outline |
| `glow-color` | | Outline colour for display bodies, like `#ff4b2b` or `red` |
| `view-range` | `48` | How far away the robot can be seen, in blocks |
| `item` | | What an `item_display` shows |
| `block` | | What a `block_display` shows |

## Mobs

```yaml
appearance:
  body: mob
  mob:
    type: drowned
    baby: true
    scale: 0.8
```

| Key | Description |
| --- | --- |
| `type` | Any living mob, like `zombie`, `skeleton`, `villager`, `piglin` or `iron_golem` |
| `baby` | Use the baby version, for mobs that have one |
| `scale` | Size, using the scale attribute. `0` leaves it alone. |

Robot mobs have no AI, can't be hurt, don't burn in sunlight, don't target anyone and don't change into other mobs.

## Equipment

Mobs and armour stands can wear armour and hold items.

```yaml
appearance:
  body: armor_stand
  equipment:
    helmet:
      material: player_head
      head-texture: "eyJ0ZXh0dXJlcy..."
    chestplate:
      material: leather_chestplate
      color: "#3a5f0b"
    leggings: iron_leggings
    boots: iron_boots
    main-hand: diamond_pickaxe
    off-hand: nexo:robot_lamp
```

Slots: `helmet`, `chestplate`, `leggings`, `boots`, `main-hand` and `off-hand`.

An armour stand with no `helmet` wears the robot item as its head.

## Item options

Anywhere an item is asked for (`item`, equipment slots), you can write a plain name, a custom item id, or a block:

```yaml
main-hand:
  material: paper
  item-model: mypack:robot_arm
  custom-model-data: 12
  glow: true
```

| Key | Description |
| --- | --- |
| `material` | The item, or a custom item id |
| `custom-item` | A Nexo, Oraxen or ItemsAdder item |
| `head-texture` | Base64 skin for player heads |
| `item-model` | A resource pack item model, like `mypack:robot_arm` |
| `custom-model-data` | Custom model data number |
| `color` | Dye colour for leather armour, like `#3a5f0b` |
| `glow` | Enchanted shine |

Use `none` to leave a slot empty.

## Armour stands

```yaml
appearance:
  body: armor_stand
  armor-stand:
    small: true
    arms: true
    base-plate: false
    invisible: false
    pose:
      head: 5, 0, 0
      right-arm: -40, 0, 10
```

Pose parts: `head`, `body`, `left-arm`, `right-arm`, `left-leg` and `right-leg`. Each takes three angles in degrees, like `-40, 0, 10` or `[-40, 0, 10]`.

## ModelEngine

```yaml
appearance:
  model-engine:
    id: robot_miner
    idle-animation: idle
    work-animation: mine
```

`idle-animation` plays when the robot appears. `work-animation` plays every time it finishes a cycle. Needs ModelEngine R4 or newer.

## MythicMobs

```yaml
appearance:
  mythicmobs-id: RobotMiner
```

The mob is spawned with its AI turned off, so it stands still. Equipment from `equipment:` is added on top of anything the mob already wears.

## Holograms

```yaml
appearance:
  hologram:
    enabled: true
    height: 1.2
    update-interval: 2s
    owner-only: false
    lines:
      - "%name%"
      - "%status_colored%"
      - "%progress_bar%"
    style:
      background: "#60300000"
      shadow: true
```

| Key | Default | Description |
| --- | --- | --- |
| `enabled` | `true` | Show a hologram for this type |
| `height` | `1.2` | Height above the robot |
| `update-interval` | `2s` | How often the text refreshes |
| `owner-only` | `false` | Only the owner can see it |
| `lines` | from `config.yml` | Text lines. Leave empty to use the lines in `config.yml`. |
| `style` | from `config.yml` | Any of the [hologram style](../config-yml/#holograms) keys. Anything you leave out comes from `config.yml`. |

Lines can use any [robot placeholder](../menus-and-messages/#robot-placeholders), plus PlaceholderAPI and MiniPlaceholders placeholders.

## Particles and sound

Played every time the robot finishes a cycle.

```yaml
appearance:
  particle:
    type: BLOCK
    data: STONE
    count: 6
    spread: 0.35
  work-sound:
    sound: BLOCK_STONE_BREAK
    volume: 0.4
    pitch: 1.0
```

| Key | Description |
| --- | --- |
| `particle.type` | Any particle |
| `particle.data` | The block or item for particles that need one, like `BLOCK` or `ITEM` |
| `particle.color` | Colour for `DUST` and similar particles |
| `work-sound` | A sound name, or a section with `sound`, `volume` and `pitch` |

Turn all robot particles off with `settings.particles.enabled` in `config.yml`.
