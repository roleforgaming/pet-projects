# Writers Suite MVP Specification (FINAL)

**Date:** 2026-02-11
**Project:** Writers Suite - ADHD-Friendly Writing Tool with Digital Body Doubling Pet
**Timeline:** 2-3 Week Sprint (14 days estimated)

---

## Executive Summary

Writers Suite is a **writing tool for non-linear storytellers** that combines:
- A **continuous document editor** for flow-state writing
- **Inline annotations** with freeform user-defined prefixes for contextual notes
- A **digital body double pet** that provides ADHD support through presence, progress visualization, and celebratory feedback

**Differentiator:** This is the only writing tool that combines inline annotations with a persistent, rewarding pet companion designed for ADHD executive function support.

---

## MVP Feature Set

### 1. PROJECT SETUP & CONFIGURATION

**On Project Creation:**
- [ ] Project title input
- [ ] Genre selection dropdown:
  - Short Story (≤7,500 words)
  - Novella (7,500 - 20,000 words)
  - Novel (50,000 - 110,000 words)
  - Novella+ (20,000 - 50,000 words)
  - Epic (110,000+ words)
- [ ] Total manuscript goal (pre-populated from genre, editable)
- [ ] Daily word count goal (as percentage of total, e.g., 2%)
- [ ] Auto-calculated daily goal (display for clarity)

**Anytime Access:**
- [ ] Edit daily/total goals
- [ ] Change genre (auto-update total goal)

---

### 2. GLOBAL SETTINGS (User-Defined)

**Annotation Prefixes:**
- [ ] Add custom annotation prefixes (prefix + label + color picker)
- [ ] Edit existing prefixes
- [ ] Delete prefixes
- [ ] Example defaults provided: `>>` (Notes), `##` (Characters), `!!` (Plot)

**Tag Customization:**
- [ ] @ tag color customization (global default)

---

### 3. BEAT EDITOR (CORE)

**Beat CRUD:**
- [ ] Create new beat (button or keyboard shortcut)
- [ ] Edit beat title
- [ ] Edit beat content (rich text with annotation support)
- [ ] Delete beat
- [ ] Duplicate beat

**Continuous Document View:**
- [ ] All beats rendered in sequence
- [ ] Clean separation between beats (visual divider)
- [ ] Real-time word count display (manuscript words only)
- [ ] Beat-level metadata (created date, last edited, word count)

**Reorganization:**
- [ ] Drag-and-drop beat reordering (with snap animation < 0.5s)
- [ ] Up/Down arrow buttons (< 0.5s feedback animation)
- [ ] Instant visual feedback (flash/highlight on move)

---

### 4. ANNOTATION SYSTEM

**Creating Annotations:**
- [ ] Type annotation prefix + content (e.g., `>>research note`)
- [ ] Custom prefixes autocomplete from user-defined list
- [ ] @ tags created on-the-fly (no preset list, dynamic creation)
- [ ] Inline visual styling for each annotation type

**Annotation Display States:**
- [ ] **Show Annotations:** Full visibility of inline annotations with distinct colors
- [ ] **Minimize Annotations:** Faintly colored underlines show annotated text (visual indicator, no text shown)
- [ ] **Hide Annotations:** Complete invisibility, no underlines
- [ ] **State persistence:** Remember user's chosen state per project

**Smart Creation:**
- [ ] When annotations are hidden, new annotations auto-hide immediately after creation
- [ ] User can still create annotations in hidden mode (they hide on escape)

**Word Count Handling:**
- [ ] Manuscript word count EXCLUDES all annotation markers and content
- [ ] Example: `"Annie looked at her hands >>>fear of fire<<<. She gasped."` = 7 manuscript words
- [ ] Real-time recalculation as user edits

---

### 5. PET GAMIFICATION (ADHD Body Double)

**Pet Sprite & Animations:**
- [ ] Simple SVG character (cute, non-threatening)
- [ ] Mood states: happy, excited, napping
- [ ] Celebratory animations (bounce, particles, happy expression)

**Reward Triggers (In Priority Order):**

| Trigger | Pet Behavior | Frequency |
|---------|--------------|-----------|
| **Active Typing** | Happy animation | Every 5-10 second intervals of activity |
| **Partial Progress** | Celebration/encouragement | At 25%, 50%, 75% of daily goal |
| **Daily Goal Met** | Major celebration | Once per day when goal is met |
| **Idle Detection** | Takes a nap | After 5+ minutes of typing idle |
| **Return from Idle** | Wakes up, greets user | On typing resume |

**Idle Definition:**
- **Triggers nap:** 5+ minutes with NO typing activity
- **Wakes from nap:** Only on TYPING (not clicking, not scrolling)
- **Does NOT track:** Mouse clicks, scrolling, UI navigation (only typing idle)

**Visual Progress Indicator:**
- [ ] Daily progress bar (current day's words vs. daily goal)
- [ ] Total progress bar (total words written vs. total manuscript goal)
- [ ] Pet displayed near progress bars or in corner
- [ ] Session status indicator ("Today's goal: X/Y words")

---

### 6. PERSISTENCE & AUTO-SAVE

**localStorage Structure:**
```
writersSuite_globalSettings
writersSuite_projects_{projectId}
writersSuite_beats_{projectId}
writersSuite_petState_{projectId}
writersSuite_sessions_{projectId}
```

**Auto-Save:**
- [ ] Save on every content change (debounced 500ms)
- [ ] Auto-save on annotation creation
- [ ] Auto-save on reorganization
- [ ] Visual indicator when saving ("Saving..." → checkmark)
- [ ] Handle offline gracefully (queue changes, sync on reconnect)

---

## Technical Architecture

### Technology Stack
- **Frontend:** React 18+ with TypeScript
- **Editor:** Custom React component (NOT Slate/Prosemirror - need fine-grained annotation control)
- **State Management:** Zustand (lightweight, perfect for this scale)
- **Persistence:** localStorage (MVP only; Firebase for Phase 2)
- **Animations:** Framer Motion
- **Build:** Vite

### Data Model

**Global Settings:**
```typescript
interface GlobalSettings {
  annotationPrefixes: {
    prefix: string;
    label: string;
    color: string;
  }[];
  tagColor: string;
}
```

**Project:**
```typescript
interface Project {
  id: string;
  title: string;
  genre: "short-story" | "novella" | "novel" | "novella+" | "epic" | "custom";
  totalManuscriptGoal: number;
  dailyWordCountGoal: number;
  createdAt: ISO8601String;
  lastEditedAt: ISO8601String;
}
```

**Beat:**
```typescript
interface Beat {
  id: string;
  projectId: string;
  title: string;
  content: string;
  annotations: {
    prefix: string;
    startIndex: number;
    endIndex: number;
    content: string;
  }[];
  manuscriptWordCount: number; // Calculated, excluding annotation markers
  totalWordCount: number;
  status: "outline" | "draft" | "editing" | "done";
  createdAt: ISO8601String;
  lastEditedAt: ISO8601String;
}
```

**Pet State:**
```typescript
interface PetState {
  projectId: string;
  lastSessionDate: string;
  totalSessionsCompleted: number;
  totalManuscriptWordsWritten: number;
  currentDayWordsWritten: number;
  streak: number;
  lastActivityTime: ISO8601String;
  isNapping: boolean;
  mood: "happy" | "napping" | "excited";
}
```

---

## Implementation Roadmap

### Phase 1A: Foundation (Days 1-3)
- [ ] React + TypeScript scaffold
- [ ] localStorage persistence layer
- [ ] Project CRUD
- [ ] Global settings UI (annotation prefixes, tag color)

### Phase 1B: Editor Core (Days 4-6)
- [ ] Beat CRUD operations
- [ ] Continuous document rendering
- [ ] Inline annotation parsing & display
- [ ] Three-state annotation toggle (Show/Minimize/Hide)
- [ ] Word count calculation (manuscript vs. total)

### Phase 1C: Reorganization (Days 7-9)
- [ ] Drag-and-drop beat reordering
- [ ] Up/down arrow reorganization
- [ ] Snap animations (< 0.5s)
- [ ] Instant feedback on moves

### Phase 1D: Pet & Gamification (Days 10-12)
- [ ] Pet sprite & mood animations
- [ ] Active typing detection & happy animation
- [ ] Partial progress celebration
- [ ] Daily goal tracking & celebration
- [ ] Idle detection (5+ min typing idle → nap)
- [ ] Progress visualization (daily/total bars)

### Phase 1E: Polish & Validation (Days 13-14)
- [ ] Use with real manuscript excerpt
- [ ] UX iteration based on testing
- [ ] Bug fixes & refinement
- [ ] Performance optimization

---

## Success Criteria

✅ **Functional:**
- Beats can be created, edited, deleted, and reordered
- Annotations display inline with three-state toggle
- Word count calculated correctly (manuscript words only)
- Pet animates on typing, progress, and idle
- Data persists across page refresh

✅ **UX:**
- Reorganization feels intuitive (< 5 seconds per action)
- Annotation toggle feels seamless (no mental friction)
- Pet animations feel encouraging, never annoying
- Writing experience feels better than Google Docs

✅ **ADHD Support:**
- Pet provides genuine body-doubling presence
- Progress visualization motivates continuation
- Partial progress celebration prevents all-or-nothing thinking
- Napping pet feels natural and stress-free

---

## Phase 2+ Roadmap

- [ ] Corkboard view (card-based outlining)
- [ ] Beat splitting/merging
- [ ] Advanced filtering by tag/annotation
- [ ] Session history & statistics
- [ ] Pet visual evolution (grows as you write more)
- [ ] Cloud sync (Firebase)
- [ ] Multi-device support
- [ ] Export to .docx/.pdf (metadata stripped)
- [ ] Collaborative writing (optional)

---

## Notes for Development

**Annotation Handling:**
- Store annotations with precise start/end indices in content
- When content changes, recalculate affected annotation indices
- When displaying, use `<span>` with background colors for annotations
- Ensure annotation markers (prefixes) are visually distinct from content

**Pet Behavior:**
- Track typing activity timestamp (not mouse/scroll events)
- Idle check every 30 seconds (don't recalculate constantly)
- Celebrate at 25/50/75% progress (not just 0/100%)
- Nap animation should be calming, not sad
- Wake animation should be joyful but not startling

**Word Count Accuracy:**
- Strip annotation markers and content before counting
- Handle various whitespace scenarios
- Update count in real-time as user types (debounce display update)

---

**Status:** ✅ SPECIFICATION COMPLETE - READY FOR DEVELOPMENT
