# sulsaker.github.io — personal academic site

Simen Aardal Ulsaker's homepage, served by GitHub Pages at
<https://sulsaker.github.io>.

Plain static HTML + CSS — **no build step, no dependencies**. Edit, push to
`main`, and Pages redeploys within a minute.

## Edit these

- `index.html` — the whole site, one page in reading order (about, work in
  progress, publications, contact). To add a paper, copy the commented template
  just above the Work in Progress section.
- `style.css` — all styling. Colours live in the `:root` variables at the top;
  light/dark follows the reader's OS via `prefers-color-scheme`.
- `assets/portrait.jpg` — portrait photo. **Not yet added.** Drop in a square
  JPG (600×600 or larger); until then the image box hides itself automatically
  and only the links beneath it show.
- `assets/favicon.svg` — the "SU" monogram in the browser tab.
- `papers/` — any PDFs you want to host yourself, linked from the paper list.

## The CV

`cv.pdf` at the site root is **generated — never edit or upload it by hand.**
It is compiled from `cv/cv.tex` by GitHub Actions
(`.github/workflows/build-cv.yml`) on every push that touches `cv/`. No LaTeX
installation is needed on your machine; GitHub runs TeX Live in the cloud and
commits the resulting PDF back to the repo.

So the update loop is: **change `cv/cv.tex` → push → the PDF on the site
refreshes itself in ~2 minutes.**

`cv/cv.tex` is deliberately **self-contained** — all layout macros are defined
at the top of the file. The original Overleaf version pulled in a separate
`structure.tex`, which the cloud build would not have found. Keep it that way:
if you add packages, add them in the preamble rather than in an included file.
A handful of `% TODO` comments in the source flag details that need your
decision (see the notes in the file header).

Overleaf is out of the loop entirely — this repo is the only home for the CV.
Edit `cv/cv.tex` either locally or in GitHub's web editor (press `.` on the repo
page), then push.

To check your changes before pushing, you have MiKTeX installed, so you can
compile locally:

```
cd cv
pdflatex cv.tex
```

That produces `cv/cv.pdf` for previewing. Don't commit it — it's gitignored, and
the Action builds the published copy at the repo root. The local build only
needs to succeed for the cloud build to succeed; they use the same file.

You can also rebuild the PDF without changing anything: **Actions → Build CV →
Run workflow**.

## Plumbing (rarely touched)

- `.nojekyll` — tells Pages to serve files as-is (skip Jekyll processing).
- `robots.txt` / `sitemap.xml` — search-engine hints.
- `.gitignore` — LaTeX build litter and OneDrive/Windows cruft.

## Preview locally

Any static server works, e.g. with Node installed:

```
npx http-server . -p 5320
```

then open <http://localhost:5320>. Opening `index.html` directly in a browser
also works for everything except the root-relative links.
