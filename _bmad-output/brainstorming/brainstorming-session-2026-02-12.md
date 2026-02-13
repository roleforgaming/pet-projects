---
stepsCompleted: [1, 2, 3]
inputDocuments:
  - "D:\\Development\\pet-projects\\docsref\\MVP_SPEC.md"
  - "D:\\Development\\pet-projects\\docsref\\design-thinking-2026-02-11.md"
session_topic: 'Technical Decision Validation & Constraint Analysis for Writers Suite MVP Phase 1A'
session_goals:
  - 'Validate technology stack choices (Slate.js, custom hooks, localStorage)'
  - 'Identify root causes behind architectural decisions using Five Whys'
  - 'Clarify scope constraints for Phase 1A sprint'
  - 'Establish annotation search/filter implementation strategy'
selected_approach: 'Deep Analysis with Five Whys + Failure Analysis'
techniques_used:
  - 'Five Whys Analysis (Deep)'
  - 'Constraint Mapping (Planned)'
  - 'Failure Analysis (Planned)'
  - 'PAL Technical Research'
ideas_generated: []
context_file: 'D:\Development\pet-projects\_bmad\bmm\data\project-context-template.md'
---

# Brainstorming Session Results

**Facilitator:** Savannah
**Date:** 2026-02-12
**Session Type:** Technical Decision Validation & Deep Analysis

---

## Session Overview

This brainstorming session focused on **validating core technical decisions** for Writers Suite MVP Phase 1A through systematic Five Whys root cause analysis and expert technical research. The session uncovered critical clarifications about scope, validated the technology stack, and established implementation patterns for complex features.

---

## Major Clarifications & Scope Changes

### User Requirements Clarification
1. **Rich Text Editor Requirement:** MVP requires rich text editing (NOT plain text)
   - Original assumption was custom annotation parsing with minimal framework overhead
   - New reality: MVP needs robust rich text editing + annotation search/filtering
   - **Impact:** Requires choosing industrial-strength rich text library

2. **Annotation Filtering:** Both prefix-type AND content-based search required
   - Search by annotation type (>>, ##, !!)
   - Search by content within annotations
   - Requires optimized indexing strategy

3. **Global vs. Per-Project Settings:** Confirmed GLOBAL annotation prefixes
   - Same prefixes (notes, comments, synopsis, custom tags) across all projects
   - Reduces configuration friction for ADHD-focused UX

4. **Market Scope:** Self-directed (not marketability-focused)
   - Strictly meeting personal needs
   - Market fit is a bonus, not a constraint
   - Frees design decisions from general-writer compromises

5. **Developer Context:** AI-coded implementation
   - Complex state management possible with AI development
   - Custom hooks template not required
   - Can justify more sophisticated patterns when beneficial

---

## Five Whys Analysis Results

### Decision #1: Zustand for State Management
**Root Cause:** Sprint constraints prioritized development speed over scaling needs
- Sprint timeline → needed fast validation → unknown ADHD UX risks → no benchmarks exist
- **Trade-off:** Fast iteration now vs. potential state migration costs later
- **Breaking point:** When async middleware + complex relational state emerges

**Updated Decision:** Switch from Zustand to **custom hooks pattern**
- PAL analysis recommended against Zustand for this scope
- Custom hooks better suit: localStorage-only phase, explicit control flow, ADHD cognitive clarity
- Easier Firebase migration path (isolated persistence logic)

### Decision #2: localStorage vs. Cloud/Firebase
**Root Cause:** Backend delays would extend validation timelines; UX polish required for ADHD feedback
- No backend → frontend UX validation focus → ADHD friction = abandonment → UI/flow are key
- **Accepted limitation:** Device-siloed data; no sync/recovery
- **Rearchitecture trigger:** Multi-device usage milestone

### Decision #3: Annotation System Approach
**Original Assumption:** Custom annotation parsing (lightweight, no framework)
**INVALIDATED** by requirement for rich text editing

**New Reality:** Need industrial-strength rich text editor with fine-grained annotation support
- Libraries evaluated: Slate.js, TipTap, ProseMirror, Lexical, Draft.js, Yjs
- **Recommended:** Slate.js

### Decision #4: Global Annotation Prefixes
**Root Cause:** Preventing task-switching friction outweighs customization flexibility
- Config friction → momentum loss → context switching → hyperfocus disruption → ADHD core value
- **Confirmed:** Global prefixes across all projects reduces ADHD friction

### Decision #5: ADHD-First Focus
**Root Cause:** General writer support would obscure unique ADHD requirements
- Serving general users → feature conflicts → mission dilution → UX contradictions
- **Confirmed:** ADHD focus (with bonus general support later) is strategically sound

---

## Rich Text Library Selection Analysis

### Evaluation Process
Researched 7 major libraries against Writers Suite specific constraints:
- Annotation handling + metadata tracking
- Performance at 100k+ words + 50+ beats + 100+ annotations
- Drag-and-drop beat reorganization
- Search/filter efficiency
- Word count accuracy (exclude annotation markers)
- Learning curve for solo developer
- Bundle size + localStorage efficiency
- Customization vs. framework constraints

### Top 3 Recommendations

#### 🥇 **Slate.js** (RECOMMENDED)
**Annotation Support:** ★★★★★ (native metadata)
**Performance @ 100k words:** ★★★☆ (requires virtualization)
**DnD Integration:** ★★★★★
**Search/Filter:** ★★★ (custom indexing efficient)
**Word Count Accuracy:** ★★★★
**Customization:** ★★★★★
**Bundle Size:** 50kB

**Why Slate:**
- Treats annotations as first-class citizens via metadata nodes
- Maximum control for custom prefix system
- DnD safety: clean beat reordering without state corruption
- Annotation indexing pattern provides O(1) search lookups
- Explicit control aligns with ADHD clarity principle

**Implementation Strategy:**
- Phase 1A: Scaffold + basic annotation rendering
- Phase 1B: Annotation search/filter indexing + DnD beats
- Phase 1C: Word count + performance optimization

#### 🥈 **TipTap**
- Faster MVP option (moderate learning curve)
- ProseMirror power with gentler API
- Trade-off: Less granular annotation control
- Better for less ambitious annotation filtering

#### 🥉 **Lexical**
- React-native design (Meta-backed)
- Smallest bundle (30kB)
- Immature ecosystem
- Good for future-proofing

### Critical Implementation Gotchas

1. **Drag-and-Drop State Corruption** ⚠️
   - Libraries serialize editor state during drags → breaks annotation positions
   - **Solution:** React DnD with atomic beat IDs (don't serialize mid-drag)

2. **localStorage Overflow Risk** ⚠️
   - Full document serialization → 5MB breach at scale
   - **Solution:** Save only deltas (changed beats), not full document

3. **Word Count Miscalculation** ⚠️
   - Annotation prefixes often counted as words
   - **Solution:** DOM-level text filtering in Slate

4. **Annotation Filter Complexity** ⚠️
   - Plugin-based search → bundle bloat
   - **Solution:** Custom indexing hook (provided below)

### Annotation Search/Filter Pattern

```typescript
// Build searchable index on document load + edits
const useAnnotationIndex = (beats) => {
  const index = new Map(); // prefix:query → results

  beats.forEach(beat => {
    traverseNodes(beat.content, node => {
      if (isAnnotation(node)) {
        const key = `${node.prefix}:${node.text.toLowerCase()}`;
        if (!index.has(key)) index.set(key, []);
        index.get(key).push({ beatId: beat.id, node });
      }
    });
  });

  return {
    searchByType: (prefix) => index.get(prefix) || [],
    searchByContent: (prefix, query) =>
      index.get(`${prefix}:${query.toLowerCase()}`) || [],
    searchAny: (query) => /* cross-prefix search */
  };
};
```

---

## Updated Technology Stack

### Confirmed Choices
- **Frontend:** React 18+ with TypeScript
- **Rich Text Editor:** Slate.js
- **State Management:** Custom React hooks (NOT Zustand)
- **Persistence:** localStorage (Phase 1A-1B), Firebase Phase 2
- **Animations:** Framer Motion
- **Build Tool:** Vite

### Implementation Patterns
- Custom hooks for: document state, pet state, global settings, localStorage persistence
- External annotation indexing for search/filter (decoupled from editor)
- Delta-based localStorage (save only changes, not full doc)
- Atomic beat IDs for safe DnD reorganization

---

## Decision Rationale Summary

All technology decisions follow a coherent **priority hierarchy**:
1. **Prevent distraction & avoid friction** (ADHD-specific)
2. **Protect writing momentum** (flow state preservation)
3. **Accelerate validation** (learn fast with real usage)
4. **Accept technical debt** (Phase 2 rearchitecture)

This prioritization is **internally consistent** and **orthogonal to generic engineering best practices**.

---

## Next Session Planned

**Constraint Mapping & Failure Analysis**
- Identify immovable constraints vs. flexible scope in Phase 1A
- Map implementation risks from similar tools (Google Docs, Scrivener)
- Define Phase 1A success criteria & acceptance conditions
