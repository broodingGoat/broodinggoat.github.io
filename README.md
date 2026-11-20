# Sushaant Mujoo — personal website

Jekyll site for GitHub Pages + custom domain `sushaantmujoo.com`. GitHub Pages builds it automatically on every push — no local build step needed.

## Structure

- `_config.yml` — site title, URL, and the `sections` collection
- `_layouts/default.html` — the terminal shell: head, CSS, JSON-LD Person schema, header, footer, blinking cursor, and the JavaScript that assembles the email link. Edit this only to change the look of the whole site.
- `_sections/about.md` — the About section (intro, three career stints, leadership, beyond work)
- `_sections/meta-engineering-blogs.md` — Meta Engineering Blog posts
- `_sections/tech-society.md` — tech + society articles (two clusters in one file)
- `_sections/politics.md`, `_sections/career.md`, `_sections/mindfulness.md`, `_sections/life.md` — the other writing groups
- `index.html` — the Jekyll page that assembles the sections: About open, writing groups collapsed, in `order` (1–6)
- `resume.pdf` — resume, converted from the Drive base resume (Sep 28, 2026); web version with email and phone removed
- `CNAME` — tells GitHub Pages to serve this site at sushaantmujoo.com
- `llms.txt` — machine-readable summary of the site for LLM crawlers (no contact details)
- `_backup/index.html` — the original single-file version, kept for reference (Jekyll ignores `_`-prefixed folders)

## Editing a section

Open the section's `.md` file in the GitHub web editor, edit the text, commit. Each file starts with front matter:

```yaml
---
group: writing
path: "~/politics"
order: 3
---
```

- `group`: `about` or `writing` (decides where the section renders)
- `path`: the `~/...` label shown in the collapsible heading
- `order`: sort order of the writing groups (1–6)

Writing items are Markdown list items: `- [Title](url) <span class="meta">Jan 2025</span><span class="src">linkedin</span>` — keep the `<span>` tags for the date and source labels (`meta-eng` / `medium` / `linkedin`). Small HTML blocks (like `<p class="note">` and `<p class="sub">`) are used where the design needs a styled paragraph. The email link stays JavaScript-assembled — never put a plaintext email in any file.

To add a new writing group: create `_sections/<name>.md` with `group: writing`, a `path`, and the next `order` number. It renders automatically, collapsed by default.

## Deploy to GitHub Pages

1. On GitHub, create a **public** repo named `broodinggoat.github.io` (your username + `.github.io` — the name is what makes it a user site).
2. Upload all files in this folder to the repo's default branch (`main`).
3. Repo → Settings → Pages → Source: Deploy from a branch, branch `main`, folder `/ (root)`. Save.
4. Wait a few minutes, then check `https://broodinggoat.github.io` — the site should be live there first.
5. In Settings → Pages → Custom domain, enter `sushaantmujoo.com` and save. GitHub will verify the CNAME file is present.

## Point the domain at GitHub (registrar step)

At your domain registrar for `sushaantmujoo.com`, replace the current DNS records with:

- Apex (`@`): four A records → `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`
- `www`: CNAME → `broodinggoat.github.io`

Note: the domain currently resolves to `198.18.92.243` — that record must be replaced, not added to. After DNS propagates (up to a day, usually minutes), turn on "Enforce HTTPS" in Settings → Pages.

## Updating the site

Edit a `_sections/*.md` file (or `resume.pdf`), commit, push — GitHub Pages rebuilds automatically in a minute or two.

## Previewing locally

Requires Ruby + Jekyll (`gem install jekyll bundler`), then from this folder:

```
jekyll build --destination /tmp/site-preview
```

Open `/tmp/site-preview/index.html` in a browser to check the assembled page before pushing.
