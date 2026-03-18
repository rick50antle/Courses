# Continuation Brief

## CMU METALS Prework Redesign — Session of March 18, 2026

**Paste this document at the start of a new chat to resume work.**

### Purpose of This Document

This brief summarizes a working session on March 18, 2026 in which Rick Antle and Claude (Opus 4.6) significantly advanced the redesign of the CMU METALS Prework. It continues from the March 17 session (documented in CMU_METALS_Continuation_Brief.docx). All files are in the folder: **Accounting Pre-work/CMU METALS Prework Redesign/**

### Companion Documents (all in that folder)

- **CMU_METALS_Prework_Redesign.docx** — Full module redrafts from March 17 (prose narratives + slide outlines, all 8 modules). Still the baseline reference, but Module 1 is now superseded by today's work.
- **CMU_METALS_Continuation_Brief.docx** — March 17 continuation brief. Still valid for background context.
- **Terminology_and_Language_Conventions.md** — Active language constraints for all drafting. MUST be read before any writing.
- **Module1_Revised.md** — March 18 METALS-team-facing narrative for Module 1 (supersedes Module 1 in the March 17 doc).
- **Module1_Mockup.html** — Interactive HTML mockup of the Module 1 landing page as students would see it. Includes configurable institutional theming.
- **Prework_Idea_Flows_Memo.docx** — Early draft of idea flows memo. Rick edited the first paragraph. Needs to be rewritten at a more concrete level (see "What Still Needs to Be Done" below).

---

## What Changed on March 18

### Major Framing Shift: Information System (not just Information Architecture)

The March 17 session established "accounting is an information architecture" as the unifying thesis. On March 18, this was pushed further: accounting is an **information system** — with inputs (economic events), processing (the disciplined architecture with the identity as core constraint), outputs (financial statements as four windows), and users (investors, lenders, managers, regulators, courts) who come to the system with different questions.

The "information architecture" framing is retained but operationalized — architecture describes the deep structure; system describes it functioning.

### Three New Intellectual Moves (Module 1)

**Move 1: Complexity as the reason the system exists.** The system exists because economic activity, past a certain scale, exceeds what any individual or group can hold in their heads. This is established through analogy: simple information systems (a scale, a tape measure) report on well-defined properties. Complex information systems (climate models, CEO dashboards) exist because the thing they inform us about is too complex to observe directly. They compress, and compression requires choices that involve tradeoffs. Accounting systems belong to this family.

**Move 2: Architecture vs. Instance.** The general architecture (identity, double-entry, four output channels, input boundary) is shared by every accounting system on earth. An instance is what you get when a rule-making body makes specific choices for a specific class of entities (US GAAP via FASB, IFRS via IASB, governmental via GASB). The prework studies one instance (US GAAP, for-profit corporation, CVS Health) but the pedagogical goal is the architecture. Whenever a GAAP-specific rule appears, it is identified as an instance choice.

**Move 3 (implicit, never stated to students): Complementary cognitive artifact.** The system works with human judgment, not in place of it. The system does not produce "answers." It produces structured representations that require interpretation by a person who understands what the system did and what it left out. This is conveyed by never presenting a rule without its tradeoff, never presenting a number without asking what it captures and omits.

### Tradeoffs Are Inevitable

Because the system must compress complex reality into a form human minds can work with, every design choice involves a tradeoff. There is no tradeoff-free accounting system — that would be reality itself. This principle runs through every module:
- Historical cost: verifiability gained, timeliness sacrificed
- Adjustments away from cost: relevance gained, verifiability sacrificed
- Estimation and allocation: completeness gained, precision sacrificed
- The accounting identity itself: internal consistency gained, flexibility sacrificed
- The incomplete markets principle: tractability gained, completeness sacrificed

### Module 1 Landing Page Design

The landing page was redesigned to be **spare** — not a wall of text. The student sees:

1. **Banner** — configurable per institution (colors, logo, course title)
2. **Subtitle** — "Accounting as an Information System"
3. **Rick's video** — 3-5 minutes, the first substantive thing the student encounters
4. **Roadmap** — vertical timeline showing the modules as a walk through the system (outside in)
5. **How to Use This Prework** — three info boxes (new to accounting / some background / everyone)
6. **Background Assessment** — diagnostic quizzes, clearly labeled as not graded
7. **Transition** — one-line bridge to Module 2

The full information-systems opening text (climate models, dashboards, accounting systems belong to this family) is **not** on the landing page. It is either what Rick covers in the video or what the student encounters when they click into Module 1 content. The landing page is the lobby, not the first lecture.

### Institutional Configurability

The mockup demonstrates that the prework can be rebranded per institution by changing CSS variables: primary color, accent color, logo, and course title. Examples implemented:
- Yale SOM (Yale blue, "Accounting Pre-Work")
- Yale Law (Yale blue, "Accounting Pre-Work for LAW21474")
- Carnegie Mellon (Carnegie red, "Accounting Pre-Work for Tepper MBA")
- Generic (neutral palette)

The content is identical across all deployments. Only the skin changes.

---

## Terminology and Language Conventions (Summary)

Full document: **Terminology_and_Language_Conventions.md** — read it before any drafting.

Key constraints:

1. **Never "measurement" or "measure"** — use express, quantify, estimate, assess, allocate
2. **Never "need"** for the user's relationship to understanding — use "want to understand." People choose to understand, and make better choices when they do.
3. **Never "the answer"** or imply the system produces answers — use outputs, reports, representations. The system informs judgment; it does not replace it.
4. **"Worth" not "value"** — softer, more honest, carries incomplete markets implications. Exception: technical terms (fair value, book value, net realizable value).
5. **Money "expresses" worth** — does not "measure" it
6. **"Accounting systems" not "accounting"** — concrete, points to designed artifacts, prepares for architecture/instance distinction
7. **Four financial statements are "four windows onto one structure"** — never four independent documents
8. **Historical cost is the "strongest epistemic anchor for worth"** — arm's-length transaction as direct market evidence
9. **The accounting identity is "imposed"** — not derived or discovered
10. **"Helping them learn" not "teaching them"** — the student is the agent; the prework starts the journey

---

## Student-Facing Opening Text (Working Draft)

This is the approved-in-principle text for what the student reads or hears in Module 1. It will serve as the basis for video scripts and other material:

---

*You already rely on information systems, even if you don't call them that. A scale tells you how much something weighs. A tape measure tells you how long something is. These are simple information systems — they report on a single, well-defined physical property.*

*But many of the things we want to understand aren't like that. We want to understand them, and we make better choices when we do — but they don't reduce to a single property that an instrument can read.*

*Consider a climate model. It takes ocean temperatures, atmospheric chemistry, land use patterns, and solar radiation data and produces projections. But the projections depend on assumptions, and different assumptions produce different projections. And different people come to the same model with different questions. A coastal city planner wants to know whether sea levels are rising. A ship captain wants to know wave heights in the North Atlantic next week. A farmer in the Midwest wants to know whether rainfall patterns are shifting. An insurance company wants to know how often Category 4 hurricanes will hit the Gulf Coast over the next decade. They are all drawing on the same underlying science, the same kinds of data — but the questions they bring shape what they look for in the output.*

*Or consider something closer to everyday business. A CEO's dashboard takes thousands of data points about a company and presents a handful of numbers. Which numbers? That's a design choice. The CFO is looking at whether cash covers next month's payroll. The head of sales is looking at which product lines are growing. The board is looking at whether the company hit its annual targets. Same organization, same underlying activity — but different people with different questions, each one looking for something different in the same system's output.*

*What do these systems have in common? They all exist because the thing they inform us about is too complex to observe directly. They all compress — taking vast, messy reality and producing something structured enough to work with. And because they compress, they all make choices about what to include and what to leave out. Those choices involve tradeoffs. The output is useful, but it is never the whole picture. It always requires a person who understands what the system did and what it didn't.*

*Accounting systems belong to this family. They are information systems designed to inform us about the economic activity of organizations — something no individual can observe directly once an organization reaches any real scale. Like a climate model, they depend on assumptions and conventions. Like a dashboard, they compress by design, and the people who use them come with different questions. An investor, a lender, a manager, a tax authority, a judge — same organization, same underlying economic activity, different questions.*

*That is what this prework is about.*

---

## What Still Needs to Be Done

### Immediate (Next Session)

1. **Continue working through the Module 1 idea flow.** We completed the opening text (information systems family, complexity, accounting systems belong here). The next ideas to work through at the same ground level:
   - The architecture/instance distinction — made concrete for the student
   - The roadmap — explaining the sequence as a walk through a system
   - The background quiz framing

2. **Rewrite the idea flows memo at a concrete level.** Rick said the first draft was "much too high a level." The memo needs to work through each idea the way we worked through the opening text — at the level of what a student actually reads or hears, not at the level of an abstract. This memo will also serve as the basis for scripts and other material.

3. **Draft Rick's video script for Module 1.** The opening text is the intellectual content; the video script is how Rick delivers it in 3-5 minutes on camera.

### Subsequent

4. **Apply the information system framing to Modules 2-8.** The March 17 drafts need to be revised to incorporate:
   - The complexity argument
   - The architecture/instance distinction (labeling GAAP rules as instance choices)
   - The tradeoffs framing
   - The complementary artifact stance (implicit)
   - All terminology constraints

5. **Revise Module 3** — the historical cost reframing (still pending from March 17). Three-part structure: transactions as anchor, adjustments away from cost, estimation and allocation.

6. **Full consistency review** across all modules (language, visual callbacks, closing transitions, information architecture echoes).

### Design/Production

7. **Finalize the landing page mockup** for METALS team review
8. **Develop the institutional theming system** into a production-ready configuration
9. **Design the "different doors" visual** — updated to carry the architecture/instance distinction
10. **Design the four-bridge diagram** (Module 4) — the signature structural diagram

---

## Open Questions (Carried Forward)

- Should Modules 5, 6, 7 be consolidated into one CVS module with three sections?
- Ponzi schemes as an example in Module 3 — placement TBD
- Statement of changes in shareholders' equity — excluded from CVS tour; introduced in course proper
- Harari quote removed. Buffett quote considered but may not do enough work. Current approach: no quote on landing page; the pull-quote "We want to understand them, and we make better choices when we do" may serve as eye candy if needed.
- How much of the opening text goes in the video vs. on the page vs. both?

---

## Project Background (Unchanged)

The CMU METALS Capstone Project is a collaboration between Yale SOM (Rick Antle and Stanley Garstka) and Carnegie Mellon University, with Pierre Liang as CMU-side content expert and liaison. The CMU METALS team (four students, including project manager Sarah) brings learning science expertise. Advisors: John Stamper and Eric Harpstead.
