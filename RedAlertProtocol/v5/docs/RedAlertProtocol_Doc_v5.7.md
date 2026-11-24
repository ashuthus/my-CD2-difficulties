# Red Alert Protocol

> This doc is based on Red Alert Protocol v5.7.

## Table of Contents <!-- omit in toc -->

- [Concept](#concept)
- [Public Lobby Notes](#public-lobby-notes)
- [What's New](#whats-new)
  - [v5 - Encounter Overhaul](#v5---encounter-overhaul)
  - [v4 - Combat Expansion](#v4---combat-expansion)
  - [v3 - Gameplay Expansion](#v3---gameplay-expansion)
  - [v2 - Events](#v2---events)
  - [v1 - Core Difficulty](#v1---core-difficulty)
- [Enemy Count Targets](#enemy-count-targets)
- [Average Parameter Values Compared to Hazard 5](#average-parameter-values-compared-to-hazard-5)
- [Changes](#changes)
  - [General Difficulty](#general-difficulty)
  - [Mission Events](#mission-events)
  - [Stationary Enemy Changes](#stationary-enemy-changes)
  - [Elite \& Custom Enemies](#elite--custom-enemies)
  - [Enemy Balance](#enemy-balance)
  - [Mission-specific Changes](#mission-specific-changes)
  - [Miscellaneous](#miscellaneous)
- [Current Changes](#current-changes)
- [Future Plans](#future-plans)

## Concept

A public-lobby-oriented difficulty based on Hazard 5 pacing and core gameplay,  
while preserving the vanilla experience.

Generally designed around T1 difficulty,  
but may reach T2 levels depending on the mission, events, cave generation, and other mods in use.  
(e.g. additional Stationary enemies in Sabotage or custom cave layouts)

Designed to scale enemy counts through the Hazard 5+ More Enemies modifier,  
with ME2 targeting Haz5.5x2-like enemy density.

Difficulty peaks are concentrated around Alert Swarms,  
while pressure outside major engagements is kept roughly comparable to vanilla.

Emphasizes target prioritization, situational awareness, and Nitra management alongside increased enemy density.
Features custom enemies, Elite variants, events, and mission-specific gameplay adjustments.

## Public Lobby Notes

- Balanced for public lobbies
- No client-side mods required
- Alert Swarms are the primary source of danger
- Prioritizing high-value targets is essential
- Nitra cost: 80

## What's New

### v5 - Encounter Overhaul

- Egg Hunt Adjustments  
  Reworked non-Swarm Egg Ambush enemy count scaling to increase with each successive ambush
- Expanded RED ALERT variants  
  Added Heavy (multiplayer only) and Swarmer Waves to increase encounter variety
- Expanded RED ALERT coverage  
  Point Extraction Swarms, Salvage Uplink / Refuel defense phases, and On-site Refining's refining phase can now trigger RED ALERT
- Added a Halloween event featuring Elite Halloween Skull

### v4 - Combat Expansion

- Stationary Enemy Expansion  
  Added Elite Breeder and Sprout as new Stationary Enemy variants.
- New Elite Enemy Variants  
  Added new Elite enemy variants and expanded promotion behavior.
- Enemy Balance Improvements  
  Adjusted Fear resistance and improved the viability of Fire-based builds against Dreadnoughts.
- Dreadnought Encounter Adjustments  
  Reduced Dread Helper health to improve the balance of Dreadnought encounters.
- Mission-specific Improvements  
  Adjusted Industrial Sabotage, Salvage Extraction, Point Extraction, and Deep Scan.

### v3 - Gameplay Expansion

- New Enemy Variants  
  Added Crawler, Elite Trawler, Elite Youngling, and Elite Patrol Bot.
- Expanded Enemy Group System  
  Added the Melee Special group and expanded the HVT Disruptive group to support the new Elite variants.
- Expanded Enemy Pools  
  Expanded Enemy Pool and Stationary Pool sizes to preserve encounter variety.
- Mission Event Improvements  
  Added a Bulk Detonator event for Dreadnought encounters, player-count scaling to Egg Waves, and Phase Bombs during Hack-C.
- Enemy Balance Improvements  
  Rebalanced various enemies, including Elite and custom variants, and adjusted spawn and temperature settings.

### v2 - Events

- Introduced RED ALERT and Gold Risk events

### v1 - Core Difficulty

- Established the core difficulty and enemy scaling of Red Alert Protocol

## Enemy Count Targets

- ME0 : ~Haz5   x 1.5
- ME1 : ~Haz6   x 1.5
- ME2 : ~Haz5.5 x 2

Enemy counts are tuned for each Hazard 5+ Modifier level,  
allowing the selected Modifiers to remain the primary driver of difficulty.

## Average Parameter Values Compared to Hazard 5

- Enemy Count Modifier         : 1.113 -> 1.58 (ME1: 1.89 / ME2: 2.36)
- Encounter Difficulty         :   337 -> 240
- Stationary Difficulty        :   158 -> 168  *1
- Enemy Wave Interval (Alert)  :  240s -> 241s
- Enemy Normal Wave Interval   :  161s -> 211s *2
- Enemy Normal Wave Difficulty :   400 -> 270  *2

*1 Stationary enemies are now more consistent.  
   Empty rolls have been removed, while the average difficulty  
   remains close to Hazard 5 after accounting for Enemy Count scaling.

*2 Normal Waves are heavily reduced on average  
   to shift the difficulty focus toward Alert Swarms.

However, high-roll values can still occur:

- ~10% chance for ~105s intervals
- ~5% chance for ~600 difficulty

Note:  
Aggressive Enemies can push speed modifiers beyond Hazard 7 levels  
when combined with this preset.

Expect highly aggressive enemies and occasionally overtuned behavior.

## Changes

### General Difficulty

- Adjusted EnemyCount scaling separately for ME0 / ME1 / ME2  (Haz5x1.5 / Haz6x1.5 / Haz5.5x2)
- Reduced enemy pressure outside of Alert Swarms (Encounter / Stationary / Enemy Normal Wave)
- Increased MinPoolSize from 8 to 10  
  (to preserve enemy variety after expanding the EnemyPool)
- Adjusted Elite damage resistance to 1.3 / 1.3 / 1.5 / 1.65 by player count

### Mission Events

- Added Gold Risk system
  - Mining a certain amount of Gold triggers an event (Compressed Gold excluded)
  - Displays warning messages at 50%, 75%, and 90% progress
  - Displays a final alert when the event is triggered
  - At 75% progress, periodic Mini Waves of Elite Ebonite Glyphid Grunts begin appearing
    - Added collision, allowing players to stomp and defeat them (Goomba-style)
    - They now drop enough Gold to increase Gold Risk progress by 1%
  - Reaching 100% progress attracts an Elite Glyphid Crassus Detonator
    - Added a permanent outline
- Added RED ALERT system
  - Alert Swarms have a low chance to escalate into a RED ALERT
  - Base RED ALERT chance is 15%
  - Each normal Swarm increases the chance by 5%, up to a maximum of 25%
  - Triggering a RED ALERT resets the chance to 0%
  - RED ALERT events display a warning message when the Swarm begins
  - Triggers a separate bonus wave, tuned to roughly 50% of the original Swarm
    - RED ALERT variants: Grunt, Mactera, Ranged, and Exploder Reinforcements
  - Added an audio cue when RED ALERT is triggered

### Stationary Enemy Changes

- Stationary Difficulty can no longer roll empty results  
  (average value adjusted from 158 to 168 while maintaining  
   roughly Hazard 5-equivalent total difficulty after Enemy Count scaling)
- Increased StationaryEnemyCount from 4 to 5, or 6 when Sprout is available
- Increased Stationary Enemy Diversity from 2–4 to 3–5, or 4–6 when Sprout is available
- Added Elite Cave Leech  
  (40% slower tentacle speed, 25% increased effective HP, 240 EHP on P4, silent)
- Brood Nexus adjustments
  - Brood Nexus can now spawn creatures other than Glyphid Spawn  
    (because they tend to be ignored)
  - Increased creature spawn interval from 10s to 30s
  - Reduced death-spawn count from 15 to 10
- Increased Cave Leech MaxDropPlayerDuration from 2 to 10
- Added Sprout to the Stationary Pool at a spawn rate similar to Barrage Infector  
  (Faster projectiles with standard Sprout damage)
- Added Elite Breeder
  - 33% promotion chance, no Enemy Group
  - 5× movement speed, 2,250 effective HP on P4
  - Eggs spawn 4 enemies instead of regular Hatchlings
  - Egg count and enemies spawned per Egg are reduced based on the number of downed dwarves
  - Spawns Hatchlings on death

### Elite & Custom Enemies

- Added Sentinel to the Enemy Pool at a spawn rate similar to Praetorian
- Added Crawler to the Enemy Pool with a spawn rate similar to Tri-Jaw
  - Temperature thresholds: Same as Spreader (Ignite 35, Freeze -50)
  - MaxSpawnCount: 2/2/3/4 based on player count
- Added custom Enemy groups (LST Disruptive, HVT Disruptive, Melee Special, and Ranged Special)
  - Enemy promotions are now regulated by group-specific cooldowns
- Added Acid Queen to the Ranged Special Enemy Group
  - DamageMultiplier set to 5, ~600 EHP
  - Poison Damage Resistance increased to 80%  
    (to make it less likely to drop below half health from its own area attacks)
  - Promoted from Acid Spitters with a 10% chance
- Added Elite Snowball Spreader to the Ranged Special Enemy Group  
  (fires frost projectiles instead of Red Sepsis, 480 EHP on P4, 2x temperature thresholds)
- Added Elite Stingtail to the HVT Disruptive Enemy Group  
  (shorter grab cooldown, immune to fear, 480 EHP on P4, 1.5x temperature thresholds)
- Added Elite Warden to the LST Disruptive Enemy Group  
  (2x buff radius and maximum buffed targets, immune to stun and fear, 1200 EHP on P4, 1.5x temperature thresholds)
- Added Mactera Fire Bomber  
  (can only be promoted from Mactera Goo Bomber)
- Added Elite Trawler to the Melee Special Enemy Group  
  (480 EHP on P4, 2x temperature thresholds, more aggressive behavior)
- Added Elite Youngling to the Melee Special Enemy Group  
  (300 EHP on P4, 1.5x temperature thresholds, prioritizes rolling attacks)
- Added Elite Patrol Bot to the HVT Disruptive Enemy Group  
  (324 EHP on P4, 0.5x ignite threshold, 0.4x freeze threshold,  
   rapidly fires normal projectiles, no bump attack, cannot be hacked)
- Added Elite Frost Bomber to the LST Disruptive Enemy Group
  - Promoted from Mactera Goo Bomber (except in Magma Core)
  - 1200 EHP on P4, Burn Temperature 52.5, Douse Temperature 7.5, Freeze Temperature 375, Warming Rate 60
  - Fires Snowball projectiles
- Added Elite Fire Bomber to the LST Disruptive Enemy Group
  - Promoted from Mactera Goo Bomber (except in Glacial Strata)
  - 1200 EHP on P4, Burn Temperature 52.5, Douse Temperature 7.5, Freeze Temperature 250, Warming Rate 40
  - Fires Hiveguard Fire Mortars (each projectile deals damage equivalent to a Sprout)
- Added Elite Swarmer to the Melee Special Enemy Group
  - 108 EHP on P4, 5x movement speed, 2x attack damage
  - Immune to fear, does not die when ignited or frozen
  - Burn Temperature 6, Douse Temperature 2, Freeze Temperature -6, Unfreeze Temperature 0, Cooling Rate 6, Warming Rate 6
- Added Elite Exploder to the Melee Special Enemy Group
  - 108 EHP on P4, 2x movement speed, 40% increased explosion range
  - Immune to fear and stun, Exploder Infestation variants cannot be promoted
  - Burn Temperature 999, Douse Temperature 0, Freeze Temperature -999, Unfreeze Temperature 0, Cooling Rate 100, Warming Rate 100
- Added Elite Stalker to the HVT Disruptive Enemy Group
  - 432 EHP on P4, 1.5x movement speed, 0.75x attack damage
  - Immune to fear, Stagger Duration x1, Stagger Immunity 2s
  - Damage Threshold reduced from 80 (normal Stalker) to 40
  - Burn Temperature 45, Freeze Temperature -75
- Added Elite Fireball Spreader to the Ranged Special Enemy Group
  - Promoted from Septic Spreader only in Magma Core
  - 480 EHP on P4, 2x movement speed, 0.6x attack damage
  - Fires Hiveguard Fire Mortars
  - Burn Temperature 70, Douse Temperature 10, Freeze Temperature -100, Unfreeze Temperature 0, Cooling Rate 6, Warming Rate 12

### Enemy Balance

- Adjusted vanilla event Crawler spawn count (MinSpawnCount 1 -> 0, MaxSpawnCount 9999 -> 1)
- Adjusted Scrab spawn count (MinSpawnCount 4 -> 1, MaxSpawnCount 9999 -> 20, SpawnAmountModifier 1 -> 0.5)
- Adjusted Pit Jaw spawn count (MinSpawnCount 1 -> 0, MaxSpawnCount 9999 -> 1, SpawnAmountModifier 1 -> 0.5)
- Limited Swarmer MaxSpawnCount to 100
- Limited Shredder MaxSpawnCount to 20
- Limited Egg Spider spawn count to 1
- Reduced Goo Bomber resistance to freezing (FreezeTemperature 320 -> 250, WarmingRate 50 -> 40)
- Reduced Fire Bomber resistance to freezing (FreezeTemperature 320 -> 250, WarmingRate 50 -> 40)
- Reduced Frost Bomber resistance to freezing (FreezeTemperature 560 -> 375, WarmingRate 75 -> 60)
- Reduced Youngling temperature thresholds by 25% (FreezeTemperature 90, BurnTemperature 75)
- Increased Menace resistance to freezing (FreezeTemperature 50 -> 100, UnfreezeTemperature 0 -> 50, WarmingRate 6 -> 10)
- Reduced Patrol Bot resistance to freezing (FreezeTemperature 375 -> 150, UnfreezeTemperature 10)
- Reduced Shredder resistance to freezing (FreezeTemperature 1250 -> 75, WarmingRate 20 -> 30)
- Reduced Nemesis resistance to freezing (FreezeTemperature 300, UnfreezeTemperature 150, WarmingRate 75 -> 30)
- Reduced Sentinel SpawnSpread during Hiveguard encounters from 1500 to 500
- Increased Brood Nexus OnFireHeatRange from 150 to 250 (from VEA)
- Removed Piercing resistance from Praetorian (including Frost) and Oppressor (from VEA)
- Swarmer balance adjustments (excluding Dreadnought Pheromone Swarmer)
  - Reduced effective HP to 1/3
  - Changed Freeze Temperature to 8 (excluding Ice Glyphid Swarmer)
- Stalker: Attack Damage x0.75, Stagger Duration x1, Stagger Immunity 2s
- Fear balance adjustments
  - Increased Grunt-type Courage from 0.5 to 0.6
  - Increased Praetorian-type Courage from 0.5 to 0.6
  - Increased Mactera Spawn, Tri-Jaw, and Brundle Courage from 0 to 0.3
  - Increased Courage to 0.6 for special enemies: Spreader, Stalker, Stingtail, Warden, Grabber, and Bomber-type enemies
  - Note: Does not affect Fear effects with 250% or higher chance (e.g. Coil Gun, Aggressive Venting)
- Dreadnought temperature and Fire resistance adjustments
  - Changed Burn Temperature from 1000 to 100, Douse Temperature from 100 to 25, and Cooling Rate from 30 to 20
  - Increased Fire damage taken by 30% relative to vanilla resistance

### Mission-specific Changes

- All Missions
  - Increased enemy count during Extraction phases (including Point Extraction escape countdown)
- Egg Hunt
  - Increased enemy counts during non-Swarm Egg ambushes  
    (scales with player count: x2.0 / x2.0 / x2.5 / x3.0)
- On-site Refining
  - Reduced enemy pressure during broken pipeline events in Refinery
- Salvage Operation
  - Mini Mule leg scan duration is reduced from 2s to 1s
  - Repair duration scales with player count from 10s to 10 / 20 / 30 / 40s
  - Number of required legs for repair is randomized between 2–5
  - Interaction multiplier for MiniMule, Uplink, and Refuel is set to x5 for multiplayer scaling
  - Enemy count gradually increases over time during Salvage extraction
    - Enemy Count Modifier gradually increases from 2/3, reaching approximately 2x by the time the Drop Pod doors open
    - Enemy count continues increasing until extraction is complete
  - Added Sentinel reinforcements during Uplink and Refuel defense phases (to discourage overly defensive terrain setups)
- Point Extraction
  - Limited the vanilla-level Enemy Count Modifier reduction to the early phase
    - Remains at 2/3 for the first 2 minutes, then gradually increases back to 1.0x by approximately 7 minutes
- Escort Duty
  - Removed the large-hit damage threshold
  - Reduced large-hit resistance from 0.5 to 0.75
- Elimination
  - Added Dread Helper
    - A custom Bulk Detonator that may appear as an additional threat during Dreadnought encounters
    - A set of Dreadnought types eligible for Dread Helper is selected at mission start
    - Specially spawned Dreadnoughts are also eligible for Dread Helper
    - Results in a ~46% average chance of Dread Helper appearing per encounter
    - Reduced Dread Helper health to 11/12 (5500 HP on P4)
- Industrial Sabotage
  - Reduced Industrial Sabotage Turret count to 2/3
  - Added periodic Phase Bombs during Hack-C defense phases
  - Note: A separate mod is recommended for vanilla Stationary enemy spawning in Sabotage due to hardcoded behavior
- Deep Scan
  - Increased enemy count by 20% during the Drillevator phase

### Miscellaneous

- Added a random sound cue when a player is downed
- Added global spawn sound cue for Acid Queen
- Added Space Rig tips for this difficulty
  - Displays information about custom mechanics, enemies, and gameplay changes
- Added mission-specific gameplay notifications
  - Displays important gameplay changes at the start of affected missions
- QoL: Disabled Mission Control warnings when no players are inside the Uplink/Fuel Cell zone
- QoL: Adjusted solo penalty behavior when no players are inside the Uplink/Fuel Cell zone
- CD2-only: Renamed custom Elite variants
- CD2-only: Adjusted colors for selected custom Elite variants
- CD2-only: Renamed Sentinel, Crawler, and similar enemies to distinguish them from event spawns
- CD2-only: Custom Elite names omit redundant enemy family names (e.g. "Glyphid")

## Current Changes

- General Difficulty
  - Adjusted mission-specific Enemy Count Modifier compensation based on the P4 scaling (x1.4 relative to Haz5)
    - Point Extraction, Salvage Extraction, RefiningStalled, and Sabotage DuringEncounters
  - Increased average Encounter Difficulty from 190 to 240
    - Reduced extreme difficulty rolls in favor of more consistent encounters
  - Adjusted Swarm interval distribution
    - Reduced unusually short and long intervals, making Swarm timing more consistent
    - Maintained the average interval at approximately 241s
- Mission Events
  - Gold Risk
    - Adjusted GOLD RISK maximum Gold reward in Salvage based on Mini-Mule count
      - 2 Mini-Mules: 300 Gold / 3 Mini-Mules: 350 Gold
  - RED ALERT
    - Occurrence & Triggers
      - Updated RED ALERT occurrence chance
        - Initial chance: 20%, increasing by 5% per normal Swarm (max 30%)
        - Fixed at 20% after the first RED ALERT
      - Added Point Extraction Swarms as RED ALERT triggers
        - Unlike regular RED ALERTs, vanilla mechanics limit advance warning and preparation time
      - Added Salvage Uplink and Refuel defense phases as RED ALERT triggers
      - Added the On-site Refining refining phase as a RED ALERT trigger
      - Added Escort Duty's Ommoran Heartstone phase as a RED ALERT trigger
    - Variants & Wave Composition
      - Reworked RED ALERT variant selection logic
      - Equalized the selection weights of all RED ALERT variants
      - Added Heavy Wave (Praetorians and Sentinels, multiplayer only)
      - Added Swarmer Wave (Swarmers and Shockers)
      - Added Goo Bomber and Grabber to Mactera Wave compositions
      - Adjusted Mactera and Ranged Wave selection weights to better reflect vanilla enemy rarities
    - Spawn Patterns
      - Changed Ranged to use a Constant Pressure spawn pattern
      - Adjusted RED ALERT Difficulty during the On-site Refining phase by player count (x1.2 / x1.2 / x1.3 / x1.4)
    - Notifications & Fixes
      - Moved both notification timings 2 seconds earlier
      - Fixed timing inconsistencies when RED ALERT is retriggered
  - Halloween Event
    - Added Elite Halloween Skull
      - Movement speed: x1.5 (health unchanged)
      - Triggers an Instant Wave upon death
      - Displays a notification when spawned
- Elite & Custom Enemies
  - Increased Elite Stalker movement speed from x1.5 to x2.0
- Mission-specific Changes
  - Egg Hunt
    - Increased enemy counts during non-Swarm Egg ambushes
      - Base multiplier: x2.0, scaling from x0.8 to x1.2 with each successive ambush
      - Final multiplier: x1.6 / x1.8 / x2.0 / x2.2 / x2.4
  - Salvage Operation
    - Fixed Sentinel reinforcement spawn counts during Uplink and Refuel defense phases to match the intended values
    - Capped the Extraction Enemy Count Modifier at x2.0
  - Industrial Sabotage
    - Adjusted Encounter Difficulty to x1.4 and rebalanced Enemy Count Modifier compensation

## Future Plans

- General Difficulty
  - Review overall difficulty balance
- Mission Events
  - Gold mining system improvements
    - Balance adjustments and event tuning
    - Additional mining-related enemy encounters
    - Remove Elite status from the Gold Risk Crassus Detonator
      - Restore its Gold appearance and improve compatibility with Direct controls
      - Change death carve diameter to match a normal Bulk Detonator
      - Remove meatballs on death
  - Expanded RED ALERT mechanics
    - Rework additional Wave patterns and their Difficulty distribution
    - Test additional Wave patterns:
      - Peak: Follow the original Swarm spawn curve
      - Sustain: Compensate for the original Swarm's declining spawn intensity to maintain consistent spawn pressure throughout the Swarm
      - Constant Pressure: Reinforce the original Swarm Constant Pressure
      - Offset Pressure: Add Constant spawns offset from the original Swarm spawn timing
    - Additional RED ALERT-exclusive enemies and encounters
      - e.g. Enemy Mutations, more Elites, etc.
    - Continue adjusting overall RED ALERT event content and balance
- Elite & Custom Enemies
  - CD2-only: Change the appearance of Sentinel and Crawler spawned through the regular Enemy Pool
  - Adjust Elite Spreader snowball behavior
- Mission-specific Changes
  - Restrict Stationary and Special enemies during Escort phases (e.g. Fire Bomber, Scalebramble)
  - Balance adjustments for Egg Hunt, Elimination, and Sabotage
  - Implement Waves for Sabotage
  - Elimination
    - Adjust Dreadnought Health Gates
    - Rework Dread Helpers and add additional Waves
    - Make the purpose of Dread Helpers easier to understand for players unfamiliar with the system
- Additional Elite variants and spawn rate adjustments
  - Add Elite variants that do not exist in vanilla
  - Add Rockpox-derived Elite variants
  - Add high-threat Elite variants
  - Increase the importance of dealing with high-Courage enemies, LST and HVT
- Increased number and variety of stationary enemies
- Enemy Balance
  - Balance temperature thresholds
  - Balance Fear mechanics
  - Adjust spawn counts for certain enemies affected by higher Enemy Count Modifier and More Enemies
    - e.g. Scrab, Patrol Bot, Nemesis
- Miscellaneous
  - Additional QoL improvements
    - Disable terrain destruction from Bulk Detonators during Salvage
    - Improve tracking of enemies such as Acid Queen where spawn, health, and defeat status are important
  - Add resupply availability messages (for future Nitra cost changes)
