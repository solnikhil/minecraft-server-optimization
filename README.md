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
simulation-distance=6
network-compression-threshold=256
max-players=20
entity-broadcast-range-percentage=100
max-world-size=29999984
spawn-protection=16
max-tick-time=60000
use-native-transport=true
enable-jmx-monitoring=false
enable-command-block=false
allow-nether=true
sync-chunk-writes=true
enable-query=false
prevent-proxy-connections=true
spawn-monsters=true
enforce-whitelist=false
spawn-npcs=true
generate-structures=true
max-chained-neighbor-updates=1000000
```