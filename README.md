# Portfolio — Sarah Yuzi Sandström

Computer Science student · Software & data projects

A static portfolio presenting software, data and machine-learning projects — Python, SQL, REST APIs, validated data pipelines, automated testing and CI — built as plain HTML and CSS and published with GitHub Pages.

## Pages

- `/` — homepage
- `/projects/` — project index (featured projects, then other technical work)
- `/projects/skillpath/` — SkillPath Navigator case study
- `/projects/privacy-security-awareness/` — GDPR guide & staff workshop case study (supporting; linked from About)
- `/about/` — about
- `/cv/` — CV

## Run locally

```bash
python3 -m http.server 8000
```

Then open http://localhost:8000. Serve it this way rather than opening the files directly, so the fonts and styles load.

## Structure

Plain HTML per route with a shared `styles.css` for base styling and responsive breakpoints. Every internal link, stylesheet, image and favicon path is relative, so the site works at a GitHub Pages sub-path (`https://<user>.github.io/<repo>/`) as well as under a custom domain. Keep new paths relative: a path starting with `/` would break under the sub-path.

Note that `styles.css` targets the inline `style` strings in the markup (for example `[style*="300px minmax(0, 1fr)"]` and `[style*="padding: 0 80px 128px"]`) to fold the desktop layout down for tablet and mobile. New markup should reuse those exact inline strings, or it will not respond at the breakpoints.

## Featured projects

Featured projects are marked in `index.html` and `projects/index.html` with `<!-- FEATURED 01 -->`-style comments. The third slot is reserved: to add a project, copy the article for featured project 02, change its label and content, and place it at the `FEATURED 03` comment. Smaller projects live in the "Other technical work" section below it. Only list technologies that a project's repository actually verifies.

## CV

The CV page is `cv/index.html`. Its download button links to `documents/Sarah_Sandstrom_CV.pdf`.

The PDF is generated from an editable source, `documents/cv-source.html`: one self-contained HTML file with inline CSS, laid out for a single A4 page. It loads Literata and IBM Plex Sans from Google Fonts, so generating the PDF needs an internet connection; there are no other assets.

To regenerate the PDF after editing the source, run from the repository root:

```bash
google-chrome --headless=new --disable-gpu --no-pdf-header-footer \
  --virtual-time-budget=8000 \
  --print-to-pdf=documents/Sarah_Sandstrom_CV.pdf \
  "file://$PWD/documents/cv-source.html"
```

`chromium` works in place of `google-chrome`; the virtual-time budget gives the web fonts time to load. Then check that the result is still one page, for example with `pdfinfo documents/Sarah_Sandstrom_CV.pdf`. If it spills onto a second page, tighten the text or the spacing in the source's `<style>` block. Keep the PDF filename unchanged so the download link stays valid.
