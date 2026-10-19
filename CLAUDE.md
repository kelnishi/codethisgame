# CLAUDE.md

This repo is Kelvin's fork of meg-ray/codethisgame, the companion code for the book
*Code This Game!*, updated to run on Python 3.14 with pygame-ce. Nothing goes back
upstream.

- **Pushing:** granted. Commit straight to `master` and run `git push origin master`.
  Don't open PRs. `gh` defaults a fork's PRs to the parent repo, which here belongs to
  someone else.
- **Fidelity:** readers compare these files against the printed book. Fix only what is
  broken, and keep the book's names, comments, and `from pygame import *` style.
- **Corrections log:** `README.md` lists every change from the original. Add a row to
  its Corrections table with each fix.

```sh
python3.14 -m venv .venv && .venv/bin/pip install -r requirements.txt
.venv/bin/python -W error vampirepizza_chapter9.py   # run from the repo root; assets load by bare filename
```
