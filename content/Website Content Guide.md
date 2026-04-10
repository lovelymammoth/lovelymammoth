---
title: Website Content Guide
tags:
  - website
  - documentation
  - hugo
aliases:
  - Content Guide
  - CMS Guide
created: 2026-04-10
draft: true
---

# Website Content Guide

This guide covers how to update and extend the Lovely Mammoth website without touching the theme or layout code. All content lives inside `content/` and `static/images/`.

> [!tip] Obsidian workflow
> This vault is configured to save image attachments directly to `static/images/`. Drag any image into Obsidian and it lands in the right place — no manual copying needed.

---

## 1. Adding a New Work Category

### Step 1 — Register the category name

Open [[themes/lmp/layouts/index.html]] and add the new name to the `$categories` slice:

```go
{{ $categories := slice "Characters & Creatures" "Digital Sculpting" "VR Sculpture" "Experience Design" }}
```

The order of names here is the order they appear on the homepage.

### Step 2 — Create the category page

Create a new file in `content/work/`, for example `content/work/experience-design.md`:

```markdown
---
title: "Experience Design"
category: "Experience Design"
layout: gallery
weight: 4
cover:
  - images/cover-1.jpg
  - images/cover-2.jpg
  - images/cover-3.jpg
draft: false
---

![[your-first-image.jpg]]
![[your-second-image.jpg]]
![[your-third-image.jpg]]
```

> [!info] cover vs gallery
> - **`cover`** — the 2–3 images shown as the preview strip on the homepage. Keep this in frontmatter with `images/` prefix.
> - **Gallery images** — go directly in the body as `![[filename.jpg]]` wikilinks. Obsidian renders them visually so you can see and arrange them. Hugo converts them to the web gallery automatically.

> [!warning] weight does NOT control category order
> The `weight` field has no effect on which category section appears first on the homepage. The order is set by the `$categories` slice in `themes/lmp/layouts/index.html` — rearrange the strings there to change the order. `weight` only matters if a category ever has multiple pages (to sort between them).

> [!tip] Hiding without deleting
> Set `draft: true` in any entry's frontmatter to hide it from the site without removing the file.

---

## 2. Adding Images

### Drop the file

Drag the image into Obsidian — it saves automatically to `static/images/`. Alternatively, copy it there manually.

Supported formats: `.jpg`, `.jpeg`, `.png`, `.gif`, `.webp`

### Add it to a gallery

Open the category file (e.g. [[characters-creatures]]) and add a wikilink in the body:

```
![[your-image.jpg]]
```

Obsidian shows a live preview of the image. Drag the lines to reorder — the website gallery reflects that order exactly.

### Make an image open a link instead of the lightbox

Add a URL after the filename with a `|` separator:

```
![[your-image.jpg|https://example.com]]
```

- Images **without** a URL → click opens the lightbox as usual
- Images **with** a URL → click opens the link in a new tab; a `↗` indicator appears on hover
- Linked images are excluded from the lightbox counter

> [!warning] Cover images use a different format
> The `cover:` list in the frontmatter still uses the full path with `images/` prefix:
> ```yaml
> cover:
>   - images/your-image.jpg
> ```
> Only the body gallery uses `![[filename.jpg]]`.

---

## 3. Adding Embedded Videos and 3D Players

Paste any `<iframe>` in the body of the category file, below the image wikilinks. It renders in a separate embeds section below the image grid — images and iframes stay separate automatically.

### YouTube

```html
<iframe
  src="https://www.youtube.com/embed/VIDEO_ID"
  height="500"
  allowfullscreen>
</iframe>
```

Replace `VIDEO_ID` with the ID from the YouTube URL (e.g. `dQw4w9WgXcQ`).

### Vimeo

```html
<iframe
  src="https://player.vimeo.com/video/VIDEO_ID"
  height="500"
  allowfullscreen>
</iframe>
```

### Sketchfab

```html
<iframe
  title="Model name"
  src="https://sketchfab.com/models/MODEL_ID/embed"
  height="500"
  allowfullscreen>
</iframe>
```

> [!tip] Mixing images and embeds
> You can have both in the same file. Put `![[image]]` wikilinks first, then iframes below. They render in separate sections — gallery grid on top, embeds below.

> [!note] Other services that work
> Any service with an `<iframe>` embed works: ArtStation players, Google Maps, Spotify, p5.js sketches, and more.

---

## 4. Adding a Research Entry

Create a new `.md` file inside `content/research/`. Name it with a number prefix to control sort order, e.g. `content/research/02-avatars-presence.md`:

```markdown
---
title: "Avatars and Presence in Social VR"
entrynum: "R2"
status: "In Progress"
weight: 2
tags:
  - VR
  - Avatars
  - Presence
draft: false
---

Write your research description here as plain text.

This supports **bold**, *italic*, and any standard Markdown.
```

### Field reference

| Field | Purpose |
| --- | --- |
| `title` | Displayed as the entry heading |
| `entrynum` | Code shown in the left column — use `R1`, `R2`, etc. |
| `status` | Shown in the right aside — e.g. `In Progress`, `Published`, `Submitted` |
| `weight` | Sort order (lower = first) |
| `tags` | Rendered as pills at the bottom of the entry |
| `draft: true` | Hides the entry without deleting the file |

> [!tip]
> The body text supports full Markdown — use it for abstracts, methodology notes, or publication references.

---

## Quick Reference

| Task | What to edit |
| --- | --- |
| Add a new work category | 1. `themes/lmp/layouts/index.html` — add name to `$categories` slice<br>2. New file in `content/work/` |
| Reorder category sections | Edit the string order in the `$categories` slice in `themes/lmp/layouts/index.html` |
| Rename a category | Update the string in `index.html` **and** the `category:` field in the `.md` file |
| Change homepage cover images | Edit `cover:` list in frontmatter (use `images/filename.jpg`) |
| Add/reorder gallery images | Edit `![[filename.jpg]]` lines in the body of the category `.md` |
| Add video or 3D embed | Paste `<iframe>` in the body of the category `.md` |
| Add a research entry | New file in `content/research/` |
| Hide content without deleting | Set `draft: true` in frontmatter |
| Change bio, email, or social links | [[_index]] |
| Change site title | `hugo.toml` — `title` field |

---

> [!warning] After making changes
> Hugo rebuilds automatically while the dev server is running. To start it:
> ```bash
> cd lovelymammoth-alt && hugo server --port 1314 --bind 127.0.0.1
> ```
> Then open [http://127.0.0.1:1314](http://127.0.0.1:1314) to preview before committing.
