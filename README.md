King Oddball Access Mod 0.17.5
==============================

A screen reader accessibility mod for the Steam PC version of King Oddball.
It speaks menus and on-screen text, announces the world map, lists enemies,
and adds a line-up tone so you can hear when the swinging rock is aimed at a
target. It changes no game files on disk: it is a winmm.dll (plus NVDA's
controller client DLL) placed next to the game.

Requirements
- King Oddball, Steam version (Windows, app 525450). Other versions are not
  supported (see Troubleshooting).
- Speech: JAWS and NVDA are both supported natively. If JAWS is running, the
  mod speaks through JAWS (its COM interface). Otherwise, if NVDA is running,
  it speaks through NVDA (nvdaControllerClient.dll, included). Otherwise it
  uses the Windows SAPI voice. If nvdaControllerClient.dll is missing, the
  mod still works and uses JAWS or the Windows voice. To force one, set
  speech_backend in KO_config.ini to jaws, nvda or sapi.
- Keyboard works. An Xbox-style controller is supported for the mod shortcuts
  listed below.

Install
- Easy way: run install.bat. It looks for the game in the usual Steam folders,
  then in every Steam library listed in Steam's libraryfolders.vdf. If it still
  cannot find the game, it asks you to type or paste the game folder (the
  folder that has KingOddball.exe in it). Quotes around the path are fine. If
  the folder is wrong it tells you and asks again; press Enter on an empty
  line, or type Q, to cancel. You can also drag the game folder onto
  install.bat, or run:
    install.bat "C:\path\to\King Oddball"
  Any existing winmm.dll that is not this mod is backed up as winmm.dll.bak.
  An older copy of this mod is replaced. Your existing KO_config.ini is kept
  (backed up once as KO_config.ini.bak if the installer is about to leave it
  alone; a missing ini is copied from the package).
- install.bat also copies the JAWS keymap (KingOddball.jkm / .jss / .jsb) into
  every %APPDATA%\Freedom Scientific\JAWS\*\Settings\<lang> folder it finds.
  Restart JAWS (or Alt+Tab out of the game and back) so the keymap loads.
- Manual way: copy winmm.dll, nvdaControllerClient.dll and KO_config.ini into
  the folder that has KingOddball.exe. For JAWS, also copy the three files
  from the jaws folder into your JAWS user Settings\<lang> folder (see JAWS
  keymap below).

Uninstall
- Run uninstall.bat (same folder search and prompt as install). It removes
  winmm.dll and nvdaControllerClient.dll, restores winmm.dll.bak if there was
  one, and removes the KingOddball JAWS keymap files it installed. Your
  KO_config.ini is left in place so your toggles are kept if you reinstall.
- Or delete winmm.dll and nvdaControllerClient.dll from the game folder, and
  delete KingOddball.jkm / .jss / .jsb from your JAWS Settings folder.

Line-up tone (default ON)
-------------------------
While the rock is swinging, the mod plays a soft continuous hum.

- Pitch: the tone rises as the rock's current travel direction points closer
  to a remaining enemy, and falls again as the swing moves past. With several
  enemies left, you hear a peak for each one and a dip between them. The tone
  does not predict where the rock will land; it only reflects the aim right
  now.
- Pan: the tone eases toward the left or right to match the target it is
  tracking, so the image drifts gently instead of jumping.
- Latency correction: by default the mod leads the aim by about 80 ms
  (lineup_lead_ms in KO_config.ini). That only cancels this mod's own audio
  delay (mixer buffers and the pan/pitch glide). It is not extra aim assist.
- Tips: listen for the peak, then release with Space, Enter, or controller A.
  If nothing releases, the mod says "No rocks left" or "Not ready". F7 toggles
  the tone. Legacy swing tick clicks can be turned on with swing_ticks=1 in
  the ini (off by default).

World map: review cursor and jump
---------------------------------
- Arrow keys (and the controller stick / D-pad) move the real map marker. Moving
  onto an unfinished playable level starts it (game behaviour).
- Page Down / Page Up (or right / left trigger) walk a review cursor across
  every cell without moving the marker. Locked cells say "Locked" first, then
  the rest of the info. Home (or left stick click) puts the review cursor back
  on the marker.
- Enter, or controller A while the review cursor is away from the marker, plays
  the reviewed cell the same way a mouse click would (including "Locked" or
  "Not available" when the game refuses it). Otherwise A is left to the game.
- F9, or right stick click, jumps the real marker to the next unfinished
  playable level (playable and not yet conquered — the same cells a sighted
  player can open). Order is nearest to the marker first, then onward, wrapping
  around. Any pending review is cleared. Off the map it says "Not on the world
  map". If none are left it says "No unfinished levels available".
- Moving the marker onto a cell does not start the level by itself; press Enter
  (or controller A while reviewing away from the marker) to play. That matches
  clicking the cell you are already on.
- If an arrow key or D-pad direction does not move the marker, the mod says
  "Can't move there". The game refused that step (map edge, or a cell that is
  not reachable yet — the same limit a sighted player sees).

Keyboard (F-keys ignored while Alt / Ctrl / Shift / Win held;
Shift+F8 is the one exception — it toggles enemy-list speech)
-------------------------------------------------------------
F1   Help (lists keys and on/off state)
F2   Toggle speech
F3   Re-speak neighbour / unexplored directions from your map marker
     (if F3 is silent on your keyboard, use Control Shift U)
F4   Toggle region names on the world map
F5   Toggle map cell announcements
F6   Toggle combo announcements
F7   Toggle line-up tone
F8   List enemies left to right; each name starts with a panned click from that spot (destroyed marks from destroy events)
Shift+F8   Toggle enemy-list speech only (pings keep playing). Says "Enemy speech off" or "on"; saved as enemy_speech
F9   Jump to next unfinished playable level (world map)
Control Shift R   Read all text on the screen
Control Shift T   Speech test
Control Shift U   Same as F3
Control Shift [   Music volume down 5% (saved like Options Ok)
Control Shift ]   Music volume up 5% (saved like Options Ok)
Space / Enter     Release rock (in a level); Enter also plays a reviewed cell
Page Down / Up    Review map cells
Home              Return review cursor to marker

Xbox controller (XInput; edge-triggered; only free buttons)
-----------------------------------------------------------
Game already uses: A (release / confirm), B (cancel / back), D-pad and sticks
(move), Start (pause). Y is also the Mustache easter-egg hotkey on some menus.

Y                 List enemies (same as F8; in a level or on Level completed)
X                 Neighbour hints (same as F3); on the map during review,
                  re-speak the current review cell
LB / RB           Music volume down / up 5% (saved)
Back + Y          Toggle line-up tone (F7)
Back + X          Toggle combo announcements (F6)
Back + RB         Toggle speech (F2)
Back + LB         Speak this controller layout
Back + RT         Toggle enemy-list speech (same as Shift+F8)
World map only:
  LT / RT         Review previous / next cell
  Left stick click    Return review to marker
  Right stick click   Jump to next unfinished level (same as F9)
  A (while reviewing away from the marker)   Play the reviewed cell

JAWS keymap
-----------
JAWS binds many keys (arrows, F3, Enter, Space and others) for its own
commands. While KingOddball.exe is focused, those bindings would stop the
game and this mod from seeing the real key. The included KingOddball.jkm
unassigns those keys for this game only (including F3, Shift+F8, Extended
arrow keys, Enter and SpaceBar), so they pass through. JAWS stays awake and still speaks.
Insert / Caps Lock JAWS commands keep working. install.bat places
KingOddball.jkm, KingOddball.jss and the precompiled KingOddball.jsb into
each JAWS user Settings language folder it finds. After installing, restart
JAWS or Alt+Tab away from the game and back. Insert+Shift+B (or JAWSKey+
Shift+B) says "King Oddball keymap active" when the file is loaded. To remove
the keymap, run uninstall.bat or delete those three files.

Speech
------
Prefers JAWS COM, then NVDA (nvdaControllerClient.dll in the game folder),
then SAPI. Force one with speech_backend=jaws|nvda|sapi in KO_config.ini.

Config (KO_config.ini)
----------------------
[features]
lineup_tone=1
swing_ticks=0
enemy_speech=1

[settings]
pan_speed=28
lineup_window_deg=80
lineup_lead_ms=80
force_music_volume=0     ; keep game Options music (default)
; music_volume=50        ; only when force_music_volume=1
logging=0                ; KO_log.txt off by default
research_log=0
speech_backend=auto      ; auto | jaws | nvda | sapi

Fairness
--------
The mod only announces or acts on information a sighted player can already
see or click: on-screen text, map cell state the game exposes, enemies drawn
on the level, and the same cell-click path the mouse uses. The line-up tone
tracks current aim direction only; it does not predict landings. Jump and
review play only unfinished cells the game itself marks playable.

Troubleshooting
---------------
- Nothing speaks: press F2. Check speech_backend. Confirm JAWS or NVDA is
  running, or allow SAPI. Make sure winmm.dll and (for NVDA) 
  nvdaControllerClient.dll are next to KingOddball.exe.
- F3, arrows, Enter or Space do nothing with JAWS: install the JAWS keymap
  (install.bat) and restart JAWS. Without it, JAWS may swallow those keys.
- F3 still silent on some keyboards: use Control Shift U.
- Wrong game / no install found: run install.bat with the King Oddball folder
  as an argument, or drag the folder onto install.bat. The folder must contain
  KingOddball.exe.
- Music hotkeys do nothing until Options music is ready: open Options once, or
  wait until the title has finished loading.
- Logging: leave logging=0 unless you are sending a bug report. research_log
  stays off unless you are helping develop the mod.

Uninstall notes
---------------
uninstall.bat restores a pre-mod winmm.dll.bak when present. KO_config.ini and
any KO_log.txt / KO_research.txt are left in the game folder.

Credits
-------
King Oddball Access Mod contributors. King Oddball is a trademark of its
respective owners; this mod is not affiliated with them and ships no game
files.
