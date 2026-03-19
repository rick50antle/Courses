# Tutorial Development Standards
## Accounting Origins Project

**Version:** 2.0
**Date:** February 8, 2026

This document defines standards for developing tutorials in the Accounting Origins project. Read this document before coding any new tutorial.

---

## Table of Contents

1. [Project Structure](#project-structure)
2. [Color Palette](#color-palette)
3. [Component Architecture](#component-architecture)
4. [Header with Progress Bar](#header-with-progress-bar)
5. [Historical Liberties Note](#historical-liberties-note)
6. [Complete Screen Structure](#complete-screen-structure)
7. [Input Components](#input-components)
8. [Answer Evaluation](#answer-evaluation)
9. [Sound Feedback](#sound-feedback)
10. [Tablet Display Format](#tablet-display-format)
11. [Mobile Responsiveness](#mobile-responsiveness)
12. [State Management](#state-management)
13. [Naming Conventions](#naming-conventions)
14. [Terminology Guidelines](#terminology-guidelines)
15. [Common Components](#common-components)
16. [Accessibility](#accessibility)
17. [Testing Checklist](#testing-checklist)

---

## Project Structure

### File Format

**REQUIRED: All tutorials must be standalone HTML files.** Each tutorial is a single `.html` file that includes all CSS, JavaScript, and React code inline. Tutorials use React 18 via CDN with Babel standalone for in-browser JSX transpilation. No build tools or development server required — files open directly in any modern browser.

### File Naming
```
NFP-Tutorial-1-Financial-Position.html
NFP-Tutorial-2-Net-Asset-Categories.html
NFP-Tutorial-3-Statement-of-Activities.html
NFP-Tutorial-4-Cash-Flows.html
NFP-Tutorial-5-Liquidity-and-Expenses.html
NFP-Tutorial-6-Putting-It-Together.html
```

For Accounting Origins tutorials:
```
tutorial-1-4.html           # Lowercase with hyphens
act-i-welcome.html
```

### HTML File Structure

Each tutorial HTML file must include:
1. `<!DOCTYPE html>` declaration
2. `<meta charset="UTF-8">` and `<meta name="viewport">` tags
3. Google Fonts import for Inter
4. React 18 and ReactDOM via CDN (`https://unpkg.com/react@18/umd/react.production.min.js`)
5. Babel standalone (`https://unpkg.com/@babel/standalone/babel.min.js`)
6. All CSS in a `<style>` tag
7. All React/JSX code in a `<script type="text/babel">` tag
8. Icons as unicode characters (no lucide-react dependency)

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Tutorial Title - NFP Financial Literacy</title>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    <style>
        /* All CSS here */
    </style>
</head>
<body>
    <div id="root"></div>
    <script src="https://unpkg.com/react@18/umd/react.production.min.js"></script>
    <script src="https://unpkg.com/react-dom@18/umd/react-dom.production.min.js"></script>
    <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
    <script type="text/babel">
        const { useState } = React;
        // React component code here
        const root = ReactDOM.createRoot(document.getElementById('root'));
        root.render(<TutorialComponent />);
    </script>
</body>
</html>
```

### Icon Replacements (No External Icon Libraries)

Since tutorials are standalone HTML, use unicode characters instead of lucide-react:

| Icon | Unicode |
|------|---------|
| BookOpen | 📖 |
| RotateCcw/RefreshCw | ↺ |
| ArrowRight/ChevronRight | → |
| Trophy/Award | 🏆 |
| Volume2 | 🔊 |
| VolumeX | 🔇 |
| Star | ⭐ |
| X | ✕ |
| HelpCircle | ❓ |
| Eye | 👁 |
| Lightbulb | 💡 |
| CheckCircle | ✓ |
| AlertTriangle | ⚠ |
| ChevronDown | ▼ |
| ChevronUp | ▲ |

---

## Color Palette

**STANDARD COLORS — Use this exact object in every tutorial:**

```jsx
const colors = {
  // Primary
  primary: '#00356b',       // Yale Blue — headers, buttons, emphasis
  
  // Earth tones (historical/narrative feel)
  sand: '#f5f1e8',          // Background, narrative blocks
  earth: '#8b7355',         // Secondary text, borders
  earthLight: '#d4c4a8',    // Light borders, dividers
  earthDark: '#5c4d3d',     // Dark text on light backgrounds
  accent: '#c9a227',        // Gold — callouts, narrative borders
  
  // Clay tones (tablets)
  clay: '#c4a574',          // Tablet background
  clayLight: '#e8dcc8',     // Tablet header, light areas
  clayDark: '#a08050',      // Tablet borders
  
  // Feedback
  success: '#22c55e',       // Correct answers
  successBg: '#f0fdf4',     // Success panel background
  warning: '#f59e0b',       // Hints, partial answers
  warningBg: '#fffbeb',     // Warning panel background
  error: '#dc2626',         // Wrong answers (3rd strike)
  errorBg: '#fef2f2',       // Error panel background
  
  // Optional (used in some tutorials)
  profit: '#16a34a',        // Financial gains
  loss: '#dc2626',          // Financial losses
  royal: '#7c3aed',         // Royal/king's scenes
  royalBg: '#f5f3ff'        // Royal background
};
```

---

## Component Architecture

### Version Comment Block

**REQUIRED:** Every tutorial file must include a version comment block inside the `<script type="text/babel">` tag:

```jsx
/**
 * Tutorial 2.1: The Scribe's Craft
 * Accounting Origins Project
 *
 * @version 1.0
 * @date 2025-12-16
 * @description Introduction to T-account mechanics through tablet recording
 */

const { useState } = React;
```

Update the version number and date whenever significant changes are made.

### Phase-Based Structure
Tutorials use a phase-based approach:

```jsx
const [phase, setPhase] = useState('welcome');
// Typical phases: 'welcome', 'phase1', 'phase2', ..., 'coda', 'complete'

// Render based on phase
if (phase === 'welcome') return renderWelcome();
if (phase === 'phase1') return renderPhase1();
// etc.
```

### React Hooks (Standalone HTML)
Since tutorials use React via CDN (not ES modules), hooks are accessed from the global `React` object:
```jsx
const { useState, useEffect } = React;
```

**Do NOT use `import` statements** — React and ReactDOM are loaded as UMD scripts and available globally.

---

## Header with Progress Bar

**REQUIRED:** Every tutorial must use a consistent header with progress bar. This header should appear on ALL phases, including the welcome screen.

### Progress Calculation

```jsx
// Define phase order for progress calculation
const phaseOrder = ['welcome', 'phase1', 'phase2', ..., 'complete'];
const currentPhaseIndex = phaseOrder.indexOf(phase);
const progress = Math.round((currentPhaseIndex / (phaseOrder.length - 1)) * 100);
```

### Standard Header Component

```jsx
const HeaderWithControls = () => (
  <div 
    className="rounded-lg p-4 mb-4"
    style={{ backgroundColor: colors.primary }}
  >
    <div className="flex justify-between items-start">
      <div onClick={handleHeaderClick} style={{ cursor: 'pointer' }}>
        <div className="flex items-center gap-2">
          <MapPin className="w-4 h-4 text-white" />
          <h1 className="text-lg font-bold text-white">Tutorial X.X: Title</h1>
        </div>
        <p className="text-sm mt-1" style={{ color: colors.earthLight }}>
          Setting, ~Date • ~XX min
        </p>
      </div>
      <div className="flex items-center gap-2">
        <button
          onClick={() => setShowGlossary(true)}
          className="p-2 rounded-lg hover:bg-white/10"
          title="Glossary"
        >
          <Book className="w-5 h-5 text-white" />
        </button>
        <button
          onClick={handleRestart}
          className="p-2 rounded-lg hover:bg-white/10"
          title="Restart tutorial"
        >
          <RefreshCw className="w-5 h-5 text-white" />
        </button>
      </div>
    </div>
    
    {/* Progress bar */}
    <div className="mt-4">
      <div className="flex justify-between text-xs text-white/70 mb-1">
        <span>Progress</span>
        <span>{progress}%</span>
      </div>
      <div className="h-2 rounded-full" style={{ backgroundColor: 'rgba(255,255,255,0.2)' }}>
        <div 
          className="h-full rounded-full transition-all duration-500"
          style={{ width: `${progress}%`, backgroundColor: colors.accent }}
        />
      </div>
    </div>
    
    {/* Dev mode controls (optional, shown when devMode is true) */}
    {devMode && (
      <div className="mt-3 pt-3 border-t border-white/20">
        <p className="text-xs text-white/70 mb-2">Dev Mode: Skip to phase</p>
        <div className="flex flex-wrap gap-1">
          {phaseOrder.map(p => (
            <button
              key={p}
              onClick={() => { setStep(0); setPhase(p); }}
              className={`px-2 py-1 rounded text-xs ${phase === p ? 'bg-white text-blue-900' : 'bg-white/20 text-white'}`}
            >
              {p.split('-')[0]}
            </button>
          ))}
        </div>
      </div>
    )}
  </div>
);
```

### Dev Mode Toggle

Dev mode is activated by triple-clicking the header title area:

```jsx
const [devMode, setDevMode] = useState(false);
const [headerClickCount, setHeaderClickCount] = useState(0);

const handleHeaderClick = () => {
  const newCount = headerClickCount + 1;
  setHeaderClickCount(newCount);
  if (newCount >= 3) {
    setDevMode(!devMode);
    setHeaderClickCount(0);
  }
};
```

---

## Historical Liberties Note

**REQUIRED:** Every tutorial must include a collapsible "Note on Historical Liberties" section. This note:

1. **Appears on the welcome screen only**
2. **Is placed at the bottom of the welcome content**, just above the "Continue" or "Begin" button
3. **Contains content specific to that tutorial** — do NOT copy the same text across tutorials

### Component Structure

```jsx
const HistoricalNote = () => (
  <div className="mb-4">
    <button
      onClick={() => setShowHistoricalNote(!showHistoricalNote)}
      className="w-full flex items-center justify-between p-3 rounded-lg text-sm"
      style={{ backgroundColor: colors.clayLight, color: colors.earthDark }}
    >
      <div className="flex items-center gap-2">
        <Info className="w-4 h-4" />
        <span className="font-medium">A Note on Historical Liberties</span>
      </div>
      {showHistoricalNote ? <ChevronUp className="w-4 h-4" /> : <ChevronDown className="w-4 h-4" />}
    </button>
    
    {showHistoricalNote && (
      <div 
        className="mt-2 p-4 rounded-lg text-sm border"
        style={{ backgroundColor: 'white', borderColor: colors.earthLight, color: colors.earthDark }}
      >
        {/* CONTENT VARIES BY TUTORIAL — see examples below */}
        <p className="mb-3">
          [First paragraph: What historical liberty is being taken]
        </p>
        <p className="mb-3">
          [Second paragraph: Why we're doing it this way]
        </p>
        <p className="italic">
          This is historical fiction in service of teaching accounting concepts.
        </p>
      </div>
    )}
  </div>
);
```

### State Required

```jsx
const [showHistoricalNote, setShowHistoricalNote] = useState(false);
```

### Placement in Welcome Screen

```jsx
const renderWelcome = () => (
  <div className="min-h-screen" style={{ backgroundColor: colors.sand }}>
    <HeaderWithControls />
    <div className="p-4 max-w-2xl mx-auto">
      
      {/* Narrative content */}
      <NarrativeBlock>...</NarrativeBlock>
      
      {/* "In This Tutorial" box */}
      <div className="p-4 rounded-lg border-2 mb-4" style={{ ... }}>
        ...
      </div>
      
      {/* Historical Note — ALWAYS just before Continue button */}
      <HistoricalNote />
      
      {/* Continue button */}
      <ContinueButton onClick={() => { setStep(0); setPhase('next-phase'); }}>
        Begin Tutorial
      </ContinueButton>
      
    </div>
  </div>
);
```

### Content Examples by Act/Tutorial

#### Act I (Pre-urban river valley, ~3500 BCE)
```
This tutorial takes creative liberties with prehistoric trade. We have no written 
records from this period—writing had not yet been invented. The specific scenarios, 
characters, and trade goods are imagined to illustrate economic concepts that would 
have applied to early agricultural communities.

We use this setting to help you experience the information problems that existed 
before markets and record-keeping emerged.
```

#### Act II (Babylon, ~1800 BCE)
```
While Babylonian scribes did keep detailed records on clay tablets, the specific 
scenarios and characters in this tutorial are fictional. The tablet formats shown 
are simplified for teaching purposes—actual cuneiform records were more complex.

We use authentic Babylonian names and institutions to create immersion while teaching 
fundamental accounting concepts.
```

#### Act III (Sardis, ~550 BCE)
```
There is no evidence that Lydian merchants used clay tablets like the Babylonians—
Lydians may have used other recording methods (wax tablets, papyrus, or oral 
agreements) that have not survived.

We employ the familiar clay tablet format to maintain pedagogical continuity with 
Acts I and II, allowing you to apply skills you've already learned to a new context.
```

#### Act IV (Venice, ~1494 CE)
```
While Luca Pacioli did document double-entry bookkeeping in 1494, the specific 
merchants and transactions in this tutorial are fictional. The method itself was 
already in use by Italian merchants before Pacioli's famous treatise.

We use this setting to show how the concepts you've learned culminate in the formal 
accounting system still used today.
```

### Key Requirements

1. **Collapsible by default** — Students can skip it if they wish
2. **Content is tutorial-specific** — Address the specific historical liberties taken
3. **Always ends with** — "This is historical fiction in service of teaching accounting concepts."
4. **Placed consistently** — Bottom of welcome content, above Continue button

---

## Complete Screen Structure

**REQUIRED:** Every tutorial must have a consistent Complete screen with these elements in order:

### Structure

```jsx
const renderComplete = () => (
  <div className="min-h-screen" style={{ backgroundColor: colors.sand }}>
    <div className="p-4 max-w-2xl mx-auto">
      <Header />
      
      {/* 1. Trophy/Success indicator */}
      <div className="text-center mb-6">
        <div 
          className="inline-flex items-center justify-center w-20 h-20 rounded-full mb-4"
          style={{ backgroundColor: colors.accent }}
        >
          <Trophy className="w-8 h-8 text-white" />
        </div>
        <h2 className="text-2xl font-bold" style={{ color: colors.primary }}>
          Tutorial Complete!
        </h2>
      </div>
      
      {/* 2. What You Discovered */}
      <div 
        className="rounded-lg p-4 mb-4 border-2"
        style={{ backgroundColor: 'white', borderColor: colors.success }}
      >
        <h3 className="font-bold mb-3" style={{ color: colors.primary }}>What You Discovered</h3>
        <ol className="space-y-2 text-sm" style={{ color: colors.earthDark }}>
          <li className="flex gap-2">
            <span style={{ color: colors.success }}>✓</span>
            [Key insight 1]
          </li>
          <li className="flex gap-2">
            <span style={{ color: colors.success }}>✓</span>
            [Key insight 2]
          </li>
          {/* ... more insights */}
        </ol>
      </div>
      
      {/* 3. The Deeper Point (optional but recommended) */}
      <KeyInsightBox>
        <p className="font-semibold mb-2">The Deeper Point</p>
        <p>[Synthesis of the core lesson]</p>
      </KeyInsightBox>
      
      {/* 4. Coming Next */}
      <div 
        className="rounded-lg p-4 mb-4"
        style={{ backgroundColor: colors.clayLight }}
      >
        <h3 className="font-bold mb-2" style={{ color: colors.primary }}>Coming Next</h3>
        <p className="text-sm" style={{ color: colors.earthDark }}>
          [Bridge to next tutorial]
        </p>
        <p className="font-bold mt-2" style={{ color: colors.primary }}>
          Next: Tutorial X.X — [Title]
        </p>
      </div>
      
      {/* 5. Next Tutorial Button */}
      <button
        onClick={() => { playContinueClick(); window.location.href = '[NEXT_TUTORIAL_URL]'; }}
        className="w-full py-3 rounded-lg font-bold text-white flex items-center justify-center gap-2 mb-3"
        style={{ backgroundColor: colors.primary }}
      >
        Next Tutorial <ChevronRight className="w-5 h-5" />
      </button>
      
      {/* 6. Restart Button */}
      <button
        onClick={handleRestart}
        className="w-full py-3 rounded-lg font-bold border-2 flex items-center justify-center gap-2 hover:bg-gray-50"
        style={{ borderColor: colors.primary, color: colors.primary }}
      >
        <RefreshCw className="w-5 h-5" /> Restart Tutorial
      </button>
      
    </div>
  </div>
);
```

### Complete Screen Elements

| Element | Required | Description |
|---------|----------|-------------|
| Trophy/Success | Yes | Visual celebration of completion |
| What You Discovered | Yes | Bulleted list of key insights with checkmarks |
| The Deeper Point | Recommended | Synthesis box highlighting core lesson |
| Coming Next | Yes | Bridge text and title of next tutorial |
| Next Tutorial Button | Yes | Primary button linking to next tutorial |
| Restart Button | Yes | Secondary button to replay current tutorial |

### Next Tutorial Button

The Next Tutorial button should:
- Use primary button styling (solid background)
- Include ChevronRight icon
- Play continue click sound on click
- Navigate to the next tutorial URL

```jsx
{/* Next Tutorial Button */}
<button
  onClick={() => { playContinueClick(); window.location.href = '[NEXT_TUTORIAL_URL]'; }}
  className="w-full py-3 rounded-lg font-bold text-white flex items-center justify-center gap-2 mb-3"
  style={{ backgroundColor: colors.primary }}
>
  Next Tutorial <ChevronRight className="w-5 h-5" />
</button>
```

**Note:** When building a tutorial before the next one exists, use a placeholder:
```jsx
onClick={() => { playContinueClick(); /* Link will be added later */ }}
```

---

## Input Components

### STANDARD: Numeric Input (Preferred)

**Always use simple text/number input for numeric answers. No sliders.**

**REQUIRED:** The Enter key must submit the answer, in addition to clicking the Check button.

```jsx
// Standard numeric input with submit button
<div className="flex gap-2 items-center">
  <input
    type="text"                    // Use "text" not "number" for better mobile control
    inputMode="numeric"            // Shows numeric keyboard on mobile
    pattern="[0-9]*"               // Validates numeric input
    value={answer}
    onChange={(e) => setAnswer(e.target.value)}
    onKeyDown={(e) => { if (e.key === 'Enter' && !submitted) handleSubmit(); }}
    disabled={submitted}
    placeholder="?"
    className="w-20 p-2 border rounded text-center font-mono text-lg"
    style={{ borderColor: colors.earthLight }}
  />
  {!submitted && (
    <button
      onClick={handleSubmit}
      className="px-4 py-2 rounded font-bold text-white"
      style={{ backgroundColor: colors.primary }}
    >
      Check
    </button>
  )}
</div>
```

**Mobile considerations:**
- Use `inputMode="numeric"` to show number pad on mobile
- Minimum touch target: 44×44 pixels
- Input width: minimum `w-20` (80px)
- Button padding: minimum `px-4 py-2`

### STANDARD: Text/Essay Input

**REQUIRED:** The Enter key (without Shift) must submit the answer, in addition to clicking the Submit button. Shift+Enter should insert a newline.

```jsx
<div className="space-y-2">
  <textarea
    value={answer}
    onChange={(e) => setAnswer(e.target.value)}
    onKeyDown={(e) => { if (e.key === 'Enter' && !e.shiftKey && !submitted && answer.trim().length >= 10) { e.preventDefault(); handleSubmit(); } }}
    disabled={submitted}
    placeholder="Your answer..."
    rows={3}
    className="w-full p-3 border rounded text-sm resize-none"
    style={{ borderColor: colors.earthLight }}
  />
  {!submitted && (
    <button
      onClick={handleSubmit}
      disabled={answer.trim().length < 10}
      className="w-full py-3 rounded-lg font-bold text-white disabled:opacity-50"
      style={{ backgroundColor: colors.primary }}
    >
      Submit
    </button>
  )}
</div>
```

### STANDARD: Two-Choice Questions

For binary choices, use button-based selection:

```jsx
const TwoChoiceQuestion = ({ 
  question, 
  optionA, 
  optionB, 
  optionAValue, 
  optionBValue,
  selectedAnswer, 
  attempts, 
  submitted, 
  onSubmit,
  hints = [],
  correctAnswer,
  explanation
}) => (
  <div className="bg-white rounded-lg p-4 mb-4 shadow-sm">
    <p className="text-sm mb-4" style={{ color: colors.earthDark }}>
      <strong>Question:</strong> {question}
    </p>
    
    <div className="grid grid-cols-2 gap-3 mb-3">
      <button
        onClick={() => !submitted && onSubmit(optionAValue)}
        disabled={submitted}
        className="p-4 rounded-lg border-2 text-center font-bold transition-all"
        style={{ 
          borderColor: submitted && optionAValue === correctAnswer 
            ? colors.success 
            : selectedAnswer === optionAValue 
              ? colors.primary 
              : colors.earthLight,
          backgroundColor: submitted && optionAValue === correctAnswer
            ? colors.successBg
            : selectedAnswer === optionAValue 
              ? colors.sand 
              : 'white',
          color: colors.earthDark
        }}
      >
        {optionA}
      </button>
      
      <button
        onClick={() => !submitted && onSubmit(optionBValue)}
        disabled={submitted}
        className="p-4 rounded-lg border-2 text-center font-bold transition-all"
        style={{ 
          borderColor: submitted && optionBValue === correctAnswer 
            ? colors.success 
            : selectedAnswer === optionBValue 
              ? colors.primary 
              : colors.earthLight,
          backgroundColor: submitted && optionBValue === correctAnswer
            ? colors.successBg
            : selectedAnswer === optionBValue 
              ? colors.sand 
              : 'white',
          color: colors.earthDark
        }}
      >
        {optionB}
      </button>
    </div>
    
    {/* Hints and explanation handling */}
  </div>
);
```

### Two-Choice with Explanation

When you need students to select Yes/No AND explain their reasoning:

```jsx
{/* Yes/No buttons */}
<div className="grid grid-cols-2 gap-3 mb-4">
  <button
    onClick={() => !submitted && setChoice('yes')}
    disabled={submitted}
    className={`p-4 rounded-lg border-2 text-center font-bold ${
      choice === 'yes' ? 'border-blue-500 bg-blue-50' : 'border-gray-200'
    }`}
  >
    Yes
  </button>
  <button
    onClick={() => !submitted && setChoice('no')}
    disabled={submitted}
    className={`p-4 rounded-lg border-2 text-center font-bold ${
      choice === 'no' ? 'border-blue-500 bg-blue-50' : 'border-gray-200'
    }`}
  >
    No
  </button>
</div>

{/* Explanation text area (appears after selection) */}
{choice && !submitted && (
  <div className="mb-3">
    <label className="block text-sm font-medium mb-2">Explain briefly:</label>
    <textarea
      value={explanation}
      onChange={(e) => setExplanation(e.target.value)}
      placeholder="Why do you think that?"
      rows={2}
      className="w-full p-3 border rounded-lg text-sm resize-none"
    />
  </div>
)}

{/* Single submit for both choice + explanation */}
{!submitted && choice && (
  <button onClick={handleSubmit} disabled={explanation.length < 5}>
    Check
  </button>
)}
```

---

## Answer Evaluation

### Three-Strike System

All questions use a three-strike system:
- **Strike 1:** Show hint 1, allow retry
- **Strike 2:** Show hint 2, allow retry  
- **Strike 3:** Play buzzer, reveal correct answer, allow continue

```jsx
const handleSubmit = () => {
  const isCorrect = evaluateAnswer(answer);
  
  if (isCorrect) {
    playSuccessTone();
    setSubmitted(true);
  } else {
    const newAttempts = attempts + 1;
    setAttempts(newAttempts);
    
    if (newAttempts >= 3) {
      playBuzzer();
      setSubmitted(true);  // Reveal answer, allow continue
    } else {
      playSoftNope();
      // Hint will display based on attempts count
    }
  }
};
```

### Hint Display

```jsx
{attempts > 0 && attempts < 3 && !submitted && (
  <div className="mt-2 p-3 rounded-lg" style={{ backgroundColor: colors.warningBg }}>
    <p className="text-sm" style={{ color: '#92400e' }}>
      <strong>Hint {attempts}/2:</strong> {hints[attempts - 1]}
    </p>
  </div>
)}
```

### Third Strike Reveal

```jsx
{submitted && attempts >= 3 && (
  <div className="mt-2 p-3 rounded-lg" style={{ backgroundColor: colors.warningBg, borderColor: colors.warning }}>
    <p className="text-sm font-medium" style={{ color: '#92400e' }}>
      Here's what we were looking for:
    </p>
    <p className="text-sm mt-1" style={{ color: '#92400e' }}>
      {correctAnswer}
    </p>
  </div>
)}
```

---

## Sound Feedback

### Standard Sound Functions

Include these in every tutorial:

```jsx
const createAudioContext = () => {
  return new (window.AudioContext || window.webkitAudioContext)();
};

// Success: Ascending triad (C-E-G)
const playSuccessTone = () => {
  try {
    const ctx = createAudioContext();
    const notes = [523.25, 659.25, 783.99];
    const startTime = ctx.currentTime;
    
    notes.forEach((freq, i) => {
      const oscillator = ctx.createOscillator();
      const gainNode = ctx.createGain();
      
      oscillator.connect(gainNode);
      gainNode.connect(ctx.destination);
      
      oscillator.frequency.value = freq;
      oscillator.type = 'sine';
      
      const noteStart = startTime + (i * 0.1);
      const noteEnd = noteStart + 0.15;
      
      gainNode.gain.setValueAtTime(0, noteStart);
      gainNode.gain.linearRampToValueAtTime(0.3, noteStart + 0.02);
      gainNode.gain.exponentialRampToValueAtTime(0.01, noteEnd);
      
      oscillator.start(noteStart);
      oscillator.stop(noteEnd + 0.1);
    });
    
    setTimeout(() => ctx.close(), 600);
  } catch (e) {
    console.log('Audio not available');
  }
};

// Soft nope: Gentle descending two notes
const playSoftNope = () => {
  try {
    const ctx = createAudioContext();
    const notes = [400, 300];
    const startTime = ctx.currentTime;
    
    notes.forEach((freq, i) => {
      const oscillator = ctx.createOscillator();
      const gainNode = ctx.createGain();
      
      oscillator.connect(gainNode);
      gainNode.connect(ctx.destination);
      
      oscillator.frequency.value = freq;
      oscillator.type = 'sine';
      
      const noteStart = startTime + (i * 0.12);
      const noteEnd = noteStart + 0.12;
      
      gainNode.gain.setValueAtTime(0, noteStart);
      gainNode.gain.linearRampToValueAtTime(0.2, noteStart + 0.02);
      gainNode.gain.exponentialRampToValueAtTime(0.01, noteEnd);
      
      oscillator.start(noteStart);
      oscillator.stop(noteEnd + 0.05);
    });
    
    setTimeout(() => ctx.close(), 400);
  } catch (e) {
    console.log('Audio not available');
  }
};

// Buzzer: Third strike sound
const playBuzzer = () => {
  try {
    const ctx = createAudioContext();
    const oscillator = ctx.createOscillator();
    const gainNode = ctx.createGain();
    
    oscillator.connect(gainNode);
    gainNode.connect(ctx.destination);
    
    oscillator.frequency.value = 150;
    oscillator.type = 'sawtooth';
    
    const startTime = ctx.currentTime;
    gainNode.gain.setValueAtTime(0.25, startTime);
    gainNode.gain.exponentialRampToValueAtTime(0.01, startTime + 0.3);
    
    oscillator.start(startTime);
    oscillator.stop(startTime + 0.35);
    
    setTimeout(() => ctx.close(), 400);
  } catch (e) {
    console.log('Audio not available');
  }
};

// Click: Navigation sound
const playContinueClick = () => {
  try {
    const ctx = createAudioContext();
    const oscillator = ctx.createOscillator();
    const gainNode = ctx.createGain();
    
    oscillator.connect(gainNode);
    gainNode.connect(ctx.destination);
    
    oscillator.frequency.value = 600;
    oscillator.type = 'sine';
    
    const startTime = ctx.currentTime;
    gainNode.gain.setValueAtTime(0, startTime);
    gainNode.gain.linearRampToValueAtTime(0.15, startTime + 0.01);
    gainNode.gain.exponentialRampToValueAtTime(0.01, startTime + 0.08);
    
    oscillator.start(startTime);
    oscillator.stop(startTime + 0.1);
    
    setTimeout(() => ctx.close(), 150);
  } catch (e) {
    console.log('Audio not available');
  }
};
```

### When to Play Each Sound

| Event | Sound Function |
|-------|----------------|
| Correct answer | `playSuccessTone()` |
| Wrong answer (1st or 2nd attempt) | `playSoftNope()` |
| Wrong answer (3rd attempt) | `playBuzzer()` |
| Continue/Next button | `playContinueClick()` |
| Reflection submitted | `playSuccessTone()` |

---

## Tablet Display Format

### Standard T-Account Tablet

```jsx
const TAccountTablet = ({ 
  title, 
  leftHeader, 
  rightHeader, 
  leftEntries = [], 
  rightEntries = [],
  highlightLeft = false,
  highlightRight = false 
}) => (
  <div 
    className="rounded-lg border-2 overflow-hidden mb-4"
    style={{ backgroundColor: colors.clay, borderColor: colors.clayDark }}
  >
    {/* Title bar */}
    <div 
      className="py-2 text-center font-bold border-b-2 text-sm"
      style={{ backgroundColor: colors.clayLight, borderColor: colors.clayDark, color: colors.earthDark }}
    >
      {title}
    </div>
    
    {/* Two-column structure */}
    <div className="grid grid-cols-2">
      {/* Left column */}
      <div 
        className="border-r p-3"
        style={{ borderColor: colors.earthLight }}
      >
        <p className="text-xs font-bold mb-2 text-center" style={{ color: colors.earthDark }}>
          {leftHeader || 'RECEIVED'}
        </p>
        {leftEntries.map((entry, i) => (
          <div key={i} className="text-sm" style={{ color: colors.earthDark }}>
            {entry}
          </div>
        ))}
      </div>
      
      {/* Right column */}
      <div className="p-3">
        <p className="text-xs font-bold mb-2 text-center" style={{ color: colors.earthDark }}>
          {rightHeader || 'DISTRIBUTED'}
        </p>
        {rightEntries.map((entry, i) => (
          <div key={i} className="text-sm" style={{ color: colors.earthDark }}>
            {entry}
          </div>
        ))}
      </div>
    </div>
  </div>
);
```

See `Tablet-Format-Specification.md` for detailed tablet formatting requirements.

---

## Mobile Responsiveness

### Key Requirements

1. **Touch targets:** Minimum 44×44 pixels for all interactive elements
2. **Input font size:** Minimum 16px to prevent iOS zoom
3. **Layouts:** Stack side-by-side elements on mobile (`grid md:grid-cols-2`)
4. **Input width:** Minimum `w-24` (96px) for numeric inputs
5. **No horizontal scroll:** Test at 320px width

### Responsive Patterns

```jsx
{/* Stack on mobile, side-by-side on desktop */}
<div className="space-y-4 md:space-y-0 md:grid md:grid-cols-2 md:gap-4">
  <Component1 />
  <Component2 />
</div>

{/* Responsive spacing */}
<div className="p-3 md:p-4">
<div className="text-sm md:text-base">
```

See `Mobile-Usability-Analysis.md` for detailed mobile requirements.

---

## State Management

### Standard State Structure

```jsx
// Phase control
const [phase, setPhase] = useState('welcome');

// UI state
const [showGlossary, setShowGlossary] = useState(false);
const [showHistoricalNote, setShowHistoricalNote] = useState(false);
const [devMode, setDevMode] = useState(false);
const [headerClickCount, setHeaderClickCount] = useState(0);

// Per-question state (repeat for each question)
const [q1Answer, setQ1Answer] = useState('');
const [q1Attempts, setQ1Attempts] = useState(0);
const [q1Submitted, setQ1Submitted] = useState(false);
```

### Restart Handler

```jsx
const handleRestart = () => {
  playContinueClick();
  setPhase('welcome');
  // Reset all question state
  setQ1Answer('');
  setQ1Attempts(0);
  setQ1Submitted(false);
  // ... repeat for all questions
  setShowHistoricalNote(false);
};
```

---

## Naming Conventions

### Variables

| Type | Convention | Example |
|------|------------|---------|
| State | camelCase | `showGlossary`, `q1Attempts` |
| Constants | UPPER_SNAKE | `MAX_ATTEMPTS`, `PHASE_ORDER` |
| Colors | camelCase in object | `colors.earthDark` |
| Handlers | handleAction | `handleSubmit`, `handleRestart` |
| Sound | `play` prefix | `playSuccessTone`, `playSoftNope` |

### Components

| Type | Convention | Example |
|------|------------|---------|
| Layout | Descriptive | `HeaderWithControls`, `Footer`, `Card` |
| Feedback | Type + Panel | `InsightPanel`, `WarningPanel` |
| Display | Content type | `TAccountTablet`, `DialogueBlock` |
| Modal | Name + Modal | `GlossaryModal`, `HintModal` |

---

## Terminology Guidelines

### Historical Authenticity

**Act I (Pre-urban, ~3500 BCE):** No writing exists. Avoid terms that imply written records.

| Avoid | Use Instead |
|-------|-------------|
| "posted rates" / "posted prices" | "shouted rates" / "the rates everyone calls out" |
| "price list" | "what traders are calling out" |
| "written" / "recorded" | "remembered" / "known" |

**Act II (Babylon, ~1800 BCE):** Writing exists but modern accounting terms are anachronistic.

| Avoid | Use Instead |
|-------|-------------|
| "T-account" | "two-column tablet" / "tablet with RECEIVED/DISTRIBUTED" |
| "double-entry bookkeeping" | "coordinated records" / "tablets that speak with one voice" |
| "debit/credit" | "received/distributed" / "inflow/outflow" |

### Technical Terms: Experience First, Name Later

**IMPORTANT:** Students should experience a concept before learning its technical name.

**Pattern:**
1. Students experience the problem/phenomenon
2. Students work through the implications
3. THEN introduce the formal term: "This process has a name: **[term]**."

**Example (Tutorial 1.4):**
- Students watch Kira profit from trading cycles
- Students discover that rates must "line up" or gaps can be exploited
- Students understand WHY rates become consistent
- THEN: "This process has a name: **arbitrage**."

**Avoid:** Introducing technical terms in "What You'll Discover" boxes before students have experienced the concept.

### Plain Language Preferences

| Technical/Academic | Plain Language |
|-------------------|----------------|
| "cohere" / "coherent" | "line up" / "consistent" |
| "numeraire" | "common standard" |
| "commensurable" | "able to compare" / "in the same terms" |
| "arbitrage creates coherent price relationships" | "traders calling out rates leads to consistency" |

---

## Common Components

### Narrative Block

```jsx
const NarrativeBlock = ({ children }) => (
  <div 
    className="p-4 rounded-lg border-l-4 italic mb-4"
    style={{ backgroundColor: colors.sand, borderColor: colors.accent }}
  >
    <div className="text-gray-700">{children}</div>
  </div>
);
```

### Dialogue Block

```jsx
const DialogueBlock = ({ speaker, children }) => (
  <div className="mb-4 p-4 rounded-lg" style={{ backgroundColor: colors.clayLight }}>
    <p className="font-bold mb-2" style={{ color: colors.primary }}>{speaker}:</p>
    <div className="italic" style={{ color: colors.earthDark }}>{children}</div>
  </div>
);
```

### Insight Panel (Success)

```jsx
const InsightPanel = ({ title, children }) => (
  <div 
    className="p-4 rounded-lg border-2 mb-4"
    style={{ backgroundColor: colors.successBg, borderColor: colors.success }}
  >
    <div className="flex items-start gap-2">
      <CheckCircle className="w-5 h-5 mt-0.5 flex-shrink-0" style={{ color: colors.success }} />
      <div>
        {title && <p className="font-bold mb-2" style={{ color: colors.success }}>{title}</p>}
        <div style={{ color: '#166534' }}>{children}</div>
      </div>
    </div>
  </div>
);
```

### Warning Panel

```jsx
const WarningPanel = ({ title, children }) => (
  <div 
    className="p-4 rounded-lg border-2 mb-4"
    style={{ backgroundColor: colors.warningBg, borderColor: colors.warning }}
  >
    <div className="flex items-start gap-2">
      <AlertCircle className="w-5 h-5 mt-0.5 flex-shrink-0" style={{ color: colors.warning }} />
      <div>
        {title && <p className="font-bold mb-2" style={{ color: '#92400e' }}>{title}</p>}
        <div style={{ color: '#92400e' }}>{children}</div>
      </div>
    </div>
  </div>
);
```

### Key Insight Box

```jsx
const KeyInsightBox = ({ children }) => (
  <div 
    className="p-4 rounded-lg border-2 mb-4"
    style={{ backgroundColor: '#fef9e7', borderColor: colors.accent }}
  >
    <div className="flex items-start gap-3">
      <Lightbulb className="w-5 h-5 flex-shrink-0 mt-0.5" style={{ color: colors.accent }} />
      <div style={{ color: colors.earthDark }}>{children}</div>
    </div>
  </div>
);
```

### Continue Button

```jsx
const ContinueButton = ({ onClick, children = "Continue" }) => (
  <button
    onClick={() => { playContinueClick(); onClick(); }}
    className="w-full py-3 rounded-lg font-bold text-white flex items-center justify-center gap-2"
    style={{ backgroundColor: colors.primary }}
  >
    {children} <ChevronRight className="w-5 h-5" />
  </button>
);
```

### Glossary Modal

```jsx
const GlossaryModal = () => (
  <div className="fixed inset-0 bg-black/50 flex items-center justify-center p-4 z-50">
    <div className="bg-white rounded-xl max-w-md w-full max-h-[80vh] overflow-y-auto">
      <div className="p-4 border-b sticky top-0 bg-white flex justify-between items-center">
        <h3 className="font-bold" style={{ color: colors.primary }}>Glossary</h3>
        <button 
          onClick={() => setShowGlossary(false)} 
          className="text-gray-500 hover:text-gray-700 text-xl"
        >
          ×
        </button>
      </div>
      <div className="p-4 space-y-3 text-sm">
        {glossaryTerms.map((item, i) => (
          <div key={i}>
            <p className="font-medium" style={{ color: colors.primary }}>{item.term}</p>
            <p className="text-gray-600 text-xs">{item.definition}</p>
          </div>
        ))}
      </div>
    </div>
  </div>
);
```

---

## Accessibility

### Required Attributes

```jsx
// Images
<img src="..." alt="Description of image" />

// Interactive elements
<button aria-label="Continue to next step" title="Continue">
  <ChevronRight />
</button>

// Form inputs
<label htmlFor="answer">Your answer:</label>
<input id="answer" ... />

// Progress indicators
<div role="progressbar" aria-valuenow={progress} aria-valuemin={0} aria-valuemax={100}>
  Progress: {progress}%
</div>
```

### Keyboard Navigation

- All interactive elements must be reachable via Tab
- **Enter must submit/check answers** on all input types (numeric, text, reflection)
- For textareas, Enter submits; Shift+Enter inserts a newline
- Escape should close modals

### Color Contrast

- Text on primary (#00356b): Use white
- Text on sand (#f5f1e8): Use earthDark (#5c4d3d) or primary
- Text on clay (#c4a574): Use earthDark or primary

---

## Testing Checklist

Before submitting any tutorial:

### Functionality
- [ ] All questions evaluate correctly
- [ ] Three-strike system works for each question
- [ ] Hints appear on 1st and 2nd incorrect attempts
- [ ] Answer revealed on 3rd strike
- [ ] Sound feedback plays (success, soft nope, buzzer, click)
- [ ] **Enter key submits answers** on all numeric and text inputs
- [ ] Restart button resets all state
- [ ] Progress bar updates correctly

### Navigation
- [ ] All phases reachable
- [ ] Continue buttons advance correctly
- [ ] Back navigation works (if implemented)
- [ ] No dead ends
- [ ] No blank screens on phase transitions

### Header & Controls
- [ ] Header with progress bar appears on ALL phases including welcome
- [ ] Glossary button opens modal
- [ ] Restart button works from any phase
- [ ] Dev mode activates on triple-click
- [ ] Dev mode phase buttons work correctly

### Historical Note
- [ ] Historical Liberties note appears on welcome screen
- [ ] Note is collapsible (collapsed by default)
- [ ] Note content is specific to this tutorial
- [ ] Note is placed above Continue button

### Complete Screen
- [ ] Trophy and success message display
- [ ] "What You Discovered" lists key insights
- [ ] "Coming Next" shows next tutorial title
- [ ] Next Tutorial button present and styled as primary
- [ ] Restart button present and styled as secondary

### Mobile (Test at 320px width)
- [ ] All content visible without horizontal scroll
- [ ] Touch targets ≥ 44px
- [ ] Inputs large enough to tap
- [ ] Text readable (≥ 14px body, ≥ 16px inputs)
- [ ] No overlapping elements
- [ ] Modals close properly

### Visual
- [ ] Colors match palette
- [ ] Tablets use standard format
- [ ] Consistent spacing
- [ ] No broken layouts

### Content
- [ ] No character encoding issues (—, ", ', etc.)
- [ ] Glossary terms accurate
- [ ] Historical terminology consistent
- [ ] Technical terms introduced AFTER experience

---

## Version History

| Date | Version | Changes |
|------|---------|---------|
| 2025-12-16 | 1.0 | Initial standards document |
| 2025-12-16 | 1.1 | Added Header with Progress Bar section; Added Historical Liberties Note section with placement requirements and per-act content examples; Added TwoChoiceQuestion component; Updated phase transition guidance |
| 2025-12-19 | 1.2 | Added Complete Screen Structure section with Next Tutorial button; Added Terminology Guidelines section (historical authenticity, experience-first naming, plain language); Added Two-Choice with Explanation pattern; Added KeyInsightBox component; Updated testing checklist for Complete screen |
| 2026-02-08 | 2.0 | **Breaking change:** Tutorials now required as standalone HTML files (not JSX). Uses React 18 via CDN with Babel standalone. Replaced lucide-react icons with unicode characters. Updated file naming, structure, and import conventions. |

---

## Quick Reference Card

```
REMINDER: The current year is 2026. Use this in all version dates.

FILE FORMAT: Standalone HTML with React via CDN + Babel standalone
ICONS: Unicode characters only (no lucide-react)

VERSION BLOCK (required in <script type="text/babel"> of every tutorial)
------------------------------------------------------------------------
/**
 * Tutorial X.X: [Title]
 * Accounting Origins Project
 *
 * @version 1.0
 * @date 2026-MM-DD
 * @description [Brief description]
 */

WELCOME SCREEN STRUCTURE
------------------------
1. HeaderWithControls (with progress bar)
2. Narrative content
3. "What You'll Discover" box (avoid technical terms!)
4. Historical Liberties Note (collapsible)
5. Begin Tutorial button

COMPLETE SCREEN STRUCTURE
-------------------------
1. Header (with 100% progress)
2. Trophy / Success indicator
3. "What You Discovered" (checkmarked list)
4. "The Deeper Point" (optional insight box)
5. "Coming Next" (bridge to next tutorial)
6. Next Tutorial button (primary)
7. Restart button (secondary/outline)

COLOR QUICK REFERENCE
---------------------
Primary button:     backgroundColor: colors.primary, color: white
Secondary button:   backgroundColor: colors.sand, color: colors.earthDark
Outline button:     border: colors.primary, color: colors.primary
Success feedback:   backgroundColor: colors.successBg, borderColor: colors.success
Warning feedback:   backgroundColor: colors.warningBg, borderColor: colors.warning
Error feedback:     backgroundColor: colors.errorBg, borderColor: colors.error
Tablet background:  backgroundColor: colors.clay, borderColor: colors.clayDark
Narrative block:    backgroundColor: colors.sand, borderColor: colors.accent

SOUND QUICK REFERENCE
---------------------
Correct answer:     playSuccessTone()
Wrong (1st/2nd):    playSoftNope()
Wrong (3rd):        playBuzzer()
Navigation:         playContinueClick()

TERMINOLOGY QUICK REFERENCE
---------------------------
Act I: "shouted rates" not "posted prices"
Act II: "two-column tablet" not "T-account"
General: "line up" not "cohere"
General: Introduce technical terms AFTER experience

INPUT QUICK REFERENCE
---------------------
Numeric:    <input type="text" inputMode="numeric" pattern="[0-9]*" />
Text:       <textarea rows={3} />
Two-choice: Button-based selection
Two-choice + explanation: Buttons + textarea, single submit

PHASE TRANSITION
----------------
ALWAYS: onClick={() => { setStep(0); setPhase('next-phase'); }}
```
