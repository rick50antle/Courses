# Continuation Brief

## CMU METALS Prework Redesign — Session of March 21, 2026 (Session 3)

**Paste this document at the start of a new chat to resume work.**

### Purpose of This Document

This brief captures the third working session on March 21, 2026, in which Rick Antle and Claude (Opus 4.6) undertook three major tasks: (1) renumbered the learning objectives from 1–18 (with a gap at the dropped Objective 3) to a clean 1–18 sequence; (2) began reworking objective titles from shorthand labels into proper learning objective statements via a one-by-one interview; and (3) combined two overlapping objectives (old 7 and 8), reducing the total from 18 to 17. The session also produced a Learning Objectives Memo as a Word document addressed to the CMU METALS Capstone Team.

### All Files Are In

**Accounting Pre-work/CMU METALS Prework Redesign/**

With the working site in the **site/** subfolder.

### Companion Documents to Read Before Resuming

1. **Continuation_Brief_March21_Session3.md** — This document. The most current session brief.
2. **Continuation_Brief_March21_Session2.md** — Previous session brief (content support assessment, full objective review).
3. **Terminology_and_Language_Conventions.md** — Active language constraints. Includes: accounting systems evolved, don't say "designed"; dividends are "declared and paid"; and all other conventions.
4. **prework-adopted-standards.md** (in parent folder: Accounting Pre-work/) — Standards adopted from the Accounting Origins project.
5. **Learning_Objectives.md** — **NOT YET UPDATED this session.** Still has the old 1–19 numbering and original titles. Needs to be rebuilt with 1–17 numbering and revised titles once the title interview is complete.
6. **Learning_Objectives_Matrix.xlsx** — **Partially updated this session.** Was renumbered to 1–18 and had terminology fixed ("Designed Artifact" → "Evolved Information System"). Needs further update to 1–17 with combined objectives and revised titles.
7. **Learning_Objectives_Memo.docx** — **Created this session.** Word memo from Rick Antle to CMU METALS Capstone Team, CC Stan Garstka and Pierre Liang. Presents the learning objectives for the first time. Currently has the 1–18 numbering and original titles. Needs to be rebuilt with 1–17 numbering, revised titles, and pagination fix (keepNext to prevent title/table page splits).
8. **site/** — No changes to site files this session.

---

## What Was Done This Session

### 1. Created the Learning Objectives Memo (Word Document)

Generated a Word memo using docx-js (`memo2.js`) addressed to the CMU METALS Capstone Team from Rick Antle, CC Stan Garstka and Pierre Liang. The memo is framed as Rick presenting the learning objectives for the first time — the METALS team has not seen any of Rick's work on objectives before. It includes an overview, assessment design patterns, all objectives by group with assessment designs and content support indicators, a content gaps table, and notes for assessment design.

### 2. Renumbered Objectives 1–18

Removed the gap left by the dropped Objective 3. The matrix and memo were rebuilt with clean sequential numbering 1–18 (before the later combining step reduced this to 17).

### 3. Fixed Terminology in Matrix

Changed "The System as a Designed Artifact" to "The System as an Evolved Information System" in the Learning Objectives Matrix to comply with the Terminology and Language Conventions.

### 4. Reworked Objective Titles — One-by-One Interview (Partially Complete)

Rick observed that shorthand labels like "Two conventions, neither wrong" are not learning objectives. We began a one-by-one interview to rework each title into a statement of what the student will be able to do. Rick's key feedback pattern: titles should state the broader capability the student carries forward, not describe the specific assessment example.

During this process, old Objectives 7 and 8 were found to overlap after restatement, and Rick directed combining them — reducing the total from 18 to 17.

**The interview is partially complete.** Titles 1–10 are finalized. Titles 11–17 remain to be reviewed.

### 5. Combined Old Objectives 7 and 8

Old Objective 7 ("Appreciate the usefulness of imposing an identity when we start telling the financial story") and old Objective 8 ("Whether spending creates an asset or an expense") overlapped in substance. Rick directed combining them into a single objective.

---

## Revised Objective Titles (Current State)

Titles 1–10 are finalized. Titles 11–17 still carry their original shorthand labels and need to be reviewed.

| # | Revised Title | Status |
|---|--------------|--------|
| 1 | Appreciate that different conventions arise in response to different problems and that none should be judged as inherently right or wrong. | **Final** |
| 2 | Show that the identity holds under different conventions and distinguish architecture from instance. | **Final** (unchanged) |
| 3 | Understand the importance of the entity boundary decision and recognize that boundaries are drawn differently for different purposes. | **Final** |
| 4 | Appreciate what factors influence whether economic information is recognized by the system. | **Final** |
| 5 | Appreciate how different conventions serve different purposes and involve different tradeoffs. | **Final** |
| 6 | Recognize the factors that influence accounting treatment. | **Final** |
| 7 | Appreciate the usefulness of imposing an identity, and recognize that it requires classification decisions — such as whether spending creates an asset or an expense. | **Final** (COMBINED from old 7+8) |
| 8 | Appreciate why decomposing a total that is already determined by subtraction can still add information. | **Final** (formerly Obj 9) |
| 9 | Explain why the architecture applies to any entity and how the residual decomposition changes. | **Final** (formerly Obj 10, kept as-is) |
| 10 | Trace a transaction through the identity and verify balance. | **Final** (formerly Obj 11, kept as-is) |
| 11 | Distinguish stocks from flows and locate each in the identity. | **Needs review** (formerly Obj 12) |
| 12 | What each flow statement decomposes, and the nesting relationship. | **Needs review** (formerly Obj 13) |
| 13 | Why cash gets its own statement. | **Needs review** (formerly Obj 14) |
| 14 | NI vs. CFO gap: trace it. | **Needs review** (formerly Obj 15) |
| 15 | NI vs. CFO gap: interpret it. | **Needs review** (formerly Obj 16) |
| 16 | Convention spectrum (lightened). | **Needs review** (formerly Obj 17) |
| 17 | Read statements together, drilling down from retained earnings. | **Needs review** (formerly Obj 18) |

---

## Key Decisions Made This Session

1. **Memo framed as first presentation.** The METALS team has not seen any of Rick's work on learning objectives. The memo introduces them for the first time, written in first person from Rick.

2. **Objective titles must be proper learning objectives.** Not just shorthand labels but statements of what the student will be able to do — the broader capability, not the specific assessment example.

3. **Old Objectives 7 and 8 combined** because they overlapped after restatement. Both concerned imposing the identity and the classification decisions it requires.

4. **Rabbit hole about factors influencing accounting treatment** — Rick requested a note to include content about what factors influence accounting treatment. One factor is information most useful for a given purpose; another is "production cost" (e.g., verification). Full set of factors still needs brainstorming.

5. **Pagination fix needed in memo.** Rick requested that objective titles not appear on a different page than their tables — requires keepNext/keepLines in docx-js.

6. **Interactive identity walkthrough placement decided.** Sequence: Module 4 §1 → definitions → walkthrough → transaction sequencer → assessment.

---

## What Still Needs to Be Done

### Immediate (Next Session)

1. **Complete the one-by-one title interview** for Objectives 11–17. The last reviewed objective was 10 ("Trace a transaction through the identity and verify balance" — kept as-is). The next to review is **Objective 11** (formerly 12): "Distinguish stocks from flows and locate each in the identity."

2. **Rebuild the memo** with all 17 objectives, revised titles, combined objectives, and pagination fix (keepNext/keepLines).

3. **Rebuild the matrix** with 17 objectives and revised titles.

4. **Update Learning_Objectives.md** with 1–17 numbering and revised titles. This document has not been touched this session and still carries the old 1–19 numbering.

5. **Brainstorm factors that influence accounting treatment** with Rick — for the planned rabbit hole content. Identified so far: information most useful for a given purpose, production cost (e.g., verification).

### Carried Forward from Previous Sessions

6. **Draft new prework content** for identified gaps — priorities: asset vs. expense classification, safeguarding of assets, predictions in definitions, manager-auditor asymmetry, equities decomposition, multi-period gap persistence.

7. **Convert final memo to PDF** (Rick's original plan after Word review).

8. **Decide on the real-world case(s).** CVS Health, or add/replace with other companies?

9. **Rename "Module" to "Part" across the site.** Decided but still deferred.

10. **Renumber Parts** with final sequence.

11. **Fill in placeholder URLs** — Accounting Origins project link and Rick's Madoff video interview.

12. **Review the S&P 500 data question** — price-only vs. total return in reflect3.html.

13. **Add IT vocabulary acknowledgment** — info box in Module 2 (or Module 1).

14. **Consider alternative recognition rules interactive.**

15. **Build the real-world case modules.**

16. **The repeating cycle** — material stating that the system operates as a repeating cycle (impose → operate → impose → explain) should be added before the transaction sequencer.

---

## Open Questions (Updated)

- Which company or companies for the real-world case?
- Where does the manager-auditor information asymmetry content go?
- Where does the predictions-in-definitions content go?
- What is the full set of factors that influence accounting treatment? (Brainstorm needed)
- Part renumbering: what is the final sequence?
- Diagnostic before Module 4: what does it assess?
- Should Objective 15's persistent-gap assessment be scaled back or should multi-period content be added?

---

## Site File Inventory (Unchanged)

```
site/
  index.html              — Landing page (Module 1)
  config.js               — Default configuration
  shared.css              — All shared styles
  shared.js               — Glossary (30 terms), nav, progress, accordion, config
  setup.html              — Instructor intake agent
  standards-selector.html — Interactive standards review tool
  module-template.html    — Blank template
  module2.html            — Module 2: Why Accounting Systems Exist (FULLY DRAFTED)
  reflect2.html           — React reflection page for Module 2
  entity-diagram.html     — The Entity Boundary (React Q&A)
  module3.html            — Module 3: Worth, Quantification, and Limits (FULLY DRAFTED)
  reflect3.html           — Ponzi scheme staged-reveal reflection
  module4.html            — Module 4: The Architecture (FULLY DRAFTED)
  reflect4.html           — The System in Action: A Simple Case (progressive reveal, animated numbers)
  reflect4-prompts.html   — Pause and Reflect: What the Numbers Tell You Together
  module5.html            — [placeholder — real-world case TBD]
  module6.html            — [placeholder]
  module7.html            — [placeholder]
  module8.html            — Module 8: The Analyst's Toolkit (placeholder)
```

### Non-Site Files (Updated)

```
Continuation_Brief_March21_Session3.md — This document
Continuation_Brief_March21_Session2.md — Previous session brief
Continuation_Brief_March21.md          — Earlier session brief (today)
Continuation_Brief_March19_Session2.md — Previous day's session brief
Continuation_Brief_March19.md          — Earlier session brief
Continuation_Prompt_March21_Session3.md — Companion prompt (read this brief first)
Terminology_and_Language_Conventions.md — Active language constraints
Learning_Objectives.md                 — All objectives (NOT YET UPDATED — still old 1-19 numbering)
Learning_Objectives_Matrix.xlsx        — Traceability matrix (needs update to 1-17)
Learning_Objectives_Memo.docx          — Word memo to METALS team (needs rebuild with 1-17 and revised titles)
memo2.js                               — JavaScript source for memo generation (in session working dir)
```

---

## Project Background (Unchanged)

The CMU METALS Capstone Project is a collaboration between Yale SOM (Rick Antle and Stanley Garstka) and Carnegie Mellon University, with Pierre Liang as CMU-side content expert and liaison. The CMU METALS team (four students, including project manager Sarah) brings learning science expertise. Advisors: John Stamper and Eric Harpstead.
