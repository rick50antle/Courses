# Continuation Brief

## CMU METALS Prework Redesign — Session of March 19, 2026 (Session 2)

**Paste this document at the start of a new chat to resume work.**

### Purpose of This Document

This brief captures the second working session on March 19, 2026, in which Rick Antle and Claude (Opus 4.6) drafted Module 4: The Architecture, built an interactive transaction sequencer ("The System in Action: A Simple Case"), created a separate reflection page with four prompts, and made several significant conceptual and terminological decisions.

### All Files Are In

**Accounting Pre-work/CMU METALS Prework Redesign/**

With the working site in the **site/** subfolder.

### Companion Documents to Read Before Resuming

1. **Continuation_Brief_March19_Session2.md** — This document. The most current session brief.
2. **Continuation_Brief_March19.md** — Previous session brief (Module 3, Entity Boundary, Ponzi reflection).
3. **Terminology_and_Language_Conventions.md** — Active language constraints (updated this session with six new conventions).
4. **prework-adopted-standards.md** (in parent folder: Accounting Pre-work/) — Standards adopted from the Accounting Origins project.
5. **site/module4.html** — Module 4: The Architecture (fully drafted, 3 accordion sections).
6. **site/reflect4.html** — The System in Action: A Simple Case (interactive transaction sequencer, 8 transactions).
7. **site/reflect4-prompts.html** — Pause and Reflect: What the Numbers Tell You Together (4 prompts with transaction context).
8. **site/shared.css** and **site/shared.js** — Shared styles and scripts (glossary now 30 terms).
9. **site/config.js** — Default configuration with audience field.

---

## What Was Built This Session

### 1. Module 4: The Architecture (Fully Drafted)

**module4.html** — Complete prose content with three accordion sections. The three-move structure: impose the identity, take two snapshots, explain the difference.

**Opening prose:** "You have an entity. You have aspirations. How do you actually build the system?" Three structural moves introduced.

**Section 1 — Imposing the Identity.** Presents A = L + E (familiar form), then rearranges to A − L = E and explains why the rearranged form reveals the definitional character: equities is the difference, not an independent third quantity. The identity is a tautology. Defines assets (present rights to economic benefits), liabilities (present obligations), equities (the difference — not "what's left"). Then the nonprofit move: no owners? Same identity, just call the difference "net assets." Everything transfers without modification — evidence of how deep the design goes. Why impose: self-balancing, double-entry enforcement, error detection. Rabbit hole: 500-year durability of the design choice.

**Section 2 — Two Snapshots.** The identity at two dates gives two balance sheets. SVG timeline diagram (two bars with three flow statement boxes spanning the gap). Blood pressure analogy: snapshots frame the question, they don't provide the explanation. Rabbit hole: recognition, classification, quantification — the three steps for working the identity.

**Section 3 — Explaining the Change.** Decompose the change in equities into categories. Operations → income statement. Cash → cash flow statement. Owner transactions → statement of changes in equities. Then "One change, decomposed" — the key conceptual move. The flow statements don't "agree with" the balance sheets; they *are* explanations of parts of the change. They cannot be inconsistent because they are not separate accounts of the same events — they are breakdowns. Rabbit hole: why single out cash for its own statement (cash is a count vs. income is conventions; CFO vs NI comparison; solvency vs liquidity; crypto coda).

**Bridge text** leads to the interactive: "Next, you will see this architecture in action — first through a simple hypothetical entity where you step through every transaction yourself, then through the actual financial statements of a real company."

### 2. The System in Action: A Simple Case (reflect4.html)

**Interactive transaction sequencer.** React component. Three-column desktop layout: Opening Balance Sheet (left, never changes) | Transaction (center) | Closing Balance Sheet (right, evolves).

**Sticky identity bar** at top: A − L = E with live numbers, always visible.

**8 transactions:**
1. Owner invests $100,000 cash
2. Borrow $30,000 from bank
3. Buy equipment for $20,000 cash
4. Provide $43,000 of services ($25K cash, $18K on credit)
5. Pay employee salaries $15,000
6. Collect $12,000 from customer
7. Record depreciation $4,000 (no cash)
8. Pay $5,000 dividend to owner

**Final balances:** Assets $149K (Cash $127K, A/R $6K, Equipment $16K) − Liabilities $30K (Loan) = Equities $119K (CC $100K, RE $19K).

**Key numbers:** Net Income $24K, Cash from Operations $22K. Gap explained by $6K uncollected revenue and $4K non-cash depreciation.

**Flow statements in scrollable box below,** ordered: Statement of Changes in Equities first (the full bridge), Cash Flow Statement second, Income Statement last (as a decomposition of the "Net Income" line in the equities statement). Each prefixed with a "Change in X" summary bar showing the total being decomposed. Brief note explains why the ordering differs from standard practice.

**Reveal stage** at the end points out the NI vs CFO gap.

**Accounting conventions:** Negative numbers displayed with parentheses: ($15,000) not -$15,000.

### 3. Reflection Page (reflect4-prompts.html)

**4 prompts, each with transaction context repeated:**

1. **Revenue** — repeats the $43K service revenue transaction with its three account effects. Asks: "The system recorded $43,000 in revenue. The cash flow shows $25,000 collected. These are not competing numbers — they are two facts about the same event. What does comparing them tell you about this entity's situation right now?"

2. **Depreciation** — repeats the $4K depreciation entry. Asks: "No cash moved, but the income statement recorded an expense and the balance sheet changed. What is the system trying to capture? What would be missing if the system only recorded events that involved cash?"

3. **NI vs CFO** — shows both numbers in a comparison box ($24K vs $22K, gap $2K explained). Asks: "Net income and cash from operations come from the same set of transactions, decomposed differently. What does the gap between them tell you? What questions would it lead you to ask?"

4. **The full set** — describes all three decompositions. Asks: "Different people come with different questions — a lender, an owner, a regulator. What can they learn from looking at the decompositions together that they could not learn from any single one?"

### 4. Navigation Chain Updated

Full navigation flow:
```
index.html → module2.html → reflect2.html → entity-diagram.html → module3.html → reflect3.html → module4.html → reflect4.html → reflect4-prompts.html → module5.html → ...
```

### 5. Glossary Updates (shared.js)

Now 30 terms. Changes this session:
- **Assets** — made plural, expanded: present rights to economic benefits
- **Liabilities** — made plural, expanded: present obligations to transfer economic benefits
- **Equities** — rewritten: the difference, not "what's left." Decomposition is where the information is (contributed capital vs retained earnings for for-profit; restricted vs unrestricted net assets for nonprofit).
- **Accounting identity** — now uses A − L = E form; preserves definitional character
- **Balance sheet** — now uses A − L = E form; "snapshot of position, not explanation of how"
- **Architecture** — reframed around two balance sheets + decomposition structure
- **Financial statements** — rewritten: decompositions, not separate reports that "agree"
- **Income statement** — rewritten: decomposition of operating portion of change in equities
- **Statement of cash flows** — rewritten: decomposition of change in cash
- New: **Revenue** — gross inflows of worth from entity's activities
- New: **Expense** — resources consumed in generating revenues
- New: **Accrual accounting** — conventions that decouple recognition from cash movement
- New: **Recognition** — the gatekeeper decision

### 6. Terminology Conventions (6 new)

1. **Write identity as A − L = E** (introduce A = L + E first, then rearrange)
2. **Equities is "the difference," not "what's left"**
3. **Never use "articulation" or "consistent"** for the relationship between statements — use "decomposition"
4. **Never frame questions as "if you could only see one number"** — false choice; the set of numbers is the point
5. **Cash: you just count it** — and the CFO vs NI comparison reveals how much the conventions are doing
6. **Flow statements are decompositions** — they don't "agree with" balance sheets; they ARE the change, broken into pieces

---

## Key Decisions Made This Session

1. **Module title: "The Architecture"** (not "The Architecture Itself"). Clean, direct.

2. **Identity presented as A = L + E first, then rearranged to A − L = E.** The familiar form first, then the insight: equities is the difference, the identity is a tautology.

3. **"The difference," not "what's left."** "What's left" implies scraps. "The difference" is precise.

4. **Nonprofit elevated to main text, not a rabbit hole.** The fact that A − L = E works for nonprofits by just relabeling the difference "net assets" is evidence of how deep the design goes.

5. **"Decomposition" replaces "articulation" everywhere.** The flow statements are not separate reports that happen to fit together. They are decompositions of one change. The income statement cannot be "inconsistent with" the balance sheet because it IS an explanation of part of the change.

6. **No false choices.** Never ask "if you could only see one number." The whole point is reading the numbers together. The gap is where the information lives.

7. **Cash flow statement is useful, not structurally required.** The identity doesn't need it. It's a choice to decompose the change in one particular asset because (a) cash is a count — no conventions — and (b) comparing CFO to NI tells you how much the income statement conventions are doing.

8. **Income statement presented last in the flow statements.** Not standard, but reflects logical structure: SCE is the full bridge, CFS decomposes cash, IS decomposes one line of the SCE (net income). A note explains why the ordering differs from standard practice.

9. **Three-column layout for the interactive.** Opening BS (anchor, never changes) | Transaction (center) | Closing BS (evolves). The student literally sees the two snapshots with activity between them.

10. **Reflections on a separate page.** The interactive exercise is pure experience — no interruptions. Reflections come after, with transaction context repeated. "Experience first, name later."

11. **The interactive is its own Part: "The System in Action: A Simple Case."** The CVS modules become "The System in Action" with real financial statements. Narrative arc: architecture → simple case → real case.

12. **Service revenue as one transaction.** $43K total ($25K cash, $18K on credit), not two separate transactions. Creates the accrual/cash gap within a single event.

13. **The decomposition of equities is where the information is** (not where the analytical work is). The total is just arithmetic. The breakdown into contributed capital vs retained earnings tells you where it came from.

14. **Acknowledge the IT vocabulary.** The prework deliberately borrows terms from information technology — "architecture," "instance," "input boundary," "output channels," "design choice." This should be explained to students early on (probably Module 2 where architecture/instance is introduced). Accounting systems *are* information systems, and the IT vocabulary captures structural distinctions that traditional accounting vocabulary does not.

---

## Rick's Thoughts to Capture

- **CVS may not be the only real-world case.** Rick wants to decide whether CVS is still the right (or only) case to use. Could do more than one company. This is an open question for the next session.

- **Two different recognition rules.** Rick liked the idea of showing what happens when you change a recognition convention (e.g., recognize revenue when cash is collected vs. when earned) and watching how the income statement changes but the cash flow statement doesn't. Not implemented yet — could go in the simple case interactive, or could be its own exercise. "If we don't use it here, we will use it elsewhere."

- **The income statement decomposes one line of the SCE.** This is the reason to present IS last — it is not a peer of the other statements. It is a drill-down into the "Net income" line. The standard ordering (IS first) reflects user interest, not logical structure.

- **Equities decomposition is the key.** If you know total assets and total liabilities, you know total equities — arithmetic. So what is equities for? Its decomposition: how did the residual get there? Contributed by owners (Common Stock) vs. generated by activities and retained (Retained Earnings). For nonprofits: net assets with vs. without donor restrictions.

- **IT vocabulary is deliberate and should be acknowledged.** Terms like "architecture," "instance," "input boundary" are borrowed from software engineering. This is not decoration — accounting systems are information systems, and the IT vocabulary makes structural features visible that traditional accounting vocabulary obscures. "Architecture vs. instance" captures the distinction between the shared design and specific implementations. "Design choice" makes clear that rules could have been made differently. Students should be told this early and told why.

---

## What Still Needs to Be Done

### Immediate (Next Session)

1. **Decide on the real-world case(s).** CVS Health, or add/replace with other companies? Rick is reconsidering.

2. **Rename "Module" to "Part" across the site.** Decided but still deferred. Propagates from shared.js MODULES array.

3. **Renumber Parts.** With Entity Boundary as its own Part, the simple-case interactive as its own Part, and the reflection pages, the sequence needs to be finalized.

4. **Visual QA on reflect4.html.** The three-column layout, sticky identity bar, and scrollable flow statements box need browser testing. Chrome timed out during this session.

5. **Fill in placeholder URLs** — Accounting Origins project link (module3.html) and Rick's Madoff video interview (reflect3.html).

6. **Review the S&P 500 data question** — price-only vs. total return in reflect3.html chart data.

7. **Add IT vocabulary acknowledgment** — info box in Module 2 (or Module 1) explaining why we borrow terms from software engineering.

### Subsequent

8. **Alternative recognition rules interactive** — show what happens to the IS (but not the CFS) when you change a convention.
9. **Build the real-world case modules** (CVS Health or other).
9. **Refactor index.html** to use shared.css and shared.js.
10. **Build the diagnostic assessment** before Module 4.
11. **Data collection layer** and anonymous student ID system.
12. **Production deployment** with README for adopting instructors.

---

## Open Questions (Updated)

- Which company or companies for the real-world case? CVS Health still? Others?
- Alternative recognition rules: where does it go — inside the simple case, or its own exercise?
- Part renumbering: what is the final sequence?
- Diagnostic before Module 4: what does it assess?
- Module → Part rename: when?

---

## Site File Inventory

```
site/
  index.html              — Landing page (Module 1) with nav, progress, glossary, transcript, Next button
  config.js               — Default configuration (Yale/Rick), with audience field
  shared.css              — All shared styles for module pages
  shared.js               — Glossary (30 terms), nav, progress, accordion, config functions
  setup.html              — Instructor intake agent
  standards-selector.html — Interactive standards review tool
  module-template.html    — Blank template for new module pages
  module2.html            — Module 2: Why Accounting Systems Exist (FULLY DRAFTED)
  reflect2.html           — React reflection page for Module 2 (audience-conditional)
  entity-diagram.html     — The Entity Boundary (OWN PART, React Q&A, stuff/rights/promises reflection)
  module3.html            — Module 3: Worth, Quantification, and Limits (FULLY DRAFTED, 3 sections)
  reflect3.html           — Ponzi scheme staged-reveal reflection (React, 12 stages, 5 prompts, SVG charts)
  module4.html            — Module 4: The Architecture (FULLY DRAFTED, 3 sections + SVG diagram)
  reflect4.html           — The System in Action: A Simple Case (React, 3-column layout, 8 txns, decomposition tracker)
  reflect4-prompts.html   — Pause and Reflect: What the Numbers Tell You Together (4 prompts with context)
  module5.html            — [placeholder — real-world case TBD]
  module6.html            — [placeholder]
  module7.html            — [placeholder]
  module8.html            — Module 8: The Analyst's Toolkit (placeholder)
```

---

## Project Background (Unchanged)

The CMU METALS Capstone Project is a collaboration between Yale SOM (Rick Antle and Stanley Garstka) and Carnegie Mellon University, with Pierre Liang as CMU-side content expert and liaison. The CMU METALS team (four students, including project manager Sarah) brings learning science expertise. Advisors: John Stamper and Eric Harpstead.
