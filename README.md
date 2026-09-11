# mwegit.github.io

Personal site — https://mwegit.github.io

Jekyll, built natively by GitHub Pages. There is no build step to run and no CI
workflow: push to `main` and GitHub rebuilds the site in under a minute.

```
_config.yml                 site settings (title, email, permalinks)
_layouts/default.html       shared shell — nav, footer, <head>
_layouts/post.html          article layout
assets/style.css            all styling; light/dark via prefers-color-scheme
index.html                  home — intro, skills, experience, education
projects.html               /projects/
blog.html                   /blog/  (lists everything in _posts/)
feed.xml                    /feed.xml Atom feed
_posts/                     one Markdown file per article
```

## Writing a post

Create `_posts/YYYY-MM-DD-some-slug.md`:

```markdown
---
title: "Your title here"
date: 2026-09-14
tags: [terraform, azure]
---

Opening paragraph — this becomes the excerpt on the blog index.

## A heading

Body text, `inline code`, **bold**, [links](https://example.com), lists,
tables, and fenced code blocks all work.
```

Commit and push. It appears at `/blog/2026/09/some-slug/` and at the top of
`/blog/`. The filename date sets the URL and the sort order.

Useful front matter:

| Key | Effect |
|---|---|
| `published: false` | Keeps a draft out of the built site entirely |
| `tags: [a, b]` | Renders as chips on the index and the article |
| `description:` | Overrides the `<meta name="description">` for that page |

## Editing the rest

Content lives in the three `.html` files. Styling is all in `assets/style.css` —
colors are CSS custom properties on `:root`, with a `prefers-color-scheme: dark`
block overriding them. Change colors in those two blocks only.

## Local preview (optional)

Not required — pushing is the normal loop. If you want one:

```bash
gem install bundler jekyll && jekyll serve
```

## Deliberate omissions

- **No phone number and no home city.** Public pages get scraped.
- **No links to private repos.** The `tralhos-capital` work and the internal
  C.H. Robinson platform are described, not linked.
- **No strategy parameters.** The trading projects describe architecture only.
