# Teaching Material Development Process

**Version:** 1.0
**Date:** February 12, 2026
**Purpose:** Govern the end-to-end process of creating teaching materials, ensuring consistency with established standards while making the collaboration between Rick and Claude as efficient as possible.

---

## How This Document Works

This document defines the phases Claude follows when helping Rick create teaching materials. It emphasizes rapid, decision-driven planning so that high-quality tutorials can be built without unnecessary back-and-forth. Claude should internalize this process at the start of every new teaching material session.

---

## Phase 1: Planning

The Planning Phase is where every new teaching material begins. Claude's role is to accelerate Rick's decision-making by doing the analytical heavy lifting, presenting clear alternatives, and always making a recommendation.

### 1.1 Initiating a New Project

When Rick requests a new teaching material, Claude should immediately:

1. **Read this process document** to refresh on the workflow.
2. **Read the relevant standards documents** — at minimum:
   - `Project-Standards/Core-Pedagogical-Standards.md` (pedagogical rules, terminology)
   - `Project-Standards/Tutorial-Development-Standards.md` (technical format, components)
   - Any project-specific standards if the material extends an existing series. These live in `Project-Standards/` subfolders within each project directory (e.g., `TimeValueMoney/Project-Standards/`, `NFP-Financial-Literacy/Project-Standards/`) or as standalone files in the project root (e.g., `Accounting_Origins/Tutorial-Development-Standards.md`, `Accounting_Origins_TimeMachine/DEVELOPMENT_STANDARDS.md`).
3. **Scan existing materials** in the working folder to identify:
   - Related tutorials that inform scope and tone.
   - Patterns that should carry forward (narrative style, question types, color palette).
   - Gaps that the new material might fill.
4. **Use subagents for speed.** When multiple files need reading or multiple analyses need running, Claude should launch parallel subagents rather than working sequentially.

### 1.2 Decision Framework

Every planning session involves a series of decisions. Claude handles these as follows:

**For each decision point, Claude must:**

- Identify 2–4 concrete alternatives (not vague options — each should be specific enough to act on).
- Recommend one alternative, marked clearly as "(Recommended)".
- Present the alternatives using the AskUserQuestion tool so Rick can click to select.
- Include a brief rationale for each option (one sentence) so the tradeoffs are visible at a glance.

**Show First, Then Decide:**

Claude should present all recommendations up front — as a numbered summary showing each decision, the alternatives considered, and which one Claude recommends — so Rick can see the full picture before committing to anything.

After presenting the summary, Claude uses the AskUserQuestion tool with:

> "Here are my [N] recommendations. How would you like to proceed?"

Options:
- **Accept all recommendations** — Claude locks in all recommended options and moves forward.
- **I want to change some** — Claude presents only the decisions Rick wants to revisit, one at a time using AskUserQuestion. Everything else stands as recommended.

**The key principle:** Rick always sees what he's agreeing to before agreeing to it. No blind acceptance.

### 1.3 Planning Decisions — Standard Checklist

The following decisions arise in most teaching material projects. Claude should address each one, skipping only those that are clearly predetermined by context.

#### A. Project Identity

| Decision | What Claude Analyzes | Typical Alternatives |
|----------|---------------------|---------------------|
| **Series or standalone?** | Existing series in folder, natural fit | Extend existing series / New standalone / New series |
| **Project name** | Naming conventions of existing projects | 2–3 name options following established patterns |
| **Target audience** | Audience of related materials | Same audience as [X] / New audience specification |

#### B. Pedagogical Approach

| Decision | What Claude Analyzes | Typical Alternatives |
|----------|---------------------|---------------------|
| **Narrative frame** | Frames used in existing tutorials (historical fiction, case study, character journey, direct instruction) | Historical narrative / Case-study driven / Character arc / Direct with embedded scenarios |
| **Concept delivery model** | Core Pedagogical Standards (experience-first, name-later) | Full experience-first / Guided discovery / Hybrid (experience-first for key concepts, direct for supporting) |
| **Question strategy** | Question types across existing tutorials | Numeric + text mix / Primarily conceptual text / Two-choice with follow-up reasoning / Scenario-based |
| **Enrichment approach** | Rabbit Holes and Deep Dives in Time Machine; simpler models in earlier projects | Rabbit Holes only / Deep Dives only / Both / Neither (lean tutorial) |

#### C. Content Architecture

| Decision | What Claude Analyzes | Typical Alternatives |
|----------|---------------------|---------------------|
| **Number of tutorials** | Series lengths across projects (6–10 typical) | Specific count with rationale based on topic scope |
| **Tutorial length target** | Existing tutorial lengths (15–25 min typical) | Short (10–15 min) / Standard (15–25 min) / Deep (25–40 min) |
| **Arc structure** | How existing series build (linear progression, widening lens, case comparison) | Linear build / Widening lens / Comparative / Problem-first then systematic |
| **Case data / source material** | Available real-world data, existing case organizations | Specific case options with pros and cons |

#### D. Technical Format

| Decision | What Claude Analyzes | Typical Alternatives |
|----------|---------------------|---------------------|
| **File format** | Current standard (standalone HTML with React via CDN) vs. older JSX | Standalone HTML (current standard) / JSX (if build pipeline exists) / Markdown (non-interactive) |
| **Component set** | Components available in the current standards | Full interactive (questions, rabbit holes, deep dives, glossary, sound) / Medium (questions, glossary) / Light (narrative with inline reflection prompts) |
| **Color palette** | Established palette vs. new project needs | Standard Yale Blue palette / Modified palette for new context / Custom (specify) |
| **Sound feedback** | Standard four-tone system | Standard sounds / Custom sounds / No sound |

### 1.4 Planning Deliverable

At the end of the Planning Phase, Claude produces a **Tutorial Series Plan** following the pattern established in existing plans (e.g., `NFP-Financial-Literacy/Tutorial-Series-Plan.md`). This plan includes:

1. **Series overview** — what it teaches, who it's for, how it connects to existing materials.
2. **Design decisions** — a record of every decision made in 1.3, with the selected option.
3. **Pedagogical approach** — the specific teaching philosophy for this series.
4. **Individual tutorial outlines** — for each tutorial:
   - Working title
   - What this tutorial shows/teaches
   - Key "aha" moments
   - Question topics (not full questions yet)
   - Case data or narrative context needed
   - Enrichment content (rabbit holes, deep dives) planned
5. **Series arc summary** — how tutorials connect and build.
6. **Data and source material requirements** — what Rick needs to provide or what Claude needs to research.
7. **Implementation sequence** — dependency order, which tutorials to build first.

Claude drafts this plan and presents it for Rick's review. Once approved, it becomes the governing document for the Development Phase.

---

## Phase 2: Standards Alignment

**Gate:** This phase begins only after Rick approves the Tutorial Series Plan produced in Phase 1. Approval can be explicit ("looks good") or implicit (Rick begins requesting development work based on the plan).

### 2.1 Standards Audit

Claude reviews and presents:

- **Which existing standards apply** to this project (pedagogical, technical, project-specific).
- **Any conflicts** between the plan and current standards.
- **Any gaps** — decisions or patterns not yet covered by standards that should be documented.

### 2.2 Standards Update (if needed)

If the project introduces new patterns (e.g., a new question type, a new enrichment format, a new audience-specific language rule), Claude proposes updates to the relevant standards documents. These updates are presented for Rick's approval before development begins.

---

## Phase 3: Development

**Gate:** Development begins after Standards Alignment is complete — meaning Rick has confirmed the applicable standards and approved any proposed updates.

### 3.1 Tutorial Build Order

Claude follows the implementation sequence from the plan. For each tutorial:

1. **Draft the tutorial** in the specified file format, applying all relevant standards.
2. **Self-check against standards** — Claude verifies terminology, question design, component usage, and pedagogical approach against the standards before presenting to Rick.
3. **Present the tutorial** for Rick's review.

### 3.2 Efficiency Principles

- **Subagents for parallelism.** When multiple tutorials have no dependencies, Claude should draft them in parallel using subagents.
- **Incremental review.** Rather than drafting all tutorials before any review, Claude presents tutorials in batches (e.g., 2–3 at a time) to catch issues early.
- **Pattern reuse.** Claude should extract and reuse components, narrative patterns, and question structures from existing tutorials rather than reinventing them each time.

### 3.3 Question Design Protocol

For each question in a tutorial, Claude specifies:

- The question text (no format-revealing placeholders).
- The evaluation logic (keywords, acceptable synonyms, numeric tolerances).
- Two hints (progressive, not answer-revealing).
- The third-strike reveal text.
- Enter-key submission behavior.

Claude should test that the evaluator logic aligns with what the question actually asks — this is a known failure mode flagged in the Core Pedagogical Standards.

---

## Phase 4: Review and Quality Assurance

### 4.1 Standards Compliance Review

Claude runs a systematic check of each tutorial against:

- **Core Pedagogical Standards** — terminology, teaching approach, required distinctions.
- **Tutorial Development Standards** — technical format, component structure, accessibility.
- **Project-specific standards** — any rules unique to this series.

Claude presents findings as a checklist with pass/fail for each item.

### 4.2 Cross-Tutorial Consistency

Claude checks across the full series for:

- Consistent terminology usage.
- Consistent UI behavior (phase transitions, sound triggers, glossary terms).
- Arc coherence — does each tutorial build on the previous one as planned?
- No orphaned references (e.g., "as we saw in Tutorial 3" when Tutorial 3 doesn't cover that).

### 4.3 Accessibility and Usability

Per the Mobile Usability Analysis standard:

- Keyboard navigation works for all interactive elements.
- Color contrast meets WCAG guidelines.
- Touch targets are adequately sized for mobile.
- Content reflows properly on smaller screens.

---

## Phase 5: Iteration

### 5.1 Post-Review Revision

After Rick reviews tutorials, Claude:

- Collects all feedback.
- Groups feedback by type (content, pedagogical, technical, aesthetic).
- Presents a revision plan with estimated scope.
- Executes revisions, applying the same standards compliance check to revised content.

### 5.2 Version Management

- Tutorial files use the naming conventions established in their project folder.
- Standards documents are versioned (major.minor) with changelog entries.
- Superseded versions are preserved (not overwritten) unless Rick requests otherwise.

---

## Appendix: Interaction Patterns for Claude

### Using AskUserQuestion Effectively

When presenting decisions, Claude should:

- **Batch related decisions** — group 2–4 related decisions into a single AskUserQuestion call rather than asking one at a time.
- **Lead with the recommendation** — the recommended option should always be the first option in the list, marked "(Recommended)".
- **Keep descriptions actionable** — each option description should make the tradeoff clear in one sentence.
- **Always offer Accept All** — as the first question in any batch, give Rick the chance to accept all recommendations at once.

### Using Subagents for Speed

Claude should use subagents when:

- Reading multiple standards documents at the start of a session.
- Analyzing existing tutorials for patterns.
- Drafting multiple tutorials that don't depend on each other.
- Running quality checks across a full series.

### Session Continuity

At the end of any session where work is incomplete, Claude should produce or update a `HANDOFF.md` file in the project folder (following the pattern in Accounting Origins TimeMachine) that captures:

- What was completed.
- What remains.
- Any open decisions.
- Any known issues.

This ensures the next session — whether with the same or a different Claude instance — can resume without lost context.

---

## Appendix: Existing Project Reference

| Project | Folder | Format | Tutorials | Audience |
|---------|--------|--------|-----------|----------|
| Accounting Origins v1 | `Accounting_Origins/Accounting_Origins_v1/` | HTML | ~14 | Introductory accounting students |
| Accounting Origins TimeMachine | `Accounting_Origins/Accounting_Origins_TimeMachine/` | HTML | 31 experiences | Introductory accounting students |
| Time Value of Money | `TimeValueMoney/` | JSX + HTML | 9 JSX + 6 HTML | Finance students |
| NFP Financial Literacy | `NFP-Financial-Literacy/` | HTML | 7 | Nonprofit board members/trustees |
| Sophia Story | `Sophia-Story/` | HTML | 10 chapters | General audience |
| Cash Flow / Value Flow | `CashFlowValueFlow/` | HTML | 2 | Intermediate students |
| 165WA Bond Pricing | `165WA/` | HTML | 2 | Finance students |

---

*This process document should be read by Claude at the start of every teaching material development session.*
