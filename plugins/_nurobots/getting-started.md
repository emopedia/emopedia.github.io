---
title: Getting Started
nav_order: 3
---

# Getting Started

This page covers how robots work in game, from buying one to upgrading it.

## Getting a robot

- **Shop:** `/robots shop`, or `/robots` and then the shop button. Robots cost money when Vault is installed.
- **Admins:** `/nurobots give <player> <type> [level] [amount]`.

A robot starts as an item in your inventory.

## Placing a robot

Right click a block while holding the robot item. The robot appears on top of the block you clicked.

Placing can be refused when:
- you've already placed as many robots as you're allowed (see [Permissions](../permissions/#robot-limits))
- another robot is standing there or something is in the way
- the robot type has placement rules, like certain worlds or heights, or a distance from other robots of its kind
- you can't build there because of WorldGuard

## Using a robot

Right click a placed robot to open its menu. From there you can:

| Button | What it does |
| --- | --- |
| Storage | Left click to open, right click to collect everything, shift click to sell everything |
| Upgrade | Raise the robot's level for the listed price |
| Skills | Buy and level up skills |
| Fuel | Fill the tank from your inventory |
| Durability | Left click to repair with money, right click to repair with items |
| Pause / Resume | Stop and start the robot |
| Auto sell | Sell output as it's made instead of storing it |
| Item filter | Choose which items the robot keeps |
| Trusted players | Let friends use the robot |
| Rename | Give the robot its own name |
| Pick up | Take the robot back, keeping its level, skills and storage |

Shortcuts on the robot itself:
- **Right click with fuel** in your hand to refuel it.
- **Right click with a repair item** in your hand to repair it.
- **Sneak and right click** to pick it up.

## Your robots

`/robots manage` lists every robot you own, placed or not.

- **Left click** a robot to open it.
- **Right click** a placed robot to pick it up.
- **Right click** an unplaced robot, then right click a block, to place it.
- **Shift right click** an unplaced robot to take it as an item, for example to give or trade it.

## Robot status

| Status | Meaning |
| --- | --- |
| Working | Doing its job |
| Idle | Placed but not working right now, for example if its owner needs to be online |
| Paused | Paused by its owner |
| Storage full | Collect the items or turn on auto sell |
| Out of fuel | Needs refuelling |
| Broken | Needs repairing |
| Can't work here | Blocked by region protection, or a fisher with no water nearby |
| Not placed | In your robot list, not in the world |

Owners get a chat message when a robot runs out of fuel, fills up, breaks or levels up. You can turn that off in `config.yml`.

## Levels and experience

Robots can level up in two ways, set per robot type:

- **Paid upgrades** from the Upgrade button.
- **Experience.** Robots earn XP as they work. They either level up on their own, or need a full XP bar before the paid upgrade unlocks.

Higher levels usually mean more speed, more output and more storage.

## Trusted players

Trusted players can open the robot, collect from it, refuel it and repair it. Only the owner can upgrade it, buy skills, change the filter, rename it or pick it up.

## Item filter

Click items in your own inventory while the filter menu is open to add them.

- **Only keep listed items** throws away everything else.
- **Throw away listed items** keeps everything else.

Filtered items are thrown away, so they never fill up storage.
