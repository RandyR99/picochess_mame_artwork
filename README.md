# picochess_mame_artwork

Custom artwork for the chess computers that [picochess](https://github.com/JohanSjoblom/picochess) emulates with MAME. It has photos and drawings of the real machines, with clickable buttons, LEDs, displays and pieces. The layouts are for **MAME 0.289**.

This repo holds only the files added on top of MAME's own `artwork` folder. It is not a complete artwork folder by itself.

## Contents

| Path | What it is |
|---|---|
| `<set>/<set>.lay` | The layout for one machine, with its views (see below). `<set>` is the MAME set name, for example `van16` or `sfortea`. |
| `<set>/*.png`, `*.jpg` | The pictures that layout uses. Layouts also use pictures from other folders through `../`. |
| `pieces/` | Piece sets (3D photos and flat 2D pieces). |
| `leds/`, `buttons/`, `misc/` | Shared LEDs, buttons, backgrounds and panels. |
| `chess/` | PNG pieces, added next to the SVG pieces in MAME's own `artwork/chess`. |

Some folders hold only pictures that other layouts use. For example, `feag68k/` serves the Elite Avant Garde layouts.

A clone set without a folder of its own uses its parent's. For example, `tascr30g` shows the `tascr30` views.

## Installing

picochess runs MAME from `/opt/picochess/engines/mame_emulation`, which has `artpath artwork` in its `mame.ini`. Build that `artwork` folder from MAME 0.289's own artwork with this repo on top:

```
cd /opt/picochess/engines/mame_emulation
cp -r <mame-0.289-source>/artwork artwork
rsync -a --exclude .git --exclude .gitignore --exclude README.md <this-repo>/ artwork/
```

You can also unpack a ready-made `artwork.tar.gz`, if one was shared with you, in the same place.

picochess shows the artwork when its artwork display is switched on. It then starts the machine with its `<set>_art` script, which opens a MAME window.

## Views

Most machines have several views, for example a photo with 3D pieces, the same with flat 2D pieces, or a modular board with a different display module. The view names say who made them ("artwork by luis", "2d artwork by volodymyr/luis", ...).

To pick a view, open MAME's menu (Tab) and go to Video Options. MAME remembers the choice per set in `cfg/<set>.cfg`. To try a view directly, use `mess <set> -view "<view name>"`.

## Editing

- **MAME loads only `<set>/<set>.lay`** (or `default.lay`). Any other `.lay` file in the folder is ignored. Put an alternative look in the same file as an extra view.
- **Names must match MAME 0.289.** Outputs (`piece_a1`, `led0`, `digit0`, ...) and input tags (`IN.0`, `RESET`, `board:RANK.1`, ...) are checked against the 0.289 drivers. A button with an unknown tag does nothing.
- **Linux file names are case-sensitive.** MAME has no case-insensitive lookup, so `file="..."` must match the file name exactly. Use `/` in paths.
- **Layouts are UTF-8 with LF line endings.** Names (folders, files, elements, views) are in English.
- Folder names are 0.289 set names. Artwork from pre-0.289 set names was moved to the set's current name.

To check a change, open the view in a window. F12 saves a snapshot to `snap/`.

```
cd /opt/picochess/engines/mame_emulation
./mess <set> -window -view "<view name>"
```

## Credits

The artwork was made by **Luis** and **Volodymyr** for MAMEChess and the Mysticum Project (**Guido Marquardt**), and is compatible with the PicoChess project's MAME implementation. This repo starts from the version which was updated to work with PicoChess v4 (first commit). Later commits adapt it to MAME 0.289 on Linux: file name case, encodings, input tags, renamed sets, missing pictures and layout fixes. The commit history lists each change.

Some layouts carry a CC0 note in their header. The photos and drawings remain the work of their authors.
