# Setup Guide — Personal Site + Blog Cross-posting

## Architecture overview

```
┌─────────────────────────────────────────────┐
│  GitHub repo: c-bartley.github.io           │
│  ├── Jekyll site (auto-built by GH Pages)   │
│  ├── Blog posts in _posts/ (markdown)       │
│  └── Generates feed.xml (Atom/RSS)          │
└──────────────┬──────────────────────────────┘
               │
    ┌──────────┴──────────┐
    │                     │
    ▼                     ▼
  Served at            gaelgai.im/blog
  c-bartley.           fetches feed.xml
  github.io            and renders posts
                       tagged crosspost
```

You write a blog post once as a markdown file. Push to GitHub. Both sites
update: the personal site rebuilds automatically via GitHub Pages, and the
gaelgai.im blog page fetches the RSS feed client-side.

---

## Part 1 — Deploy the personal site

### 1. Create the GitHub Pages repository

```bash
# On your local machine
cd ~/projects  # or wherever
git init c-bartley.github.io
cd c-bartley.github.io
```

Copy the entire contents of the `site/` folder into this directory (all the
files from the download: `_config.yml`, `_layouts/`, `_posts/`, `assets/`,
`index.html`, `research.md`, `projects.md`, `blog.html`, `cv.md`,
`robots.txt`, `404.html`, `Gemfile`).

```bash
git add -A
git commit -m "Initial site"
git remote add origin git@github.com:c-bartley/c-bartley.github.io.git
git push -u origin main
```

### 2. Enable GitHub Pages

1. Go to **github.com/c-bartley/c-bartley.github.io → Settings → Pages**
2. Under "Build and deployment", set Source to **Deploy from a branch**
3. Set Branch to **main**, folder to **/ (root)**
4. Click Save

The site will be live at **https://c-bartley.github.io** within a few
minutes. GitHub will automatically run Jekyll on every push.

### 3. (Optional) Custom domain

A custom domain like `chrisbartley.com` or `chrisbartley.dev` improves
branding and SEO authority over time. Steps:

1. Buy a domain (Namecheap, Cloudflare, Porkbun — ~£8–12/year)
2. In your DNS, add:
   - **A records** pointing to GitHub Pages IPs:
     ```
     185.199.108.153
     185.199.109.153
     185.199.110.153
     185.199.111.153
     ```
   - **CNAME** for `www` → `c-bartley.github.io`
3. In the repo, create a `CNAME` file containing just the domain:
   ```
   chrisbartley.com
   ```
4. In Settings → Pages, enter the custom domain and tick "Enforce HTTPS"
5. Update `url` in `_config.yml` to `https://chrisbartley.com`
6. Update `robots.txt` sitemap URL to match

---

## Part 2 — Set up the GitHub Profile README

The `c-bartley/c-bartley` repo is special — its README shows on your GitHub
profile page.

1. Create the repo at **github.com/new** → name it `c-bartley`, tick
   "Add a README file"
2. Replace the auto-generated README.md with the contents of
   `GITHUB_PROFILE_README.md` from the download
3. Commit and push

Your GitHub profile at `github.com/c-bartley` will immediately show the
README with your research summary, links, and project descriptions.

---

## Part 3 — Blog workflow

### Writing a post

Create a new file in `_posts/` following the naming convention:

```
_posts/YYYY-MM-DD-slug-title.md
```

Every post needs YAML front matter:

```yaml
---
layout: post
title: "Your post title"
date: 2026-07-15
description: "One-sentence summary for SEO and social cards"
tags:
  - manx-gaelic
  - speech-technology
crosspost: true       # Set to true to show on gaelgai.im
---

Your markdown content here.

Use <!--more--> to set where the excerpt cuts off on listing pages.
```

### Publishing

```bash
git add _posts/2026-07-15-your-new-post.md
git commit -m "Post: Your post title"
git push
```

GitHub Pages rebuilds automatically. The post appears on your site within
1–2 minutes, and the RSS feed updates immediately after.

### Cross-posting to gaelgai.im

Posts with `crosspost: true` in their front matter will appear on
gaelgai.im's blog page (once you add the widget — see below).

The `crosspost` value is exposed as a `<category>` tag in the Atom feed,
so the widget can filter on it. By default the widget shows all posts,
but you can uncomment the filter line in the JavaScript to show only
crossposted ones.

---

## Part 4 — Add the blog page to gaelgai.im

### Option A: Client-side widget (simplest)

1. Create a new route or page on gaelgai.im at `/blog`
2. Drop in the contents of `gaelgai-blog-widget.html`
3. Style to match the rest of the site

The widget fetches the Atom feed from your GitHub Pages site on page load
and renders the posts. No server-side changes needed.

**CORS note:** GitHub Pages serves feeds with permissive CORS headers, so
this should work directly. If you hit CORS issues during development,
the widget includes a commented-out proxy fallback.

### Option B: Server-side rendering (better for SEO)

If you want the blog posts to be indexable by search engines on gaelgai.im
too (rather than just on the personal site), you can fetch and cache the
feed server-side. Since gaelgai.im appears to run on a Python backend:

```python
# Example: Flask route that fetches and caches the feed
import feedparser
from functools import lru_cache
from datetime import datetime

@lru_cache(maxsize=1)
def _fetch_feed(cache_key):
    """cache_key changes hourly to refresh."""
    return feedparser.parse('https://c-bartley.github.io/feed.xml')

@app.route('/blog')
def blog():
    cache_key = datetime.utcnow().strftime('%Y-%m-%d-%H')
    feed = _fetch_feed(cache_key)
    posts = [e for e in feed.entries if 'crosspost' in
             [t.term for t in getattr(e, 'tags', [])]]
    return render_template('blog.html', posts=posts)
```

Install `feedparser` on the server: `pip install feedparser`

### Option C: GitHub Action → deploy (most automated)

A GitHub Action in the personal site repo can, on push, copy crossposted
markdown files to the gaelgai.im repo. This requires a deploy key or PAT.

This is the most complex option and only worth it if you want the full
markdown source in both repos. For most purposes, Option A or B is
simpler and sufficient.

---

## Part 5 — SEO checklist

The site is already configured for strong SEO out of the box. Here's what's
in place and what to do next:

### Already done (built into the site)

- [x] `jekyll-seo-tag` generates `<title>`, `<meta description>`, Open
      Graph, Twitter Cards, and JSON-LD for every page
- [x] Additional `Person` schema in the default layout with your name,
      affiliation, research topics, and social links
- [x] `jekyll-sitemap` generates `sitemap.xml` automatically
- [x] `jekyll-feed` generates an Atom feed at `/feed.xml`
- [x] `robots.txt` with sitemap reference
- [x] Semantic HTML5 throughout (`<article>`, `<nav>`, `<header>`, etc.)
- [x] Clean permalink structure (`/blog/2026/07/title/`)
- [x] Mobile responsive design
- [x] Skip-to-content link for accessibility
- [x] `rel="me"` on social links (supports IndieWeb verification)
- [x] Dark mode support via `prefers-color-scheme`

### Manual steps after deployment

1. **Google Search Console** — go to search.google.com/search-console,
   add your site, verify ownership (HTML file or DNS), submit your sitemap
   (`/sitemap.xml`). This is the single most important step for indexing.

2. **Google Scholar** — your Interspeech paper should appear automatically
   if it's indexed by the conference proceedings. Link your Scholar profile
   from your site.

3. **Bing Webmaster Tools** — similar to Search Console. Submit sitemap.

4. **Cross-linking** — add a link to the personal site from gaelgai.im
   (the "About Me" section already links to GitHub, so add the personal
   site URL there too). Bidirectional linking between your properties
   strengthens authority.

5. **University profile** — if Sheffield has a staff/student page for you,
   make sure it links to your personal site.

6. **Regular posting** — search engines reward fresh content. Even one post
   a month makes a difference.

---

## Quick reference

| What | Where |
|---|---|
| Personal site | `c-bartley.github.io` (or custom domain) |
| Blog | `c-bartley.github.io/blog/` |
| RSS feed | `c-bartley.github.io/feed.xml` |
| Sitemap | `c-bartley.github.io/sitemap.xml` |
| GitHub profile | `github.com/c-bartley` |
| Gaelg AI | `gaelgai.im` |
| Gaelg AI blog | `gaelgai.im/blog` (after widget install) |

### File locations

| File | Purpose |
|---|---|
| `_config.yml` | Site title, description, author, plugins |
| `_posts/*.md` | Blog posts |
| `index.html` | Home page |
| `research.md` | Research & publications |
| `projects.md` | Project descriptions |
| `cv.md` | Curriculum vitae |
| `blog.html` | Blog listing page |
| `assets/css/style.css` | All styling |
| `_layouts/default.html` | Base template (edit nav, footer, structured data) |
| `_layouts/post.html` | Blog post template |
