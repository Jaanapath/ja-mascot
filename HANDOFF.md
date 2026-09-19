# Handoff: Ja Mascot Page

## What this is
GitHub Pages site: a looping mascot ("Ja", a pregnant anime character) with a
talking speech bubble, on a pastel pink background.

- **Live**: https://jaanapath.github.io/ja-mascot/
- **Repo**: https://github.com/Jaanapath/ja-mascot (owner: Jaanapath)
- **Local path**: `/Users/nlp/Desktop/VS code/ja-mascot`

## Stack
Plain HTML/CSS/JS, single file (`index.html`), no build step, no dependencies.
Deploys via GitHub Pages serving from `main` branch root.

## Files
- `index.html` — everything: markup, inline `<style>`, inline `<script>`.
- `mascot.png` — the character image (AI-generated, background made transparent, see below).
- `README.md` — user-facing instructions (swap image, add bubble lines, push commands).

## Key implementation details
- **Mascot image swap**: `<img id="mascot" src="mascot.png">` has an `onerror`
  handler that falls back to a CSS-drawn placeholder blob (`#placeholder`) if
  `mascot.png` is missing. If you replace the image, no code changes needed.
- **Gotcha already hit and fixed**: `#mascot` must have `display: block` by
  default (not `display: none`), because `onerror` only fires on *failure* —
  if it defaults to `none`, a successfully-loaded image never gets shown.
- **Transparency gotcha**: the original AI-generated PNG had a baked-in
  checkerboard pattern as actual opaque pixels (alpha=255 everywhere), not
  real transparency, despite claiming to have an alpha channel. Fixed with a
  Python flood-fill (numpy + scipy `label`) starting from the image border,
  removing near-white/light-gray connected regions and setting their alpha to
  0. If a new mascot image is swapped in and shows a checkerboard box, it
  likely has the same issue — same fix applies.
- **Animation**: the `.scene` div (wraps both `.bubble` and `.mascot-wrap`)
  has the `bob` keyframe animation, so the speech bubble and mascot move
  together as one unit — not the mascot alone. Keyframes do a bigger
  side-to-side sway (±50px) plus vertical bob (-34px) plus slight rotate tilt,
  4s loop, ease-in-out.
- **Bubble text cycling**: plain JS array `lines` near the bottom of
  `index.html`, cycles every 5s via `setInterval`. Currently only one line:
  `"Baby in process!"`. Add more strings to the array to cycle through them.

## Environment note (may not apply to you)
The assistant's Bash tool ran in a sandbox that shared the filesystem
(could read/write files, git commit locally) but could NOT see installed
CLI tools like `brew`/`gh`, and couldn't push to GitHub (no credentials).
All `git push` calls had to be run manually by the user in their own
Terminal. If you have full shell access, ignore this section.

## Open / not done
- Only one speech bubble line exists; more were planned "to be designed
  later" but never specified.
- Repo name is `ja-mascot` (not the mascot's name choice reasoning — just
  picked to match); mascot character itself is named "Ja".
- No favicon, no mobile-specific layout testing done beyond default responsive flex centering.
