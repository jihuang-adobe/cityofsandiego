# Secondary Site Migration Guide

A guide for migrating a Kaiser Permanente secondary sales site into AEM Edge Delivery Services using the Experience Modernization Agent (EMA).

---

## What you need

One URL — the root of the secondary site to migrate.

**Example:** `https://choose.kaiserpermanente.org/google`

---

## How to run it

Open Claude Code in this repository and type:

```
/migrate-secondary-site
```

Provide the source URL when asked. EMA handles the rest.

---

## What EMA does

EMA runs five steps and pauses for your confirmation before moving to the next:

| Step | What happens |
|---|---|
| 1 — Discover pages | Finds every page on the site and captures the full nav structure |
| 2 — Extract content | Reads each page section by section — all text, images, links, and legal copy exactly as written |
| 3 — Map to blocks | Assigns the correct AEM block to each section using the ak-kaiserpermanente block library |
| 4 — Generate HTML | Produces one DA-ready HTML file per page plus a `nav.html` for the site header |
| 5 — Migration summary | Reports what was migrated, what blocks were used, and what needs review |

---

## What you get back

At the end of the migration, EMA produces a set of HTML files and a summary report.

### Files generated

| File | DA upload path |
|---|---|
| `nav.html` | `/fragments/nav/header` |
| `index.html` | `/[employer-name]/index` |
| `plans.html` | `/[employer-name]/plans` |
| `getting-care.html` | `/[employer-name]/getting-care` |
| *(one file per page)* | `/[employer-name]/[page-name]` |

### Migration summary

- Total pages migrated, sections, and blocks used
- A checklist of items that need review before publishing

---

## Uploading to DA

1. Go to [DA](https://da.live/#/adobedrago/ak-kaiserpermanente/)
2. Upload `nav.html` first → `/fragments/nav/header`
3. Create a new folder `/[employer-name]/`
4. Upload each page file to its corresponding path
5. Preview the site at:
   `https://main--ak-kaiserpermanente--adobedrago.aem.page/[employer-name]/`

---

## Before you publish

Review the flagged items in the migration summary before going live:

- **Images** — all images point to the source CDN and will load immediately, but should be replaced with DA media URLs after uploading images to DA
- **Missing alt text** — any image that had no alt text in the source; auto-filled with empty `alt=""` and flagged for review
- **Unmigrated content** — forms, iframes, or embedded videos that could not be automatically migrated and need manual handling
- **No-match sections** — any section that didn't fit a known block and was output as default content

---

## One-time fork setup

Each secondary site is a fork of this repository with its own GitHub repo, DA, and `.page/.live` site. Before a forked site goes live, one code change is required:

In `blocks/footer/footer.js`, update `FOOTER_PATH` to load the shared footer from the template site:

```js
// Change this:
const FOOTER_PATH = '/fragments/nav/footer';

// To this:
const FOOTER_PATH = 'https://main--ak-kaiserpermanente--adobedrago.aem.page/fragments/nav/footer';
```

This is done once per fork — it is not part of the per-migration steps above.
