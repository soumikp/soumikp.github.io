# soumikp.github.io — Quarto site

Personal academic website for Soumik Purkayastha, built with [Quarto](https://quarto.org).

## Site structure

```
.
├── _quarto.yml                    Site configuration
├── styles.css                     Shared stylesheet
├── index.qmd                      Homepage
├── research.qmd                   Research program
├── software.qmd                   Open-source R packages
├── teaching.qmd                   Courses and teaching
├── working-with-me.qmd            For prospective students and collaborators
├── includes/
│   ├── nav.html                   Top navigation (shared across pages)
│   └── footer.html                Footer with external links
├── files/
│   └── Purkayastha_CV.pdf         CV (you add this)
├── .github/workflows/publish.yml  Auto-build on push
└── .gitignore
```

## Local development

```bash
# Install Quarto if you haven't already: https://quarto.org/docs/get-started/
# Then in this directory:

quarto preview              # Live-reload local preview at http://localhost:4321
quarto render               # Build the static site to _site/
```

## Deployment

The site auto-deploys via GitHub Actions on every push to `master` (or `main`). The `.github/workflows/publish.yml` workflow runs `quarto render` and publishes the output to a `gh-pages` branch.

**One-time GitHub setup:**

1. Push this repo to `soumikp/soumikp.github.io` on GitHub.
2. In the repo's **Settings → Pages**, set the source to the `gh-pages` branch.
3. The first push to `master` triggers a build. Subsequent pushes auto-deploy.

## Migration from the existing Jekyll site

Your current `soumikp.github.io` is a Jekyll fork of academicpages. To migrate:

```bash
# 1. Back up the existing Jekyll content (recommended)
git clone https://github.com/soumikp/soumikp.github.io.git soumikp-jekyll-backup

# 2. In your working repo, create a clean branch for the Quarto migration
git checkout master
git checkout -b quarto-migration

# 3. Remove the Jekyll files (keep .git)
git rm -rf .
git clean -fd

# 4. Drop in this Quarto project's files
cp -R /path/to/this/quarto-site/. .

# 5. Add your CV
cp /path/to/Purkayastha_CV.pdf files/

# 6. Verify locally
quarto preview

# 7. Commit and push
git add .
git commit -m "Migrate to Quarto site"
git push origin quarto-migration

# 8. Open a PR, review, merge to master
# 9. The Action will build and publish to gh-pages
# 10. Configure GitHub Pages to serve from gh-pages (Settings → Pages)
```

## Editing content

Pages are `.qmd` files containing a YAML header and a single `{=html}` raw HTML block (extracted from the design mockups). To edit content, just edit the HTML inside the block.

If you want to gradually migrate sections to idiomatic Quarto markdown, you can replace HTML blocks with markdown + `:::` divs that use the same CSS classes (e.g., `::: {.thrust}`). The CSS selectors in `styles.css` will match either way.

## Adding new content

- **News / announcement:** Edit the news section in `index.qmd`.
- **New publication:** None needed — the Publications nav item links directly to your Google Scholar profile.
- **New software package:** Add a new `<article class="pkg-entry">` block in `software.qmd`.
- **New course:** Add a new `<article class="course">` block in `teaching.qmd`.
- **CV:** Replace `files/Purkayastha_CV.pdf`.

## Design notes

- Background: warm cream (`#FBFAF6`)
- Accent: deep navy (`#0A4D8C`) — passes WCAG AAA contrast
- Fonts: Apple system stack (`-apple-system`, SF Pro on Apple devices, falls back gracefully)
- All design tokens are CSS variables at the top of `styles.css` — change them in one place.
