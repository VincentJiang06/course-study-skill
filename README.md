# course-study

> Turn course PDFs into comprehensive study notes — with worked examples, cross-lecture connections, and external sourcing. Built for exam season.

---

## What problem does this solve?

You have a stack of lecture PDFs. Your exam is in three days. You need study notes that actually help you understand, not just a pile of bullet points you copied from slides.

Standard summarizers give you a compressed version of what you already have. **This skill gives you something different:**

- Every concept defined, explained with intuition, and grounded with a worked example
- Connections between lectures that the slides never made explicit
- Gaps in your course flagged against standard curricula (so you know what the slides skipped)
- External sourcing from industry docs and academic papers, not just the textbook
- Notes you can export as clean Markdown or PDF

---

## Who is this for?

Any university or college student preparing for exams, writing summaries, or trying to deeply understand a course — **in any subject:**

- STEM (math, physics, chemistry, biology, engineering, computer science)
- Social sciences (economics, psychology, political science)
- Humanities (history, philosophy, literature)
- Professional programs (law, medicine, business)

The only requirement: course materials in PDF format (or a topic list, or just a course name).

---

## How it works

The skill runs in four phases. You stay in control at every step.

```
Phase 1 — Extract
  Every page of every PDF is processed via the /pdf skill. Nothing is skipped or merged.
  Output: lecture-by-lecture extraction with all concepts, formulas, and diagrams.

Phase 2 — Synthesize
  Concepts are connected across lectures. Dependencies mapped. Gaps identified
  against standard curricula for your subject (via live search).
  Output: a full knowledge architecture of the course.

Phase 3 — Expand  [optional, Complete mode only]
  Key concepts traced to real-world implementations, original papers, and
  industry documentation. Every external claim is sourced.
  Output: annotated expansion of concepts worth knowing beyond the slides.

Phase 4 — Study
  Everything integrated into final study notes: structured by lecture, enriched
  with examples and connections, ready for Markdown or PDF export.
  Output: study-notes.md
```

After each phase, the skill gives a one-line status and asks if you want to adjust or continue.

---

## Supported input

| Input | How to provide |
|---|---|
| **PDF** (slide export, scanned, standalone) | Upload directly — primary format |
| PowerPoint / PPTX, Word / DOCX, images | Convert to PDF first using `/pdf` skill, then upload |
| Topic / concept list | Paste in chat — skips Phase 1, goes straight to Phase 2 |
| Just a course name | Type it — skill searches for a standard syllabus and builds from there |

> All PDF reading is handled by the `/pdf` skill. No Python file I/O is used.

---

## Output

All study notes are written in format-agnostic Markdown:

- **Renders** in any Markdown viewer (Obsidian, Notion, VS Code, GitHub)
- **Exports** to PDF via the `/pdf` skill — with full font support for Chinese, Japanese, Korean, and other non-Latin scripts
- **Readable** as plain text even with all formatting stripped

Each concept block includes:

```
Definition       — exact wording from the source, then clarified
Intuition        — why this concept exists, what problem it solves
Formal treatment — formula or algorithm in LaTeX or code
Worked example   — step-by-step, concrete numbers or cases
Real-world use   — industry implementations or research context
Connections      — what this requires, and what it enables
Misconceptions   — what students commonly get wrong
```

---

## Scale handling

The skill estimates total page count upfront and picks a processing strategy automatically:

| Course size | Strategy |
|---|---|
| ≤ 60 pages | Full extraction, no compression |
| 61–200 pages | Batch by lecture |
| 201–400 pages | Batch + compress intermediate output |
| > 400 pages | Recommend splitting by module |

Large courses are processed in batches — nothing is silently skipped.

---

## Depth modes

**Complete** *(default)* — All four phases. Best for learning something new or preparing a thorough review.

**Focused** — Phases 1, 2, and 4 only. Skips external expansion. Faster; best when you know the field and need notes quickly.

Both modes produce full-quality notes with worked examples. Neither is a shortcut that produces worse output.

---

## Phase 3 and web access

Phase 3 requires network access (WebSearch + WebFetch).

- **With web access:** searches industry documentation, engineering blogs, GitHub implementations, and academic papers. Every claim is sourced.
- **Without web access:** expansion uses stable domain knowledge. All claims are marked `[Standard curriculum knowledge]`. No hallucinated sources.

The skill detects network access at intake and tells you which mode applies.

---

## Changelog

### v1.1.0
- **PDF-only input:** all course file reading now routes through the `/pdf` skill; direct Python/file I/O banned
- **Faster intake:** Phase 0 compressed to a single exchange — no more multi-step question forms
- **Faster checkpoints:** post-phase check simplified to a one-line prompt instead of a three-question form
- **Smarter batching:** Phase 2 explicitly batches large courses to avoid context overflow
- **Faster Phase 4 verification:** completeness check is now a spot-check pass, not a full re-read

### v1.0.0
- Initial release: four-phase Extract → Synthesize → Expand → Study workflow
- Dual-mode Phase 3 (web-enabled / curriculum-grounded)
- Scale-aware compression strategy
- CJK font support for bilingual PDF export
- Live curriculum search for any academic subject

---

## File structure

```
course-study/
├── SKILL.md                  # Entry point, intake flow, global rules
├── README.md                 # This file
└── rules/
    ├── phase-extract.md      # Phase 1: PDF extraction via /pdf skill
    ├── phase-synthesize.md   # Phase 2: cross-lecture synthesis and gap analysis
    ├── phase-expand.md       # Phase 3: external knowledge expansion
    ├── phase-study.md        # Phase 4: final study notes
    ├── templates.md          # Markdown/PDF formatting rules + CJK font configuration
    └── subject-coverage.md   # Live search strategy for any subject's standard curriculum
```

---

## Example session

```
User: I have 6 lecture PDFs for my Organic Chemistry course. Finals in 4 days.

Skill: Got it — 6 PDFs, ~180 pages. Batching by lecture. Web access ✓.
  Mode: Complete or Focused?  Output folder?

User: Complete. Save to ./orgo-notes/

Skill: Starting Phase 1...
  [reads each PDF via /pdf skill, extracts page by page]

  ✓ Phase 1 done — 6 lectures, 180 pages, 94 concepts extracted.
  Issues? Or say "continue".

User: Continue.

Skill: ✓ Phase 2 done — 5 modules mapped, 3 gaps flagged
  (stereochemistry and reaction mechanisms lighter than standard orgo curricula).
  Continue to Phase 3?

User: Yes.

[Phase 3 and 4 follow...]

Skill: ✓ study-notes.md complete — 24 core concepts, all with worked examples.
```
