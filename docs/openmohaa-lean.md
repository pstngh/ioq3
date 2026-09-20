# OpenMoHAA-style leaning

Build and run the modified client, game, and cgame together. This changes the
player-state network format and uses protocol 72, so both client and server
must be built from this fork. Existing protocol 71 servers and demos are not
compatible with this lean state.

Copy `misc/openmohaa-lean.cfg` into your `baseq3` game directory, then enter
`exec openmohaa-lean.cfg` in the console. Put that command in `autoexec.cfg`
if you want the keys loaded on each launch. The binds apply only to your local
config. Shift leans left, Space leans right, F jumps, C toggles between running
and walking, and X crouches. The config also selects the rebuilt native game
and cgame modules; install those in the active `baseq3` game directory.

The movement equations and parameters are from OpenMoHAA's Allied Assault
multiplayer profile: 40-degree maximum, 10 approach factor, 15 recovery
factor, and 4 speed factor. The eye rotates around a point 28.7 units below
it. Quake 3's player models and weapon system differ from OpenMoHAA's, so
the camera, shot origin, and torso use matching lean angles while retaining
Quake 3's existing animations. Bots cannot lean.

Reference code: [OpenMoHAA movement](https://github.com/openmoh/openmohaa/blob/main/code/fgame/bg_pmove.cpp),
[profile values](https://github.com/openmoh/openmohaa/blob/main/code/cgame/cg_predict.c), and
[camera offset](https://github.com/openmoh/openmohaa/blob/main/code/cgame/cg_view.c).
