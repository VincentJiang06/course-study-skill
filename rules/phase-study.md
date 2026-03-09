# Phase 4: Structured Deep Study Notes

## Goal

Produce the **final, comprehensive study notes** integrating all prior phases into a single authoritative document. This is the deliverable the student will actually use.

## What this phase is — and isn't

Phase 4 is a creative synthesis, not a rewrite of Phase 1. It:
- Follows the **backbone structure** (lecture/section order from Phase 1) as the skeleton
- Weaves in **cross-lecture connections** from Phase 2 at the right moments
- Integrates **external knowledge** from Phase 3 where it deepens understanding
- Adds **concrete worked examples** for every non-trivial concept
- Maintains **concise, precise technical writing** — not verbose, not skeletal

The backbone from Phase 1 is the spine. Phases 2 and 3 are the flesh.

## Procedure

### Step 1: Build the document skeleton

Follow the backbone structure strictly. Every backbone unit (lecture page group or section) becomes a heading. A reader can hold the original slides / topic list in one hand and the study notes in the other and see a 1:1 correspondence.

```markdown
# [Course Name] — Study Notes

## About these notes
[What these notes cover, how they're structured, what sources they draw from]

## Lecture 1 / Module 1: [Title]
### 1.1 [Topic] ([source location])
...
### 1.2 [Topic] ([source location])
...
```

Source location format — use whichever applies:
- PDF input: `(Lecture 1, pp. 3-7)`
- Topic list input: `(Section 1.2)`

### Step 2: Write each concept block

Calibrate depth to concept importance:

```markdown
### [Concept Name] ([source location])

**What it is:** [1-3 sentence definition. Instructor's phrasing first, then clarification.]

**Intuition:** [Why does this exist? What problem does it solve? Use analogies for complex ideas.]

**Formal treatment:**
[Formula / algorithm in LaTeX or code block. Explain each symbol/variable.]

**Example:**
[Concrete, worked example. For algorithms: step-by-step trace. For formulas: plug in numbers.]

**Real-world application:** [From Phase 3. How used in industry? Specific tools, cases.]

**Connections:** [From Phase 2. Prerequisites + what this concept enables.]

**Common misconceptions:** [What do students typically get wrong?]

**References:** [source location + Phase 3 source if used]
```

| Concept weight | Required sections |
|---|---|
| Core / exam-critical | All seven |
| Important supporting | What + Formal + Example + Connections |
| Minor / context | What + brief note |

### Step 3: Insert cross-lecture bridges

At every lecture/module boundary, insert a bridge:

```markdown
---
> **Bridge:** Lecture 3 introduced the problem of [X]. Lecture 4 now presents [Y] as a solution. The key shift is from [understanding the problem] to [designing a mechanism]. Note that [Y] assumes [Z] from Lecture 2 ([source location]).
---
```

Bridges transform a set of notes into a coherent learning narrative.

### Step 4: Verify completeness

**Per-lecture:** Does every concept from Phase 1's concept lists appear in the study notes? Cross-reference.

**Examples:** Every "Core" concept has at least one worked example. No `[TODO]` placeholders.

**Phase 3 integration:** Every expansion entry from `course-expansion.md` appears at the relevant concept block.

**Source traceability:** Every concept has a source location. Every external claim has a Phase 3 source.

### Step 5: Format output

Write in format-agnostic Markdown. See [templates.md](templates.md) (in the same `rules/` folder). Generate `study-notes.md` as primary output. If user requested PDF, apply the pdf skill.

## Writing style

**Concise but complete.** Every sentence earns its place. Cut filler, keep substance.

**Active voice.** "The scheduler assigns processes" not "Processes are assigned."

**Technical precision.** Correct terminology. Define on first use.

**Progressive disclosure.** Within each concept: intuition first (accessible) → formal (precise) → example (concrete) → connections (advanced). A reader can stop at any level and still learn something.

**Code and formulas are first-class.** Format correctly, comment where non-obvious, never truncate.

## Anti-patterns

- **DO NOT** produce study notes shorter than Phase 1 extractions. Phase 4 is longer because it adds examples, connections, and explanations.
- **DO NOT** skip examples. "Definition without example" is the single most common failure mode.
- **DO NOT** break the backbone order. Forward/backward links are fine; the primary structure must follow it.
- **DO NOT** omit Phase 3 expansion content if Phase 3 was run.
- **DO NOT** write walls of text — use headings, code blocks, and formula blocks for visual rhythm.
- **DO NOT** produce content that only works in Markdown — follow templates.md format rules throughout.
