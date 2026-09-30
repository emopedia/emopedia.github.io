---
title: Troubleshooting
nav_order: 11
---

# Troubleshooting

Start with `/nurobots debug`. It turns on extra console output and lists every config problem NuRobots found. `/nurobots version` shows your server, storage, Redis and which integrations are active.

## "NuRobots is shutting down: this copy of NuRobots was not downloaded from BuiltByBit"

NuRobots only runs from a copy downloaded from BuiltByBit. Download it again from the resource page while logged into the BuiltByBit account you bought it with, and replace the jar. Don't use a copy someone else sent you.

## "could not confirm the licence"

NuRobots checks your licence with BuiltByBit now and then. If BuiltByBit can't be reached, it keeps running and tries again later, so a short outage won't affect you. If this keeps showing up, make sure your server can reach `api.builtbybit.com`. If the licence was revoked or refunded, NuRobots shuts down and tells you why.

## A command prints nothing

Your `messages.yml` is probably from an older version. Current versions move old message files to `backups/` and make a fresh one on startup. If you've since edited it and a message is missing, delete `messages.yml` and restart to get a clean copy.

## My robot isn't working

Check its status in the robot menu:

| Status | Fix |
| --- | --- |
| Storage full | Collect the items, turn on auto sell or buy a storage skill |
| Out of fuel | Refuel it from the menu or right click it with fuel |
| Broken | Repair it from the menu or right click it with a repair item |
| Can't work here | It's in a region its owner can't build in, or the region denies `nurobots-work`. A fisher also shows this with no water nearby. |
| Idle | The owner has to be online, either from `require-owner-online` or the type's `work-offline: false` |
| Paused | Press resume |

Physical robots (mine, farm, chop, fish, hunt, ranch, collect) only work while their chunk is loaded. Virtual robots always work.

## A physical robot isn't breaking anything

- Is the block on the type's `blocks` list?
- Can the owner build there with WorldGuard?
- Does the block need a better pickaxe? Give the robot a `tool_tier` skill.
- Containers, spawners, signs, beds and similar blocks are never broken unless `allow-protected-blocks` is on.

## I can't place a robot

The chat message tells you why. The usual reasons are:
- the robot limit (see [Permissions](../permissions/#robot-limits))
- the type's `placement` rules
- WorldGuard
- another robot in the way

## Prices show but buying does nothing

Vault needs an economy plugin, such as EssentialsX or CMI. If `/nurobots version` doesn't list Vault, no economy is hooked.

## Placeholders show as text

- **PlaceholderAPI:** make sure it's installed. NuRobots registers its own placeholders, so there's no eCloud download needed.
- **MiniPlaceholders:** it needs version 3 or newer.

Test them with `/papi parse me %nurobots_count%` or `/miniplaceholders parse me <nurobots_count>`.

## Custom items don't show up

- Check the prefix: `nexo:`, `oraxen:` or `itemsadder:namespace:`.
- Make sure the item exists in that plugin.
- ItemsAdder loads its items late. If items are missing right after startup, run `/nurobots reload` once ItemsAdder has finished loading.

## Robots appeared twice across servers

Two servers are sharing a `server-id`. Give each server its own id. See [Cross-Server](../cross-server/).

## Reporting a bug

Include:
- the output of `/nurobots version`
- your `robots.yml` from `/nurobots export robots`
- any errors from the console

It also helps to say what you expected to happen and what actually happened.
