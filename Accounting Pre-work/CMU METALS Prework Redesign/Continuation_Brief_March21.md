# Continuation Brief

## CMU METALS Prework Redesign — Session of March 21, 2026

**Paste this document at the start of a new chat to resume work.**

### Purpose of This Document

This brief captures the working session on March 21, 2026, in which Rick Antle and Claude (Opus 4.6) made significant changes to the reflect4.html transaction sequencer, drafted 19 learning objectives, then systematically reviewed and restated the objectives one by one — arriving at substantially different and sharper versions. The session also surfaced new content ideas that need to be added to the prework.

### All Files Are In

**Accounting Pre-work/CMU METALS Prework Redesign/**

With the working site in the **site/** subfolder.

### Companion Documents to Read Before Resuming

1. **Continuation_Brief_March21.md** — This document. The most current session brief.
2. **Continuation_Brief_March19_Session2.md** — Previous session brief (Module 4, transaction sequencer, reflection prompts).
3. **Terminology_and_Language_Conventions.md** — Active language constraints.
4. **prework-adopted-standards.md** (in parent folder: Accounting Pre-work/) — Standards adopted from the Accounting Origins project.
5. **Learning_Objectives.md** — The original 19 objectives (now being substantially revised; see this brief for the revised versions).
6. **Learning_Objectives_Matrix.xlsx** — Traceability matrix (needs updating once objectives are finalized).
7. **site/reflect4.html** — Updated this session with progressive reveal, animated numbers, and other changes.
8. **site/module4.html**, **site/reflect4-prompts.html**, **site/shared.css**, **site/shared.js**, **site/config.js** — Unchanged this session.

---

## What Was Built This Session

### 1. Progressive Reveal in reflect4.html (Transaction Sequencer)

Major changes to how the balance sheets work in the interactive transaction sequencer:

**Progressive account revelation.** Balance sheet accounts (Cash, Equipment, Bank Loan, etc.) only appear when a transaction first introduces them. The structure grows as the business takes shape. Before any transactions, the balance sheet frame shows headers (Assets / Liabilities / Equities) but no account rows, with a message: "The entity exists but has no recorded activity yet."

**Highlighting.** All accounts affected by the current transaction get a gold highlight. The highlight persists until the student clicks Next — it does not auto-fade. Accounts not affected by the current transaction are dimmed (opacity 0.35).

**Opening BS pales.** As soon as the first transaction is recorded, the entire opening balance sheet drops to low opacity so the student's attention goes to the closing BS.

**Totals removed.** Per-column totals were removed from the balance sheet grids — the sticky identity bar already shows A − L = E.

**Animated number changes.** When a transaction changes an account's value, the old number flashes 3 times in accent color (~750ms), then snaps to the new value. Uses a dedicated `AnimatedValue` React component.

**Complete button fix.** The final "reveal" stage now shows "Continue to Reflection →" linking to reflect4-prompts.html, instead of a disabled "Complete" button.

**Net new code:** approximately 148 lines added to reflect4.html (file went from 932 to 1,080 lines).

### 2. Learning Objectives — Original Draft

**Learning_Objectives.md** — 19 objectives organized into six groups:
1. The System as a Designed Artifact (3 objectives)
2. The Entity and Its Boundary (2 objectives)
3. Conventions, Worth, and Limits (3 objectives)
4. The Identity and the Architecture (4 objectives)
5. Two Snapshots and Three Decompositions (3 objectives)
6. Reading the Statements Together (4 objectives)

### 3. Traceability Matrix

**Learning_Objectives_Matrix.xlsx** — 19 objectives × 13 content locations, each cell coded P (primary), R (reinforced), or A (assessed). Needs updating once objectives are finalized.

### 4. Learning Objectives — Systematic Revision (In Progress)

Rick and Claude reviewed objectives one by one, substantially restating each. The revision is partially complete (through Objective 12 in the new numbering). Key principles that emerged:

- **Don't ask "why" when you want the student to demonstrate a consequence.** "Explain why X" invites philosophical answers. "Given this scenario, show what happens" is assessable.
- **Give two alternatives, ask the student to reason about them.** This pattern works for conventions, recognition rules, entity boundaries — consistently through the objectives.
- **Multiple choice is appropriate for students at this stage** on several objectives. They can reason about alternatives put in front of them; they can't yet generate specific examples from scratch.
- **"Which one is right?" is a powerful discriminator.** The student who says "neither — they're different conventions" has internalized the central insight.

---

## Restated Learning Objectives (Through Objective 12)

### Objective 1
**Original:** Explain why accounting systems are designed information systems, not measurement instruments.

**Restated:** Given two conventions applied to the same economic event, explain why they produce different financial representations and why neither is inherently wrong.

**Assessment design:** Present a scenario — an entity holds an investment purchased for $80,000, now worth $120,000, not sold. Convention A recognizes the $40,000 gain on this year's income statement. Convention B recognizes no gain until the entity sells. Three-part question: (1) What's different about the financial statements? (2) Is one right and the other wrong? (3) What does the existence of both tell you about what an income statement is?

**Key insight:** The "which one is right" question is the real discriminator. The student who answers "neither — they're both design choices" has internalized the objective.

---

### Objective 2
**Original:** Distinguish between the architecture and specific instances of accounting systems.

**Restated:** Given the same economic event recorded under two different sets of conventions, show that the identity holds in both cases and explain what differs and why.

**Assessment design:** An entity spends $50,000 on product development. Under System A, it's recorded as an asset. Under System B, it's expensed immediately. Show that A − L = E holds in both cases. Explain what's different (the convention choice) and what's the same (the architecture).

**Key insight:** The student is *doing* the architecture/instance distinction rather than naming it.

---

### Objective 3
**DROPPED.** Original asked students to explain why the prework uses IT vocabulary. This asks about a pedagogical choice, not about understanding the system. The concept it carried (understanding what "instance" means) is demonstrated through Objective 2.

---

### Objective 4
**Original:** Define the entity as an organizational boundary and explain what that boundary determines.

**Restated:** Given a transaction between two entities within a larger group, show its effects on each entity's identity separately, and explain why it has no effect on the consolidated entity's identity.

**Assessment design:** Subsidiary A sells $10,000 of inventory to Subsidiary B for cash. Show effects on A's identity, effects on B's identity. Then draw the boundary around the consolidated group — what are the effects on the group's identity? Answer: none, because nothing crossed the group's boundary. The cash and inventory moved within the boundary.

**Key insight from Rick:** Frame as two legal entities owned by the same parent transacting with each other. Two separate identities change; the consolidated identity does not. This is the boundary concept demonstrated, not defined.

---

### Objective 5
**Original:** Explain why the recognition decision is the gatekeeper of the system, and identify what it excludes.

**Restated:** Given examples of economic resources that are and are not recorded by the system, identify what determines whether something enters the system and recognize what this means for interpreting the balance sheet.

**Assessment format: Multiple choice.** The entity has a purchased patent and an internally developed workforce. Why does the patent appear on the balance sheet and the workforce does not? Choices include:
- The patent is more valuable than the workforce (wrong — recognition isn't about importance)
- The patent was acquired in a transaction at a verifiable amount; the workforce was not (correct)
- The patent is a physical asset; the workforce is not (wrong — assets are rights, not physical things)
- The system only records things that can be sold (wrong)

Follow-up: What does this mean for someone reading the balance sheet? Correct answer: the balance sheet may omit some of the entity's most important economic resources.

**Key insight from Rick:** Students at this stage can reason about alternatives put in front of them; they can't generate the reasoning from scratch. Multiple choice is the right format.

---

### Objective 6
**Original:** Explain why conventions are necessary and what work they do in the system.

**Restated:** Given two conventions applied to the same event, identify the relative strengths and weaknesses of each.

**Assessment format: Multiple choice.** Capitalize R&D vs. expense R&D. What is a strength of capitalizing? (Reflects the entity's expectation of future benefits.) What is a strength of expensing? (Less costly to audit.) Note: "less costly to audit" not "easier to audit" — the precision matters.

**Key insight from Rick:** Expensing is less costly to audit because it eliminates the prediction-laden asset and all the ongoing audit work that asset generates.

---

### Objective 7
**Original:** Explain why historical cost is the strongest epistemic anchor for worth.

**Restated (substantially expanded):** Identify the predictions embedded in balance sheet items, explain why those predictions are a source of uncertainty in the numbers, and explain why they generate audit costs — including the information asymmetry between managers and auditors.

**Assessment design:** Give the student three items — cash, a receivable, capitalized R&D. Rank by how much audit work they require and explain why. The ranking follows the degree of prediction each one requires. Cash: just count it. Receivable: predict whether the customer will pay. Capitalized R&D: predict whether the project will produce any benefit at all.

**Key insights from Rick:**
1. Hidden in the definition of assets and liabilities is the need to make a prediction. "Present rights to future economic benefits" — but with R&D, is there a benefit at all? Or was it a failed attempt?
2. Every prediction on the balance sheet generates audit costs. The further from cash you move, the more audit work.
3. The manager has better information than the auditor. If the manager wants to capitalize and the auditor thinks it should be expensed, they negotiate — and the auditor is at an informational disadvantage. This negotiation is costly.
4. A convention that creates more room for managerial discretion is a convention that generates more audit cost, precisely because of the information asymmetry.

**NEW CONTENT NEEDED IN PREWORK:** The manager-auditor information asymmetry is not in the prework yet. Rick identified this as something that should be added — probably in Module 3 (conventions and limits) or as a rabbit hole in Module 4 connected to recognition. A short concrete example: the manager wants to capitalize $50,000 of R&D, the auditor must evaluate whether that's justified, the manager knows more about the project's prospects.

---

### Objective 8 (NEW — not in original 19)
**New objective:** Given several cash outflows, classify each as creating an asset or incurring an expense, and explain what determines the difference.

**Assessment design:** Three cash outflows of $50,000 each — equipment purchase, this month's rent, R&D spending. Which is an asset, which is an expense? What's the difference? Equipment: clearest asset (predictable useful life). Rent: clearest expense (benefit consumed this month). R&D: contested middle ground — asset or expense depending on whether future benefit is sufficiently predictable.

**Key insight from Rick:** The original objectives didn't explicitly ask whether students understand the identity's elements in practice — what assets and liabilities actually are, and what it takes to determine that spending created an asset rather than an expense. This is more fundamental than the structural objectives about the identity; it should come before them.

---

### Objective 9
**Original:** Explain why the accounting identity is imposed as a structural constraint, not derived or discovered.

**Restated:** Recognize that the accounting identity is a constraint imposed on the information system, not a description of a natural relationship, and explain what the constraint makes possible — including self-balancing and error detection.

**Assessment design:** After a transaction is recorded, an accountant notices that total assets don't equal total liabilities plus equities. What does this tell you? Multiple choice:
- The transaction was unusual and doesn't fit the system (wrong)
- An error was made in recording the transaction (correct)
- The identity only holds approximately (wrong)
- Some transactions affect only one side of the identity (wrong)

**Key emphasis from Rick:** Make clear it is a self-imposed constraint on the information processing system.

---

### Objective 10
**Original:** Explain why A − L = E reveals something A = L + E hides.

**Restated:** Explain that total equities is determined by the asset and liability recordings, and that the decomposition of equities into components (contributed capital vs. retained earnings; restricted vs. unrestricted net assets) is a deliberate information design choice that reveals how the residual got there.

**Assessment design:** After all eight transactions, total equities is $119,000 (from A − L = E). Given that you already know the total, what do you learn from seeing it broken into Contributed Capital $100,000 and Retained Earnings $19,000? For a nonprofit with the same total: what do you learn from restricted $24,000 vs. unrestricted $95,000?

**Key insight from Rick:** If you know total assets and total liabilities, you already know total equities — it's just arithmetic. For the equities section to tell you anything new, there have to be details. The decomposition is where the information is. This emphasizes the information framing versus the measurement framing.

---

### Objective 11
**Original:** Explain why the same architecture works for any entity with resources and obligations.

**Restated:** Explain why the same architecture applies to any entity with resources and obligations — for-profit, nonprofit, government — and how the decomposition of the residual changes to serve the information needs of different users.

**Assessment design:** Side-by-side: a corporation with equities $119,000 (CC $100K / RE $19K) and a nonprofit hospital with net assets $119,000 (unrestricted $95K / restricted $24K). What's the same? What's different? Why does the decomposition differ?

**Key insight from Rick:** This deserves its own objective because the nonprofit case is the strongest demonstration that the system is about information, not measurement. A measurement instrument wouldn't work the same way on two fundamentally different organizations.

---

### Objective 12
**Original:** Given a transaction, determine which accounts are affected, in which direction, and verify that the identity holds.

**Status:** Reviewed briefly. This is the operational skill. The transaction sequencer already provides practice. Assessment gives the student a new transaction and asks them to trace it. May stand as originally written, but we moved on before finalizing the statement.

**Discussion point:** Claude suggested the prepaid insurance example (pay $3,000 for six months of insurance — what accounts change?). Rick had not yet responded when we moved on.

---

### Objective 13
**Original:** Explain why the flow statements are decompositions of the change between two balance sheets, not independent reports that happen to agree.

**Restated:** Explain why decomposing the change between two balance sheets adds information that the change alone does not provide.

**Assessment design:** Present two balance sheets showing retained earnings of $100,000 at the start and $119,000 at the end. Ask: "The change in retained earnings is $19,000. Which of the following can you determine from that number alone?"
- (a) The entity earned $19,000 from operations — *distractor: assumes no dividends*
- (b) The entity was profitable — *distractor: $19K could reflect operations plus dividends netting to $19K*
- (c) The entity's equities increased by $19,000 from retained activities, but you cannot tell how much came from operations versus how much was paid out — *correct*
- (d) The entity collected $19,000 in cash — *distractor: confuses accrual with cash*

Follow-up: "What additional information does the income statement provide that the $19,000 change does not?"

**Key insight from Rick:** Frame positively. The flow statements exist because decomposing a change is an opportunity to add information. The income statement tells you *how* income was generated. The cash flow statement tells you how much was backed by cash. The statement of changes in equities shows the full bridge. Each decomposition adds information the balance sheet change, by itself, cannot provide.

**Rick's framing question:** "Why doesn't the simple change in a balance sheet account tell you all you want to know? Explaining the changes is an opportunity to add information."

---

## Objectives Not Yet Reviewed

The following objectives from the original list have not yet been discussed in the one-by-one review. They should be reviewed in the next session using the same approach (restate around assessable student behavior, design concrete assessments, consider multiple choice where appropriate):

- **Original 14:** What each flow statement decomposes
- **Original 15:** Why single out cash for its own statement
- **Original 16:** NI vs. CFO gap — trace it
- **Original 17:** NI vs. CFO gap — interpret it
- **Original 18:** Convention-shaped vs. observable facts
- **Original 19:** Read statements together

---

## New Ideas and Content Needs Identified This Session

### 1. Manager-Auditor Information Asymmetry
The prework should include material on the information asymmetry between the people who prepare the financial statements (managers) and the people who check them (auditors). When the manager wants to capitalize R&D, the auditor must evaluate that claim but has less information about the project. The negotiation is costly. A convention that creates more room for managerial discretion generates more audit cost. **Suggested location:** Module 3 (conventions and limits) or rabbit hole in Module 4. **Status:** Not yet drafted.

### 2. Predictions Embedded in Definitions
The definitions of assets and liabilities embed predictions about the future. "Present rights to future economic benefits" requires predicting the benefit will arrive. With R&D, the question isn't just when the benefit arrives — it's whether there is a benefit at all. This is a deeper source of convention-dependence than recognition timing alone. **Suggested location:** Module 4 §1 (when discussing asset/liability definitions) or Module 3. **Status:** Identified as important for Objectives 7 and 8; not yet drafted in prework.

### 3. Assessment Design Patterns
Three consistent patterns emerged for assessment:
- **Two conventions, same event:** Present two alternatives, ask what differs, ask which is right. (Objectives 1, 2, 6)
- **Multiple choice with distractor misconceptions:** For students at this stage who can reason about alternatives but can't generate from scratch. (Objectives 5, 6, 9)
- **Work the identity:** Give a scenario, ask the student to trace effects and verify balance. (Objectives 4, 8, 12)

### 4. "Less Costly to Audit" Not "Easier to Audit"
Rick corrected the language: the strength of expensing R&D is that it is "less costly to audit," not "easier." The precision matters — it points to real economic consequences for the oversight process.

### 5. The Repeating Cycle
The system operates as a repeating cycle: impose identity → operate → impose identity again → explain changes. This should be stated explicitly in the prework before the transaction sequencer. A **second transaction sequencer** that picks up from the closing balance sheet of the first would demonstrate the cycle concretely.

### 6. Closing-to-Opening Cycle
Note for course material (not necessarily prework): the closing balance sheet becomes the next period's opening balance sheet. This reinforces the repeating nature of the system.

### 7. Flow Statements as Information-Adding Decompositions
Objective 13's positive framing: the flow statements exist because decomposing a change is an opportunity to add information. The change in retained earnings is one number — it doesn't tell you whether the entity earned that much, or earned more and paid some out, or earned less and received contributions. The decomposition tells you *how* the change happened, not just *that* it happened.

---

## Key Decisions Made This Session

1. **Learning objectives should be stated as assessable student behaviors,** not as "explain why" prompts that invite philosophical answers.

2. **"Which one is right?" is a powerful assessment question** because the correct answer — "neither, they're different conventions" — is the central insight of the prework.

3. **Objective 3 (IT vocabulary) dropped.** The concept is demonstrated through Objective 2.

4. **A new Objective 8 was added** about classifying cash outflows as assets or expenses — this was missing from the original 19 and is more fundamental than the structural identity objectives.

5. **Objective 7 was substantially expanded** from historical cost to encompass embedded predictions, audit costs, and information asymmetry.

6. **Objective 10 was expanded** to include the decomposition of equities as a deliberate information design choice.

7. **Objective 11 retained as separate** from Objective 10 because the nonprofit case is the strongest demonstration that the system is about information, not measurement.

8. **Progressive reveal in reflect4.html** reinforces the architecture lesson — the student sees structure emerge from transactions.

9. **Objective 13 reframed positively** — from "not independent reports" to "decomposition adds information the change alone doesn't provide." Rick's key framing: "Explaining the changes is an opportunity to add information."

10. **The repeating cycle should be in the prework.** The method — impose identity, go forward, impose identity again, explain changes — is applied repeatedly. Material should be added before the transaction sequencer to make this explicit. A second transaction sequencer that picks up where the first one leaves off would reinforce this.

11. **Closing-to-opening cycle should be in the course material.** Note for CMU team: include material on how the closing balance sheet becomes the next period's opening balance sheet.

---

## What Still Needs to Be Done

### Immediate (Next Session)

1. **Complete the one-by-one objective review** — Objectives 14–19 (original numbering) still need to be reviewed and restated. Objective 13 was restated this session.
2. **Update Learning_Objectives.md** with the restated objectives.
3. **Update Learning_Objectives_Matrix.xlsx** once objectives are finalized.
4. **Draft manager-auditor information asymmetry content** for the prework (Module 3 or Module 4 rabbit hole).
5. **Draft predictions-in-definitions content** for the prework.

### Carried Forward from Previous Sessions

6. **Decide on the real-world case(s).** CVS Health, or add/replace with other companies?
7. **Rename "Module" to "Part" across the site.** Decided but still deferred.
8. **Renumber Parts** with final sequence.
9. **Fill in placeholder URLs** — Accounting Origins project link and Rick's Madoff video interview.
10. **Review the S&P 500 data question** — price-only vs. total return in reflect3.html.
11. **Add IT vocabulary acknowledgment** — info box in Module 2 (or Module 1).
12. **Consider alternative recognition rules interactive** — showing what changes in the IS when you change a convention while the CFS stays the same.
13. **Build the real-world case modules** (CVS Health or other).

---

## Open Questions (Updated)

- Which company or companies for the real-world case?
- Where does the manager-auditor information asymmetry content go — Module 3, Module 4 rabbit hole, or its own section?
- Where does the predictions-in-definitions content go?
- Alternative recognition rules interactive: where does it go?
- Part renumbering: what is the final sequence?
- Diagnostic before Module 4: what does it assess? (Now informed by the restated objectives.)

---

## Site File Inventory (Updated)

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
  reflect4.html           — The System in Action: A Simple Case (UPDATED — progressive reveal, animated numbers)
  reflect4-prompts.html   — Pause and Reflect: What the Numbers Tell You Together
  module5.html            — [placeholder — real-world case TBD]
  module6.html            — [placeholder]
  module7.html            — [placeholder]
  module8.html            — Module 8: The Analyst's Toolkit (placeholder)
```

### Non-Site Files

```
Continuation_Brief_March21.md         — This document
Continuation_Brief_March19_Session2.md — Previous session brief
Continuation_Brief_March19.md          — Earlier session brief
Terminology_and_Language_Conventions.md — Active language constraints
Learning_Objectives.md                 — Original 19 objectives (being revised)
Learning_Objectives_Matrix.xlsx        — Traceability matrix (needs updating)
```

---

## Project Background (Unchanged)

The CMU METALS Capstone Project is a collaboration between Yale SOM (Rick Antle and Stanley Garstka) and Carnegie Mellon University, with Pierre Liang as CMU-side content expert and liaison. The CMU METALS team (four students, including project manager Sarah) brings learning science expertise. Advisors: John Stamper and Eric Harpstead.
