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