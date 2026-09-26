# Asterix XXL Advance Studio

Modding tool for **Asterix & Obelix XXL** (Game Boy Advance, European version, code BLXP, 8 MB).
Same layout and style as Driv3r Advance Studio – the game uses the same VD-dev engine.
Runs in the browser without installation: **double-click `index.html`** (or `Asterix XXL Advance Studio starten.bat`).
Tested with Chrome/Edge. Expected ROM: SHA-1 `7145d02143c1a81f6ea72063ac798642b2aaec3c`.

## Getting started

1. Open `index.html`, **Load ROM** (or drop the .gba onto the window). UI language: top right.
2. Pick an area on the left, export, edit, import.
3. Save the project regularly under **ROM & project** (`.axstudio` – contains only your changes).
4. **Save ROM** writes the finished `.gba` (header checksum fixed). Always test in mGBA. Or create an **IPS patch**.

The original file is never modified. When space runs out, data is relocated to the end of the ROM, pointers are
updated and the ROM is expanded to 16 MB if needed (the EEPROM save does not allow more).

## Areas

| Area | Content |
|---|---|
| Level editor | all 43 levels (31 adventure stages in 6 worlds + 12 Obelix sleigh tracks), textured top view and optional **3D view** (also side by side): paint ground textures and flags, shape terrain, move ground points, edit the walking corridor, split/append/remove sections, draw completely new tracks, set the start point, move/copy/delete all objects (also groups), collision walls, texture frames, ground palette, raw .bin export/import |
| Images & textures | 58 full-screen images (menus, title, cutscenes) and 6 world texture atlases 256×656 |
| Sprites | 102 named animation sets, 3660 frames (Asterix, Obelix, enemies, villagers) in their real game colours incl. colour variants, single frames or sheets |
| HUD & sky | HUD, shop/control labels, 6 sky panoramas |
| Palettes | 73 palette files + 35 character palettes |
| Texts | menus, cutscene subtitles, dialogues, shop, credits in 6 languages (FR EN DE ES IT NL), CSV |
| Sound & music | 11 songs (GBAMOD30), 100 instruments, 42 effects – WAV, MIDI |
| Full package | everything as ZIP and back (unchanged package keeps the ROM byte-identical) |

Level editor changes are kept in a working copy with undo; **Write to ROM** packs and stores the level.

* Cell flags (verified in the emulator): bit 1 = solid ground (without it Asterix falls through), bit 2 = water, bit 5 = dangerous (costs lives),
  bit 3 = special surface (relocates the character), bit 0 = alternative drawing routine for flat floor, bit 6 = draw later (overhang).
* Walking corridor (yellow/orange lines): the game keeps Asterix between these lines. Drag the corner points to change the walkable area.
* Sections: split, remove, append at start/end, place invisible collision walls. **New track**: click a course and the whole level is rebuilt
  along it from a template section, with end walls at both ends.
* Objects: all types can be moved/copied/deleted; Shift/Ctrl+click or Shift+drag selects groups (e.g. tree = crown + trunk + collision body).
  The coordinate fields of every record type are learned statistically from all 43 levels.
* Sprites are drawn by software into the 8-bit bitmap with 15-colour character palettes (0x480614 hero, 0x48079C enemies/villagers);
  the studio shows each set with the palette the game uses. After deleting or copying collectibles, adjust the **target value for 100 %**.

## 3D editor (optional)

Choose **View: 2D / 3D / 2D + 3D** at the top of the level editor – the choice is remembered, the 2D top view stays the default.
The 3D view shows the level the way the engine builds it: textured ground with heights, 3D objects (walls, houses, bridges),
billboards (trees, bushes), characters/items as coloured diamonds, walking corridor, start flag and the world's sky panorama.
All tools work here too and act on the same working copy (undo, Write to ROM); in "2D + 3D" every change shows in both views at once.

| Action | Control |
|---|---|
| Rotate | left mouse button in the "View" tool, otherwise Alt + left button |
| Pan | right or middle mouse button |
| Zoom | mouse wheel (zooms towards the cursor) |
| Fly | click the 3D view, then W A S D, Q/E = down/up (AZERTY: Z Q S D, A/E) |
| Center | double-click the ground; F shows the current selection |
| Cameras | "Game camera" = view like in the game behind the start point, "From above", "Fit" = whole level |
| Paint ground / start / sections | click the ground (dragging keeps painting) |
| Terrain | click/drag raises, right-click or Shift lowers (brush circle shown) |
| Points | drag a point up/down = height, Shift + drag = move along the ground |
| Walking corridor | drag the corner points along the ground |
| Objects | drag = along the ground, Alt + drag = height, Shift/Ctrl + click or Shift + rectangle = multi-select, Del = delete |
| New track | click course points on the ground |

Display options: collision bodies (type 0, otherwise invisible) and invisible ground faces as glass, fog on/off.
Needs WebGL (any current Chrome/Edge/Firefox); without WebGL the 2D view remains fully usable.

The technical notes are in [LIESMICH.md](LIESMICH.md) (German).
