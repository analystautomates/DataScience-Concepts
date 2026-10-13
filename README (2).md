# Analyst Automates

A public learning notebook, built with Jekyll and hosted free on GitHub Pages.

- **Learning section:** Data Science, But Make It Make Sense
- **22 concepts** across 4 categories, each with its own page
- No build tools, no Node, no GitHub Actions — you push a file, GitHub publishes it

---

## 1. First-time setup (about 5 minutes)

**Step 1 — create the repo.**

Two options, and they change one setting:

| Repo name | Your site lives at | `baseurl` in `_config.yml` |
|---|---|---|
| `YOUR-USERNAME.github.io` | `https://YOUR-USERNAME.github.io` | leave as `""` |
| `analyst-automates` | `https://YOUR-USERNAME.github.io/analyst-automates` | set to `"/analyst-automates"` |

The first is cleaner if this is your main site. Pick one.

**Step 2 — upload these files.**

On GitHub: **Add file → Upload files**, drag in everything from this folder, then **Commit changes**. The files must sit at the top level of the repo — `_config.yml` should be visible on the repo's front page, not inside another folder.

**Step 3 — turn on Pages.**

Repo **Settings → Pages**. Under *Build and deployment*, set **Source** to `Deploy from a branch`, branch `main`, folder `/ (root)`. Save.

**Step 4 — fill in your details.**

Open `_config.yml` and set `github_url` to your GitHub profile URL, plus `baseurl` if you chose a project repo. Commit.

Wait about a minute, then visit your URL. Done.

---

## 2. Writing a concept page

This is the thing you'll do most, so it's deliberately one file and one edit.

1. Go to the `_concepts/` folder in your repo.
2. Click the concept you want to write, e.g. `regression.md`.
3. Click the pencil icon (**Edit this file**).
4. Change `status: coming-soon` to `status: written`.
5. Write your explanation **below** the second `---`, in Markdown.
6. Scroll down, click **Commit changes**.

A file goes from this:

```markdown
---
title: "Regression"
section: ml-fundamentals
order: 1
status: coming-soon
blurb: "Predicting a number."
---
```

to this:

```markdown
---
title: "Regression"
section: ml-fundamentals
order: 1
status: written
blurb: "Predicting a number."
---

Regression is what you reach for when the answer is a number rather
than a category.

## The idea

Your notes here. Normal Markdown works: **bold**, *italic*,
`inline code`, lists, links, images.

## Where I got stuck

Write this bit honestly — it's the most useful part of the notebook.
```

Flipping `status` to `written` does three things automatically: the Coming Soon box disappears, the square on the homepage fills in, and the counter in the footer goes up. You never edit the homepage by hand.

You can also click **Write it now** on any Coming Soon page — it opens that exact file in GitHub's editor.

### The front matter fields

Everything between the two `---` lines is settings, not content. Keep the lines in place.

| Field | What it does |
|---|---|
| `title` | Page heading and the link text in the index |
| `section` | Which category it belongs to. Must match an `id` in `_data/sections.yml` |
| `order` | Position within its category, and the prev/next order |
| `status` | `coming-soon` or `written` |
| `blurb` | One short line shown under the title in the index |

---

## 3. Adding a brand new concept

Go to `_concepts/`, click **Add file → Create new file**, name it `cross-validation.md` (lowercase, hyphens, `.md` on the end — this becomes the URL), and paste:

```markdown
---
title: "Cross-validation"
section: ml-fundamentals
order: 6
status: coming-soon
blurb: "Testing on every slice of the data."
---
```

Commit. It appears in the index, gets a square on the homepage, and lives at `/learn/cross-validation/`. No other file needs changing.

---

## 4. Everyday edits

| To change | Edit this |
|---|---|
| Menu items | `nav:` in `_config.yml` |
| Category names, colours, one-line descriptions | `_data/sections.yml` |
| Homepage headline and intro | `index.html` |
| About page | `about.md` |
| Projects page | `projects.md` |
| Colours, fonts, spacing | the `:root` block at the top of `assets/css/main.css` |
| Header or footer | `_includes/nav.html`, `_includes/footer.html` |

The header and footer are written once in `_includes/` and pulled into every page, so adding a menu item updates all 26 pages at once.

---

## 5. How deploying works

There's no deploy step. Committing to `main` *is* deploying.

1. Edit a file on github.com (or push from your machine).
2. GitHub rebuilds the site automatically.
3. Changes are live in roughly 30–90 seconds.

To check a build, open the **Actions** tab in your repo. A green tick means it published; a red X means something in the YAML is malformed — click it to see which file.

---

## 6. Previewing locally (optional)

Only worth setting up if you're redesigning. For writing, editing on github.com is faster.

```bash
gem install bundler
bundle install
bundle exec jekyll serve
```

Then open `http://localhost:4000`. It rebuilds as you save. Note that `_config.yml` changes need a restart.

---

## 7. When something breaks

**Red X in the Actions tab.** Almost always the front matter. Check that the file has both `---` lines, that titles with a colon in them are wrapped in quotes, and that you haven't used tabs for indentation in `_config.yml` or `_data/sections.yml` — YAML wants spaces.

**A concept doesn't appear in the index.** Its `section` value doesn't match any `id` in `_data/sections.yml`. They're case-sensitive.

**The site loads but has no styling.** Your `baseurl` doesn't match your repo name. See the table in step 1.

**Nothing at all at your URL.** Check Settings → Pages is still pointing at `main` / `/ (root)`, and that `_config.yml` sits at the top level of the repo.

---

## 8. Project layout

```
_config.yml           site settings, nav, collection config
_data/sections.yml    the four categories
_layouts/             page skeletons (base, page, concept)
_includes/            header, footer, reusable index block
_concepts/            one markdown file per concept → /learn/<name>/
assets/css/main.css   the only stylesheet
index.html            homepage
learn.md              full index
projects.md, about.md placeholder pages
```
