# MINECRAFT JAVA SERVER OPTIMIZATION GUIDE

This guide will focus on the optimization part of the minecraft java version. Please make sure to read the whole part for smoother part of the optimization.

## CHOOSING THE RIGHT JAR FILE!

Before getting started with the optimisation part well take a look on the choosing the JAR part.

[PaperMC](https://papermc.io/software/paper) - Offers significant performance improvements over vanilla.

[Purpur](https://purpurmc.org) - A fork of PAPAERMC, Provides better performance than paper.

[Folia](https://papermc.io/software/folia) - Designed for multi-threaded performance on larger server. Not compatible with all plugins.

Each of these jar's provide excellent performace improvements over the vanilla minecraft. PaperMC is standard for performance and compatiblity, but the other jar's offer additional benifits.

### WHAT SHOULD YOU AVOID

- Avoid any **PAID** server JAR that claimes async things.
- Refain from using the old Bukkit/Spigot jars as they are extremely outdated to the softwars i have mentioned above.


Before doing any optmisations we should get to know about some plugins which can helo us with server performance.

[ClearLag](https://www.spigotmc.org/resources/clearlagg.68271/) - Removes entities, limits mob spawning, and cleans up the server.

[Chunky](https://www.spigotmc.org/resources/chunky.81534/) - Pre-Generate minecraft chunks to reduce lag during exploration.

[Spark] - Advanced profiler for analyzing and pptimizing minecraft server performance. (Pre downloaded in GB Nodes and other hostings.)

[EmtityTrackerFixer](https://www.spigotmc.org/resources/entity-tracker-fixer-2-1-18-1-1-18-2.101145/) - Reduces lag caused by entitiy tracking.

These are the recommended plugins that i like to use for optimising server's performance.

## SERVER CONFIGURATIONS


`server.properties`
```
view-distance=8
# Reason: Reduces the number of chunks that need to be loaded and sent to players, significantly reducing server load.

simulation-distance=6
# Reason: Limits the distance at which game mechanics are simulated, further reducing server load without significantly impacting gameplay.

network-compression-threshold=256
# Reason: Balances between bandwidth usage and CPU load for packet compression.

max-players=20
# Reason: Set this to your expected player count. Lower values can help with resource allocation.

max-tick-time=60000
# Reason: Prevents the server from prematurely shutting down due to temporary lag spikes.

use-native-transport=true
# Reason: Enables optimized packet sending on Linux systems.

enable-command-block=false
# Reason: Command blocks can be used for exploits and can cause lag if used excessively.

sync-chunk-writes=true
# Reason: Helps prevent chunk corruption, especially on servers with frequent restarts or crashes.

spawn-protection=16
# Reason: Protects the spawn area from griefing. Adjust based on your server's needs.
```

`spigot.yml`
```
settings:
  save-user-cache-on-stop-only: true
  # Reason: Reduces frequent writes to the user cache file, improving performance.

world-settings:
  default:
    mob-spawn-range: 6
    # Reason: Reduces the range at which mobs spawn around players, reducing entity count and improving performance.

    entity-activation-range:
      animals: 32
      monsters: 32
      raiders: 48
      misc: 16
      # Reason: Reduces the range at which entities are ticked, significantly improving performance.

    tick-inactive-villagers: false
    # Reason: Prevents villagers from being ticked when far from players, reducing CPU usage.

    merge-radius:
      item: 2.5
      exp: 3.0
      # Reason: Causes nearby item entities and experience orbs to merge, reducing entity count.

    item-despawn-rate: 6000
    # Reason: Items despawn faster (5 minutes), reducing entity count.

    arrow-despawn-rate: 1200
    # Reason: Arrows despawn faster (1 minute), reducing entity count.

    nerf-spawner-mobs: true
    # Reason: Mobs from spawners have reduced AI, improving performance.

    max-entity-collisions: 8
    # Reason: Limits the number of entities that can collide, reducing CPU usage.

    max-tick-time:
      tile: 50
      entity: 50
      # Reason: Prevents excessive time being spent on single tile entities or entities, improving overall performance.
```

`bukkit.yml`
```
spawn-limits:
  monsters: 50
  animals: 10
  water-animals: 5
  water-ambient: 20
  ambient: 5
  # Reason: Limits the number of mobs that can spawn, significantly reducing server load.

chunk-gc:
  period-in-ticks: 600
  # Reason: Runs garbage collection for chunks every 30 seconds, freeing up memory.

ticks-per:
  animal-spawns: 400
  monster-spawns: 1
  # Reason: Reduces the frequency of animal spawns while keeping monster spawns frequent for difficulty.

  autosave: 6000
  # Reason: Sets autosave to occur every 5 minutes, balancing between data safety and performance.
```

`paper.yml`
```
max-auto-save-chunks-per-tick: 24
# Reason: Limits the number of chunks saved per tick, preventing auto-save from causing lag spikes.

optimize-explosions: true
# Reason: Uses a more efficient algorithm for explosion calculations.

mob-spawner-tick-rate: 2
# Reason: Reduces the tick rate of mob spawners, improving performance without significantly impacting spawn rates.

container-update-tick-rate: 3
# Reason: Reduces the frequency of container updates, improving performance.

grass-spread-tick-rate: 4
# Reason: Slows down grass spreading, which can be CPU intensive.

despawn-ranges:
  monster:
    soft: 32
    hard: 128
  # Reason: Adjusts mob despawn ranges to balance between performance and mob presence.

hopper:
  disable-move-event: true
  # Reason: Disables firing of move events for items in hoppers, significantly improving performance of hopper-heavy contraptions.

anti-xray:
  enabled: true
  engine-mode: 1
  # Reason: Enables basic anti-xray protection without significant performance impact.

use-faster-eigencraft-redstone: true
# Reason: Uses a more efficient redstone implementation, significantly improving performance of redstone contraptions.

armor-stands-tick: false
# Reason: Prevents armor stands from ticking, improving performance especially with many armor stands.

per-player-mob-spawns: true
# Reason: Enables more efficient mob spawning around players.

alt-item-despawn-rate:
  enabled: true
  items:
    COBBLESTONE: 300
    # Reason: Makes certain common items despawn faster, reducing entity count.
```

Make sure to take a backup of your current configurations before doing anything.

## Lets talk about malware

### How to detect if you are infected?

THere are different types of malware, however you can detect if you have malware by the following ways:

- Spike in resource usage. - Genereally malware do things such as crypto mining or logging and reporting activity to a local server, these tasks take up a lot of resources and are easy to know.

- Increase in plugin file size. - Some malware hides itself in plugin's ar files to make it harder to detect.

- Strange errors.

### How to avaoid malware?

Well its pretty easy to avoid malware just follow these steps:

- Avoid using unkown plugins or newly uploaded plugins.
- Use only official downloads.
- Dont download plugins from any cracked website like blackspigot or spigotunlocked etc.

### How to get rid of it

Many minecraft malware tries to spread itself to other jar files on your server.

Follow these steps to red rid of malware:

- Reinstall every single jar files. - Every single one present on the server


























Credits!
Maddy Miller - https://madelinemiller.dev/blog/
YouHaveTrouble - https://github.com/YouHaveTrouble/minecraft-optimization/blob/1.21/README.md