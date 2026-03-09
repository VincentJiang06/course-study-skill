---
name: course-study
description: Comprehensive course study, exam revision, and structured study note generation from lecture slides, course PDFs, or topic outlines. Use when the user wants to study a course, review or summarize lecture slides/PDFs, generate lecture notes or a study guide, prepare for exams (midterm, final, quiz), create revision notes or formula sheets, extract key concepts/definitions/formulas from course materials, synthesize knowledge across multiple lectures, expand understanding beyond course scope with external sources, or asks for help learning, reviewing, or revising any university or college course content in any academic subject (CS, engineering, math, science, humanities, etc.). Produces deep, multi-format study notes (Markdown + PDF) with worked examples, LaTeX formulas, cross-lecture connections, and concept dependency maps — not shallow summaries.
---

# Course Study

A structured four-phase workflow for deep learning of any university or college course: Extract → Synthesize → Expand → Study. Produces high-fidelity, multi-format study notes with strict source alignment.

## Phase 0: Intake

Run all steps below before starting any phase.

### Step 1: Accept input materials

**Supported file formats:** PDF, PPT/PPTX, DOCX, plain text, images of slides. Upload files directly — Claude can read all these formats. If you have a format that requires conversion first, use the `/pdf` skill to convert before proceeding.

Ask the user:

> What course materials do you have?
> 1. **Course slides / PDFs** — Provide files. Proceed to Phase 1 (page-level extraction).
> 2. **A knowledge point list** — Paste or upload a structured topic list. Skip Phase 1; use the list as the backbone for Phase 2.
> 3. **Just a course name / topic area** — Agent searches for the standard curriculum of that subject (if web access is available), then generates a syllabus outline for the user to approve before proceeding to Phase 2.

### Step 2: Estimate content scale

**Before doing any work**, count the total volume:

- If PDF/slides: count total pages across all files.
- If topic list: count the number of distinct concepts/sections.
- If broad topic: estimate based on standard curriculum (8-15 lectures).

Apply this compression strategy upfront:

| Total pages / concepts | Strategy |
|---|---|
| ≤ 60 pages | Full extraction, no compression needed |
| 61–200 pages | Batch by lecture; summarize per lecture before synthesis |
| 201–400 pages | Batch by lecture; additionally compress Phase 1 output before Phase 2 (keep concept inventory, drop raw bullet repetition) |
| > 400 pages | Warn the user. Recommend splitting into course modules and running the skill per module. |

Tell the user the estimated scale and the strategy you'll use before proceeding.

### Step 3: Check network availability (for Phase 3)

Ask or detect: does this Claude Code session have WebSearch / WebFetch access?

- **Yes → Phase 3 runs at full depth** (web + academic sources).
- **No → Tell the user:** "Web access is unavailable. Phase 3 will be replaced with curriculum-grounded expansion using standard CS/engineering domain knowledge — no web sources will be invented. All claims will be explicitly marked `[Standard curriculum knowledge]`. This avoids hallucination but limits external depth."

If the user prefers to skip Phase 3 entirely in this case, that is fine — record the choice.

### Step 4: Set depth preference

Ask the user which mode:

> **Study depth:**
> 1. **Focused** — Phases 1, 2, 4. Skip Phase 3 expansion. Faster; still produces complete, example-rich notes. Good when you already know the field or time is short.
> 2. **Complete** *(default)* — All four phases. Adds external sourcing, real-world grounding, and academic references. Best for learning a new area deeply.

Neither mode is a "quick and dirty" shortcut — both produce full study notes. "Focused" just omits external expansion.

### Step 5: Confirm output location

Ask: "Where should I save the output files?" Default: current working directory. The workflow produces:

- `lecture-XX-extract.md` (one per lecture/file) — Phase 1
- `course-synthesis.md` — Phase 2
- `course-expansion.md` — Phase 3 (if running)
- `study-notes.md` — Phase 4

If any of these files already exist, ask: overwrite or resume from that phase?

### Step 6: Confirm and start

Summarize the plan:
- Input: [N files / topic list / broad topic]
- Total scale: [X pages]
- Compression strategy: [which tier]
- Phase 3: [full / curriculum-only / skipped]
- Mode: [Focused / Complete]
- Output dir: [path]

Ask for confirmation, then proceed phase by phase.

---

## Workflow

```
Phase 0: Intake
  ├── Has files → Phase 1 (Extract) → backbone = lecture pages
  ├── Has topic list → backbone = section outline → Phase 2
  └── Has broad topic → generate syllabus → backbone = syllabus → Phase 2

Phase 1: Extract (per file, page/section-aligned)
  └── Output: lecture-XX-extract.md (one per file)
  └── [Phase Checkpoint]

Phase 2: Synthesize (all extracts + world knowledge)
  └── Output: course-synthesis.md
  └── [Phase Checkpoint]

Phase 3: Expand (web + arxiv + industry, OR curriculum-grounded)
  └── Output: course-expansion.md
  └── [Phase Checkpoint]

Phase 4: Study (final structured notes, multi-format)
  └── Output: study-notes.md
  └── [Phase Checkpoint]
```

---

## Phase Checkpoint (after each phase)

After completing every phase, pause and ask the user these three questions before proceeding:

```
Phase [X] complete — [N] items processed.

Quick check before Phase [Y]:

1. Coverage — does the output cover everything you expected?
   a) Looks complete
   b) Minor gaps (which topics?)
   c) Significant gaps — redo this phase

2. Depth — is the level of detail right?
   a) Appropriate
   b) Too shallow — add more detail
   c) Too verbose — needs compression

3. Continue?
   a) Proceed to Phase [Y]
   b) Adjust first
   c) Stop here — this output is the deliverable
```

If the user selects (a) for all three, proceed immediately. Otherwise, address the feedback before moving on.

---

## Global Rules

1. **Backbone fidelity.** When the backbone is a PDF, every concept traces back to its page. When the backbone is a section outline (topic list or generated syllabus), every concept traces back to its section number. Never lose this traceability.

2. **Length guarantee.** Each extraction unit must have substantive content proportional to the source. A 40-page lecture cannot produce a 10-line summary.

3. **No fabrication.** In Phase 3 with no web access, every claim must be marked `[Standard curriculum knowledge]` or `[Phase 1/2 source: Lecture X]`. Do not invent paper titles, URLs, or implementation details.

4. **Multi-format output.** Final notes must render correctly in Markdown, convert cleanly to PDF, and read well as plain text. See [templates.md](templates.md).

5. **Examples are mandatory.** Phase 4 must include concrete, worked examples for every non-trivial concept.

6. **Track progress.** Use TodoList to track which lectures/sections have been processed through which phases.

7. **Intermediate output discipline.** Phase 1 and Phase 2 intermediate files are for traceability, not for reading. Keep them structured and complete, but do NOT pad them with repeated explanations. The value is in Phase 4.

---

## Reference files

- [rules/phase-extract.md](rules/phase-extract.md) — Phase 1
- [rules/phase-synthesize.md](rules/phase-synthesize.md) — Phase 2
- [rules/phase-expand.md](rules/phase-expand.md) — Phase 3
- [rules/phase-study.md](rules/phase-study.md) — Phase 4
- [rules/templates.md](rules/templates.md) — Output format and PDF/font rules
- [rules/subject-coverage.md](rules/subject-coverage.md) — Live search strategy for finding standard curriculum coverage for any subject (used in Phase 0 Mode 3 and Phase 2 gap analysis)
