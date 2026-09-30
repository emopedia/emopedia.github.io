---
title: Menus and Messages
parent: Configuration
nav_order: 6
---

# Menus and Messages

## messages.yml

Every chat message NuRobots sends. Messages use MiniMessage, and placeholders look like `%this%`.

- Set a message to `""` to turn it off.
- A message can be one line or a list of lines.
- `prefix` is added in front of single line messages.
- PlaceholderAPI and MiniPlaceholders placeholders work in every message.

```yaml
prefix: "<dark_gray>[<aqua>NuRobots<dark_gray>] <gray>"
place:
  success: "<green>%name% <green>is up and running."
  limit: "<red>You've placed the maximum number of robots. <gray>(%count%/%max%)"
```

## menus.yml

Every menu is under `menus:`: `main`, `shop`, `manage`, `detail`, `storage`, `skills`, `filter`, `trust` and `confirm`.

```yaml
menus:
  main:
    title: "<dark_gray>NuRobots"
    size: 27
    filler: GRAY_STAINED_GLASS_PANE
    refresh-ticks: 0
    items:
      shop:
        slot: 11
        material: EMERALD
        name: "<green><bold>Robot Shop"
        lore:
          - "<gray>Buy new robots."
```

### Menu keys

| Key | Description |
| --- | --- |
| `title` | Menu title. Robot menus can use robot placeholders. |
| `size` | Slots, a multiple of 9 up to 54 |
| `filler` | Item filling empty slots, or `none` |
| `refresh-ticks` | Redraw the menu this often while it's open. `0` turns it off. |
| `content-slots` | Where list menus put their entries, like `["10-16", "19-25"]` |

### Button keys

| Key | Description |
| --- | --- |
| `slot` / `slots` | One slot, or a list and ranges like `["0-8", "45"]` |
| `material` | The item |
| `custom-item` | A Nexo, Oraxen or ItemsAdder item |
| `head-texture` | Base64 skin for `PLAYER_HEAD` |
| `name`, `lore` | Text |
| `glow` | Enchanted shine |
| `amount` | Stack size |
| `custom-model-data` | Custom model data |
| `enabled` | Set to `false` to hide the button |

Buttons are found by name, so you can move, restyle or hide any of them, but not rename them. Some buttons have two versions for different states, like `pause` and `resume`, `autosell-on` and `autosell-off`, or `upgrade` and `upgrade-max`.

### Progress bars and status colours

```yaml
progress-bar:
  length: 20
  filled-char: "|"
  empty-char: "|"
  filled-color: "<#5ee7df>"
  empty-color: "<dark_gray>"

status-colors:
  WORKING: "<green>Working"
  STORAGE_FULL: "<gold>Storage full"
```

## Robot placeholders

These work in holograms, robot menus, robot messages and bound robot items.

| Placeholder | Value |
| --- | --- |
| `%id%` | Robot id |
| `%type%` | Type id |
| `%display_name%` | The type's display name |
| `%name%` | Custom name, or the type name |
| `%custom_name%` | Custom name only |
| `%description%` | Type description |
| `%owner%`, `%owner_uuid%` | Owner |
| `%server%` | Server the robot is on |
| `%level%`, `%max_level%`, `%next_level%`, `%level_roman%` | Level |
| `%upgrade_cost%` | Cost of the next upgrade |
| `%experience%`, `%experience_required%`, `%experience_progress%`, `%experience_bar%` | XP |
| `%skill_count%` | Skills learned |
| `%world%`, `%x%`, `%y%`, `%z%`, `%coords%` | Location |
| `%placed%` | `true` or `false` |
| `%status%`, `%status_colored%` | Status |
| `%speed%`, `%efficiency%` | Multipliers |
| `%progress%`, `%progress_bar%`, `%time_remaining%`, `%cycle_time%` | Current cycle |
| `%items_generated%` | Total items produced |
| `%work_mode%`, `%work_task%` | What it does |
| `%storage%`, `%storage_max%`, `%storage_percent%`, `%storage_bar%` | Storage |
| `%auto_sell%`, `%revenue%` | Selling |
| `%fuel%`, `%fuel_max%`, `%fuel_percent%`, `%fuel_bar%`, `%requires_fuel%` | Fuel |
| `%durability%`, `%durability_max%`, `%durability_percent%`, `%durability_bar%`, `%has_durability%` | Durability |
| `%trusted_count%` | Trusted players |
| `%filter_mode%`, `%filter_entries%` | Filter |
