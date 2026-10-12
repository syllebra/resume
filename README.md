# CV / Résumé — Dr Cédric SYLLEBRANQUE

Single-file, self-contained HTML résumé (French + English), served locally and
published on GitHub Pages. No build step, no framework: one `index.html` (Tailwind
via CDN, Font Awesome, Google Font Inter) plus a `media/` folder of images and
videos.

- Live page: https://syllebra.github.io/resume/
- Repository: https://github.com/syllebra/resume

## Layout

```
index.html          the whole résumé: markup + CSS + JS in one file (~2 100 lines)
LICENSE
media/              every asset the page references (no image lives outside it)
├── csy.png                             profile photo
├── dartnet/        render_0.web.jpg, generator_banner.web.jpg
├── diota/          vision/capture_demo.png · Hololens/CapturedImage146.4394_n.jpg
│   └── PCL/        poc-point-cloud.jpg + poc-point-cloud.web-720p.mp4
├── lectra/         modaris-3d-dress-fabric.jpg · -patterns.jpg · v7r2-coat-patterns.jpg
├── didhaptic/      virteasy1.jpg
└── publications/   isbms_didhaptic.pdf · 50376-2010-Syllebranque.pdf (thesis, 39 Mo)
```

`media/` is organised by **project/experience**, one sub-folder each, so a folder
can be added or removed without touching the others. Only the `.web.jpg` variants
are on the page; the 1920 px masters (DartNet `render_0.jpg`, `generator_banner.png`)
are deliberately **not tracked** — they are regenerable and heavy, see `.gitignore`.

## What the page does

| Feature | Where |
| --- | --- |
| FR / EN bilingual | every text node carries `data-fr` + `data-en`, toggled by the 🌐 buttons (`#lang-toggle`) |
| Skill filter | chips in "Compétences"; clicking one (`filterSkill(name)`) adds `active-filter` to matching chips and `highlight-card` to matching cards → **the blue left bar on an experience card only appears when a filter is active**, cards are neutral slate by default |
| Media galleries | 5 galleries: exp 4 (5 media), exp 5 (3 photos), exp 6 (3 media), DartNet (2 photos), Unit3D Pinball (6 media). Each card has a corner badge (`exp-gallery-badge`) with a chevron that folds/unfolds; hovering a card with a gallery lifts it |
| Lightbox | clicking a thumbnail opens a full-screen viewer; exit stops media and returns the click cursor |
| Local video | `data-local-video="…mp4"` plays the file instead of the YouTube iframe (Diota PCL point cloud) |
| YouTube | `data-video="<id>"` thumbs resolve to `i.ytimg.com` at request time, no remote asset stored |
| Print / PDF | `no-print` hides interactive chrome; `.data-card` rules flatten the cards for A4; button calls `window.print()` |
| Light mode | `body.light-mode` overrides (print CSS lives in the same `<style>`) |

## Serving it locally

```bash
serve_resume.sh            # python3 -m http.server on 0.0.0.0:8123, from the repo folder
```

Then <http://localhost:8123/index.html>. The server must stay on the repo folder:
all asset paths are relative.

## History of the edits

The page has been patched by idempotent python scripts kept in the assistant's
scripts folder (`web-resume-*.py`): galleries, burger menu, badge chevron, lightbox,
local videos, publications links + PDF badges, skill chips (Airflow, Java, Cobol,
HTML5, CSS, JavaScript, Babylon.js, new "Autres"/"Other" category), the Lectra and
DartNet media swaps, and the removal of every placeholder image.

**Current state:** no placeholder left, `img/` deleted (it existed only for the
dummies), all 6 experience cards use a neutral `border-slate-600` bar.

## Contribute

Edit `index.html` in place — indentation is meaningful for the div-depth checks the
patches rely on, and each gallery block is closed by matching `<div>` depths.
Never hot-link remote image URLs: download the asset into `media/<project>/`
and reference the local path (remote hosts break and the page must stay
self-contained).

```bash
git add -A && git commit -m "…" && git push -u origin galleries-and-burger
```

## License

See [LICENSE](LICENSE).
