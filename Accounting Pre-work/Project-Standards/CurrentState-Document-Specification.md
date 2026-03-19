# CurrentState Document Specification

**Version:** 1.1  
**Date:** December 18, 2025  
**Purpose:** Defines the standard format for all CurrentState documentation files in the Accounting Origins project

---

## IMPORTANT: Date Reminder

**The current year is 2025.** 

When creating or updating CurrentState documents, always verify:
- The "Last Updated" date reflects the actual current date
- Any version history entries use the correct year
- Do not default to 2024 — we are now in 2025

---

## File Naming Convention

```
[Component]-CurrentState.md
```

Examples:
- `Tutorial-3-1-CurrentState.md`
- `Act-III-Welcome-CurrentState.md`
- `Act-II-Review-CurrentState.md`

---

## Required Sections

Every CurrentState document must include these sections in this order:

### 1. Title and Status Block

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

---

### 2. Summary

A 2-4 sentence overview of what the component does and its role in the project.

```markdown
---

## Summary

[Brief description of what this component does, its pedagogical purpose, and where it fits in the project arc.]
```

---

### 3. Structure

A table or list showing the component's organization (phases, sections, screens).

```markdown
---

## Structure

| Phase/Section | Name | Purpose |
|---------------|------|---------|
| 1 | [Name] | [Purpose] |
| 2 | [Name] | [Purpose] |
...
```

For tutorials, include estimated duration and total phase count.

---

### 4. Key Design Decisions

Numbered list of important design choices and their rationale.

```markdown
---

## Key Design Decisions

### 1. [Decision Title]

[Explanation of the decision and why it was made]

### 2. [Decision Title]

[Explanation]
```

---

### 5. Interactive Mechanics (Tutorials Only)

For tutorials, document each interactive element:

```markdown
---

## Interactive Mechanics

### Q1: [Question Topic] (Phase X)
- **Type:** [Text input / Numeric input / Multiple choice / Drag-drop / etc.]
- **Question:** "[Exact question text]"
- **Keywords/Answer:** [Accepted answers or keywords]
- **Three strikes with hints**

### Q2: [Question Topic] (Phase X)
...
```

---

### 6. Key Dialogue/Narrative Moments

Important quotes that capture core insights:

```markdown
---

## Key Dialogue Moments

### [Character]'s [moment]
> "[Quote]"

### [Insight name]
> "[Quote]"
```

---

### 7. Visual Design

Document any component-specific visual elements:

```markdown
---

## Visual Design

### Color Palette
[Note if standard palette or any variations]

### Key Components
- **[ComponentName]** — [Description]
...
```

---

### 8. State Management (Tutorials Only)

```markdown
---

## State Management

```javascript
// Phase control
phase: string

// Question state
q1Answer: string
q1Attempts: number (0-3)
q1Submitted: boolean

// UI state
showGlossary: boolean
devMode: boolean
headerClickCount: number
```
```

---

### 9. Sound Integration (Tutorials Only)

```markdown
---

## Sound Integration

| Interaction | Sound |
|-------------|-------|
| Correct answer | `playSuccessTone()` |
| Wrong (attempt 1-2) | `playSoftNope()` |
| Wrong (attempt 3) | `playBuzzer()` |
| Continue buttons | `playContinueClick()` |
```

---

### 10. Testing Checklist

Comprehensive checklist for QA:

```markdown
---

## Testing Checklist

### Phase 1: [Name]
- [ ] [Test item]
- [ ] [Test item]

### Phase 2: [Name]
- [ ] [Test item]
...

### General
- [ ] All Continue buttons play click sound
- [ ] Restart button resets all state
- [ ] Glossary button opens modal
- [ ] Dev mode activates on triple-click of header
- [ ] Dev mode phase-skip buttons work correctly
- [ ] Historical Liberties note is collapsible (welcome screen)
- [ ] Progress bar updates correctly
- [ ] No character encoding issues
- [ ] Mobile responsive (test at 320px width)
```

---

### 11. Glossary Terms

```markdown
---

## Glossary Terms

| Term | Definition |
|------|------------|
| [Term] | [Definition] |
...
```

---

### 12. Bridge Notes (Where Applicable)

For components that connect to others:

```markdown
---

## Bridge Notes

### From [Previous Component]
[What students bring from the previous component]

### To [Next Component]
[What this component sets up for the next]
```

---

### 13. File Manifest

```markdown
---

## File Manifest

| File | Description |
|------|-------------|
| `[filename]` | [Description] |
...
```

---

## Optional Sections

Include when relevant:

### Historical Notes
For components with historical content, document accuracy vs. pedagogical fiction.

### Version History
For components with significant revisions:

```markdown
---

## Version History

| Version | Date | Changes |
|---------|------|---------|
| 1.0 | December 16, 2025 | Initial implementation |
| 1.1 | [Date] | [Changes] |
```

---

## Section Order Summary

1. Title and Status Block
2. Summary
3. Structure
4. Key Design Decisions
5. Interactive Mechanics (tutorials)
6. Key Dialogue/Narrative Moments
7. Visual Design
8. State Management (tutorials)
9. Sound Integration (tutorials)
10. Testing Checklist
11. Glossary Terms
12. Bridge Notes
13. File Manifest
14. Historical Notes (optional)
15. Version History (optional)

---

## Quick Reference: Status Block Template

Copy and adapt this for new CurrentState documents:

```markdown
# [Component Name] — Current State

## Status: Complete (Ready for Testing)

**Last Updated:** December 18, 2025  
**Version:** 1.0  
**Files Produced:**
- `[Component].jsx` — React component (~XXX lines)
- `[Component]-CurrentState.md` — This document

---

## Summary

[2-4 sentence description]
```

---

## Reminders

- **Year:** The current year is 2025. Double-check all dates.
- **Encoding:** Use proper UTF-8 characters (em-dashes —, not --)
- **Consistency:** Follow terminology from `Accounting-Origins-Project-State.md`
- **Completeness:** Every checkbox in Testing Checklist should be testable
- **Updates:** When modifying a component, update its CurrentState doc and increment the version
- **Dev Mode:** Every tutorial must support dev mode (triple-click header to activate, phase-skip buttons when active)

---

## Version History

| Version | Date | Changes |
|---------|------|---------|
| 1.0 | December 16, 2025 | Initial specification |
| 1.1 | December 18, 2025 | Added dev mode items to testing checklist; added devMode to state management example; added dev mode reminder |
