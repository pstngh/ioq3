# OpenMoHAA-style leaning

Build and run the modified client, game, and cgame together. This changes the
player-state network format and uses protocol 72, so both client and server
must be built from this fork. Existing protocol 71 servers and demos are not
compatible with this lean state.

Copy `misc/openmohaa-lean.cfg` into your `baseq3` game directory, then enter
`exec openmohaa-lean.cfg` in the console. Put that command in `autoexec.cfg`
if you want the keys loaded on each launch. The binds apply only to your local
config. Shift leans left, Space leans right, F jumps, C toggles between running
and walking, and X crouches. The config also selects the rebuilt native game,
cgame, and UI modules and sets `cg_fov` to 80 degrees at 4:3; install the
modules in the active `baseq3` game directory. Local matches use `sv_pure 0`
so the matching native cgame can load. As in OpenMoHAA, the horizontal FOV
adjusts to the viewport's aspect ratio while preserving the 4:3 vertical
view: 80 degrees at 4:3 becomes about 96.42 degrees at 16:9. The native UI
and HUD retain their proportions instead of stretching across a wide screen.
Set `cg_drawviewmodel 0` to hide your first-person weapon without hiding other
players' weapons. Set it back to `2` to show the weapon again.

For 1920x1080 fullscreen, set `r_mode -1`, `r_customwidth 1920`,
`r_customheight 1080`, and `r_fullscreen 1`, then run `vid_restart`.
For a high-refresh display, set `r_displayRefresh` to its supported refresh
rate before `vid_restart` (for example, `r_displayRefresh 240`). To fill a
local free-for-all match with four bots plus yourself, set `bot_minplayers 5`.
If the FPS counter (`cg_drawFPS 1`) stays below the display rate, the OpenGL 1
renderer can be selected with `cl_renderer opengl1` followed by `vid_restart`.

The movement equations and parameters are from OpenMoHAA's Allied Assault
multiplayer profile: 40-degree maximum, 10 approach factor, 15 recovery
factor, and 4 speed factor. The eye rotates around a point 28.7 units below
it. Quake 3's player models and weapon system differ from OpenMoHAA's, so
the camera, shot origin, and torso use matching lean angles while retaining
Quake 3's existing animations. Bots cannot lean.

Reference code: [OpenMoHAA movement](https://github.com/openmoh/openmohaa/blob/main/code/fgame/bg_pmove.cpp),
[profile values](https://github.com/openmoh/openmohaa/blob/main/code/cgame/cg_predict.c), and
[camera offset](https://github.com/openmoh/openmohaa/blob/main/code/cgame/cg_view.c).
