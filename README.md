# SCDA Updater

Keeps **Splinter Cell: Double Agent — Community Edition** up to date: new maps,
and changes to the game itself.

New maps arrive as their **own entry in the map list**. Nothing the game came
with is replaced: if you get "Blackwing Enhanced", your normal Blackwing is
still there, untouched, and the new one sits next to it.

Game changes — a fix or an improvement to the game itself — do replace a file.
When one does, **your original is kept**, and removing the change puts it back
exactly as it was.

## Right now

The **Main build** is deliberately empty — the base game stays stock. Everything
currently being handed out is on the **Experimental build** tab:

| | |
|---|---|
| **Night Waves** | Dawn Waves at night — an extra vent, dimmed outdoor light and capped fill lights. It is its own map: your stock Dawn Waves stays exactly where it is, and Night Waves is added at the end of the map list. |

So: download the updater, pick **Experimental Build** under VERSION, and press
**PLAY**. It checks for updates, installs what is missing and starts the game.

Choosing **Community Edition** instead gives you the plain community build — the
experimental maps are switched off, not deleted, so you can swap back and forth
whenever you like.

(There is no third option on a normal install. **Developer** only appears on a
machine that has hand-built maps belonging to no download, and all it does is
switch those on — there is nothing in it to receive.)

## Download

**[⬇ ScdaPatcher.exe](https://github.com/REALSYNCADE/SCDA-Updater/releases/latest/download/ScdaPatcher.exe)**
— that link always serves the newest build.

You only download it once. It updates the game, not itself, so keep it anywhere
you like and run it whenever you want to check for new maps.

## Using it

1. Run `ScdaPatcher.exe`. It finds your Community Edition install by itself; if
   it does not, open **Settings** and point it at the folder that contains
   `System\SCDA_Online.exe`.
2. Under **VERSION**, pick **Community Edition** or **Experimental Build**.
3. Press **PLAY**. It updates that version if anything is new — Windows may ask
   for administrator rights, because the game lives under `Program Files` — and
   then starts the game.
4. The new maps are in the map list under their own names.

**Close the game first.** The engine keeps its map files locked while it runs,
and the updater will refuse rather than half-patch a running game.

### The other buttons

| button | what it does |
|---|---|
| **Start the main game** / **Start experimental** | launches SCDA. There is one game, so both start it — the button first tells you what that tab has installed, and warns you if a *game change* from the other tab is active, because those are loaded however you start |
| **Check my game** | verifies your base game against the files Community Edition shipped, and tells you which maps can and cannot be installed, without changing anything |
| **Remove one** | takes one thing back out. An added map is deleted; a game change is undone and your original file is put back |
| **Remove everything from this tab** | undoes everything *that tab* installed, and leaves the other tab alone |
| **Restore stock** | puts back every file the updater has ever changed and removes every map it added, from both tabs. This is the clean uninstall |

## The two tabs

| tab | what is on it |
|---|---|
| **Main build** | the finished maps. This is what you want. |
| **Experimental build** | works in progress — new maps and new ideas being tested, often broken on purpose |

They are separate. Ignoring the second tab costs you nothing, and installing
from it never changes or removes anything the first one gave you.

If you do want to help test:

* Every experimental map is **its own extra entry** in the map list. The
  finished version stays exactly where it was, so you can play both and compare.
* Expect crashes, missing textures and maps that do not load. That is what the
  tab is for.
* **Remove everything from this tab** puts it all back — added maps deleted,
  replaced files restored — and the main build is untouched.
* The updater asks you to confirm once, the first time you install from it.

Play online with people on the main build and you may not be able to join a
match that uses an experimental map — take them out first if in doubt.

### Windows SmartScreen

The program is not code-signed, so the first run shows *"Windows protected your
PC"*. Click **More info → Run anyway**. If you would rather check first, the
SHA-256 of every file is published in `checksums.txt` on each release.

## What it actually does to your game

* **A new map only adds.** Four new files plus one line added to each of two
  config files. No map, package or setting the game shipped with is overwritten.
* **A game change is always reversible.** It does replace a file — that is what
  it is for — but your original is copied aside before anything is written, and
  **Remove one** or **Restore stock** puts it back byte for byte. The updater
  names the file it is about to replace before it does it.
* **Your settings are not touched.** `PlayerProfilePC.ini` and `Default.ini` are
  never part of a release — keybinds, mouse sensitivity, video and gameplay
  options all stay exactly as you have them.
* **If you added your own maps, they survive.** The map list and the map-name
  file are *edited*, not replaced, so anything else in them stays where it is.
* **Your base game is checked first.** If a file a map is built from has been
  modified, that map is held back and named, and the rest still install.
* **Maps are patches, not copies of the game.** An enhanced Blackwing is a 16 KB
  download, because the patch is the difference against a map you already own.
* **Nothing is written until every file has been rebuilt and checked** against
  its published SHA-256. If one file cannot be built, the update stops before
  touching anything — a half-patched game is not a state it can reach.
* **Going back always works.** The first time a file is changed, your original
  is copied to `%LOCALAPPDATA%\SCDA-CE-Patcher\`. That copy is what **Restore
  stock** puts back.

## Command line

`ScdaPatcher-cli.exe` is the same program with a console:

```
ScdaPatcher-cli.exe --cli check
ScdaPatcher-cli.exe --cli update
ScdaPatcher-cli.exe --cli verify
ScdaPatcher-cli.exe --cli remove --addon BLKGE
ScdaPatcher-cli.exe --cli restore
ScdaPatcher-cli.exe --cli update --install "D:\Games\SCDA Community Edition"

ScdaPatcher-cli.exe --cli check  --track experimental
ScdaPatcher-cli.exe --cli update --track experimental
ScdaPatcher-cli.exe --cli remove-track --track experimental
```

Without `--track` everything is the main build.

## Trouble

| what you see | what it means |
|---|---|
| *"needs your original `<file>`, which is missing or already modified"* | a file that map is built from has been changed by something else. **Restore stock**, or reinstall Community Edition, then update again |
| *"map ID N is already used by `<CODE>`"* | another custom map on your install claims the same slot ID. Remove that one first, or ask for a rebuild on a free ID |
| *"no write access"* | run it as administrator (right-click → Run as administrator) |
| *"SCDA is running"* | close the game |
| *"could not reach the update channel"* | no internet, or GitHub is unreachable. On the Experimental tab it can also mean there is no experimental build published right now |
| *"menu name slot NN already belongs to …"* | two maps want the same name slot. Remove the one it names, or ask for a rebuild |

## Requirements

An existing SCDA Community Edition install. This adds maps to CE — it is not an
installer for the game itself and it does not distribute the base game.
