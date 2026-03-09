# course-study

> Turn any lecture slides, course PDFs, or topic list into comprehensive study notes — with worked examples, cross-lecture connections, and external sourcing. Built for exam season.

---

## What problem does this solve?

You have a stack of lecture slides. Your exam is in three days. You need study notes that actually help you understand, not just a pile of bullet points you copied from slides.

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

The only requirement: you have some course materials to work from (slides, PDFs, notes, or even just a course name).

---

## How it works

The skill runs in four phases. You stay in control at every step.

```
Phase 1 — Extract
  Every page of every slide is processed. Nothing is skipped or merged.
  Output: lecture-by-lecture extraction with all concepts, formulas, and diagrams.

Phase 2 — Synthesize
  Concepts are connected across lectures. Dependencies mapped. Gaps identified
  against standard curricula for your subject (via live search).
  Output: a full knowledge architecture of the course.

Phase 3 — Expand  [optional]
  Key concepts are traced to real-world implementations, original papers, and
  industry documentation. Every external claim is sourced.
  Output: annotated expansion of concepts worth knowing beyond the slides.

Phase 4 — Study
  Everything integrated into final study notes: structured by lecture, enriched
  with examples and connections, ready for Markdown or PDF export.
  Output: study-notes.md
```

After each phase, the skill pauses and asks: does this look right? You can adjust, stop, or continue.

---

## Supported input formats

Upload your materials directly — no conversion needed in most cases:

| Format | Notes |
|---|---|
| PDF (slide export, scanned, standalone) | Fully supported |
| PowerPoint / PPTX | Fully supported |
| Word / DOCX | Fully supported |
| Images of slides (PNG, JPG) | Fully supported |
| Plain text or Markdown notes | Fully supported |
| Topic / concept list (pasted in chat) | Skips to Phase 2 |
| Just a course name | Skill searches for a standard syllabus and builds from there |

> Need to convert a file first? Use the `/pdf` skill.

---

## Output

All study notes are written in format-agnostic Markdown:

- **Renders** in any Markdown viewer (Obsidian, Notion, VS Code, GitHub)
- **Exports** to PDF via pandoc or the `/pdf` skill — with full font support for Chinese, Japanese, Korean, and other non-Latin scripts
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

## Scale and context management

Before starting, the skill estimates your total content volume and picks a strategy:

| Course size | Strategy |
|---|---|
| ≤ 60 pages | Full extraction, no compression |
| 61–200 pages | Batch by lecture |
| 201–400 pages | Batch + compress intermediate output |
| > 400 pages | Recommend splitting by module |

Large courses are handled in batches — the skill will never silently truncate or skip material.

---

## Depth modes

**Complete** *(default)* — All four phases. Best for learning something new or preparing a thorough review.

**Focused** — Phases 1, 2, and 4 only. Skips external expansion. Useful when you know the field and need notes fast.

Both modes produce full-quality notes with worked examples. Neither is a shortcut that produces worse output.

---

## Phase 3 and web access

Phase 3 requires network access (WebSearch + WebFetch).

- **With web access:** searches industry documentation, engineering blogs, GitHub implementations, and academic papers. Every claim is sourced.
- **Without web access:** expansion uses stable domain knowledge instead. All claims are marked `[Standard curriculum knowledge]`. No hallucinated sources.

The skill detects network access at the start and tells you which mode it will use.

---

## File structure

```
course-study/
├── SKILL.md                  # Entry point, intake flow, global rules
├── README.md                 # This file
└── rules/
    ├── phase-extract.md      # Phase 1: page-level extraction
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

Skill: [Phase 0]
  Input: 6 PDFs — estimated 180 pages total
  Strategy: batch by lecture, per-lecture summaries before synthesis
  Web access: available — Phase 3 will run at full depth
  Mode: Complete
  Output: ./orgo-notes/
  Confirm?

User: Yes, let's go.

Skill: [Phase 1] Extracting lecture-01-extract.md...
  ...6 lectures processed.

  Phase 1 complete.
  1. Coverage: looks complete / gaps / significant gaps?
  2. Depth: appropriate / too shallow / too verbose?
  3. Continue to Phase 2?

User: Looks good. Continue.

Skill: [Phase 2] Building course-synthesis.md...
  ...cross-lecture connections mapped, gaps identified.

  Key gaps found: stereochemistry and reaction mechanisms in Phase 1
  are lightly covered compared to standard orgo curricula.
  Flagged for Phase 3 expansion.

[Continues through Phase 3 and Phase 4...]

Skill: study-notes.md complete — 87 pages, 24 concepts with full worked examples.
```
