---
title: Developer API
nav_order: 10
---

# Developer API

NuRobots has a small API for other plugins, in the `com.nurobots.api` package. Ask for the `nurobots-api` jar, or build it from source, and add it as a compile-only dependency:

```kotlin
dependencies {
    compileOnly(files("libs/nurobots-api-1.0.0.jar"))
}
```

Then declare NuRobots in your `paper-plugin.yml` so it loads first:

```yaml
dependencies:
  server:
    NuRobots:
      load: BEFORE
      required: true
      join-classpath: true
```

## Getting the API

```java
NuRobotsAPI api = NuRobotsProvider.get();

// or without a hard dependency
if (NuRobotsProvider.isAvailable()) {
    NuRobotsAPI api = NuRobotsProvider.get();
}
```

It's also registered with Bukkit's services manager as `NuRobotsAPI`.

## Reading robots

```java
Collection<Robot> robots = api.getRobots(player.getUniqueId());
Optional<Robot> robot = api.getRobotAt(block.getLocation());
int placed = api.countPlacedRobots(player.getUniqueId());
int limit = api.getRobotLimit(player);
```

`Robot` gives you:
- its type, owner and level
- XP, status, storage, fuel and durability
- location, skills, trusted players, filter and name

Read methods are safe from any thread.

## Changing robots

```java
api.setLevel(id, 5);
api.setSkillLevel(id, "fortune", 2);
api.addFuel(id, 100);
api.repair(id);
api.setPaused(id, true);
api.setAutoSell(id, true);
List<ItemStack> items = api.emptyStorage(id);
api.trust(id, friendId);
api.removeRobot(id);
```

Create a robot in a player's collection:

```java
api.createRobot(ownerId, type, 1).thenAccept(robot -> {
    // runs off the main thread
});
```

Give a robot item:

```java
ItemStack item = api.createRobotItem(api.getRobotType("miner").orElseThrow(), 3);
```

## Events

All events are in `com.nurobots.api.event`. The cancellable ones can be cancelled to stop the action.

| Event | Cancellable | When |
| --- | --- | --- |
| `RobotPlaceEvent` | yes | A player places a robot |
| `RobotRemoveEvent` | yes | A robot is picked up, removed or reset. `setRefundItem` controls whether the player gets the item back. |
| `RobotWorkEvent` | yes | A robot finishes a cycle. The output list and XP can be changed. |
| `RobotCollectEvent` | yes | A player collects storage |
| `RobotUpgradeEvent` | yes | A player upgrades a robot. The cost can be changed. |
| `RobotSkillUpgradeEvent` | yes | A player buys a skill level. The cost can be changed. |
| `RobotFuelEvent` | yes | Fuel is added. The amount can be changed. |
| `RobotAutoSellEvent` | yes | Output is sold. The revenue can be changed. |
| `RobotStatusChangeEvent` | yes | A robot's status changes |
| `RobotLevelUpEvent` | no | A robot levels up from XP |
| `RobotBreakdownEvent` | no | A robot runs out of durability |

```java
@EventHandler
public void onWork(RobotWorkEvent event) {
    if (event.getRobot().getType().getId().equals("miner")) {
        event.getOutput().add(new ItemStack(Material.GOLD_NUGGET));
    }
}
```

## Custom skill effects

Add new behaviour that server owners can use in `robots.yml` with `effect: myplugin_overdrive`.

```java
public final class OverdriveEffect implements SkillEffect {

    @Override
    public String getId() {
        return "myplugin_overdrive";
    }

    @Override
    public String getDescription() {
        return "Works much faster but wears out twice as quickly.";
    }

    @Override
    public void apply(SkillContext context) {
        WorkModifiers mods = context.getModifiers();
        mods.multiplySpeed(1.0 + context.getMultiplier());
        mods.multiplyDurabilityUse(2.0);
    }
}
```

```java
NuRobotsProvider.get().getSkillEffectRegistry().register(this, new OverdriveEffect());
```

Your effects are removed automatically when your plugin is disabled.

`WorkModifiers` has levers for:
- yield, speed, efficiency and double chance
- XP, fortune, silk touch, auto smelt and replant
- fuel use, durability use and sell price
- radius, blocks per cycle, bonus drops and extra targets
- custom values that effects can share with each other

`apply` can run often and off the main thread, so keep it fast and don't touch the world from it. Use `RobotWorkEvent` for anything that needs the world.
