# Pocket Boost (Fabric, Minecraft 1.21.1, client only)

Adaptive quality governor for low-end devices. It checks your FPS every second.
If the average stays low, it steps down a ladder of vanilla settings. When FPS
has been healthy for a while, it steps back up and finally restores YOUR own
settings exactly.

No mixins. It only changes vanilla options, so it cannot conflict with Sodium,
Lithium, FerriteCore, Iris or Fabric API. Lowering simulation distance also
reduces how many entities the singleplayer server ticks (extra help on top of
Lithium).

## Quality ladder
1. Entity shadows off, clouds off
2. Fewer particles, entity distance 0.75
3. Render distance -2, simulation distance 8
4. Render distance -4, simulation distance 6, minimal particles
5. Render distance = minViewDistance (default 4), simulation distance 5, entity distance 0.5

It never raises anything above what you had set yourself.

## Chat commands
- /pocketboost          status
- /pocketboost on|off   enable or disable (off restores your settings)
- /pocketboost reset    restore your own settings right now

Tip: if you want to change video settings yourself, run /pocketboost reset first.

## Config: config/pocketboost.properties (created on first launch)
- lowFps (24): average below this lowers quality
- highFps (45): average above this for recoverSeconds raises quality
- windowSeconds (5): seconds of FPS averaged
- recoverSeconds (30): seconds above highFps before restoring a step
- graceSeconds (20): ignored time after joining a world / changing dimension
- minViewDistance (4): lowest render distance it may use
- notifyChanges (true): action-bar message on changes
Keep highFps under your FPS cap (Pojav default is fine) or it will never restore.

## Build
Option A - on a PC: install JDK 21 and Gradle 8.10+, then run `gradle build` in this folder.
Option B - on the phone: upload this folder to a new GitHub repo; the included
workflow (.github/workflows/build.yml) builds it. Download the jar from the
Actions run's Artifacts.
The jar is build/libs/pocketboost-1.0.0.jar (not the -sources one). Put it in your mods folder.
