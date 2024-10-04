# ENHANCED MINECRAFT JAVA SERVER OPTIMIZATION GUIDE

This comprehensive guide focuses on optimizing Minecraft Java servers. Please read the entire guide for a thorough understanding of server optimization techniques.

## CHOOSING THE RIGHT JAR FILE

Before diving into optimization, let's look at choosing the right server JAR:

1. [PaperMC](https://papermc.io/software/paper) - Offers significant performance improvements over vanilla.
2. [Purpur](https://purpurmc.org) - A fork of PaperMC, provides even better performance than Paper.
3. [Folia](https://papermc.io/software/folia) - Designed for multi-threaded performance on larger servers. Note: Not compatible with all plugins.
4. [Aikars Flags](https://aikar.co/2018/07/02/tuning-the-jvm-g1gc-garbage-collector-flags-for-minecraft/) - While not a JAR, these are optimized JVM flags that can significantly improve server performance.

Each of these JARs provides excellent performance improvements over vanilla Minecraft. PaperMC is the standard for performance and compatibility, but the other JARs offer additional benefits.

### WHAT TO AVOID

- Avoid any **PAID** server JARs that claim async capabilities.
- Refrain from using old Bukkit/Spigot JARs as they are extremely outdated compared to the software mentioned above.

## PERFORMANCE-ENHANCING PLUGINS

Consider these plugins to help with server performance:

1. [ClearLag](https://www.spigotmc.org/resources/clearlagg.68271/) - Removes entities, limits mob spawning, and cleans up the server.
2. [Chunky](https://www.spigotmc.org/resources/chunky.81534/) - Pre-generates Minecraft chunks to reduce lag during exploration.
3. [Spark](https://spark.lucko.me/) - Advanced profiler for analyzing and optimizing Minecraft server performance.
4. [EntityTrackerFixer](https://www.spigotmc.org/resources/entity-tracker-fixer-2-1-18-1-1-18-2.101145/) - Reduces lag caused by entity tracking.
5. [FastAsyncWorldEdit (FAWE)](https://www.spigotmc.org/resources/fastasyncworldedit.13932/) - Optimized version of WorldEdit for faster world manipulation.
6. [TickProfiler](https://github.com/MinecraftForge/TickProfiler) - Diagnoses lag sources and provides detailed server performance analysis.
7. [Lag Assist](https://www.spigotmc.org/resources/lagassist-%E2%9A%A1-advanced-performance-optimization.56399/) - Comprehensive lag reduction and server optimization plugin.
8. [Farm Limiter](https://www.spigotmc.org/resources/farm-limiter.1419/) - Limits farm sizes to prevent excessive lag from large automated farms.
9. [VillagerOptimiser](https://www.spigotmc.org/resources/villager-optimiser-1-14-2-1-16-5.68517/) - Optimizes villager behavior to reduce server load.

## SERVER CONFIGURATIONS

### server.properties

```properties
view-distance=8
simulation-distance=6
network-compression-threshold=256
max-players=20
max-tick-time=60000
use-native-transport=true
enable-command-block=false
sync-chunk-writes=true
spawn-protection=16
entity-broadcast-range-percentage=100
```

### spigot.yml

```yaml
settings:
  save-user-cache-on-stop-only: true
  max-tick-time:
    tile: 1000
    entity: 1000

world-settings:
  default:
    mob-spawn-range: 6
    entity-activation-range:
      animals: 32
      monsters: 32
      raiders: 48
      misc: 16
    tick-inactive-villagers: false
    merge-radius:
      item: 2.5
      exp: 3.0
    item-despawn-rate: 6000
    arrow-despawn-rate: 1200
    nerf-spawner-mobs: true
    max-entity-collisions: 8
    growth:
      cactus-modifier: 100
      cane-modifier: 100
      melon-modifier: 100
      mushroom-modifier: 100
      pumpkin-modifier: 100
      sapling-modifier: 100
      beetroot-modifier: 100
      carrot-modifier: 100
      potato-modifier: 100
      wheat-modifier: 100
      netherwart-modifier: 100
      vine-modifier: 100
      cocoa-modifier: 100
    hopper-amount: 1
    dragon-death-sound-radius: 0
    seed-village: 10387312
    seed-desert: 14357617
    seed-igloo: 14357618
    seed-jungle: 14357619
    seed-swamp: 14357620
    seed-monument: 10387313
    seed-shipwreck: 165745295
    seed-ocean: 14357621
    seed-outpost: 165745296
    seed-endcity: 10387313
    seed-slime: 987234911
    seed-nether: 30084232
    seed-mansion: 10387319
    seed-fossil: 14357921
    seed-portal: 34222645
```

### bukkit.yml

```yaml
spawn-limits:
  monsters: 50
  animals: 10
  water-animals: 5
  water-ambient: 20
  ambient: 5

chunk-gc:
  period-in-ticks: 600

ticks-per:
  animal-spawns: 400
  monster-spawns: 1
  autosave: 6000

aliases: now-in-commands.yml
```

### paper.yml

```yaml
max-auto-save-chunks-per-tick: 24
optimize-explosions: true
mob-spawner-tick-rate: 2
container-update-tick-rate: 3
grass-spread-tick-rate: 4
despawn-ranges:
  monster:
    soft: 32
    hard: 128
hopper:
  disable-move-event: true
anti-xray:
  enabled: true
  engine-mode: 1
use-faster-eigencraft-redstone: true
armor-stands-tick: false
per-player-mob-spawns: true
alt-item-despawn-rate:
  enabled: true
  items:
    COBBLESTONE: 300
    NETHERRACK: 300
    DIRT: 300
    SAND: 300
max-entity-collisions: 2
tick-rates:
  sensor:
    villager: 1
    raid: 1
    hoglin: 1
collisions:
  allow-vehicle-collisions: false
  fix-climbing-bypassing-cramming-rule: true
  only-players-collide: true
entity-per-chunk-save-limit:
  experience_orb: 16
  snowball: 16
  ender_pearl: 16
  arrow: 16
prevent-moving-into-unloaded-chunks: true
use-faster-threadlocalrandom: true
lava-flow-speed:
  normal: 30
  nether: 10
```

### purpur.yml (if using Purpur)

```yaml
settings:
  use-alternative-item-despawn-rate: true
  use-faster-night-skip: true
  use-faster-eigencraft-redstone: true
  dont-send-useless-entity-packets: true
  dont-send-useless-lightning-packets: true
  keep-spawn-loaded: false
  keep-spawn-loaded-range: 8

world-settings:
  default:
    mobs:
      cow:
        ridable: true
        controllable: true
      chicken:
        ridable: true
        controllable: true
    gameplay-mechanics:
      disable-ice-and-snow: true
      disable-teleportation-suffocation-check: true
      disable-chest-cat-detection: true
      disable-end-credits: true
      disable-phantom-spawns: true
      disable-pillager-patrols: true
```

## ADDITIONAL OPTIMIZATION TIPS

1. **Pre-generate your world**: Use a plugin like Chunky to pre-generate your world. This reduces lag caused by chunk generation during gameplay.

2. **Optimize your network settings**: 
   - Use a wired connection instead of Wi-Fi.
   - Configure your router's Quality of Service (QoS) settings to prioritize Minecraft traffic.
   - Increase the `network-compression-threshold` in server.properties for better network performance.

3. **Use SSDs for storage**: SSDs can significantly improve chunk loading and saving times.

4. **Monitor and adjust**: Regularly use tools like Spark or Timings to monitor your server's performance and adjust settings accordingly.

5. **Keep software updated**: Regularly update your server software, Java version, and plugins to benefit from the latest optimizations and bug fixes.

6. **Limit redstone complexity**: Excessively complex redstone contraptions can cause significant lag. Consider using plugins that optimize redstone or limit its complexity.

7. **Control entity cramming**: Use the `max-entity-cramming` gamerule to limit the number of entities that can be pushed into one block.

8. **Optimize plugin usage**: Only use necessary plugins and ensure they are compatible and optimized for your server version.

9. **Configure view distance dynamically**: Consider using a plugin like [ViaVersion](https://www.spigotmc.org/resources/viaversion.19254/) to dynamically adjust player view distances based on server load.

10. **Limit chunk loading**: Use a plugin like [ChunkMaster](https://www.spigotmc.org/resources/chunkmaster.71351/) to control and optimize chunk loading, especially for teleportation and world generation.

11. **Optimize mob spawning**: Adjust mob spawn limits and frequencies in bukkit.yml and spigot.yml to reduce server load from excessive mob spawning.

12. **Use server-side protection**: Implement server-side protection plugins like WorldGuard to prevent client-side exploits and reduce server load from malicious actions.

13. **Implement an anti-cheat system**: Use plugins like NoCheatPlus or Matrix to prevent cheating and reduce server load from illegitimate player actions.

14. **Optimize inventory handling**: Use plugins like InventoryTweaks or FastInv to optimize inventory operations and reduce server load from frequent inventory interactions.

15. **Implement chunk loading optimization**: Use plugins like ChunkLoader or FastChunkPregen to optimize chunk loading and generation processes.

16. **Use memory-efficient data structures**: When developing custom plugins, use memory-efficient data structures and algorithms to reduce server memory usage.

17. **Implement caching mechanisms**: Use caching for frequently accessed data to reduce database queries and improve server response times.

18. **Optimize database queries**: If using a database, optimize your queries and indexes to improve performance and reduce server load.

19. **Use asynchronous processing**: When possible, use asynchronous processing for non-critical tasks to reduce main thread load.

20. **Implement proper garbage collection**: Use appropriate garbage collection settings (like Aikar's Flags) to optimize memory management and reduce lag spikes.

Remember to always backup your configurations before making changes. Server optimization is an ongoing process, so continually monitor your server's performance and adjust settings as needed.

## Credits

- Maddy Miller - https://madelinemiller.dev/blog/
- YouHaveTrouble - https://github.com/YouHaveTrouble/minecraft-optimization/blob/1.21/README.md
- PaperMC Documentation - https://docs.papermc.io/paper/optimization
- Aikar's Flags - https://aikar.co/2018/07/02/tuning-the-jvm-g1gc-garbage-collector-flags-for-minecraft/