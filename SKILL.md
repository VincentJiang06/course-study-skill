---
name: course-study
version: 1.1.0
description: Comprehensive course study, exam revision, and structured study note generation from lecture slides, course PDFs, or topic outlines. Use when the user wants to study a course, review or summarize lecture slides/PDFs, generate lecture notes or a study guide, prepare for exams (midterm, final, quiz), create revision notes or formula sheets, extract key concepts/definitions/formulas from course materials, synthesize knowledge across multiple lectures, expand understanding beyond course scope with external sources, or asks for help learning, reviewing, or revising any university or college course content in any academic subject (CS, engineering, math, science, humanities, etc.). Produces deep, multi-format study notes (Markdown + PDF) with worked examples, LaTeX formulas, cross-lecture connections, and concept dependency maps — not shallow summaries.
---

# Course Study

A structured four-phase workflow for deep learning of any university or college course: Extract → Synthesize → Expand → Study. Produces high-fidelity, multi-format study notes with strict source alignment.

## Phase 0: Intake

Run all steps below before starting any phase. **Keep this fast** — intake should take one exchange, not five.

### Step 1: Accept input materials

**Supported input: PDF only.** All course materials must be in PDF format.
- If the user has PPT/PPTX, DOCX, or images: use the `/pdf` skill to convert first, then return here.
- Do NOT attempt to read non-PDF files directly.

Ask the user in a single message:

> What do you have?
> 1. **PDF files** — upload them and we start Phase 1.
> 2. **A topic/concept list** — paste it and we skip to Phase 2.
> 3. **Just a course name** — tell me and I'll search for a standard syllabus first.
>
> Also: how many pages total (rough estimate is fine)? Preferred output language?

### Step 2: Estimate scale and pick compression tier

Count total pages from the user's answer. Apply immediately — do not ask again:

| Total pages | Tier | Strategy |
|---|---|---|
| ≤ 60 | Light | Full extraction per page |
| 61–200 | Medium | Batch by lecture; summarize per lecture |
| 201–400 | Heavy | Batch + compress Phase 1 before Phase 2 |
| > 400 | Split | Warn user; recommend per-module runs |

### Step 3: Detect network and set mode

Detect WebSearch availability silently. Tell the user in one line:
- ✓ Web access available → Phase 3 will use live sources
- ✗ No web access → Phase 3 will use curriculum knowledge only (no hallucinated sources)

### Step 4: Ask depth + output dir in the same message

> **Mode:** Focused (Phases 1+2+4, faster) or Complete (all 4 phases, deeper)?
> **Output folder:** where to save files? (default: current directory)

### Step 5: Confirm and go

One-line summary, then start immediately on user confirmation. Do not ask further questions before Phase 1.

---

## Workflow

```
Phase 0: Intake (single exchange)
  ├── PDFs → Phase 1 (Extract via /pdf skill)
  ├── Topic list → Phase 2 directly
  └── Course name → quick syllabus search → Phase 2

Phase 1: Extract (per PDF, page-aligned, using /pdf skill)
  └── Output: lecture-XX-extract.md

Phase 2: Synthesize
  └── Output: course-synthesis.md

Phase 3: Expand (web sources OR curriculum-grounded)
  └── Output: course-expansion.md

Phase 4: Study (final notes)
  └── Output: study-notes.md
```

Each phase ends with a **brief checkpoint** (see below).

---

## Phase Checkpoint

After each phase, one compact message:

```
✓ Phase [X] done — [summary in one line].
Issues? (coverage gaps / too shallow / too verbose)
Type to adjust, or just say "continue".
```

If no response issues → proceed immediately. No multi-question forms.

---

## Global Rules

1. **PDF-only input.** Use the `/pdf` skill to read all course files. Do not use Python file I/O or direct file reading for PDFs.

2. **Backbone fidelity.** Every concept traces back to its source: page number (PDF) or section number (topic list). Never lose traceability.

3. **Speed discipline.** Minimize round-trips. Batch questions. Skip steps that aren't needed for the current tier. Phase 1 and 2 intermediate files should be dense and compact — no padding, no repeated meta-commentary.

4. **No fabrication.** Phase 3 without web access: every claim marked `[Standard curriculum knowledge]`. No invented URLs, paper titles, or authors.

5. **Examples are mandatory.** Phase 4 must include worked examples for every non-trivial concept.

6. **Track progress.** Use TodoList to track which lectures have been processed.

7. **Multi-format output.** Final notes render in Markdown, PDF, and plain text. See [rules/templates.md](rules/templates.md).

---

## Reference files

- [rules/phase-extract.md](rules/phase-extract.md) — Phase 1
- [rules/phase-synthesize.md](rules/phase-synthesize.md) — Phase 2
- [rules/phase-expand.md](rules/phase-expand.md) — Phase 3
- [rules/phase-study.md](rules/phase-study.md) — Phase 4
- [rules/templates.md](rules/templates.md) — Output format and PDF/font rules
- [rules/subject-coverage.md](rules/subject-coverage.md) — Live search strategy for curriculum gap analysis
