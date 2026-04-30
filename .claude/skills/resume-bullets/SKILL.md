---
name: resume-bullets
description: >
  Write or rewrite resume bullets in this repo's style — outcome-first, one
  rendered line each, bold for impact terms, no fluff. Use whenever editing
  bullets in resume.yaml (experience or projects) or when the user asks to
  add, rewrite, tighten, or critique a resume bullet.
user-invokable: true
---

# Resume Bullets — House Style

This skill captures the rules for bullets in `resume.yaml`. Apply them every time you add or rewrite a bullet.

## The Five Rules

1. **Lead with what it does, not how it was built.** The reader is a recruiter or hiring manager skimming for value. They do not care that the matcher was hand-rolled. They care that the extension turns IndexedDB into a real database client. Save the implementation story for the project README or a blog post.

2. **One rendered line, hard limit.** Each bullet must fit on a single rendered line in the compiled PDF (roughly 105–120 characters of plain text once `**bold**` markup is stripped). If it wraps, cut words until it doesn't.

3. **Bold the impact terms.** Bold the surface (`**Chrome DevTools extension**`), the verbs of value (`**query, edit, and export**`), the named tech a recruiter scans for (`**MongoDB-style filters**`, `**TanStack Table**`), and the numbers (`**60%**`, `**~150 ms CPU inference**`, `**129 countries**`). Do not bold filler.

4. **Concrete numbers when they exist; never invent them.** Real metrics from this resume include `**60%** of L2 tickets`, `**$600** savings per 100 cases`, `**37%** provisioning reduction`, `**129 countries**`, `**9K+ impressions**`, `**5.5% CTR**`, `**~150 ms CPU inference**`. If a project has no number, skip the number — do not pad with vague claims.

5. **Two bullets per project max, three to six per role.** Projects get a one-line "what it is + where it lives" bullet and a one-line "what users do with it + signal of reach" bullet. Roles get one bullet per genuinely distinct contribution; merge or drop overlapping ones.

## The Pattern for Project Bullets

```
- Shipped a **<surface>** that <one-line value to user>.
- Lets <user> **<verbs>** with **<distinctive feature>** -- <signal: live on X / reached Y / solved Z>.
```

Worked example (IdxBeaver — kept after several rewrites):

```yaml
- Shipped a **Chrome DevTools extension** that turns Chrome's read-only IndexedDB
  inspector into a full **database client**.
- Lets developers **query, edit, and export** browser-stored data with **MongoDB-style
  filters** -- live on the **Chrome Web Store**.
```

What we rejected and why:

| Bullet | Why we cut it |
|---|---|
| "Hand-rolled a query matcher inlined into the inspected page's MAIN world to preserve IDBKeyRange index hints, paired with TanStack Table + virtualization for editing up to 5000 rows." | Two lines; reads like a commit message; centers on implementation a recruiter cannot evaluate. |
| "Built a Chrome DevTools extension with MongoDB-style queries, schema inference, and grid editing with undo/redo — published on the Chrome Web Store." | One line but a feature dump, not an outcome. "Turns Chrome's read-only inspector into a full database client" is the *change* this delivers; that framing wins. |

## The Pattern for Experience Bullets

```
- <Verb> a **<system / surface>** that <what it does for the business>, <mechanism in one clause>.
```

Worked examples already in the resume:

```yaml
- Shipped an **AI copilot Chrome extension** for Salesforce that reduces manual
  CRM data entry by auto-linking activities to deals, extracting field values
  from transcripts, and suggesting pipeline stage transitions.
- Built backend for **AI-driven CX system** with multiple LLM agents (RAG,
  diagnosis, evaluation, query handling), now resolving **60%** of L2 tickets
  automatically.
```

Notice: each names the system, says what it does for the business, and (when available) ends in a metric. None of them describe the framework, the language, or the file layout.

## What to Drop on Sight

- Bullets describing internal tooling that didn't ship to a customer or didn't move a metric — they dilute stronger lines next to them.
- Bullets bragging about Lighthouse 100, "best practices", "cutting-edge", "scalable" with no number behind it.
- Bullets that overlap another bullet on the same role; merge them.
- Bullets where the bold markup is on filler words (`**built**`, `**designed**`, `**delivered**`). Bold things a recruiter would search for, not verbs.

In this session we deliberately removed:
- "Delivered an image augmentation service leveraging Moore's Voting and BiRefNet…" — internal tool, name-drops without a business outcome.
- "Designed a self-serve internal tool for product team to generate SEO-optimized content…" — vague, no metric.
- "Achieved 100/100 Lighthouse across all 4 categories…" — sat beside a stronger bullet about reaching 129 countries with 5.5% CTR; the country/CTR signal is the one to keep.

## Workflow

1. Read the bullet (or the user's draft) and ask: **what does this thing do for whoever uses it?** Answer in one sentence. That's bullet 1.
2. Ask: **what's the strongest signal of reach, scale, or quality?** A live URL, a store listing, a percentage, a dollar number, a country count. That's bullet 2.
3. Strip every word that is not load-bearing.
4. Bold the surface, the user-facing verbs, the named tech a recruiter scans for, and the numbers.
5. Compile the PDF with `make compile` and verify each bullet renders on a single line. If any wraps, cut until it doesn't.

## Source of Truth

Bullets live in `resume.yaml`. The `.tex` files in `sections/` are generated by `scripts/generate_resume.py` — never edit them by hand. After changing yaml, run `make generate` (or `make compile`, which generates as a dependency) and re-check the PDF.
