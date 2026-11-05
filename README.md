# picochess_mame_artwork

Custom artwork for the chess computers that [picochess](https://github.com/JohanSjoblom/picochess) emulates with MAME. It has photos and drawings of the real machines, with clickable buttons, LEDs, displays and pieces. The layouts are for **MAME 0.289**.

This repo is a complete `artwork` folder: the custom artwork plus the files of MAME 0.289's own `artwork` folder.

## Contents

| Path | What it is |
|---|---|
| `<set>/<set>.lay` | The layout for one machine, with its views (see below). `<set>` is the MAME set name, for example `van16` or `sfortea`. |
| `<set>/*.png`, `*.jpg` | The pictures that layout uses. Layouts also use pictures from other folders through `../`. |
| `pieces/` | Piece sets (3D photos and flat 2D pieces). |
| `leds/`, `buttons/`, `misc/` | Shared LEDs, buttons, backgrounds and panels. |
| `chess/` | MAME's SVG pieces, and PNG pieces that were added next to them. |
| `bgfx/`, the `.png` files in the top folder | MAME's own shaders and screen effects, unchanged. |

Some folders hold only pictures that other layouts use. For example, `feag68k/` serves the Elite Avant Garde layouts.

A clone set without a folder of its own uses its parent's. For example, `tascr30g` shows the `tascr30` views.

## Installing

picochess runs MAME from `/opt/picochess/engines/mame_emulation`, which has `artpath artwork` in its `mame.ini`. Clone this repo and make that `artwork` folder a link to the clone:

```
git clone https://github.com/RandyR99/picochess_mame_artwork.git ~/github/picochess_mame_artwork
cd /opt/picochess/engines/mame_emulation
rm -rf artwork
ln -s ~/github/picochess_mame_artwork artwork
```

A `git pull` in the clone then updates the artwork.

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

## Licensing

There is no single license for this repo:

- **MAME's own files (`bgfx/`, the top-level effect `.png` files):** CC0, see `LICENSE.mame`. The SVG pieces in `chess/` are BSD-3-Clause, see `chess/README.md`.
- **Layout files (`.lay`):** some carry a CC0 note in their header. The changes made in this repo are released under CC0 as well.
- **Photos and drawings:** they remain the work of their authors (the artists named above and the photographers of the original machines). They are shared here the same way they were shared with MAMEChess and PicoChess, free of charge, for use with these emulated chess computers.

If you hold the rights to any of this artwork and want it credited differently or removed, please open an issue.
