A Minecraft-inspired game, written entirely with Gemini AI 2.5 using Threes.js and HTML

![image](https://github.com/user-attachments/assets/c3395acd-7c59-445b-8bb2-1604e30c508d)

Create a Minecraft clone using Three.js (WebGLRenderer, no antialiasing), HTML, CSS, and JavaScript.

**The Promt:**

**World:**
* Generate a procedural world (default 48x48) using Perlin noise terrain.
* Include grass, dirt, and stone blocks based on height. Generate water blocks below Y=-1 (sea level). Max terrain height around 15.
* Use simple, procedurally generated pixel-art style textures for all block types (grass, dirt, stone, water). Water should be semi-transparent.
* Implement block placement (right-click) based on selected block type.
* Implement block removal (left-click) for *any* block.

**Player & Controls:**
* Implement a player controller using `PointerLockControls`.
* Use an intermediate `Object3D` (`playerObject`) for controls and collision, with the `Camera` as a child offset slightly upwards (e.g., `[0, 0.15, 0]`) relative to the `playerObject`'s center. This is to allow looking over 1-block high obstacles when standing.
* Player collision height should be 1.9 when standing, and 0.9 when crouching (allowing fitting into 1-block gaps).
* Implement standard FPS WASD controls (W/S forward/backward relative to camera, A/D strafe left/right relative to camera).
* Implement jumping (Space).
* Implement crouching (Shift): Reduce height to 0.9 and instantly adjust the `playerObject` Y position down/up by the difference in half-heights (0.5) to keep feet planted.
* Implement sprinting (double-tap W): Increase base speed significantly (e.g., walk 25, sprint 50, crouch 12.5). Sprint should stop on W release, S press, or crouching, but *not* on jump.
* Implement basic water physics: Slow down movement and reduce jump height when the player is in water blocks.

**UI & Menu:**
* Add a simple block selector UI (Grass, Dirt, Stone, Water) at the bottom, selectable with keys 1-4.
* Add a coordinate display (X, Y, Z, 1 decimal place) at the top-left.
* Implement an in-game menu activated by the Escape key:
    * Menu should pause the game (unlock pointer, stop physics updates).
    * Allow setting world width and depth (range 16-128, step 16) and restarting the game with a newly generated world of that size (must clean up old world correctly and return to the "Click to Play" screen).
    * Include a checkbox to toggle the coordinate display.
    * Include a checkbox to toggle fog and a slider to adjust the fog's far distance (e.g., 20-150). Fog should be enabled by default.
    * Include a checkbox to toggle Noclip mode (disables gravity and collisions).
    * Include a checkbox to toggle Fly mode (disables gravity, enables vertical movement with Space/Shift, automatically enables Noclip). Disabling Fly should also disable Noclip.

**Optimizations:**
* Use individual block meshes for the world (allowing full interaction).
* Implement a spatial grid (`cellSize` approx 4) to optimize collision detection by checking only nearby blocks.
