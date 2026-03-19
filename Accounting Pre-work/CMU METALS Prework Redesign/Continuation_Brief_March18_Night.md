# Continuation Brief

## CMU METALS Prework Redesign — Session of March 18, 2026 (Night)

**Paste this document at the start of a new chat to resume work.**

### Purpose of This Document

This brief captures the third working session on March 18, 2026, in which Rick Antle and Claude (Opus 4.6) built the module page template and navigation infrastructure, drafted Module 2 content, created React-based interactive components (reflection prompts, entity boundary diagram), and began working through Module 3 source material.

### All Files Are In

**Accounting Pre-work/CMU METALS Prework Redesign/**

With the working site in the **site/** subfolder.

### Companion Documents to Read Before Resuming

1. **Continuation_Brief_March18_Night.md** — This document. The most current session brief.
2. **Continuation_Brief_March18_Evening.md** — The earlier evening brief. Still valid for video script decisions, site architecture, and glossary.
3. **Terminology_and_Language_Conventions.md** — Active language constraints. Read before any drafting.
4. **prework-adopted-standards.md** (in parent folder: Accounting Pre-work/) — Standards adopted from the Accounting Origins project.
5. **site/Video_Script_Module1_v5.md** — Current video script (v5).
6. **site/index.html** — Landing page with nav, progress bar, glossary, video transcript, and "Next" button to Module 2.
7. **site/config.js** — Default configuration (Yale/Rick). Now includes `audience` field.
8. **site/shared.css** — All shared styles for module pages.
9. **site/shared.js** — Glossary data (21 terms), nav/progress/accordion/config functions.
10. **site/module2.html** — Module 2: Why Accounting Systems Exist (fully drafted content).
11. **site/reflect2.html** — React reflection page for Module 2 (audience-conditional text prompts).
12. **site/entity-diagram.html** — Interactive Sunder entity boundary diagram (React Q&A).
13. **site/module3.html through module8.html** — Placeholder module pages with correct navigation.

---

## What Was Built on March 18 (Night Session)

### 1. Module Page Template and Full Navigation

Created the shared infrastructure for all module pages:

- **shared.css** — Extracted all shared styles from index.html plus new styles: accordion sections, rabbit holes, instance-choice flags, prev/next navigation, module headers, responsive breakpoints.
- **shared.js** — Single source of truth for: glossary data (21 terms), MODULES array, module dropdown builder, progress tracking (localStorage), accordion/rabbit-hole toggle functions, transcript toggle, config-driven theming. Every page calls `initPage(moduleNum)`.
- **module-template.html** — Blank template. Copy, change module number, fill in content.
- **module2.html through module8.html** — All module pages created with correct section titles, prev/next links, and initPage() calls.

**Navigation chain:** index.html → module2.html → reflect2.html → module3.html → module4.html → module5.html → module6.html → module7.html → module8.html → index.html. Plus the Modules dropdown and glossary on every page.

**Note:** index.html still uses its own inline CSS/JS. When ready, it can be refactored to use shared files.

### 2. Module 2: Why Accounting Systems Exist (Fully Drafted)

Complete prose content in module2.html with four accordion sections:

**Section 1: The Users.** Investors, lenders, managers, boards, tax authorities, regulators, courts (damages example woven in), unions, suppliers. All coming to the same system with different questions.

**Section 2: Three Purposes.**
- *Informing decisions* — forward-looking, predictive. System informs choices; does not make them.
- *Influencing behavior* — backward-looking, stewardship-oriented. Two mechanisms:
  - Indirect: shaping incentives (bonus plans, compensation committees choosing which numbers to tie rewards to)
  - Direct: contractual and regulatory triggers (debt covenants, capital requirements — tripwires where consequences follow automatically)
- *Enabling coordination* — the reason the system must be shared. Coordination between the firm and its counterparties (lender on covenants, tax authority on what's owed, internal managers across divisions), and among the counterparties themselves. Without a common picture, disputes become unresolvable, contracts unenforceable.

**Rabbit hole (Section 2):** Gjesdal — stewardship vs. decision-usefulness as competing design objectives. 1979 Stanford dissertation, 1981 JAR article. What makes information good for evaluating a steward isn't always what makes it good for predicting future flows.

**Section 3: Common Architecture, Different Rules.**
- Architecture/instance callback from Module 1
- Different instances exist because different uses pull the design in different directions (tax → cash-based; GAAP → accrual)
- Economy of scope: transactions are the common foundation; every instance draws on the same recorded events. Economy of scope is strongest at the transaction base; narrows as instances recognize things beyond transactions (fair-worth adjustments, expected losses create new source data the tax system may not require)
- **Rabbit hole:** One database, many rule sets — deferred tax assets/liabilities as artifacts of running two instances off the same data

**Section 4: What This Tells Us About System Design.** Bridge to Module 3: one system, many users, can't optimize for all. Every choice is a tradeoff.

**Terminology review:** Passes all checks — no "measure," no "need," no "the answer," no standalone "value," no "teach."

### 3. Audience-Conditional Reflection Prompts (React)

**reflect2.html** — React page sitting between Module 2 and Module 3. Reads `audience` from config.js (`"executive"`, `"pre-experience"`, or `"mixed"`) and renders the matching prompt set.

- Four text areas per audience, each with a question tailored to the student's likely experience
- Auto-saves to localStorage after 800ms of inactivity, saves on blur
- Tracks answered count (green border on completed cards)
- Clearly labeled: not test questions, no right answers, saved locally

**config.js** now includes `"audience": "mixed"` field. The setup.html wizard should eventually ask which audience.

### 4. Interactive Entity Boundary Diagram (React Q&A)

**entity-diagram.html** — Major interactive component, adapted from Shyam Sunder's entity diagram (James L. Frank Professor of Accounting, Economics, and Finance, Emeritus, Yale School of Management).

**Design:**
- 7 parties in a symmetric heptagon: Owners, Lenders (split from "Money Providers"), Employees, Suppliers, Government, Customers, Managers
- SVG diagram with the entity at center, dashed animated boundary line
- Two arrow colors: teal-green (#1a8a6a) for inflows to entity, rust (#bd5319) for outflows from entity
- Legend appears once flows start
- No labels on arrows — the Q&A box does that work

**Interaction model:** 17 steps (3 intro + 14 Q&A). For each party:
1. Question appears in a box below the diagram: "What do owners provide to the entity?"
2. Student thinks, clicks "Reveal"
3. Answer appears with color-coded left border (teal for in, rust for out)
4. Corresponding arrow appears on diagram simultaneously
5. "Next →" advances to the return direction

**Key substantive content in the Q&A:**
- **Owners** provide resources (cash, land, equipment, IP) → receive two things: right to control (voting, board) and a residual claim (whatever is left after all other obligations — not a fixed amount, not guaranteed)
- **Lenders** provide cash (a defined sum) → receive a contractual obligation (right to repayment with interest — fixed, enforceable, with consequences for failure)
- **Employees** provide labor → receive compensation (salary, bonuses, benefits, sometimes equity)
- **Suppliers** provide goods/services → receive cash or promise to pay (accounts payable)
- **Government** provides public goods → receives taxes (different instance of the architecture)
- **Customers** receive goods/services → provide cash or promise to pay (accounts receivable)
- **Managers** provide managerial services → receive compensation designed to align behavior (callback to Module 2)

**Collapsible elements:** Introduction text collapses so diagram can dominate screen. Toggle button: "Hide introduction" / "Show introduction."

**"Information in transactions" framing (opening prose):** "When we observe a transaction, what do we record? The *information* in it: what was exchanged, how much, between whom, when, on what terms." Final summary: "Every arrow crossing the boundary represents the information in a transaction."

**Rabbit hole:** Consolidation — what happens when a parent owns subsidiaries and the boundary choice changes what the system sees. VIE example from the 2008 financial crisis.

### 5. Key Insight to Carry Forward: Stuff, Rights, and Promises

*Captured during discussion, not yet written into the site.*

When we observe a transaction, "stuff" crosses the entity boundary in at least one arrow direction. But what sometimes crosses the other way is not stuff — it is a right or a promise.

- Owners put resources in → what goes out? Not stuff. Rights to control and a residual claim.
- Lenders put cash in → what goes out? A promise to repay with interest.
- Employees put labor in → what goes out? Cash (stuff) — this one is stuff in both directions.
- Customers get goods (stuff) → what comes in? Cash (stuff), or a promise to pay later (accounts receivable — a right).

The first step when we observe something crossing the boundary is to **analyze it** — dig out the information in it. When we see something flow into the entity but don't see "stuff" flowing out, we look deeper for what flowed out. If it was a promise to repay, we capture that information. Doesn't matter if there was a loan document or a handshake.

**This connects directly to:** The transaction-analysis skill that journal entry notation formalizes (Module 8). The entity diagram is where students first learn to think this way. The reflection prompts for Module 3 / the entity diagram should ask students to practice this: for each party, what is "stuff" and what is a right or a promise?

---

## What Still Needs to Be Done

### Immediate (Next Session)

1. **Integrate the "stuff vs. rights/promises" insight into the entity diagram.** Either as part of the Q&A answers (revise language), as a capstone observation after the full picture, or as a reflection prompt. This is a foundational analytical habit the student should start building here.

2. **Draft Module 3 content: Worth, Quantification, and Limits.** Source material reviewed:
   - Canvas Module 3 ("Entity and Transactions" + Framework: aspirations, conventions, context)
   - Framework 1 slides (Sunder entity diagram — already built as interactive)
   - Framework 2 slides (aspirations, conventions, context — not yet read)
   - Framework 3 slides (wealth creation, Ponzi schemes — not yet read)
   - Rick's framing: "we are dealing with compacting complexity — not crisp problems with clear solutions, but aspirations, conventions, and context"

   Module 3 should open with the entity boundary (entity-diagram.html, now built), then move to aspirations, conventions, and context as the framework for understanding the choices made within that boundary.

3. **Wire entity-diagram.html into the navigation chain.** Currently a standalone page. Decision needed: does it precede module3.html (entity boundary → then worth/quantification/limits)? Or does it become the opening section of Module 3 itself?

4. **Read Framework 2 and Framework 3 slides** (in Accounting Pre-work/Framework/) for Module 3 source material.

5. **Build Module 4 content.** Rick said Module 4 is the next content priority after the template. Module 4: "The Architecture Itself" — the accounting identity and the four output channels.

### Subsequent

6. **Refactor index.html** to use shared.css and shared.js (currently inline).
7. **Build the diagnostic assessment** before Module 4.
8. **Add the climate model rabbit hole** to Module 1 web content.
9. **Build Pause and Reflect pages** for other modules (same pattern as reflect2.html).
10. **Data collection layer** and anonymous student ID system.
11. **Production GitHub Pages deployment** with README for adopting instructors.

---

## Open Questions (Updated)

- Should entity-diagram.html precede Module 3 or open Module 3?
- Ponzi schemes: placement in Module 3 (wealth creation section)? Rabbit hole?
- Should the "stuff vs. rights/promises" observation become a reflection prompt, a capstone step in the entity diagram, or both?
- How should the setup.html wizard ask about audience (executive / pre-experience / mixed)?
- Modules 5, 6, 7: consolidate into one CVS module with three sections?
- Statement of changes in shareholders' equity: excluded from CVS tour, introduced in course proper
- Diagnostic before Module 4: what does it assess?
- Climate model rabbit hole: format and exact placement

---

## Site File Inventory

```
site/
  index.html              — Landing page (Module 1) with nav, progress, glossary, transcript, Next button
  config.js               — Default configuration (Yale/Rick), now with audience field
  shared.css              — All shared styles for module pages
  shared.js               — Glossary (21 terms), nav, progress, accordion, config functions
  setup.html              — Instructor intake agent
  standards-selector.html — Interactive standards review tool
  module-template.html    — Blank template for new module pages
  module2.html            — Module 2: Why Accounting Systems Exist (FULLY DRAFTED)
  reflect2.html           — React reflection page for Module 2 (audience-conditional)
  entity-diagram.html     — Interactive Sunder entity diagram (React Q&A, 7 parties, 17 steps)
  module3.html            — Module 3: Worth, Quantification, and Limits (placeholder)
  module4.html            — Module 4: The Architecture Itself (placeholder, with rabbit hole)
  module5.html            — Module 5: CVS Health: Balance Sheets (placeholder)
  module6.html            — Module 6: CVS Health: Income Statement (placeholder)
  module7.html            — Module 7: CVS Health: Cash Flows (placeholder)
  module8.html            — Module 8: The Analyst's Toolkit (placeholder)
  Module1_Mockup.html     — Earlier mockup (superseded by index.html)
  Video_Script_Module1.md through v5.md — Script iterations
```

---

## Project Background (Unchanged)

The CMU METALS Capstone Project is a collaboration between Yale SOM (Rick Antle and Stanley Garstka) and Carnegie Mellon University, with Pierre Liang as CMU-side content expert and liaison. The CMU METALS team (four students, including project manager Sarah) brings learning science expertise. Advisors: John Stamper and Eric Harpstead.
