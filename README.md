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

Explanations:
- `view-distance=8`: Reduces the number of chunks sent to players, decreasing server load and improving performance.
- `simulation-distance=6`: Limits the distance at which entities are fully simulated, reducing CPU usage.
- `network-compression-threshold=256`: Compresses packets larger than 256 bytes, optimizing network performance.
- `max-players=20`: Limits the number of concurrent players to prevent overload.
- `max-tick-time=60000`: Prevents the server from stopping if a single tick takes up to 60 seconds, useful for temporary lag spikes.
- `use-native-transport=true`: Enables native transport optimization for improved network performance.
- `enable-command-block=false`: Disables command blocks to prevent potential exploits and reduce server load.
- `sync-chunk-writes=true`: Improves chunk saving performance by writing them asynchronously.
- `spawn-protection=16`: Protects a 16-block radius around the spawn point from modification by non-ops.
- `entity-broadcast-range-percentage=100`: Controls the percentage of the view distance at which entities are sent to clients.

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

Explanations:
- `save-user-cache-on-stop-only: true`: Reduces frequency of saving user caches, improving performance.
- `max-tick-time`: Increases the threshold for detecting hung tasks, preventing false positives.
- `mob-spawn-range: 6`: Reduces the range at which mobs spawn around players, decreasing entity count.
- `entity-activation-range`: Limits the range at which entities are fully ticked, reducing CPU usage.
- `tick-inactive-villagers: false`: Prevents inactive villagers from being ticked, saving CPU cycles.
- `merge-radius`: Increases item and experience orb merge radius, reducing entity count.
- `item-despawn-rate: 6000`: Makes items despawn faster (5 minutes), reducing entity count.
- `arrow-despawn-rate: 1200`: Makes arrows despawn faster (1 minute), reducing entity count.
- `nerf-spawner-mobs: true`: Reduces AI calculations for mobs from spawners.
- `max-entity-collisions: 8`: Limits entity collisions, reducing CPU load from collision calculations.
- `growth`: Modifies crop growth rates to balance gameplay and reduce update frequency.
- `hopper-amount: 1`: Limits the number of items transferred by hoppers per tick, reducing server load.
- `dragon-death-sound-radius: 0`: Disables the ender dragon's death sound, which can cause lag.
- `seed-*`: Consistent world generation seeds for various structures.

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

Explanations:
- `spawn-limits`: Reduces the maximum number of mobs that can spawn, decreasing entity count and CPU usage.
- `chunk-gc.period-in-ticks: 600`: Sets garbage collection for unloaded chunks to occur every 30 seconds, balancing memory usage and performance.
- `ticks-per`: 
  - `animal-spawns: 400`: Slows down animal spawning to reduce entity count.
  - `monster-spawns: 1`: Keeps monster spawning frequent for gameplay balance.
  - `autosave: 6000`: Sets autosave to occur every 5 minutes, balancing data safety and performance.

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

Explanations:
- `max-auto-save-chunks-per-tick: 24`: Limits chunks saved per tick during autosave, reducing lag spikes.
- `optimize-explosions: true`: Uses a more efficient explosion algorithm.
- `mob-spawner-tick-rate: 2`: Slows down mob spawner ticking, reducing CPU usage.
- `container-update-tick-rate: 3`: Reduces the frequency of container updates, saving CPU cycles.
- `grass-spread-tick-rate: 4`: Slows down grass spreading, reducing block updates.
- `despawn-ranges`: Adjusts mob despawn ranges to better manage entity count.
- `hopper.disable-move-event: true`: Disables firing of move events for items in hoppers, improving performance.
- `anti-xray`: Enables and configures anti-xray to prevent cheating while minimizing performance impact.
- `use-faster-eigencraft-redstone: true`: Uses a more efficient redstone algorithm.
- `armor-stands-tick: false`: Prevents armor stands from ticking, reducing entity update load.
- `per-player-mob-spawns: true`: Enables per-player mob spawning for more balanced gameplay and controlled entity counts.
- `alt-item-despawn-rate`: Configures faster despawn rates for common blocks to reduce entity count.
- `max-entity-collisions: 2`: Further limits entity collisions to reduce CPU load.
- `tick-rates`: Reduces tick rates for various game mechanics to save CPU cycles.
- `collisions`: Optimizes collision handling to reduce server load.
- `entity-per-chunk-save-limit`: Limits the number of certain entities saved per chunk to reduce file size and improve save/load times.
- `prevent-moving-into-unloaded-chunks: true`: Prevents players from entering unloaded chunks, reducing chunk loading strain.
- `use-faster-threadlocalrandom: true`: Uses a faster random number generator for improved performance.
- `lava-flow-speed`: Slows down lava flow to reduce block updates and CPU usage.

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

Explanations:
- `use-alternative-item-despawn-rate: true`: Enables more granular control over item despawn rates.
- `use-faster-night-skip: true`: Optimizes the night skipping process for better performance.
- `use-faster-eigencraft-redstone: true`: Uses an optimized redstone algorithm (similar to Paper).
- `dont-send-useless-entity-packets: true`: Reduces network traffic by not sending unnecessary entity packets.
- `dont-send-useless-lightning-packets: true`: Reduces network traffic by not sending unnecessary lightning packets.
- `keep-spawn-loaded: false`: Prevents the spawn chunks from staying loaded, saving server resources.
- `keep-spawn-loaded-range: 8`: Sets the range of spawn chunks to keep loaded if the above option is true.
- `mobs.cow/chicken.ridable/controllable: true`: Allows cows and chickens to be ridden and controlled, which can be fun for players without significant performance impact.
- `gameplay-mechanics`:
  - `disable-ice-and-snow: true`: Disables ice and snow formation to reduce block updates.
  - `disable-teleportation-suffocation-check: true`: Disables suffocation checks during teleportation, improving teleport performance.
  - `disable-chest-cat-detection: true`: Disables the check for cats sitting on chests, reducing entity interactions.
  - `disable-end-credits: true`: Disables end credits to save resources.
  - `disable-phantom-spawns: true`: Disables phantom spawning, reducing entity count and associated AI calculations.
  - `disable-pillager-patrols: true`: Disables pillager patrols, reducing entity count and associated AI calculations.

These configurations are designed to optimize various aspects of server performance while maintaining gameplay balance. Always test these settings on a staging server before applying them to a production environment, as some optimizations may affect gameplay mechanics.


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

## MONITORING AND TROUBLESHOOTING

Continuous monitoring and troubleshooting are crucial for maintaining an optimized Minecraft server. Here are some tools and techniques to help you keep your server running smoothly:

1. **Timings Reports**: Use `/timings report` in-game or console to generate a detailed report of server performance. This helps identify plugins or areas of the game causing lag.

2. **Spark Profiler**: If installed, use `/spark profiler` to get more detailed performance analysis, including CPU usage breakdowns.

3. **Console Logging**: Regularly check your server console for warnings, errors, or unusual messages that might indicate performance issues.

4. **Performance Monitoring Plugins**: Consider using plugins like LagMonitor or ServerStats to get real-time performance data.

5. **External Monitoring Tools**: Use external monitoring services like UptimeRobot to keep track of your server's availability.

6. **Regular Performance Audits**: Schedule regular audits of your server's performance, checking things like TPS (ticks per second), memory usage, and CPU load.

## BEST PRACTICES FOR ONGOING MAINTENANCE

To keep your Minecraft server optimized over time, consider the following best practices:

1. **Regular Updates**: Keep your server software, plugins, and Java runtime up to date to benefit from the latest optimizations and security patches.

2. **Plugin Management**: Regularly review your plugins. Remove any that are no longer needed, and look for lighter alternatives to heavy plugins.

3. **World Management**: 
   - Regularly prune unused chunks to keep world sizes manageable.
   - Consider using a world border to limit world size.
   - Periodically reset resource-intensive dimensions like The End or The Nether.

4. **Backup Strategy**: Implement a robust backup strategy to protect against data loss and allow for quick recovery in case of issues.

5. **Player Education**: Educate your players about lag-inducing behaviors (like creating overly complex redstone contraptions) and server-friendly practices.

6. **Scheduled Restarts**: Implement scheduled server restarts (e.g., daily) to clear memory and reset any accumulated issues.

7. **Performance-Based Decisions**: Make gameplay decisions with performance in mind. For example, limit the use of entities as decorations or the complexity of automatic farms.

8. **Scalability Planning**: Plan for scalability. As your server grows, be prepared to upgrade hardware or optimize further.

9. **Community Feedback**: Encourage your community to report performance issues and consider their feedback in your optimization efforts.

10. **Stay Informed**: Keep up with the latest Minecraft server optimization techniques by following relevant forums, blogs, and community discussions.

## CONCLUSION

Optimizing a Minecraft server is an ongoing process that requires attention to detail, regular maintenance, and a willingness to adapt to changing conditions. By implementing the configurations and practices outlined in this guide, you'll be well on your way to running a smooth, efficient Minecraft server.

Remember that every server is unique, with its own set of plugins, player behaviors, and hardware limitations. Use this guide as a starting point, but don't be afraid to experiment and find the perfect balance for your specific server.

## Credits

- Maddy Miller - https://madelinemiller.dev/blog/
- PaperMC Documentation - https://docs.papermc.io/paper/optimization
- Aikar's Flags - https://aikar.co/2018/07/02/tuning-the-jvm-g1gc-garbage-collector-flags-for-minecraft/