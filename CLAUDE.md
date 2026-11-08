# CLAUDE.md — picochess_mame_artwork

Guidance for Claude Code (and other AI coding tools) working in this repo. README.md covers installing, views and editing for users.

## What this is

A complete MAME `artwork` folder (current as of MAME 0.289) for the chess computers that [picochess](https://github.com/JohanSjoblom/picochess) emulates. It holds the custom layouts and photos, merged with MAME's own artwork files (`bgfx/`, the top-level effect PNGs, `chess/`, `LICENSE.mame`). picochess's `engines/mame_emulation/artwork` can be a symlink to a clone of this repo, so a `git pull` deploys.

- `<set>/<set>.lay` — MAME loads only this file (or `default.lay`) in each folder. An alternative look goes in the same file as an extra view.
- `pieces/`, `leds/`, `buttons/`, `misc/` — shared images, referenced through `../`.
- A clone set without a folder of its own uses its parent's.

Related repos:
- [chessengine](https://github.com/RandyR99/chessengine) — the MAME plugin.
- [mame_for_picochess](https://github.com/RandyR99/mame_for_picochess) — the launch scripts. The `<set>_art` scripts open the artwork window.
- [MAME](https://github.com/mamedev/mame) (use the tag of the targeted release, e.g. `mame0289`) — drivers in `src/mame/<maker>/` and stock layouts in `src/mame/layout/`.

## Rules

- Commit and push only after the maintainer's OK, with one commit per kind of fix.
- **Never delete artwork folders.** An old folder name usually means a renamed set: move or map it to the current MAME set name instead.
- Use English names for folders, files, elements and views.
- Layouts are UTF-8 with LF line endings and use `/` in paths. File names are case-sensitive, because MAME on Linux has no case-insensitive lookup.
- Input tags and masks, and output names (`piece_a1`, `led0`, `digit0`, ...), must match the MAME driver. A button with an unknown tag does nothing.
- A button must send the key printed on it. Swapping two valid tags still loads without errors, so check each button's label against the driver's `PORT_NAME` for its tag and mask.
- MAME finds a layout's images only in the artpath folder the layout came from.
- When moving to a newer MAME, update MAME's own artwork files by hand.

## Checking a change

```sh
mame <set> -window -view "<view name>"     # F12 saves a snapshot to snap/
```

For batch checks, run headless with `SDL_VIDEODRIVER=dummy` and take snapshots. Look at every view of a changed layout, not only the default one.
