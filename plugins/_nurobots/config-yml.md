---
title: config.yml
parent: Configuration
nav_order: 1
---

# config.yml

## Server id

```yaml
server-id: "auto"
```

Every server sharing a database needs its own id. `auto` builds one from the machine name and port. See [Cross-Server](../cross-server/).

## settings

| Key | Default | Description |
| --- | --- | --- |
| `default-max-robots` | `3` | How many robots a player can have placed. Raise it per player with `nurobots.limit.<number>`. |
| `respect-worldguard` | `true` | Stop robots being placed or working where the owner can't build |
| `tick-interval` | `20` | How often robots are updated, in ticks. Lower is smoother but costs more. |
| `require-owner-online` | `false` | Only let robots work while their owner is online |
| `auto-save-interval` | `2` | Minutes between full saves. Collecting, upgrading and buying skills always save straight away. |
| `notify-owner` | `true` | Tell owners when a robot runs dry, fills up, breaks or levels up |
| `pickup-gives-item` | `true` | Give the robot back as an item when it's picked up. When off, it only goes to `/robots manage`. |
| `allow-robot-trading` | `true` | Let a player place a robot item that came from someone else's robot and take it over |
| `upgrade-repairs` | `true` | Fully repair a robot when it's upgraded |
| `hunter-drops-xp` | `true` | Mobs killed by hunter robots still drop XP orbs |
| `max-trusted` | `10` | Trusted players per robot |
| `max-filter-entries` | `27` | Items per filter |
| `max-name-length` | `32` | Longest robot name |
| `chat-prompt-timeout` | `60` | Seconds a player has to type in chat when renaming or trusting |
| `max-view-radius` | `256` | Largest radius for `/nurobots view` |
| `debug` | `false` | Extra console output |
| `metrics` | `true` | Anonymous bStats metrics |

### robot-item

What robot items look like in inventories. `bound-name` and `bound-lore` are used for robots that were picked up, since they keep their skills and storage.

```yaml
robot-item:
  name: "%display_name% <dark_gray>[<gray>Lv. %level%<dark_gray>]"
  lore:
    - "<gray>%description%"
    - "<gray>Job: <white>%work_task%"
    - "<yellow>Right click a block to place"
```

Placeholders: `%display_name%`, `%description%`, `%type%`, `%level%`, `%max_level%`, `%level_roman%`, `%work_mode%`, `%work_task%`, `%cycle_time%` and `%storage_max%`. Bound items can also use any [robot placeholder](../menus-and-messages/#robot-placeholders).

### sounds

```yaml
sounds:
  place: BLOCK_ANVIL_USE
  remove: ENTITY_ITEM_PICKUP
  upgrade: ENTITY_PLAYER_LEVELUP
  collect: ENTITY_EXPERIENCE_ORB_PICKUP
  purchase: BLOCK_NOTE_BLOCK_PLING
  refuel: ITEM_BUCKET_EMPTY_LAVA
  repair: BLOCK_ANVIL_USE
  menu-click: UI_BUTTON_CLICK
```

### holograms

The text above robots. A robot type can use its own lines and style in [Appearance](../appearance/#holograms).

```yaml
holograms:
  enabled: true
  style:
    background: none
    shadow: true
    see-through: false
    opacity: 255
    line-width: 200
    alignment: center
    scale: 1.0
    billboard: center
  lines:
    - "%display_name% <dark_gray>[<gray>Lv. %level%<dark_gray>]"
    - "<gray>%owner%"
    - "%status_colored%"
    - "<gray>Storage <white>%storage%<gray>/<white>%storage_max%"
    - "%progress_bar%"
```

| Style key | Values |
| --- | --- |
| `background` | `none`, `default` (the vanilla grey box), `#rrggbb` or `#aarrggbb` |
| `shadow` | `true` or `false` |
| `see-through` | Show the text through blocks |
| `opacity` | `0` to `255` |
| `line-width` | Pixels before the text wraps |
| `alignment` | `center`, `left` or `right` |
| `scale` | Text size |
| `billboard` | `center` always faces the player, `fixed` never turns, `vertical` and `horizontal` lock one axis |

## auto-sell

Prices used by auto sell and the "sell everything" button. Prices set on a robot type or a loot entry win over these.

```yaml
auto-sell:
  default-price: 0.0
  prices:
    DIAMOND: 50.0
    WHEAT: 1.0
```

## database

```yaml
database:
  type: SQLITE
  host: localhost
  port: 3306
  name: minecraft
  user: root
  password: ""
  parameters: ""
  pool:
    maximum-pool-size: 8
    minimum-idle: 2
    connection-timeout: 10000
    idle-timeout: 600000
    max-lifetime: 1800000
```

| Type | Notes |
| --- | --- |
| `SQLITE` | No setup needed. Stored in `nurobots.db`. One server only. |
| `MYSQL` / `MARIADB` | Port `3306` |
| `POSTGRESQL` | Port `5432` |

`parameters` adds extra connection options, for example `useSSL=false&allowPublicKeyRetrieval=true`.

Tables are created and upgraded automatically.

## redis

Only needed when several servers share one database. See [Cross-Server](../cross-server/).

```yaml
redis:
  enabled: false
  host: localhost
  port: 6379
  username: ""
  password: ""
  ssl: false
  channel: "nurobots"
```

## integrations

```yaml
integrations:
  vault:
    enabled: true
  placeholderapi:
    enabled: true
    nutrobots-alias: true
  miniplaceholders:
    enabled: true
  custom-items:
    enabled: true
    priority:
      - Nexo
      - Oraxen
      - ItemsAdder
```

`nutrobots-alias` also makes `%nutrobots_...%` work, for anyone who typed it that way. `priority` decides which plugin to ask first when an item id could belong to more than one.
