---
title: Placeholders
nav_order: 7
---

# Placeholders

NuRobots supports both **PlaceholderAPI** and **MiniPlaceholders**, so its placeholders work whichever one your other plugins use. They also work the other way round: any PlaceholderAPI or MiniPlaceholders placeholder can be used inside NuRobots messages, menus and holograms.

## Player placeholders

| PlaceholderAPI | MiniPlaceholders | Value |
| --- | --- | --- |
| `%nurobots_count%` | `<nurobots_count>` | Robots placed |
| `%nurobots_placed%` | `<nurobots_placed>` | Same as count |
| `%nurobots_owned%` | `<nurobots_owned>` | Robots owned, placed or not |
| `%nurobots_max%` | `<nurobots_max>` | Most robots they can place |
| `%nurobots_remaining%` | `<nurobots_remaining>` | How many more they can place |
| `%nurobots_active%` | `<nurobots_active>` | Robots working right now |
| `%nurobots_count_<type>%` | `<nurobots_count_type:<type>>` | Robots of one type placed |
| `%nurobots_level_total%` | `<nurobots_level_total>` | All their robots' levels added up |
| `%nurobots_level_average%` | `<nurobots_level_average>` | Average robot level |
| `%nurobots_types%` | `<nurobots_types>` | Different robot types owned |
| `%nurobots_items_generated%` | `<nurobots_items_generated>` | Items produced by all their robots |
| `%nurobots_revenue%` | `<nurobots_revenue>` | Money earned from auto sell |

## Robot placeholders

Replace `<id>` with the robot's id.

| PlaceholderAPI | MiniPlaceholders |
| --- | --- |
| `%nurobots_<id>_<field>%` | `<nurobots_robot:<id>:<field>>` |

| Field | Value |
| --- | --- |
| `type` | Type id |
| `name` | Name |
| `level`, `max_level` | Level |
| `owner` | Owner's name |
| `status` | Status |
| `world`, `x`, `y`, `z` | Location |
| `efficiency`, `speed` | Multipliers |
| `storage`, `storage_max` | Storage |
| `progress` | Progress through the current cycle, in percent |
| `time_remaining` | Time until the next cycle finishes |
| `items_generated` | Items produced |
| `fuel`, `fuel_max` | Fuel |
| `durability`, `durability_max` | Durability |
| `experience`, `experience_required` | XP |
| `revenue` | Money earned from auto sell |
| `auto_sell` | `true` or `false` |
| `placed` | `true` or `false` |
| `server` | Server the robot is on |

Examples: `%nurobots_12_level%`, `<nurobots_robot:12:storage>`.

## Server placeholders

| PlaceholderAPI | MiniPlaceholders | Value |
| --- | --- | --- |
| `%nurobots_server_count%` | `<nurobots_server_count>` | Robots placed on the whole network |
| `%nurobots_server_players%` | `<nurobots_server_players>` | Players with a robot placed |
| `%nurobots_server_types%` | `<nurobots_server_types>` | Robot types in use |
| `%nurobots_server_active%` | `<nurobots_server_active>` | Robots working right now |
| `%nurobots_server_items_generated%` | `<nurobots_server_items_generated>` | Items produced in total |
| `%nurobots_server_id%` | `<nurobots_server_id>` | This server's id |

`%nutrobots_...%` works as well as `%nurobots_...%`. Turn that off with `integrations.placeholderapi.nutrobots-alias` in `config.yml`.

## Testing

```
/papi parse me %nurobots_count%
/miniplaceholders parse me <nurobots_count>
```
