---
title: "Writers Suite MVP Phase 1A - Refined UX Specification"
date: 2026-02-13
session: "Customer Journey Mapping - Validated Against ADHD-First Principles"
status: "Validated & Ready for Implementation"
---

# Phase 1A UX Specification – Refined from Customer Journey Mapping

**Facilitator:** Mary (Business Analyst)
**Stakeholder:** Savannah (ADHD Writer)
**Date:** February 13, 2026
**Session Type:** UX Validation & Refinement

---

## Executive Summary

This specification captures **ADHD-first UX patterns validated against real user workflows**. Unlike generic "fast UX" patterns, these are specifically tuned to:
- **Keyboard-first interaction** (minimal/no mouse use)
- **Visual feedback only** (NO audio/haptic to prevent startle)
- **Functional clutter over sterile minimalism** (show what you need, hide what you don't)
- **Cursor-synchronized DnD** (beat moves with cursor, no lag)
- **Annotation toggle semantics** (View/Minimize/Hide with distinct behaviors)
- **Last-edited tracking** (prevent "where was I?" moments)
- **Strict undo/redo semantics** (batch operations behave as atomic units)

All patterns validated by Savannah for Phase 1A implementation.

---

## 1. INTERACTION PARADIGM: Keyboard-First

### Principle
Users should **rarely or never need the mouse**. All core workflows have keyboard shortcuts.

### Keyboard Shortcuts (Phase 1A)

| Action | Shortcut | Behavior | Feedback |
|--------|----------|----------|----------|
| **New Beat** | **Double Return** | Exit current beat's editor, create new beat below | Visual underline appears, new beat auto-focused |
| **Next Beat** | **Ctrl + ↓** | Jump cursor to next beat | Subtle highlight on next beat |
| **Previous Beat** | **Ctrl + ↑** | Jump cursor to previous beat | Subtle highlight on previous beat |
| **Move Beat Up** | **Ctrl + Shift + ↑** | Move current beat up one position | Beat slides up immediately (cursor-sync, no lag) |
| **Move Beat Down** | **Ctrl + Shift + ↓** | Move current beat down one position | Beat slides down immediately (cursor-sync, no lag) |
| **Move Beat to Scene** | **Ctrl + Shift + G** | Opens scene selector, move beat to chosen scene | Highlight target scene, beat moves on confirm |
| **Create Scene** | **Ctrl + Shift + N** | Create new scene above current beat | Scene appears inline |
| **Toggle Annotations** | **Ctrl + A** | Cycle through annotation modes: View → Minimize → Hide → View | Annotation display state changes visually |
| **Add Annotation** | **Ctrl + ;** | Open annotation input for current beat | Inline annotation input appears |
| **Flow Mode** | **Ctrl + F** | Enter/exit flow mode | Sidebar collapses; breadcrumb stays visible |
| **Undo** | **Ctrl + Z** | Undo last action (or batch if multi-beat move) | Visual confirmation on affected beats |
| **Redo** | **Ctrl + Shift + Z** | Redo last undone action | Visual confirmation on affected beats |
| **Save** | **Ctrl + S** | Force immediate localStorage write (normally auto) | "Saved" badge appears briefly |

### Keyboard-First Design Rules
- ✅ **No mouse required for core workflows** (new beat, edit, move, annotate, flow mode)
- ✅ **Arrow keys + Ctrl for navigation** (familiar to writers from vim/emacs)
- ✅ **No hidden menus** – all shortcuts visible in sidebar hint or toolbar
- ✅ **Accessible from any mode** (editing, moving, flow mode)
- ❌ **NO drag-and-drop via mouse** (only keyboard shortcuts for reordering)
  - *Exception:* DnD via mouse is **allowed**, but not required; keyboard is primary

### Implementation Notes
- Display shortcut hints in sidebar ("Cmd + N: new beat") only on hover or in settings
- Tooltips for toolbar buttons include keyboard shortcut
- Focus management: When user presses Ctrl+↓, automatically focus the next beat's editor

---

## 2. FEEDBACK MODEL: Visual-Only (NO Audio/Haptic)

### Principle
Sound startles Savannah and breaks flow. Haptic feedback is unnecessary.
**All feedback is visual.** Period.

### Visual Feedback Semantics

| Event | Visual Feedback | Timing | Notes |
|-------|-----------------|--------|-------|
| **Beat created** | Green underline appears on new beat | 100ms fade-in | Persists until user interacts elsewhere |
| **Beat moved** | Brief highlight (0.15s) on destination position | Instant | Confirms drop zone |
| **Save successful** | Small green checkmark badge on beat (or status bar) | 100ms fade-in, persist 1s | Optional: status bar shows "All saved" |
| **Save failed** | Red dot on affected beat | Persist until retry succeeds | User can click to retry |
| **Annotation added** | Yellow badge on beat; annotation text highlighted | 50ms pulse | Badge stays visible |
| **Annotation toggled** | Annotation display state changes (visible/minimized/hidden) | Instant | No animation needed |
| **Flow mode entered** | Sidebar collapses; breadcrumb glows faintly | 200ms fade | Indicates "immersive mode" |
| **Unsaved changes** | Red dot on affected beat | Persist until saved | Shows which beats have pending writes |
| **Multi-beat DnD in progress** | All affected beats show light blue overlay | While dragging | Helps user preview scope |
| **Undo/Redo executed** | Affected beats briefly highlight (0.1s) | Instant | Confirms which beats were affected |

### Feedback Rules
- ✅ **Instant feedback** – visual changes appear within 100ms of user action
- ✅ **Cursor sync on DnD** – beat follows cursor with zero lag (CSS transform, not repaint)
- ✅ **No animations that obscure intent** – smooth glides okay only if they don't delay visual tracking
- ❌ **NO audio** (no chimes, no pet celebration sounds, no notification beeps)
- ❌ **NO haptic** (no vibrations, no tactile feedback)
- ✅ **High contrast** – badges, highlights use colors that stand out (green, red, yellow, blue)

### Implementation Notes
- Use CSS animations sparingly; prioritize `transform` + `opacity` over layout changes
- Test cursor sync: drag a beat, verify it moves with mouse/touch point (no lag perceptible)
- Color palette: green = success, red = error/unsaved, yellow = info, blue = highlight

---

## 3. ANNOTATION TOGGLE SYSTEM: View/Minimize/Hide

### Principle
Annotations serve **research & editing**, not real-time writing reference.
User controls visibility with 3 explicit states.

### Annotation Modes

#### **MODE 1: VIEW** (Annotations always visible)
- **Behavior:** Annotations rendered inline with full text, colored badges by type
- **Auto-close?** NO – annotations remain visible until user explicitly minimizes/hides
- **Use case:** Editing phase, referencing research while revising
- **Keyboard:** Ctrl+A cycles to next mode
- **Visual cue:** Annotation section header shows "View" badge (or no badge)

#### **MODE 2: MINIMIZE** (Annotations visible as badges only)
- **Behavior:** Annotations collapse to colored icon/badge (e.g., 📝 for note, 📖 for synopsis)
- **Badge shows:** Annotation type + count (e.g., "📝 2" means 2 notes)
- **Click badge to expand:** User can click badge to read annotation inline (hover/popover)
- **Auto-close on blur?** NO – badges remain visible; user manually clicks to read
- **Use case:** Light reference while writing, need some visual space
- **Keyboard:** Ctrl+A cycles to next mode
- **Visual cue:** Annotation section header shows "Minimize" badge

#### **MODE 3: HIDE** (Annotations completely hidden)
- **Behavior:** Annotation section not rendered at all; annotations stored but invisible
- **Reference method:** Use Phase 1B search/filter feature (not Phase 1A)
- **Auto-convert on exit:** If user creates annotation while in HIDE mode, annotation created but immediately collapses to HIDE state
- **Use case:** Pure writing flow, zero visual clutter during first draft
- **Keyboard:** Ctrl+A cycles back to VIEW
- **Visual cue:** No annotation section visible

### Annotation Type Differentiation (Icon + Color)

| Annotation Type | Icon | Color | Example |
|---|---|---|---|
| **Note** | 📝 | Blue (#4A90E2) | General writing notes, TODOs |
| **Synopsis** | 📖 | Purple (#9B59B6) | Scene summary, beat purpose |
| **Character Note** | 👤 | Green (#27AE60) | Character reference, dialogue cues |
| **Research** | 🔍 | Orange (#E67E22) | Source material, facts, quotes |
| **Custom Tag** | 🏷️ | Gray (#95A5A6) | User-defined categories |

### Validation Rules
- ✅ Annotations DO NOT auto-hide when toggled to VIEW mode
- ✅ Minimized annotations show badges with icon + count
- ✅ Hidden annotations are invisible but NOT deleted
- ✅ Annotation mode preference is per-beat (not global)
- ✅ Each annotation type has distinct icon + color for at-a-glance recognition

### Implementation Notes
- Store annotation mode in beat state: `beat.annotationDisplayMode = 'view' | 'minimize' | 'hide'`
- Badge rendering: Count visible annotations by type; show as `[icon] count`
- Popover for minimized badges: Click badge → temporary inline popover shows full annotation text
- Test at scale: With 5+ annotations per beat, verify icon colors don't cause visual confusion

---

## 4. SCENE MANAGEMENT: Color-Coded Acts

### Principle
Color + text labels make scene navigation intuitive at scale.

### Scene Labeling

#### Standard Naming Convention
- **Act 1:** Black (or Dark Gray)
- **Act 2:** Blue
- **Act 3:** Green
- **Additional Acts:** Red, Yellow, Purple, etc. (user-configurable)

#### Visual Implementation
- **Scene header:** Colored left border (3-4px) + text label + beat count
- **Scene pills in sidebar:** Show color chip + act name + beat count
- **Breadcrumb:** If in Beat #5 (Scene: Act 2, Blue), breadcrumb shows "Act 2" with blue highlight

### Sidebar Scene Navigation
- **Collapsed scene:** Shows act name + beat count; click to jump to first beat in scene
- **Expanded scene:** Shows all beats in that scene; click beat to jump
- **Scroll to scene:** Persistent scroll position preserved (don't auto-collapse other scenes)

### Validation Rules
- ✅ Color + text labels reduce cognitive load when navigating large documents
- ✅ Users can customize act colors (backlog feature, not Phase 1A)
- ✅ Scene color is OPTIONAL styling, not required for functionality

### Implementation Notes
- Scene color stored in scene metadata: `scene.color = 'black' | 'blue' | 'green' | ...`
- CSS class per act: `scene--act-1`, `scene--act-2`, etc.
- Breadcrumb uses same color palette for visual consistency

---

## 5. BEAT TRACKING: Last-Edited Indicator

### Principle
Prevent "where was I?" moments when user has many beats.

### Implementation

#### **Last-Edited Pin**
- **Visual:** Small pin/bookmark icon on sidebar and main view for most recently edited beat
- **Behavior:** Updates whenever user saves changes to any beat
- **Keyboard shortcut:** Ctrl+Home jumps to last-edited beat
- **Reset on:** Page refresh (not persisted across sessions; only during current session)

#### **Breadcrumb Display**
- **Shows:** Project > Scene (Act X) > Current Beat ID
- **Location:** Fixed at top of editor, visible at all times (even in flow mode)
- **Click to navigate:** User can click scene name to jump to first beat in that scene

#### **Validation Rules**
- ✅ Last-edited beat is always one Ctrl+Home away
- ✅ Breadcrumb shows full context path at all times
- ✅ Users never lose place even with 50+ beats

### Implementation Notes
- Track `lastEditedBeatId` in session state (not localStorage)
- Update on any beat content save
- Breadcrumb: `${projectName} > ${currentScene.name} > Beat ${beatIndex}`

---

## 6. DRAG-AND-DROP: Cursor-Synchronized Movement

### Principle
Beat must visually move **with** cursor, **not** lag behind. No perceptible delay.

### DnD Semantics

#### **Mouse/Touch Drag**
- **Initiate:** Click beat, hold, drag to new position
- **Visual feedback:**
  - Beat follows cursor immediately (CSS transform, not DOM repositioning)
  - Light blue overlay on beat indicates "being moved"
  - Drop zone preview shows where beat will land (target position highlighted)
- **Release:** Beat snaps to target position
- **Timing:** All visual updates occur within 16ms (one frame at 60fps)

#### **No Lag Rule**
- ✅ Use CSS `transform: translate()` to move beat during drag (GPU-accelerated)
- ✅ Use CSS `opacity` for overlay effects
- ❌ **NO DOM reordering during drag** – that causes layout thrashing
- ❌ **NO layout recalculations** until drag completes
- ✅ Beat position confirmed only after drop

#### **Animation After Drop**
- **Gentle slide:** If drop destination is >2 positions away, beat slides to final position (0.1-0.2s ease)
- **Instant snap:** If drop destination is <2 positions away, no animation (instant)
- **Purpose:** Visual confirmation without distraction

### Multi-Beat Reordering
- **Keyboard:** Ctrl+Shift+↑/↓ moves current beat (or batch if selected)
- **Batch move:** If 3+ beats selected and user moves them, treat as atomic undo/redo
- **Visual:** Light blue overlay on all selected beats while moving

### Validation Rules
- ✅ Cursor sync verified: drag beat, confirm no visible lag between cursor and beat
- ✅ Drop zone preview shows target position before release
- ✅ Animations (if any) do NOT interfere with cursor tracking

### Implementation Notes
- Use React DnD or manual `onMouseMove` tracking for precise cursor sync
- Measure performance: drag operations should not exceed 16ms per frame
- Test on slow devices: verify beat follows cursor even on lower-end hardware
- For Slate.js beats: hide editor during drag, restore after drop (prevents state corruption)

---

## 7. UNDO/REDO: Strict Atomic Semantics

### Principle
**Undo applies to entire operation, not individual steps.**
If user moves 3 beats, one undo should return all 3 to previous positions.

### Semantics

#### **Single Operation**
- Move beat #5 → Act 2
- **Undo:** Beat #5 returns to previous position (e.g., Act 1)
- **Redo:** Beat #5 moves back to Act 2

#### **Batch Operation**
- Select beats #3, #5, #7 → Move all to Act 2
- **Single undo:** All three beats return to previous positions (treated as ONE operation)
- **Single redo:** All three beats move back to Act 2

#### **Sequential Operations**
- Move beat #1 up → Move beat #3 down → Edit beat #7
- **Undo 1x:** Beat #7 edit undone
- **Undo 2x:** Beat #3 move undone
- **Undo 3x:** Beat #1 move undone
- **Redo 1x:** Beat #1 move redone
- **Redo 2x:** Beat #3 move redone
- **Redo 3x:** Beat #7 edit redone

### Implementation
- Store entire batch operation as single undo/redo entry
- Example: `{ type: 'move-beats', beatIds: [3, 5, 7], fromScene: 'Act1', toScene: 'Act2', timestamp }`
- Debounce content edits: rapid keystrokes within 500ms are treated as single edit operation

### Validation Rules
- ✅ Multi-beat operations are atomic (one undo/redo)
- ✅ Content edits with <500ms between keystrokes are batched
- ✅ User expects "Ctrl+Z" to undo last meaningful action, not last keystroke

### Implementation Notes
- Track `undoStack` and `redoStack` as arrays of operations
- Each operation includes: type, affected beats, old state, new state, timestamp
- Debounce content edits; batch keystrokes into single "edit" operation

---

## 8. ERROR RECOVERY: Simple & Focused

### Principle
After crash, provide minimal, clear recovery path.

### Crash Recovery Flow

#### **On App Launch After Crash**
1. **Check for unsaved draft:** Look for `sessionStorage.lastDraft` (volatile, not persisted to IndexedDB)
2. **If draft exists:**
   - Show minimal modal: "Your draft from X minutes ago is available. Recover?"
   - Buttons: [Recover] [Start Fresh]
3. **Recover path:** Load draft into editor; mark all beats as "unsaved" (red dot)
4. **Start Fresh path:** Clear session; begin blank document

#### **Visual Feedback**
- Modal appears centered, no animations
- Buttons are large (touch-friendly) and clearly labeled
- Show timestamp of last draft: "Draft from 2:45 PM (5 min ago)"

#### **Validation Rules**
- ✅ One clear recovery path (yes/no decision)
- ✅ No diff viewer or complex options (defer to Phase 2 snapshots)
- ✅ Draft is volatile (discarded on normal app close, only survives crash)

### Future Enhancement (Backlog)
- **Phase 2+:** Implement Scrivener-like snapshots system with diff tracking
- **Phase 2+:** Regular automated backups with version history

### Implementation Notes
- Store draft in `sessionStorage` (survives page refresh, wiped on normal close)
- On app startup: check `sessionStorage` for draft; if found + not same as localStorage, show recovery modal
- Recovery path: load draft into state, set all beats to `unsaved = true`, trigger visual indicators

---

## 9. SAVE STRATEGY: localStorage + Autosave + Visual Indicators

### Principle
Users should never worry about data loss. Autosave is always running.

### Save Architecture

#### **Autosave Mechanism**
- **Trigger:** Any content change (beat edit, move, annotation, scene change)
- **Debounce:** 500ms (batch rapid edits)
- **Target:** localStorage (Phase 1A only)
- **On success:** Green checkmark badge appears briefly on affected beat
- **On failure:** Red dot appears; user can click "Retry"

#### **Manual Save**
- **Keyboard:** Ctrl+S forces immediate save (even if debounce pending)
- **Feedback:** "Saved" badge appears in status bar (1s visible)

#### **Visual Persistence Indicators**
- **Red dot:** Unsaved changes (beat has pending edits not yet written to localStorage)
- **Green checkmark:** Save successful (appears after autosave completes)
- **Status bar:** Shows "X beats unsaved" or "All saved"

#### **Validation Rules**
- ✅ Autosave runs without user intervention
- ✅ Visual indicators show save state (red = unsaved, green = saved)
- ✅ No data loss on page close/crash (recovery draft in sessionStorage)
- ✅ localStorage quota monitoring (warn if >80% full)

### Implementation Notes
- Debounce autosave: `_.debounce(saveBeats, 500)`
- Track unsaved state per beat: `beat.unsaved = true | false`
- On mount: hydrate from localStorage; check for sessionStorage draft (crash recovery)
- Monitor localStorage size; warn user at 80% quota

---

## 10. FUTURE BACKLOG (NOT Phase 1A)

### Deferred Features
- ❌ **Search/filter annotations** (Phase 1B)
- ❌ **Snapshots + diff tracking** (Phase 2+)
- ❌ **Cloud sync / Firebase** (Phase 2+)
- ❌ **Custom annotation types** (Phase 1B+)
- ❌ **Collapsible scene tree** (Phase 1C+)
- ❌ **Export functionality** (Phase 2+)
- ❌ **Timeline/chronological views** (Indefinite)

---

## Implementation Checklist

### Keyboard Shortcuts
- [ ] Double Return → New beat
- [ ] Ctrl+↑/↓ → Navigate beats
- [ ] Ctrl+Shift+↑/↓ → Move beat
- [ ] Ctrl+A → Toggle annotation mode
- [ ] Ctrl+; → Add annotation
- [ ] Ctrl+F → Flow mode
- [ ] Ctrl+Z/Shift+Z → Undo/Redo
- [ ] Ctrl+S → Force save

### Visual Feedback
- [ ] Green underline on new beat
- [ ] Red dot on unsaved beat
- [ ] Green checkmark on save success
- [ ] Yellow badge on annotation
- [ ] Blue overlay on DnD

### Annotation System
- [ ] Toggle: View/Minimize/Hide modes
- [ ] Type icons + colors (Note, Synopsis, Character, Research, Custom)
- [ ] Badges show annotation type + count
- [ ] Minimized badges clickable for inline popover

### Beat Tracking
- [ ] Last-edited pin in sidebar
- [ ] Ctrl+Home → Jump to last-edited beat
- [ ] Breadcrumb: Project > Scene > Beat
- [ ] Breadcrumb visible at all times (even in flow mode)

### DnD
- [ ] Cursor-synchronized movement (CSS transform)
- [ ] Drop zone preview
- [ ] Gentle slide animation after drop (if >2 positions)
- [ ] No lag between cursor and beat

### Undo/Redo
- [ ] Atomic operations (batch moves = 1 undo)
- [ ] Debounced content edits (500ms)
- [ ] Undo/redo stack management

### Error Recovery
- [ ] Crash detection + sessionStorage draft
- [ ] Simple "Recover? Yes/No" modal
- [ ] Draft loaded with "unsaved" indicators

### Save Architecture
- [ ] Autosave with 500ms debounce
- [ ] localStorage persistence
- [ ] Save state indicators (red/green)
- [ ] Status bar: "X beats unsaved" or "All saved"

---

## Validation Summary

✅ **Keyboard-first:** All core workflows accessible without mouse
✅ **Visual-only feedback:** NO audio, NO haptic
✅ **Functional clutter:** Annotations always visible (unless explicitly hidden)
✅ **Cursor-sync DnD:** Beat moves immediately with cursor
✅ **Annotation toggles:** View/Minimize/Hide with distinct behaviors
✅ **Color-coded acts:** Black/Blue/Green scenes for easy navigation
✅ **Last-edited tracking:** Ctrl+Home always finds where you left off
✅ **Strict undo/redo:** Multi-beat operations are atomic
✅ **Simple recovery:** Yes/No modal after crash, no complex options
✅ **Auto-persistence:** Autosave with visual indicators

---

## Next Steps

1. **Implement Phase 1A UX per this spec**
2. **Test keyboard shortcuts** with real writing workflows
3. **Validate annotation toggle modes** with actual use
4. **Monitor DnD performance** (cursor sync, no lag)
5. **Gather feedback** after first week of use
6. **Iterate** on annotation type colors if needed

---

**Status:** ✅ Ready for implementation
**Last Updated:** 2026-02-13
**Owner:** Savannah
**Facilitator:** Mary (Business Analyst)
