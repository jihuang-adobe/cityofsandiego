# Skill: Output Summary

**Version:** 1.0.0
**Invoked by:** `migrate-secondary-site`

---

## Purpose

After all HTML files are generated, produce a structured migration summary report.
Gives the business owner and team a clear picture of what was migrated, what blocks
were used, and what — if anything — needs manual review before DA upload.

---

## When to Use

- Final step of every secondary site migration
- After `skills/04-generate-da-html` has produced all HTML files

---

## Workflow

### Step 5a — Compile Migration Stats

From the generated HTML files, count:
- Total pages migrated
- Total sections across all pages
- Each block type and how many times it was used

---

### Step 5b — Flag Items for Review

Identify any sections or content that may need human review:
- **All external image URLs** — every image in the generated HTML still points to the source CDN (`choose.kaiserpermanente.org/content/dam/...`). These work immediately but should be replaced with DA media URLs (`./media_[hash].[ext]`) after the business owner uploads images to DA
- Images that could not be fetched or had missing alt text
- Sections that used default content but may benefit from a block
- Content patterns that didn't cleanly match a block mapping rule
- Employer-specific content that may need brand/legal approval
- Phone numbers, plan codes, or enrollment URLs that should be verified

---

### Step 5c — Produce the Report

Output the complete migration summary in this format:

```
# Migration Summary — [Employer Name]
Source: [source URL]
Date: [today's date]

---

## Files Generated

| # | File | Destination (DA path) | Description |
|---|------|-----------------------|-------------|
| — | nav.html | /fragments/nav/header | Site navigation |
| 1 | index.html | /[employer-name]/index | Home page |
| 2 | plans.html | /[employer-name]/plans | Plans & Benefits |
| 3 | getting-care.html | /[employer-name]/getting-care | Getting Care |
| ... | | | |

---

## Pages Migrated

| # | Page | HTML File | Sections | Blocks Used |
|---|------|-----------|----------|-------------|
| 1 | Home | index.html | 11 | hero landing, columns, columns-media, tabs, cards-icon, card ×3 |
| 2 | Plans | plans.html | 9 | hero landing, plan-compare, table ×3, accordion, table ×6 |
| 3 | Getting Care | getting-care.html | 4 | hero landing, card ×3 |
| ... | | | | |

Total pages: [N]
Total sections: [N]

---

## Block Usage Summary

| Block | Variant | Times Used |
|-------|---------|------------|
| hero | landing | [N] |
| hero | default | [N] |
| tabs | — | [N] |
| columns | default | [N] |
| columns | align-vertically | [N] |
| columns-media | — | [N] |
| cards-icon | — | [N] |
| card | default | [N] |
| accordion | — | [N] |
| icons | grid | [N] |
| plan-compare | — | [N] |
| table | striped | [N] |
| table | caption striped | [N] |

---

## Items Requiring Review

- [ ] [Description of item needing attention — page, section, reason]
- [ ] [Any image that couldn't be fetched]
- [ ] [Any content that was ambiguous]

---

## Next Steps — Uploading to DA

1. Go to: https://da.live/#/adobedrago/ak-kaiserpermanente/
2. Upload the nav file first — it lives outside the employer folder:
   - `nav.html` → `/fragments/nav/header`
3. Create a new folder for this employer: `/[employer-name]/`
4. Upload each page HTML file to its corresponding path:
   - `index.html` → `/[employer-name]/index`
   - `plans.html` → `/[employer-name]/plans`
   - `getting-care.html` → `/[employer-name]/getting-care`
   - *(and so on for each page)*
5. Preview each page at:
   `https://main--ak-kaiserpermanente--adobedrago.aem.page/[employer-name]/`
6. Review the items flagged above before publishing
```

---

## Output

The complete migration summary report.
This is the final deliverable of the migration skill pipeline.
