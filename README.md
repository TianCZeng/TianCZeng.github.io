# TianCZeng.github.io

Personal academic website for Tianchu Zeng — https://TianCZeng.github.io

A single hand-written `index.html` (HTML + CSS + a small vanilla-JS block). No build
step, no framework, no dependencies. Edit the file, commit, push — GitHub Pages redeploys
in a minute or two.

## Layout

```
index.html                          the whole site
assets/
  images/                           see assets/images/README.md
    portrait.jpg
    work-biophysical-brain-models.png
    work-statistical-validity.png
    work-brain-foundation-models.png
    beyond-research.jpg
  cv/
    TianchuZeng-CV-EN.pdf           linked from the hero and the Contact section
    TianchuZeng-CV-ZH.pdf
docs/                               planning notes + image originals (git-ignored)
```

## Page structure

`Hero → News → About → Selected Work → Publications → Talks → Open Source → Beyond Research → CV & Contact`

The important rule: **each fact lives in exactly one place.**

- **Selected Work** explains *what the problem is and what we did*. Each entry is a small
  figure thumbnail on the left and the text on the right; the thumbnail is a visual label,
  not a display figure, so it has no caption and links to the full-size PNG. The section
  deliberately carries no author lists.
- **Publications** carries the formal citations — authors, venue, year, links — once.
- **News** is the only place that repeats a milestone, and only as a dated one-liner.
- **Open Source** is for released repositories: one `.repo` card each, chips + monospace
  name + two short paragraphs (what it does, then why it is built that way) + the GitHub
  link. Copy the existing card to add one.

When adding a paper, add the citation to **Publications**. Only promote it to **Selected
Work** if you have a figure and something to say about it beyond the citation.

## Editing notes

- **Images** — overwrite the file of the same name in `assets/images/`. Paths are explicit,
  so keep filenames exactly as they are. See `assets/images/README.md`.
- **CV** — overwrite the PDFs in `assets/cv/`. The buttons use `download`, so they save the
  file rather than opening it in a tab.
- **Dark mode** — follows the system setting; the header toggle overrides it and the choice
  is remembered in `localStorage`.
- **Theme colours** — all in the `:root` custom properties at the top of the `<style>` block,
  with a matching dark set. Change them in both places.
- **Adding a nav item** — add the link in `.nav-links` and give the section a matching `id`.
  The scroll-spy picks it up automatically.

## Preview locally

```bash
python3 -m http.server 8000
# then open http://localhost:8000
```

A local server is not strictly required any more, but relative paths behave more like the
deployed site than `file://` does.

## Still to do

- [ ] Add months to the **News** entries where you know them — the date column is already
      sized for `May 2026`-style labels. Only the bioRxiv preprint date is filled in.
- [ ] Confirm the official English wording of the National Level II Athlete designation.
- [ ] Swap the *Nature Methods* link from the bioRxiv preprint to the journal DOI once it
      is issued (two places: Selected Work entry 1, and Publications item 1).
- [ ] Add a link for the brain-foundation-models manuscript when the preprint goes up
      (two places: Selected Work entry 3, and Publications item 7).
- [ ] Check the AI4X 2025 poster title — Google Scholar records it as *"Optimizing
      Biophysically-Plausible Large-Scale Circuit Models With Deep Neural Networks"*,
      which differs from the title currently listed under Talks.
