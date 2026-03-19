# Documentation Specification

**Version:** 1.1  
**Date:** December 16, 2025  
**Purpose:** Defines the standard format for all documentation files in the Accounting Origins project

---

## IMPORTANT: Date and Version Reminder

**The current year is 2025.** 

**ALL documentation files MUST include date and version in the header.** This applies to:
- Master project state document
- CurrentState documents for tutorials/components
- Handoff documents
- Specification documents

When creating or updating any document, always verify:
- The "Last Updated" date reflects the actual current date
- The version number is included and incremented appropriately
- Any version history entries use the correct year
- Do not default to 2024 — we are now in 2025

---

## Document Types

### 1. Master Project State Document

**File:** `Accounting-Origins-Project-State.md`

**Required Header:**
```markdown
# Accounting Origins Project — Master State Document

**Last Updated:** [Month Day, Year]  
**Version:** [X.Y]

---
```

**Required Sections:**
1. Project Vision
2. Project Structure (acts, completion status)
3. Conceptual Arc (flow diagrams)
4. Key Insights by Act
5. Characters
6. Consistent Design Patterns
7. Technical Specifications
8. Documentation Standards
9. Historical Fiction Approach
10. Next Development Tasks
11. Contact & Context

**When to Update:**
- When any tutorial is completed
- When an act is completed
- When major design decisions change
- When starting work on a new act

---

### 2. Component CurrentState Documents

**File Naming:** `[Component]-CurrentState.md`

Examples:
- `Tutorial-3-1-CurrentState.md`
- `Act-III-Welcome-CurrentState.md`

**Required Header:**
```markdown
# [Component Name] — Current State

## Status: [Status]

**Last Updated:** [Month Day, Year]  
**Version:** [X.Y]  
**Files Produced:**
- `[filename.jsx]` — [description]
- `[filename.md]` — This document
```

**Status options:**
- `Complete (Ready for Testing)` — Fully implemented, needs testing
- `Complete (Tested)` — Implemented and tested
- `In Progress` — Partially implemented
- `Planned` — Not yet started

**Required Sections:**
1. Title and Status Block (with date/version)
2. Summary
3. Structure
4. Key Design Decisions
5. Interactive Mechanics (tutorials only)
6. Key Dialogue/Narrative Moments
7. Visual Design
8. State Management (tutorials only)
9. Sound Integration (tutorials only)
10. Testing Checklist
11. Glossary Terms
12. Bridge Notes
13. File Manifest
14. Version History

---

### 3. Handoff Documents

**File Naming:** `Handoff-[Component]-[Description].md`

Examples:
- `Handoff-Tutorial-3-1-MerchantsCraft.md`
- `Handoff-Tutorial-2-5-Rebuild.md`

**Required Header:**
```markdown
# Handoff: [Component] — [Description]

**Date:** [Month Day, Year]  
**Session:** [Brief description of work done]

---
```

**Required Sections:**
1. What Was Accomplished
2. Current State
3. Files Modified/Created
4. Known Issues
5. Next Steps
6. Key Decisions Made

---

### 4. Prompt/Specification Documents

**File Naming:** `Prompt-[Component]-[Name].md`

Examples:
- `Prompt-Tutorial-3-1-MerchantsCraft.md`
- `Prompt-Act-II-Welcome.md`

**Required Header:**
```markdown
# [Component Name] — Design Specification

**Version:** [X.Y]  
**Date:** [Month Day, Year]  
**Purpose:** [One-line description]

---
```

---

## Version Numbering

Use semantic versioning:
- **Major version (X.0):** Significant restructuring or redesign
- **Minor version (X.Y):** Feature additions, content changes
- **Increment minor** for each update session
- **Increment major** when structure fundamentally changes

Examples:
- 1.0 → Initial implementation
- 1.1 → Bug fixes, minor additions
- 2.0 → Complete rewrite or major restructuring

---

## Quick Reference: Required Headers

### Project State
```markdown
# Accounting Origins Project — Master State Document

**Last Updated:** December 16, 2025  
**Version:** 2.0

---
```

### CurrentState
```markdown
# [Component Name] — Current State

## Status: Complete (Ready for Testing)

**Last Updated:** December 16, 2025  
**Version:** 1.0  
**Files Produced:**
- `[Component].jsx` — React component (~XXX lines)
- `[Component]-CurrentState.md` — This document
```

### Handoff
```markdown
# Handoff: [Component] — [Description]

**Date:** December 16, 2025  
**Session:** [Brief description]

---
```

### Prompt/Spec
```markdown
# [Component Name] — Design Specification

**Version:** 1.0  
**Date:** December 16, 2025  
**Purpose:** [One-line description]

---
```

---

## Checklist Before Submitting Any Document

- [ ] Header includes **Last Updated** or **Date** field
- [ ] Header includes **Version** field
- [ ] Year is 2025 (not 2024)
- [ ] Version number reflects actual revision count
- [ ] Version History section updated (if applicable)
- [ ] File name follows naming convention
- [ ] All required sections present

---

## Reminders

- **Every document needs a date and version** — no exceptions
- **Year:** The current year is 2025. Double-check all dates.
- **Encoding:** Use proper UTF-8 characters (em-dashes —, not --)
- **Consistency:** Follow terminology from `Accounting-Origins-Project-State.md`
- **Updates:** When modifying any document, update its date and increment the version
