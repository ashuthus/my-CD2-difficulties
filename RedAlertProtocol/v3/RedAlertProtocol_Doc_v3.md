# Red Alert Protocol

## Table of Contents <!-- omit in toc -->

- [Concept](#concept)
- [Public Lobby Notes](#public-lobby-notes)
- [What's New v3](#whats-new-v3)
- [Enemy Count Targets](#enemy-count-targets)
- [Average Parameter Values Compared to Hazard 5](#average-parameter-values-compared-to-hazard-5)
- [Changes](#changes)
  - [General Difficulty](#general-difficulty)
  - [Mission Events](#mission-events)
  - [Stationary Enemy Changes](#stationary-enemy-changes)
  - [Elite \& Custom Enemies](#elite--custom-enemies)
  - [Mission-specific Changes](#mission-specific-changes)
  - [Miscellaneous](#miscellaneous)
- [Experimental Features](#experimental-features)
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

## What's New v3

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

## Enemy Count Targets

- ME0 : ~Haz5   x 1.5
- ME1 : ~Haz6   x 1.5
- ME2 : ~Haz5.5 x 2

Enemy counts are tuned for each Hazard 5+ Modifier level,  
allowing the selected Modifiers to remain the primary driver of difficulty.

## Average Parameter Values Compared to Hazard 5

- Enemy Count Modifier         : 1.113 -> 1.58 (ME1: 1.89 / ME2: 2.36)
- Encounter Difficulty         :   337 -> 190
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

- Enemy Count scaling adjusted separately for ME0 / ME1 / ME2 (Haz5x1.5 / Haz6x1.5 / Haz5.5x2)
- Tuned to create Haz5.5x2-like enemy density with combat intensity focused on Swarm events
- Reduced enemy pressure outside of Alert Swarms (Encounter / Stationary / Enemy Normal Wave)
- Rebalanced spawn counts for enemies disproportionately affected by Enemy Count scaling
  - Crawler, Ossirian Pit Jaw and Ossirian Scrab

### Mission Events

- Added Gold Risk system
  - Mining a certain amount of Gold triggers an event (Compressed Gold excluded)
  - Displays warning messages at 50%, 75%, and 90% progress
  - Displays a final alert when the event is triggered
  - At 75% progress, periodic Mini Waves of Elite Ebonite Glyphid Grunts begin appearing
  - Reaching 100% progress attracts an Elite Glyphid Crassus Detonator
- Added RED ALERT system
  - Alert Swarms have a low chance to escalate into a RED ALERT
  - Base RED ALERT chance is 10%
  - Each normal Swarm increases the chance by 5%, up to a maximum of 20%
  - Triggering a RED ALERT resets the chance back to 10%
  - RED ALERT events display a warning message when the Swarm begins
  - Triggers a separate bonus wave worth ~25% of the original Swarm
    - Experimental RED ALERT variants: Grunt, Mactera, Ranged, and Exploder Reinforcements

### Stationary Enemy Changes

- Stationary Difficulty can no longer roll empty results  
  (average value adjusted from 158 to 168 while maintaining  
   roughly Hazard 5-equivalent total difficulty after Enemy Count scaling)
- Increased Stationary Enemy Diversity from 2–4 to 3–5
- Added Elite Cave Leech  
  (40% slower tentacle speed, 25% increased effective HP, ~173 EHP on P4, silent)
- Brood Nexus adjustments
  - Brood Nexus can now spawn creatures other than Glyphid Spawn  
    (because they tend to be ignored)
  - Increased creature spawn interval from 10s to 30s
  - Reduced death-spawn count from 15 to 10

### Elite & Custom Enemies

- Added Sentinel to the Enemy Pool at a spawn rate similar to Praetorian
- Added Acid Queen to the Special Pool at a spawn rate similar to Menace  
  (DamageMultiplier set to 5.5, reducing effective HP to ~545)
- Fix Elite damage-resistance scaling
- Added custom Enemy groups (LST, HVT, Special, and Disruptive)
  - Enemy promotions are now regulated by group-specific cooldowns
  - Only one enemy per group can be promoted when a cooldown becomes available
- Added Elite Septic Spreader to the Ranged Special Enemy group  
  (fires frost projectiles instead of Red Sepsis, 480 EHP on P4, 2x temperature thresholds)
- Added Elite Stingtail to the HVT Disruptive Enemy group  
  (shorter grab cooldown, immune to fear, 480 EHP on P4, 1.5x temperature thresholds)
- Added Elite Warden to the LST Disruptive Enemy group  
  (1.5x buff radius, immune to stun and fear, 1200 EHP on P4, 1.5x temperature thresholds)
- Added Mactera Fire Bomber to the LST Disruptive Enemy group  
  (can only be promoted from Mactera Goo Bomber)

### Mission-specific Changes

- All Missions
  - Increased enemy count during Extraction phases (including Point Extraction escape countdown)
- On-site Refining
  - Reduced enemy pressure during broken pipeline events in Refinery
- Salvage Operation
  - Mini Mule leg scan duration is reduced from 2s to 1s
  - Repair duration scales with player count from 10s to 10 / 20 / 30 / 40s
  - Number of required legs for repair is randomized between 2–5
  - Interaction multiplier for MiniMule, Uplink, and Refuel is set to x5 for multiplayer scaling
  - Enemy count gradually increases over time during Salvage extraction
    - Enemy pressure continuously escalates throughout the entire extraction phase
    - Enemy count reaches approximately 2x by the time the Drop Pod doors open
    - Enemy count continues increasing until extraction is complete
- Point Extraction
  - Reduced enemy pressure in Point Extraction
- Escort Duty
  - Removed the large-hit damage threshold
  - Reduced large-hit resistance from 0.5 to 0.75

### Miscellaneous

- Added sound cue when a player is downed
- Added global spawn sound cue for Acid Queen
- Added Space Rig tips for this difficulty
  - Displays information about custom mechanics, enemies, and gameplay changes
- QoL: Disabled Mission Control warnings when no players are inside the Uplink/Fuel Cell zone
- QoL: Adjusted solo penalty behavior when no players are inside the Uplink/Fuel Cell zone
- CD2-only: Renamed custom Elite variants
- CD2-only: Adjusted colors for selected custom Elite variants

## Experimental Features

- General Difficulty
  - Increased MinPoolSize from 8 to 10  
    (to preserve enemy variety after expanding the EnemyPool)
  - Increased StationaryEnemyCount from 4 to 5  
    (to maintain Stationary enemy variety after adding Elite Cave Leech)
- Gold Risk system
  - Updated Elite Ebonite Grunt behavior
    - Continues to appear after reaching 75% Gold Risk progress
    - Added collision, allowing players to stomp and defeat it (Goomba-style)
    - Now drops enough Gold to increase Gold Risk progress by 1%
  - Updated Elite Crassus Detonator
    - Added a permanent outline
- Stationary Enemy Changes
  - Increased Elite Cave Leech EHP to 240 on P4
  - Increased Cave Leech MaxDropPlayerDuration from 2 to 10
- Elite & Custom Enemies
  - Added Crawler to the Enemy Pool with a spawn rate similar to Tri-Jaw  
    (same temperature thresholds as Spreader, 35 ignite threshold, -50 freeze threshold)
  - Added Elite Trawler to the Melee Special Enemy group  
    (480 EHP on P4, 2x temperature thresholds, more aggressive behavior)
  - Added Elite Youngling to the Melee Special Enemy group  
    (300 EHP on P4, 1.5x temperature thresholds, prioritizes rolling attacks)
  - Added Elite Patrol Bot to the HVT Disruptive Enemy group  
    (324 EHP on P4, 0.5x ignite threshold, 0.4x freeze threshold,  
     rapidly fires normal projectiles, no bump attack, cannot be hacked)
  - Increased Acid Queen EHP from 545 to 600 and Poison Damage Resistance increased to 80%  
    (make it less likely to drop below half health from its own area attacks)
  - Changed Acid Queen spawn behavior (to preserve Special Enemy Pool variety)
    - Removed from the Special Pool
    - Now promoted from Acid Spitters with a 10% chance
    - Added to the Ranged Special Enemy Group
  - Increased Elite Warden buff radius and maximum buffed targets to 2x
- Enemy Balance
  - Limited Swarmer MaxSpawnCount to 100
  - Limited Shredder MaxSpawnCount to 20
  - Limited Egg Spider spawn count to 1
  - Reduced Swarmer resistance to freezing (FreezeTemperature 20 -> 8) (from VEA)
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
  - Removed Piercing resistance from Praetorian (include Frost) and Oppressor (from VEA)
- Mission-specific Changes
  - Added Dread Helper
    - A custom Bulk Detonator that may appear as an additional threat during Dreadnought encounters
    - A set of Dreadnought types eligible for Dread Helper is selected at mission start
    - Results in a ~46% average chance of Dread Helper appearing per encounter
  - Egg Hunt
    - Increased enemy counts during non-Swarm Egg ambushes  
      (scales with player count: x2.0 / x2.0 / x2.5 / x3.0)
  - Salvage Operation
    - Added Sentinel reinforcements during Uplink and Refuel defense phases (to discourage overly defensive terrain setups)
  - Sabotage
    - Added periodic Phase Bombs during Hack-C defense phases
    - Note: A separate mod is recommended for vanilla Stationary enemy spawning in Sabotage due to hardcoded behavior
- Miscellaneous
  - Added mission-specific gameplay notifications
    - Displays important gameplay changes at the start of affected missions
  - CD2-only: Renamed Sentinel, Crawler, and similar enemies to distinguish them from event spawns

## Future Plans

- Gold mining system improvements
  - Balance adjustments and event tuning
  - Additional mining-related enemy encounters
  - Remove Elite status from the Gold Risk Crassus Detonator
    - Restore its Gold appearance and improve compatibility with Direct controls
    - Changed death carve diameter to match a normal Bulk Detonator
    - Removed meatballs on death
- Expanded RED ALERT mechanics
  - Additional RED ALERT-exclusive enemies and encounters
    - e.g. Enemy Mutations, more Elites, etc.
  - Further balance adjustments and event tuning
- Mission-specific mechanics and adjustments
  - Restrict Stationary and Special enemies during Escort phases (e.g. Fire Bomber, Scalebramble)
  - Adjust Drillevator enemy settings
  - Balance adjustments for Egg Hunt, Elimination, and Sabotage
  - Implement Waves for Elimination and Sabotage
- Additional Elite variants and spawn rate adjustments
  - Add Elite variants that do not exist in vanilla
  - Add high-threat Elite variants
  - Increase the importance of dealing with high-Courage enemies, LST and HVT
- Increased number and variety of stationary enemies
- Balance temperature thresholds
  - Adjust Dreadnought ignition thresholds
- Balance Fear mechanics
- Adjust spawn counts for certain enemies affected by higher Enemy Count Modifier and More Enemies
  - e.g. Scrab, Turret, Patrol Bot, Nemesis
- Additional QoL improvements
  - Disable terrain destruction from Bulk Detonators during Salvage
- Add resupply availability messages (for future Nitra cost changes)
