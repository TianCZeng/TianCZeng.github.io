# Images

Every image on the site is referenced by an **exact path** in `index.html`. To replace one,
overwrite the file with the same name — no HTML editing needed. To add a new one, add both
the file and an `<img>` tag.

> Earlier versions of this site auto-probed for file extensions and silently removed blocks
> when an image was missing. That machinery is gone: paths are now explicit, so a missing
> file shows as a broken image. Keep the filenames below exactly as they are.

| File                                  | Where it appears                   | Shape        | Size in repo   |
| ------------------------------------- | ---------------------------------- | ------------ | -------------- |
| `portrait.jpg`                        | Hero, top right                    | 4:5 portrait | 800 × 1000     |
| `work-biophysical-brain-models.png`   | Selected Work → entry 1 thumbnail  | Wide         | 1600 × 835     |
| `work-statistical-validity.png`       | Selected Work → entry 2 thumbnail  | Wide         | 1600 × 818      |
| `work-brain-foundation-models.png`    | Selected Work → entry 3 thumbnail  | Wide         | 1600 × 941     |
| `beyond-research.jpg`                 | Beyond Research, right column      | 4:5 portrait | 900 × 1125     |
| `whackamon-logo.webp`                 | Beyond Research → Whackamon card   | Wide, alpha  | 1200 × 726     |

Keep every file **under ~500 KB**. The whole `assets/` folder is currently ~1.9 MB.

The untouched originals are kept in `docs/originals/` — that folder is git-ignored, so it
stays on your machine and is never published. Re-crop from there rather than from the
downsized copies in this folder.

---

## Portrait (`portrait.jpg`)

- **800 × 1000 px** (4:5). It renders at ~232 px wide, so 800 px gives a crisp retina image.
- Crop head-and-shoulders, eyes roughly on the upper third, a little space above the head.
- Plain or softly blurred background; even, front-facing light. Avoid heavy filters.
- The site crops to 4:5 (`object-fit: cover`), so don't put anything important at the edges.
- **Eyes should be visible** — a portrait where people can see your eyes reads much better
  on an academic page than one behind sunglasses.

## Selected-work figures (`work-*.png`)

These render at **~336 px in the left column** of each Selected Work entry (~192 px on
mid-size screens). They carry **no caption**; the thumbnail links to the full-size PNG,
which is what anyone who wants detail will open.

**Prefer wide figures — roughly 2:1.** The text beside a figure is short by design, so a
wide figure lands at about the same height as the text and the two columns finish level.
A square or portrait figure forces its column tall and leaves a well of white beside it.

- **1600 px wide** (height whatever the figure needs). The thumbnail only needs ~700 px,
  but the click-through opens this file at full size, so keep it large. Crop at the source
  resolution rather than upscaling to hit 1600.
- **PNG**, not JPG — JPG puts grey mush around thin strokes and axis labels.
- **White or transparent background.** The site places figures on a white card in both
  light and dark mode, so white/transparent always looks right.
- **Crop tightly.** Trim the whitespace your plotting tool adds. One panel or a small
  multi-panel schematic reads far better on a website than a full journal figure.
- **The shape matters more than the detail.** At 336 px nobody reads the labels — what
  registers is the silhouette, so pick the panel with the most recognisable structure.
  Detail is for the click-through.
- Exporting from matplotlib:

  ```python
  fig.savefig("work-biophysical-brain-models.png", dpi=200,
              bbox_inches="tight", pad_inches=0.05, facecolor="white")
  ```

- If a figure comes out over ~500 KB, quantise it rather than switching to JPG:

  ```python
  from PIL import Image
  im = Image.open("fig.png").convert("RGB")
  im.quantize(colors=256).save("fig.png", optimize=True)
  ```

- **Permission check:** only publish figures from papers that are accepted, preprinted,
  or where all co-authors are comfortable with the panel being public.

If a figure has a *dark* background and the white card looks wrong, change that thumbnail's
tag in `index.html` from `class="work-thumb"` to `class="work-thumb thumb-plain"`.

## Beyond-research photo (`beyond-research.jpg`)

- **900 × 1125 px** (4:5 portrait). It renders at ~232 px — the same footprint as the hero
  portrait — so crop it to read at that size.
- Something real and candid rather than posed.
- Update the caption in `index.html` (search for `Away from the desk.`) to match the photo.

## Whackamon logo (`whackamon-logo.webp`)

The only **WebP** on the site, and the only file with transparency. Both are deliberate:
it is a photorealistic RGBA illustration, so palette-quantising it to fit a PNG under
500 KB produces visible banding, while WebP at `-q 82` holds the gradients at ~220 KB.

Regenerate from the original in `docs/originals/whackamon-logo.png` (1536 × 1024, 2.6 MB,
about 73 % empty transparent margin). The crop below is the measured opaque bounding box
plus ~14 px of breathing room:

```bash
ffmpeg -y -i docs/originals/whackamon-logo.png \
  -vf "crop=1314:795:41:79,scale=1200:-2:flags=lanczos" -pix_fmt rgba /tmp/wm.png
cwebp -q 82 -alpha_q 90 -m 6 /tmp/wm.png -o assets/images/whackamon-logo.webp
```

**Do not put this logo straight on the page background.** Measured on the actual pixels,
the gold lettering (`#dcad3d`) is only 2.1:1 against white, and the crow (`#17141d`) is
1.04:1 against the dark-theme background — one half or the other disappears in every
theme. The `.game-art` rule in section 13 of the stylesheet therefore gives it a fixed
slate → near-black gradient, light behind the bird and dark behind the lettering. If you
swap the art, re-check both halves before touching that gradient.

## Alt text

Every image has alt text written in `index.html`. If you swap a figure for a different one,
update its `alt="…"` — that is what screen readers and search engines read.

## The CV lives elsewhere

The CV is **not** in this folder. It is in [`assets/cv/`](../cv/) as
`TianchuZeng_Academic_CV.pdf`.
