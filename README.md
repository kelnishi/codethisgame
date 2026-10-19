# codethisgame

This repo holds the example code and game assets for
[*Code This Game!*](https://us.macmillan.com/books/9781250794796/codethisgame/) by
Meg Ray. Over the course of the book, readers build **Attack of the Vampire Pizzas!**,
a tower-defense game in Python and pygame. Each file here is the game as it stands at
the end of a chapter, hack, or mod, so a reader can check their own code against it.

It is a fork of [meg-ray/codethisgame](https://github.com/meg-ray/codethisgame). The
original code had bugs that stopped some lessons from working, and two files it loads
were missing. This fork fixes both and runs on **Python 3.14**. The fixes keep the
book's names, comments, and `from pygame import *` style, so the code still lines up
with the printed pages.

## Setup

The game needs **pygame-ce**, not `pygame`. Upstream pygame (2.6.1) has no Python 3.14
wheel, so `pip install pygame` tries to compile it locally. That build either fails or
comes out unable to load the game's `.png` and `.jpg` images. pygame-ce is the
community-maintained fork and ships ready-made 3.14 builds for Windows, macOS, and Linux.
Its import name is still `pygame`, so the book's code needs no changes.

```sh
python3.14 -m venv .venv
source .venv/bin/activate          # Windows: .venv\Scripts\activate
pip install -r requirements.txt
```

If you already installed `pygame`, run `pip uninstall pygame` first. The two packages
both install a module named `pygame` and conflict.

## Running

Every script loads its images, sounds, and font by bare filename, so run it from the
repo folder:

```sh
cd codethisgame
python vampirepizza_chapter9.py
```

| Files | What they are |
|---|---|
| `vampirepizza_chapter1.py` – `chapter12.py` | The game at the end of each chapter. Chapter 5 has no file. |
| `prepare_pizza.py` | Chapter 2's drawing practice: the pizza, a pepperoni, and a box. |
| `monster_foods.py` | A text-only classes exercise that runs in the terminal. |
| `VampirePizzaAttack.py` | The finished game. |
| `vampirepizza_hack1.py` – `hack5.py` | The hacks, which extend the finished game. |
| `vampirepizza_mod1.py` – `mod3.py` | The mods, which extend the finished game. |

## Corrections

These are the changes from the original repo. A reader whose own code shows one of
these symptoms has probably copied the original faithfully, so the fix applies to
their code too.

| File | Symptom | Fix |
|---|---|---|
| `chapter9`–`chapter12`, `VampirePizzaAttack`, `hack1`–`hack3`, `mod1`–`mod3` | A trap only worked on a vampire's left edge, and a trap in the rightmost column did nothing. | `right_tile_wall` → `right_tile`; `right_tile.x` → `right_tile.rect.x` (and the same for `left_tile`); both `< 10` bounds → `< 11`. |
| `hack4`, `hack5` | A trap in the rightmost column did nothing. | Both `< 10` bounds → `< 11`. |
| `chapter11` | Crashed at startup, and on any click once that was fixed. | Three lines that need chapter 12's tile classes go back to chapter 10's form: `BackgroundTile()`, `.effect = True` on click, and an unconditional tile redraw. |
| `hack1` | Crashed at startup. | Added the missing `explosion.png`. |
| `hack4`, `hack5` | Both levels ended in "Game Over" on their first frame. | `MAX_BAD_REVIEWS = 0` → `3`. |
| `hack4`, `hack5` | Losing level 1 flashed "Game Over", then started level 2 anyway. | `break` after the Game Over screen. |
| `hack4`, `hack5` | Finishing the last level offered another level instead of a win; after level 1 the prompt said "Level 1". | `level_cursor < len(level_config) - 1`, and `str(level_cursor + 2)`. |
| `hack4`, `hack5` | Crashed on reaching the win screen. | `end_font.render('You Won!!!', True, WHITE)`, which supplies the missing antialias and color arguments. |
| `mod2` | Crashed on Linux at startup. | `'WERE_PIZZA.png'` → `'were_pizza.png'`, the file's real name. |
| `hack4`, `hack5`, `mod2` | The were-pizza always looked like a vampire pizza. | `WerePizza` gets its own `update`, so it keeps the `WERE_PIZZA` image. |
| `hack4`, `hack5`, `mod2` | The zombie only showed its damage pictures near death. | `/ STARTING_HEALTH * 2` → `/ (STARTING_HEALTH * 2)`. |

### Added assets

| File | Used by | Made from |
|---|---|---|
| `explosion.png` | `hack1` | A new 100×100 cartoon starburst drawn as SVG, in the style of the book's art. |
| `pizza-music.ogg` | `mod3` | `pizza-music.wav`, encoded as Ogg Vorbis. |
