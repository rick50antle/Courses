# Mobile Usability Analysis
## Accounting Origins Tutorials

**Version:** 1.0  
**Date:** 2025-12-16

---

## Executive Summary

I analyzed all 16 uploaded tutorial files for mobile usability. The tutorials are generally well-structured but have several patterns that will cause problems on smartphones (320-375px width). The most significant issues are:

1. **Drag-and-drop interactions** — Don't work reliably on touch devices
2. **Small input widths** — Hard to tap accurately on phone
3. **Side-by-side layouts** — Cause horizontal scrolling or cramping
4. **Hover-dependent UI** — Invisible on touch devices

Below are specific findings and recommended fixes.

---

## Issue Inventory by Tutorial

### Act I

| Tutorial | Issue | Severity | Description |
|----------|-------|----------|-------------|
| T1-1 | Location grid | Medium | 6 location buttons in 2-column grid may be cramped |
| T1-1 | Travel log | Low | Works but dense on small screens |
| T1-2 | Negotiation input | High | Likely uses slider or small inputs |
| T1-3 | Market observation | Medium | Side-by-side trader display |
| T1-4 | Gap calculator | High | Two side-by-side number inputs, small width |
| T1-4 | Numeraire table | Medium | Table layout may not fit |
| Review | Text answers | Low | Works well, full-width textarea |

### Act II

| Tutorial | Issue | Severity | Description |
|----------|-------|----------|-------------|
| T2-1 | Drag-and-drop tablets | **Critical** | Core mechanic fails on mobile |
| T2-1 | Interactive tablet | High | Drop zones too small for touch |
| T2-2 | Official cards | Medium | Grid layout may cramp |
| T2-2 | Calculation input | Low | Single number, should work |
| T2-3 | Taxpayer tablets reveal | Medium | Click-to-reveal buttons |
| T2-3 | Running total | Low | Display only |
| T2-4 | Central hall diagram | High | Complex layout with arrows |
| T2-4 | Side-by-side tablets | High | Won't fit at 320px |
| T2-5 | TAccountTablet | Medium | Two-column internal layout |
| T2-5 | Multiple tablets | High | Side-by-side comparison |
| T2-6 | Calculator blocks | High | Input + button side-by-side |
| T2-6 | Comparison tables | Medium | May need horizontal scroll |

---

## Critical Issues (Must Fix)

### 1. Drag-and-Drop in Tutorial 2-1

**Current Implementation:**
```jsx
// From Tutorial-2-1-Final.jsx, around line 370
const InteractiveTablet = ({ entries, dragOver, onDrop, isNewTablet }) => {
  const handleDragOver = (e, side) => {
    e.preventDefault();
    if (isNewTablet) {
      setNewDraggedOver(side);
    } else {
      setDraggedOver(side);
    }
  };
  // ... drag events
```

**Problem:** Drag events don't fire reliably on mobile. The `dragstart`, `dragover`, and `drop` events are desktop-only.

**Recommended Fix — Tap-to-Place Pattern:**
```jsx
// Add state for current selection
const [selectedTransaction, setSelectedTransaction] = useState(null);

// Transaction card becomes tappable
const TransactionCard = ({ transaction, index }) => (
  <button
    onClick={() => setSelectedTransaction(index)}
    className={`w-full p-3 rounded-lg border text-left ${
      selectedTransaction === index ? 'ring-2 ring-blue-500' : ''
    }`}
  >
    {transaction.text}
  </button>
);

// Drop zones become tappable targets
const DropZone = ({ side, label }) => (
  <button
    onClick={() => {
      if (selectedTransaction !== null) {
        handlePlacement(selectedTransaction, side);
        setSelectedTransaction(null);
      }
    }}
    disabled={selectedTransaction === null}
    className={`w-full p-4 rounded-lg border-2 border-dashed ${
      selectedTransaction !== null ? 'border-blue-500 bg-blue-50' : 'border-gray-300'
    }`}
  >
    {selectedTransaction !== null ? `Tap to place in ${label}` : label}
  </button>
);
```

### 2. Gap Calculator in Tutorial 1-4

**Current Implementation:**
```jsx
// From Tutorial-1-4-Final.jsx, around line 489
<div className="flex items-center gap-2 flex-wrap">
  <span className="text-sm text-gray-600">{giveLabel}</span>
  <input 
    type="number" 
    value={giveVal}
    className="w-16 p-2 border rounded text-center font-bold"
  />
  <span className="text-sm text-gray-600">barley</span>
</div>
```

**Problem:** `w-16` (64px) is too narrow for touch. Combined with surrounding text, creates cramped layout.

**Recommended Fix:**
```jsx
<div className="space-y-3">
  {/* Stack vertically instead of inline */}
  <div>
    <label className="block text-sm font-medium mb-1" style={{ color: colors.earthDark }}>
      {giveLabel}
    </label>
    <div className="flex items-center gap-2">
      <input 
        type="text"
        inputMode="numeric"
        pattern="[0-9]*"
        value={giveVal}
        onChange={(e) => setGiveVal(e.target.value)}
        className="w-24 p-3 border rounded text-center font-mono text-lg"
        style={{ borderColor: colors.earthLight }}
        placeholder="?"
      />
      <span className="text-sm" style={{ color: colors.earth }}>barley</span>
    </div>
  </div>
  
  <div>
    <label className="block text-sm font-medium mb-1" style={{ color: colors.earthDark }}>
      {receiveLabel}
    </label>
    <div className="flex items-center gap-2">
      <input 
        type="text"
        inputMode="numeric"
        pattern="[0-9]*"
        value={receiveVal}
        onChange={(e) => setReceiveVal(e.target.value)}
        className="w-24 p-3 border rounded text-center font-mono text-lg"
        style={{ borderColor: colors.earthLight }}
        placeholder="?"
      />
      <span className="text-sm" style={{ color: colors.earth }}>barley</span>
    </div>
  </div>
</div>
```

### 3. Side-by-Side Tablets in Tutorials 2-4, 2-5

**Current Implementation:**
```jsx
<div className="grid grid-cols-2 gap-4">
  <TAccountTablet title="GRANARY" ... />
  <TAccountTablet title="CONSTRUCTION" ... />
</div>
```

**Problem:** At 320px, each tablet gets ~140px width. TAccountTablet has two internal columns, so each gets ~60px. Text truncates or overflows.

**Recommended Fix:**
```jsx
{/* Stack on mobile, side-by-side on desktop */}
<div className="space-y-4 md:space-y-0 md:grid md:grid-cols-2 md:gap-4">
  <TAccountTablet title="GRANARY" ... />
  <TAccountTablet title="CONSTRUCTION" ... />
</div>
```

Or for comparison views, use a tabbed interface:
```jsx
const [activeTablet, setActiveTablet] = useState('granary');

<div className="md:hidden">
  {/* Mobile: tabs */}
  <div className="flex gap-2 mb-4">
    <button
      onClick={() => setActiveTablet('granary')}
      className={`flex-1 py-2 rounded ${activeTablet === 'granary' ? 'bg-primary text-white' : 'bg-gray-100'}`}
    >
      Granary
    </button>
    <button
      onClick={() => setActiveTablet('construction')}
      className={`flex-1 py-2 rounded ${activeTablet === 'construction' ? 'bg-primary text-white' : 'bg-gray-100'}`}
    >
      Construction
    </button>
  </div>
  {activeTablet === 'granary' && <TAccountTablet title="GRANARY" ... />}
  {activeTablet === 'construction' && <TAccountTablet title="CONSTRUCTION" ... />}
</div>

<div className="hidden md:grid md:grid-cols-2 md:gap-4">
  {/* Desktop: side-by-side */}
  <TAccountTablet title="GRANARY" ... />
  <TAccountTablet title="CONSTRUCTION" ... />
</div>
```

---

## Medium Issues (Should Fix)

### 4. Input + Button Side-by-Side

**Current Pattern (multiple tutorials):**
```jsx
<div className="flex gap-2">
  <input className="flex-1 p-2 ..." />
  <button className="px-4 py-2 ...">Check</button>
</div>
```

**Problem:** On narrow screens, input shrinks too much.

**Recommended Fix:**
```jsx
<div className="space-y-2">
  <input className="w-full p-3 text-lg ..." />
  <button className="w-full py-3 ...">Check</button>
</div>
```

### 5. Diagrams with Arrows (T2-4)

**Current:** Uses positioned elements and arrow icons to show flows between departments.

**Problem:** Fixed positioning breaks on narrow screens.

**Recommended Fix:** Use a simplified mobile layout:
```jsx
<div className="md:hidden space-y-4">
  {/* Mobile: vertical flow */}
  <div className="p-3 rounded bg-gray-100 text-center">Tax Section</div>
  <div className="text-center text-2xl">↓</div>
  <div className="p-3 rounded bg-gray-100 text-center">Granary Section</div>
</div>

<div className="hidden md:block">
  {/* Desktop: original complex diagram */}
  <CentralRecordHallDiagram />
</div>
```

### 6. Tables in Tutorial 1-4

**Current:** Standard HTML table for numeraire values.

**Problem:** Tables don't wrap on mobile.

**Recommended Fix — Card Layout:**
```jsx
{/* Mobile: card layout */}
<div className="md:hidden space-y-2">
  {items.map((item, i) => (
    <div key={i} className="flex justify-between p-3 rounded border">
      <span className="flex items-center gap-2">
        {item.icon} {item.name}
      </span>
      <span className="font-mono font-bold">{item.value} barley</span>
    </div>
  ))}
</div>

{/* Desktop: table */}
<div className="hidden md:block">
  <table className="w-full">...</table>
</div>
```

---

## Low Priority Issues (Nice to Fix)

### 7. Dense Travel Log (T1-1)

The travel log displays location visits. On mobile, this can get long but remains usable since it's a scrollable list.

**Optional improvement:** Collapsible sections or summary counts.

### 8. Character Avatars/Icons

Some tutorials show character icons in small circles. Ensure minimum 32px diameter.

---

## General Mobile Patterns to Adopt

### Input Pattern Standard

```jsx
// Standard numeric input for all tutorials
const NumericInput = ({ value, onChange, placeholder = "?", disabled }) => (
  <input
    type="text"
    inputMode="numeric"
    pattern="[0-9]*"
    value={value}
    onChange={(e) => onChange(e.target.value)}
    disabled={disabled}
    placeholder={placeholder}
    className="w-24 p-3 border rounded text-center font-mono text-lg"
    style={{ 
      borderColor: colors.earthLight,
      minHeight: '48px'  // Touch target
    }}
  />
);
```

### Responsive Container

```jsx
// Standard page container
<div className="min-h-screen" style={{ background: `linear-gradient(...)` }}>
  <Header />
  <div className="p-4 md:p-6 max-w-2xl mx-auto">
    {/* Content */}
  </div>
</div>
```

### Responsive Spacing

```jsx
// Use responsive classes consistently
<div className="space-y-3 md:space-y-4">
<div className="p-3 md:p-4">
<div className="text-sm md:text-base">
```

---

## Recommended Testing Procedure

### Before Each Tutorial Release

1. **Chrome DevTools Mobile Mode**
   - Test at: iPhone SE (320px), iPhone 12 Pro (390px), iPad (768px)
   - Check for horizontal overflow
   - Verify all buttons are tappable

2. **Touch Interaction Simulation**
   - Click all interactive elements
   - Verify no hover-dependent features
   - Test input focus and keyboard appearance

3. **Physical Device Test**
   - Test on actual iPhone and Android
   - Pay attention to keyboard behavior
   - Check input zoom (iOS zooms if font < 16px)

### Quick Checklist

```
[ ] All inputs have inputMode="numeric" for numbers
[ ] All touch targets ≥ 44px
[ ] No side-by-side layouts under 768px
[ ] Tables have card fallback on mobile
[ ] Drag-drop has tap fallback
[ ] Diagrams have simplified mobile version
[ ] Input font size ≥ 16px
[ ] No hover-only interactions
```

---

## Prioritized Fix List

**Phase 1 — Critical (before any mobile use)**
1. Tutorial 2-1: Add tap-to-place for drag-drop
2. Tutorial 2-4/2-5: Stack tablets vertically on mobile

**Phase 2 — High (improves experience significantly)**
3. Tutorial 1-4: Widen calculator inputs, stack vertically
4. Tutorial 2-6: Stack calculation blocks
5. All tutorials: Standardize input widths to w-24 minimum

**Phase 3 — Medium (polish)**
6. Tutorial 2-4: Simplify flow diagrams for mobile
7. Tutorial 1-4: Add card layout for numeraire table
8. All tutorials: Verify 44px touch targets

**Phase 4 — Low (nice to have)**
9. Tutorial 1-1: Optimize travel log density
10. Add collapsible sections for long content

---

## Questions for Discussion

1. **Drag-drop in T2-1**: This is a core pedagogical mechanic (placing entries on tablets). Should we:
   - Replace entirely with tap-to-select?
   - Keep drag for desktop, add tap for mobile?
   - Redesign the interaction completely?

2. **Side-by-side tablets**: The comparison view is important for showing how double-entry works. Should we:
   - Use tabs on mobile?
   - Use a swipe gesture?
   - Accept that tablets stack and lose simultaneous view?

3. **Testing approach**: Do you have access to physical devices for testing, or should we rely on browser emulation?

4. **Priority**: Should we fix existing tutorials before building new ones, or document standards and apply to new development first?

---

**Version:** 1.0  
**Date:** 2025-12-16
