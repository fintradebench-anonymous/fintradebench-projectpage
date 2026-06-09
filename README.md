# FinTradeBench &mdash; Project Page

Static project page for **FinTradeBench: A Financial Reasoning Benchmark for LLMs**.

The page is a single `index.html` that uses Bulma + FontAwesome + Academicons (all loaded locally from `static/`). No build step is required &mdash; just push to GitHub Pages.

---

## 1. Folder layout

```
FinTradeBench-projectpage/
  index.html                  # the page (edit this)
  README.md                   # this file
  static/
    css/                      # bulma, fontawesome, etc. (copied from GAEA template)
    js/                       # bulma carousel + slider, fontawesome
    images/
      favicon.svg             # placeholder F + chart icon
      teaser.png              # Figure 1 from the paper
      pipeline.png            # Figure 2 (design pipeline)
      rag_architecture.png    # Figure 3 (dual-track RAG)
      results_main.png        # Table 2 (main results)
      quality_metric.png      # Figure 4 (global quality metrics)
```

---

## 2. Exporting the figures from the PDF

Open `Finbot__Neurips_version_for_arxiv_.pdf` and export each figure as a PNG/JPG at &ge;1500 px width. Two easy options on Windows:

- **Adobe Acrobat / Foxit:** right-click the figure &rarr; "Save Image As".
- **`pdftoppm` (already on your machine via MiKTeX):**
  ```powershell
  pdftoppm -png -r 200 -f 2 -l 2 "Finbot__Neurips_version_for_arxiv_.pdf" fig
  ```
  Replace `-f 2 -l 2` with the page numbers of each figure, then crop the resulting PNG.

Save them into `static/images/` using the filenames listed above (or update the `<img src=...>` paths in `index.html`).

---

## 3. Editing the page

Everything you'll want to change lives in `index.html` and is grouped by `<section>`:

| Section | What to edit |
|---|---|
| Hero / Title | Authors, affiliation, the **arXiv link** (currently `href="#"` &mdash; replace once the arXiv ID is live) |
| Teaser | One paragraph + Figure 1 caption |
| Abstract | Drop in the final abstract text if it changes |
| Contributions | Bullet list of contributions |
| Pipeline / Taxonomy / RAG | Replace figure paths and tweak captions |
| Benchmark Statistics | Table values |
| Results | Findings + Table 2 + Figure 4 |
| Social Media | **Replace placeholder cards with real links** &mdash; see &sect;4 below |
| BibTeX | Update the citation once arXiv ID + NeurIPS status are final |

---

## 4. The "In the Wild" and "Cited By" sections

The page has two related sections for tracking external interest in the paper:

- **`#cited-by`** &mdash; academic papers that cite FinTradeBench (currently arXiv preprints and one SSRN paper). Each citing paper is a single `<div class="column is-half">` block with an arXiv / SSRN icon.
- **`#social-media`** &mdash; subdivided into **Press &amp; Long-form Coverage**, **Video**, **X (Twitter)**, **LinkedIn**, **Instagram**, and **Indexing &amp; Bibliographic** (a flat row of clickable tag-pills for DBLP, ADS, AlphaXiv, RePEc, ResearchGate, CatalyzeX, SciRate, GPTGet, Scribd).

Each entry is a `<div class="column is-half">` containing a `<a class="social-card">`. Duplicate one of the existing cards to add a new entry. The pattern is:

```html
<div class="column is-half">
  <a class="social-card"
     href="https://www.youtube.com/watch?v=XXXXXXXX"
     target="_blank"
     style="display:block; color:inherit; text-decoration:none;">
    <div class="icon-row">
      <i class="fab fa-youtube" style="color:#FF0000;"></i>
      <span class="platform">YouTube</span>
    </div>
    <div class="title-text">My talk at FinNLP 2026</div>
    <div class="meta">Stanford FinNLP &middot; March 2026</div>
    <div style="margin-top:.5rem;">
      <span class="tag-pill">Talk</span>
      <span class="tag-pill">Benchmark</span>
    </div>
  </a>
</div>
```

Useful FontAwesome icon classes:

| Platform | Icon class | Brand color |
|---|---|---|
| YouTube | `fab fa-youtube` | `#FF0000` |
| X / Twitter | `fab fa-x-twitter` | `#000000` |
| LinkedIn | `fab fa-linkedin` | `#0A66C2` |
| Reddit | `fab fa-reddit` | `#FF4500` |
| Hacker News | `fab fa-y-combinator` | `#FF6600` |
| Mastodon | `fab fa-mastodon` | `#6364FF` |
| Blog / press | `fas fa-newspaper` | any |
| Podcast | `fas fa-podcast` | `#8940FA` |

The header also has a "Social Media" button next to arXiv / Dataset / Code / BibTeX that jumps to this section.

---

## 5. Local preview

You can just double-click `index.html` to open it in a browser, but some CSS files prefer being served. The simplest one-liner is:

```powershell
# from inside FinTradeBench-projectpage\
python -m http.server 8000
```

Then open `http://localhost:8000`.

---

## 6. Deploying to GitHub Pages

Two common patterns:

### Option A &mdash; dedicated repo (recommended for a project page)

```powershell
cd C:\Users\ddkxi\Downloads\FinTradeBench-projectpage
git init
git add .
git commit -m "Initial project page"
git branch -M main
git remote add origin https://github.com/<your-org>/fintradebench-projectpage.git
git push -u origin main
```

Then on GitHub: **Settings &rarr; Pages &rarr; Source: `main` / `(root)`**. The page will go live at `https://<your-org>.github.io/fintradebench-projectpage/`.

### Option B &mdash; `gh-pages` branch on your existing PaperSubmission repo

If you want it under `https://fintradebench-anonymous.github.io/PaperSubmission/`:

```powershell
cd <your-existing-PaperSubmission-clone>
git checkout --orphan gh-pages
git rm -rf .
# copy the contents of FinTradeBench-projectpage into the repo root
git add .
git commit -m "Project page"
git push -u origin gh-pages
```

Then **Settings &rarr; Pages &rarr; Source: `gh-pages` / `(root)`**.

---

## 7. Anonymity &mdash; NeurIPS policy summary

NeurIPS uses **double-blind** review, but explicitly **permits non-anonymous arXiv preprints**. The published policy (paraphrased) says:

> Authors may post a non-anonymous version of the paper to a non-anonymous archive (such as arXiv), but they should *not actively advertise* the paper during the review period (e.g. promotional tweets from the authors' own accounts, posts on personal social media driving traffic to the paper).

Since the arXiv version (arXiv:2603.19225) is already public under your real names, the project page itself can carry the author names without any additional anonymity problem &mdash; it is just the canonical home page for an already non-anonymous artifact. Two practical guardrails kept in mind on this page:

1. The page **documents third-party coverage** (the &ldquo;In the Wild&rdquo; section) rather than directing the reader to share the paper themselves. This is reporting, not advertising.
2. The hero block notes the work is &ldquo;Under review at NeurIPS&rdquo; for transparency, without naming reviewers, area chairs, or any review-private information.

What you should still avoid during the review period:

- Posting links to this page from your own personal Twitter/LinkedIn/etc. accounts.
- Adding a &ldquo;Share this paper&rdquo; or &ldquo;Tweet&rdquo; button to the page (we did not add one).
- Updating the page in ways that could communicate with reviewers (e.g. responses to specific anonymous critiques).

If your specific NeurIPS track or chair has issued tighter guidance than the default policy, follow that. When in doubt, take down or anonymize the page until decisions are out &mdash; the cost of being too cautious is much lower than the cost of a desk reject for policy violation.

---

## 8. Credit

Template adapted from the [GAEA project page](https://ucf-crcv.github.io/GAEA/), which is itself adapted from the [GigaGAN page](https://mingukkang.github.io/GigaGAN/).
