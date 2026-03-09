# Phase 1: Backbone Extraction

## Goal

Extract every concept, definition, formula, algorithm, code snippet, and diagram from the course materials, **strictly aligned to the backbone structure** (page numbers for PDFs/slides; section numbers for topic lists or generated syllabi). Zero information loss is the target.

## Backbone types

The backbone format depends on what the user provided (set in Phase 0):

| Input type | Backbone unit | Reference format |
|---|---|---|
| PDF / slide file | Page number | `Lecture X, p. Y` |
| Topic list (pasted/uploaded) | Section item | `Section X.Y` |
| Generated syllabus | Syllabus entry | `Module X, Section Y` |

All subsequent phases (Synthesis, Expansion, Study) use this same reference format. Do not mix formats within a course.

## For PDF/slide inputs

### Step 1: Read the full file first

Scan the entire file to understand scope. Note total page count — you need it for the length check.

### Step 2: Page-by-page extraction

For EVERY page, output one block:

```markdown
### Page X (of N) — [Slide title]

**Key content:**
[Extract ALL substantive content. Include:]
- Definitions (exact wording from the slide)
- Formulas ($LaTeX$ notation)
- Algorithms (pseudocode or code block)
- Diagrams (describe structure, label all named elements)
- Lists and bullet points (preserve hierarchy)
- Examples (reproduce in full)
- Emphasized or warning text

**Concepts introduced:** [comma-separated list]

**[EXPAND]:** [optional — if a concept needs external investigation, note it here with reason]
```

Title pages and transition slides still get a block:
```markdown
### Page 1 (of 30) — Course Title
**Key content:** [Title page — no substantive content]
**Concepts introduced:** —
```

### Step 3: Special content handling

**Formulas:** Always LaTeX. For complex formulas, explain each symbol below the formula.

**Code:** Reproduce in full with language annotation. Never paraphrase code.

**Diagrams:** Name every labeled element. For graphs, describe axes, scale, trends.

**Tables:** Reproduce as Markdown tables. No dropped columns or rows.

### Step 4: Verify completeness

```
Total pages in file: N
Total "### Page X" blocks: must equal N
```

For content-rich pages (not title/transition), each block should have ≥ 5 lines of substantive content. If shorter, re-read the page.

### Step 5: Lecture summary block

```markdown
## Lecture Summary

**Topic:** [main topic]
**Total pages:** N
**Key concepts (ordered by appearance):** [numbered list]
**Prerequisites assumed:** [concepts from earlier lectures]
**[EXPAND] markers:** [list with page refs]
**Open questions:** [anything unclear or contradictory]
```

---

## For topic list inputs

When the user provides a structured topic list (not a PDF), generate a backbone outline first:

### Step 1: Parse the topic list

Group items into a hierarchy:
- Top level → Lecture/Module
- Second level → Section
- Third level → Sub-concept

Assign section numbers: `1.1`, `1.2`, `2.1`, etc.

### Step 2: Write a backbone outline file

Output `course-backbone.md`:

```markdown
# Course Backbone: [Course Name]

## Module 1: [Theme]
### 1.1 [Topic]
### 1.2 [Topic]

## Module 2: [Theme]
...
```

Present this to the user and ask: "Does this structure look right?" Adjust before proceeding.

### Step 3: Populate each section

For each section node in the backbone, write a concept block using your world knowledge of the subject area:

```markdown
### Section 1.1 — [Topic Name]

**Definition:** [precise definition]
**Core content:** [key ideas, properties, distinctions]
**Formulas / algorithms:** [if applicable]
**[EXPAND]:** [if external sourcing would add value]
```

Mark all content generated this way with `[From: world knowledge — no source PDF]`.

---

## Output

One file per input: `lecture-XX-extract.md` (zero-padded). If the input was a topic list, also output `course-backbone.md`.

## Anti-patterns

- **DO NOT** merge multiple pages into one block.
- **DO NOT** skip pages you consider unimportant.
- **DO NOT** rephrase definitions in your own words without preserving the original first.
- **DO NOT** pad the extraction with repeated summaries or meta-commentary — the value is structured, dense content.
