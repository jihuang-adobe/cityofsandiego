# Skill: Generate DA HTML

**Version:** 1.0.0
**Invoked by:** `migrate-secondary-site`

---

## Purpose

Using the confirmed mapping plan and content manifest, generate one DA-compatible
HTML file per page. Each file is structured exactly as DA expects — ready for upload.

---

## When to Use

- Fourth step of every secondary site migration
- After `skills/03-map-to-blocks` has produced a confirmed mapping plan

## When NOT to Use

- Before the mapping plan is confirmed
- Modifying block CSS or JS code

---

## Before Starting

Re-read `PROJECT.md` → **DA HTML Output Format** section.
It contains the exact structural rules and code examples for every block type.

---

## Workflow

### Step 4a — Build Each Section

For each section in the mapping plan, generate the HTML using the rules below.

---

#### Default Content Sections

Plain headings, paragraphs, and links. No wrapping block div needed.

```html
<div>
  <h2>Section heading</h2>
  <p>Body paragraph text here.</p>
  <p><a href="/link">Link text</a></p>
</div>
```

For a `footnotes` styled section:
```html
<div class="footnotes">
  <p><sup>1</sup> Footnote text exactly as written.</p>
  <p><sup>2</sup> Second footnote text.</p>
</div>
```

---

#### Hero — Landing (homepage)

```html
<div class="full-width">
  <div class="hero landing">
    <div>
      <div>
        <picture>
          <source type="image/webp" srcset="[image-url]?format=webply&optimize=medium" media="(min-width: 600px)">
          <source type="image/webp" srcset="[image-url]?format=webply&optimize=medium">
          <img loading="lazy" alt="[alt text]" src="[image-url]">
        </picture>
      </div>
      <div>
        <h1>[Employer-specific headline]</h1>
        <p>[Body text]</p>
        <p><strong><a href="[CTA href]">[CTA text]</a></strong></p>
      </div>
    </div>
  </div>
</div>
```

#### Hero — Default (inner pages)

```html
<div>
  <div class="hero">
    <div>
      <div>
        <picture>
          <source type="image/webp" srcset="[image-url]?format=webply&optimize=medium" media="(min-width: 600px)">
          <source type="image/webp" srcset="[image-url]?format=webply&optimize=medium">
          <img loading="lazy" alt="[alt text]" src="[image-url]">
        </picture>
      </div>
      <div>
        <h2>[Page heading]</h2>
        <p>[Body text]</p>
      </div>
    </div>
  </div>
</div>
```

---

#### Tabs

```html
<div>
  <div class="tabs">
    <div>
      <div>[Tab 1 label]</div>
      <div>
        <h3>[Tab 1 heading]</h3>
        <p>[Tab 1 body]</p>
        <p><a href="[href]">[CTA text]</a></p>
        <picture>
          <source type="image/webp" srcset="[image-url]">
          <img loading="lazy" alt="[alt]" src="[image-url]">
        </picture>
      </div>
    </div>
    <div>
      <div>[Tab 2 label]</div>
      <div>
        <h3>[Tab 2 heading]</h3>
        <p>[Tab 2 body]</p>
      </div>
    </div>
    <!-- repeat for each tab -->
  </div>
</div>
```

---

#### Columns (default)

```html
<div>
  <div class="columns">
    <div>
      <div>
        <h3>[Left heading]</h3>
        <p>[Left body]</p>
      </div>
      <div>
        <h3>[Right heading]</h3>
        <p>[Right body]</p>
      </div>
    </div>
  </div>
</div>
```

For `pale-blue` section style:
```html
<div class="pale-blue">
  <div class="columns">
    ...
  </div>
</div>
```

For `align-vertically` variant:
```html
<div class="columns align-vertically">
```

---

#### Columns Media

```html
<div>
  <div class="columns-media">
    <div>
      <div><a href="[video-url]">[video-url]</a></div>
      <div>
        <h2>[Heading]</h2>
        <p>[Body text]</p>
      </div>
    </div>
  </div>
</div>
```

---

#### Cards Icon

```html
<div>
  <div class="cards-icon">
    <div>
      <div>
        <picture>
          <source type="image/webp" srcset="[icon-url]">
          <img loading="lazy" alt="[alt]" src="[icon-url]">
        </picture>
      </div>
      <div>
        <p><strong>[Label]</strong></p>
        <p><a href="[href]">[CTA text]</a></p>
      </div>
    </div>
    <!-- repeat for each card -->
  </div>
</div>
```

---

#### Card (author 3 in one section for a card row)

```html
<div>
  <div class="card">
    <div>
      <picture>
        <source type="image/webp" srcset="[image-url]">
        <img loading="lazy" alt="[alt]" src="[image-url]">
      </picture>
    </div>
    <div>
      <h3>[Card heading]</h3>
      <p>[Card body]</p>
    </div>
    <div>
      <p><a href="[href]">[CTA text]</a></p>
    </div>
  </div>
  <div class="card">
    <!-- second card -->
  </div>
  <div class="card">
    <!-- third card -->
  </div>
</div>
```

---

#### Accordion

```html
<div>
  <div class="accordion">
    <div>
      <div><p>[Question / label]</p></div>
      <div><p>[Answer / body content]</p></div>
    </div>
    <div>
      <div><p>[Question 2]</p></div>
      <div><p>[Answer 2]</p></div>
    </div>
    <!-- repeat for each item -->
  </div>
</div>
```

---

#### Icons (grid)

```html
<div>
  <div class="icons grid">
    <div>
      <div>
        <picture>
          <source type="image/webp" srcset="[icon-url]">
          <img loading="lazy" alt="[alt]" src="[icon-url]">
        </picture>
      </div>
      <div><p>[Body text]</p></div>
    </div>
    <!-- repeat for each item -->
  </div>
</div>
```

#### Icons (list)

```html
<div>
  <div class="icons list">
    <div>
      <div>
        <picture>
          <source type="image/webp" srcset="[icon-url]">
          <img loading="lazy" alt="[alt]" src="[icon-url]">
        </picture>
      </div>
      <div>
        <p><strong>[Item heading]</strong></p>
        <p>[Body text]</p>
      </div>
    </div>
  </div>
</div>
```

---

#### Plan Compare

```html
<div class="pale-blue">
  <div class="plan-compare">
    <div>
      <div><p><strong>[Plan A Name]</strong></p></div>
      <div><p><strong>[Plan B Name]</strong></p></div>
      <div><p><strong>[Plan C Name]</strong></p></div>
    </div>
    <div>
      <div><p>[Feature label]</p></div>
      <div><p>[Plan A value]</p></div>
      <div><p>[Plan B value]</p></div>
      <div><p>[Plan C value]</p></div>
    </div>
    <!-- repeat rows for each feature -->
  </div>
</div>
```

---

#### Table (striped)

```html
<div>
  <div class="table striped">
    <div>
      <div><p>[Col 1 header]</p></div>
      <div><p>[Col 2 header]</p></div>
      <div><p>[Col 3 header]</p></div>
    </div>
    <div>
      <div><p>[Row 1 data]</p></div>
      <div><p>[Row 1 data]</p></div>
      <div><p>[Row 1 data]</p></div>
    </div>
    <!-- repeat for each data row -->
  </div>
</div>
```

#### Table (caption striped) — for Summary of Benefits

```html
<div class="table-grid">
  <div class="table caption striped">
    <div>
      <div><p>[Caption — spans full width]</p></div>
    </div>
    <div>
      <div><p>[Col header 1]</p></div>
      <div><p>[Col header 2]</p></div>
      <div><p>[Col header 3]</p></div>
      <div><p>[Col header 4]</p></div>
    </div>
    <div>
      <div><p>[Data]</p></div>
      <div><p>[Data]</p></div>
      <div><p>[Data]</p></div>
      <div><p>[Data]</p></div>
    </div>
  </div>
  <!-- additional table blocks side by side -->
</div>
```

---

### Step 4b — Assemble the Full Page

Wrap all sections in the page wrapper:

```html
<body>
  <header></header>
  <main>
    <!-- all section divs go here, top to bottom -->
  </main>
  <footer></footer>
</body>
```

---

### Step 4c — Validate Before Output

Before producing the final HTML file, verify:

- [ ] Section count matches the mapping plan
- [ ] Every heading, paragraph, link, and phone number from the content manifest is present
- [ ] Every image has a `<picture>` wrapper with `loading="lazy"`
- [ ] The last section is always `<div class="footnotes">` with legal text
- [ ] No `<html>` or `<head>` tags present
- [ ] No placeholder text — all content is real

---

## Output

One complete, validated HTML file per page.
Named after the page path (e.g. `index.html`, `plans.html`, `support.html`).
Passed to `skills/05-output-summary` for the migration report.

**IMPORT ALL CONTENT. Partial migration is unacceptable.**
