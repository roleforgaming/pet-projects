---
stepsCompleted: [1]
inputDocuments: []
session_topic: 'MVP Prototype for Writers Suite with Block-Structured Editor & Positive Pet Gamification'
session_goals: 'Define core features for rapid prototype sprint - block editor + inline metadata + supportive pet mechanics. Personal hobby project with future commercial potential.'
selected_approach: 'PAL Collaborative Brainstorming + User Context Integration'
techniques_used: ['collaborative-thinking', 'mvp-constraint-analysis', 'prototyping-strategy', 'user-context-refinement']
ideas_generated: []
context_file: ''
---

# Brainstorming Session: Writers Suite MVP Prototype

**Facilitator:** Claude Code
**User:** Savannah
**Date:** 2026-02-11
**Project Type:** Solo developer, personal hobby project with future commercial potential
**Focus:** Rapid prototype to validate core editor + positive gamification mechanics

---

## Session Overview

**Topic:** MVP Prototype for Writers Suite with Block-Structured Editor & Inline Metadata
**Goals:** Build foundation that validates the core vision (structured editor + inline metadata + encouraging pet) before expanding to non-core features

**Core Innovation:** Externally simple document experience powered by internal block tree structure, with inline metadata annotations that stay with content when reorganized

---

## Brainstorming Results: REVISED Core Prototype Vision

### 1. WRITER CORE (THE FOUNDATION - Non-Negotiable)

This is the reason the app exists. Everything else supports it.

#### **The Editor: Externally Simple, Internally Structured**

**What Users See:**
- Single continuous document presentation
- Natural writing experience
- Drag-and-drop reorganization feels intuitive

**Internal Architecture:**
- Tree-structured hierarchy: `Acts > Chapters > Scenes`
- Each block is a content node with metadata
- Reorganization preserves all annotations as blocks move

**Example Structure:**
```
Act I
  └─ Chapter 1: The Arrival
      ├─ Scene 1: Annie's Discovery
      └─ Scene 2: The Fire in Her Hands
  └─ Chapter 2: Consequences
      └─ Scene 3: The Panic

Dragging Scene 2 to Chapter 2 carries all its metadata with it.
```

#### **Inline Metadata Annotations (The Innovation)**

Users embed structured data *within* the text using symbols. Metadata is inline but visually distinct:

| Symbol | Purpose | Example |
|--------|---------|---------|
| `@` | Tags/categories | `@Annie`, `@POV-shift` |
| `>>...<<` | Notes/research reminders | `>>Research panic attack symptoms<<` |
| `$$` | Synopsis/summary | `$$Annie experiences puzzling symptoms` |
| `//` | Comments/author notes | `//She's having a panic attack` |

**Full Example:**
```
@Annie looked at her hands. They felt like they were on fire, or like she was
holding fire. >>Research symptoms that match this<< Her chest tightened and after
a moment a gasp forced a gulp of air into her lungs. //She's having a panic attack
$$Annie experiences some puzzling symptoms and is worried about what they might mean.
```

**Critical Feature:** When you drag Scene 2 to a different chapter, all those annotations travel with it intact.

**Visual Design:**
- Each annotation type has distinct color/styling
- Annotations are visually demarcated but don't clutter
- Metadata is searchable and filterable

### 2. PET CORE (SUPPORTIVE GAMIFICATION - Non-Negotiable Philosophy)

Philosophy: **Positive Reinforcement Only. Always.**

#### **What the Pet Does**
- ✅ Reacts with joy/celebration when user completes writing sessions
- ✅ Encourages consistency through visual feedback
- ✅ Grows/evolves as user continues writing
- ❌ NEVER shows sadness, disappointment, or punishment
- ❌ NO guilt mechanics, NO streak breaking messages
- ❌ NO negative feedback for missed goals

#### **Pet Behavior Examples**
- User completes a writing session → Pet celebrates (bounce, happy animation, particles)
- User hits daily goal → Special celebration animation
- User returns next day → Encouraging message + pet excitement
- User hasn't written → Pet remains neutral/happy, no guilt

#### **The Psychology**
- Positive pressure without anxiety
- Encouragement without judgment
- User always feels supported and capable

### 3. Must-Have Features (Week 1-2 Prototype)

#### **Editor Foundation**
- [ ] Block creation and editing at scene level
- [ ] Scene organization (create, rename, delete)
- [ ] Drag-and-drop reordering of scenes within chapters
- [ ] Internal block tree persistence to localStorage
- [ ] Rich text with inline metadata parsing and display

#### **Inline Metadata System**
- [ ] Parse `@`, `>>...<<`, `$$`, `//` annotations in real-time
- [ ] Visual styling for each annotation type
- [ ] Metadata preservation during block reorganization
- [ ] Metadata moves with content when scenes are dragged

#### **Pet & Gamification**
- [ ] Pet component with encouraging animations
- [ ] Pet reacts to session completion (celebration)
- [ ] Session tracking (when user completes writing)
- [ ] Visual feedback for positive actions only
- [ ] Encouragement messages (no guilt messaging)

#### **Persistence**
- [ ] localStorage for document structure and metadata
- [ ] Auto-save on editor changes (debounced)

### 4. Nice-to-Have (If time in prototype window)

- [ ] Acts/Chapters management UI (beyond just scenes)
- [ ] Metadata search/filter functionality
- [ ] Statistics dashboard (words written, sessions completed)
- [ ] Pet customization options (simple skin swap)
- [ ] Session history view

### 5. Deliberately Deferred (Post-Prototype)

These are tempting but don't validate core functionality:

- ❌ Rich text formatting (bold, italic, headers)
- ❌ Export/publishing features
- ❌ Collaborative features
- ❌ Cloud sync / multi-device support
- ❌ Advanced gamification (levels, achievements, badges)
- ❌ Audio/sound effects
- ❌ Sharing or social features

**Rationale:** Build the editor + metadata + positive feedback loop first. Everything else comes after proving the core works for *your* writing.

### 6. Tech Stack & Architecture

#### **Frontend**
- **Framework:** React + TypeScript
- **Editor Approach:**
  - **Decision point:** Build custom block editor OR use Slate.js/Prosemirror
  - Custom = more control, longer build time
  - Framework = faster iteration, less control
- **State Management:** Zustand or Context API
- **Persistence:** localStorage for prototype; IndexedDB later for larger documents
- **Animation:** Framer Motion (smooth pet reactions, celebratory animations)

#### **Data Model (localStorage)**

```javascript
{
  // Document structure
  document: {
    acts: [
      {
        id: "act-1",
        title: "Act I",
        chapters: [
          {
            id: "ch-1",
            title: "Chapter 1: The Arrival",
            scenes: [
              {
                id: "scene-1",
                content: "Annie looked at her hands...",
                metadata: {
                  tags: ["@Annie", "@POV-shift"],
                  notes: [">>Research panic attack symptoms<<"],
                  synopsis: "$$Annie experiences puzzling symptoms...",
                  comments: ["//She's having a panic attack"]
                },
                wordCount: 245,
                createdAt: "2026-02-11T10:30:00Z",
                lastEditedAt: "2026-02-11T14:15:00Z"
              }
            ]
          }
        ]
      }
    ]
  },
  // Pet & engagement state
  petState: {
    lastSessionDate: "2026-02-11",
    totalSessionsCompleted: 23,
    totalWordsWritten: 8240,
    streak: 5,
    lastSessionWordsWritten: 1250
  }
}
```

#### **Pet Visuals**
- Single SVG character with CSS-based mood variations
- Celebratory animations (bounce, sparkles, happy expressions)
- Optional: multiple skins/variations (deferred to post-prototype)

### 7. User Journey (The Experience)

```
Open app
  ↓
See your document structure (acts/chapters/scenes) + pet in corner
  ↓
Click into a scene to edit
  ↓
Write naturally - inline metadata annotations visible
  ↓
Drag scenes between chapters - metadata moves with it
  ↓
Complete writing session (exit/save)
  ↓
Pet celebrates! 🎉 (animation + encouragement)
  ↓
Session is saved automatically
  ↓
Next day: Open app, pet greets you, continue writing
```

**Key:** The editor is the star. The pet is supporting cast that makes writing feel more rewarding.

### 8. Success Criteria (Personal Project Edition)

This is *your* tool, so success means:

- ✅ Block reorganization is intuitive via drag-and-drop
- ✅ Inline metadata doesn't clutter the writing experience
- ✅ Metadata stays with content when reorganized
- ✅ Pet reactions feel genuinely encouraging (not annoying)
- ✅ You want to use it for your actual writing projects
- ✅ Data persists reliably across sessions
- ✅ Writing in this tool feels better than Google Docs/Word

### 9. Development Timeline (2-3 Week Sprint)

#### **Week 1: Editor Foundation**
- **Day 1-2:** React scaffold, decide editor approach (custom vs. framework)
- **Day 3-4:** Basic block/scene creation and editing
- **Day 5-6:** Drag-and-drop reordering (scenes within chapters)
- **Day 7:** localStorage persistence for block structure

#### **Week 2: Inline Metadata + Pet Basics**
- **Day 8-9:** Parse and render inline annotations (`@`, `>>`, `$$`, `//`)
- **Day 10-11:** Pet component with celebratory animations
- **Day 12-13:** Session tracking and pet feedback
- **Day 14:** Polish, test with your own writing, iterate

#### **Week 3+ (If needed): Refinement**
- Use the tool yourself on a real writing project
- Identify UX friction points
- Add Acts/Chapters management if needed
- Plan next features based on actual usage

### 10. Shipping & Future Potential

#### **Phase 1 (Now):** Personal MVP
- Build for yourself
- Validate core editor + metadata + pet feedback works for your writing

#### **Phase 2 (Future):** Expand Capability
- Add Acts/Chapters management
- Metadata search/filtering
- Statistics dashboard
- Simple export options

#### **Phase 3 (Optional):** Consider Others
- If you've built something you love, others might too
- Gather feedback from other writers
- Add collaborative features if desired

#### **Phase 4 (If Ambitious):** Commercial
- Cloud sync, advanced features, premium tiers
- But this is Phase N, not Phase 1

**Philosophy:** Build what YOU love first. Everything else flows from there.

---

## Key Decisions for You

Before starting the build, confirm:

1. **Editor Implementation:** Build custom block editor, or use Slate/Prosemirror?
2. **Annotation Symbols:** Are `@`, `>>`, `$$`, `//` the right symbols, or adjust?
3. **Initial Scope:** Start with Scenes only, or include Acts/Chapters management?
4. **Pet Evolution:** Should pet visually grow/change as you write more?
5. **Timeline:** Can you commit 2-3 weeks, or different pace?
6. **Testing:** Build for yourself, or recruit early testers?
7. **Persistence:** localStorage-only, or Firebase from day 1?

---

## Next Steps

---

## Design Thinking Session Summary (2026-02-11)

A comprehensive **Design Thinking workshop** was conducted to validate and refine the MVP vision using empathy-driven, user-centered design methodology.

### Key Discoveries from User Research

**Savannah's actual writing process:**
- Non-linear, discovery-based: writes beats that grow into scenes → chapters → acts
- Structure emerges FROM the writing, not before it
- Current pain: Scrivener's fast reordering (but loses context) vs. Google Docs' continuous view (but slow reorganization)
- ADHD challenge: "Out of sight, out of mind" with fragmented tools
- Needs: Continuous document + 1-2 click reorganization + instant visual feedback

### MVP Architecture Reframed

**From:** Pre-planned Acts > Chapters > Scenes hierarchy
**To:** Flat-list beats with optional emergent grouping

**Core features:**
- ✅ Flat list of beats (smallest unit, serves outline → draft → edit)
- ✅ Continuous document view (entire story visible, no fragmentation)
- ✅ Multiple reorganization modes (drag + up/down arrows + split/merge)
- ✅ Timeline markers for non-linear editing (internal only, not exported)
- ✅ Status tracking (outline → draft → editing → done)
- ✅ Instant visual feedback (snap animation < 0.5s + flash)
- ✅ Metadata as discovery tool (filter by @tags and #periods)
- ✅ Word count tracking for progress
- ✅ Positive pet feedback on writing completion

### Beat Data Model (Finalized)

```json
{
  "id": "uuid",
  "title": "string",
  "content": "markdown",
  "tags": ["@character", ">>research"],
  "status": "outline | draft | editing | done",
  "timelineId": "timeline-1",
  "wordCount": 0,
  "lastEdited": "ISO-8601-timestamp"
}
```

This model supports the full Writers Suite lifecycle: brainstorm → research → outline → draft → edit → export.

### Timeline Strategy

**Two-view system for non-linear narratives:**
1. **Narrative View** (primary): Beats in story order
2. **Timeline View** (secondary): Beats sorted by period for chronological review

Timeline markers are **internal planning/editing tools only**. Exports will be narrative-order with metadata stripped.

### Full Writers Suite Vision (Future Phases)

| Phase | Workspace | Features |
|-------|-----------|----------|
| 1 | **Outlining** | Beat editor, drag reorganization, timeline assignment |
| 2 | **Drafting** | Content growth, split/merge, word count, pet feedback |
| 3 | **Editing** | Advanced filtering, period/tag search, timeline review |
| 4 | **Publishing** | Export to .docx/.pdf/.epub (metadata stripped) |

### Design Validation Plan

**7 testing tasks** identified to validate intuitive-ness:
1. Micro-reorganization with arrows (goal: ≤ 5 sec)
2. Macro-reorganization with drag (goal: ≤ 5 sec)
3. Beat splitting (goal: ≤ 10 sec)
4. Timeline period assignment (goal: ≤ 3 sec)
5. Timeline view toggle (goal: understand purpose)
6. Period-based filtering (goal: find beats quickly)
7. Freeform writing experience (goal: ≥ 4/5 satisfaction)

**Success criteria:**
- ≤ 5 seconds per reorganization task
- ≤ 2 mental steps to think through interaction
- ≥ 4/5 rating on intuitive-ness
- Preference over both Google Docs and Scrivener

### Next Steps (When Ready to Build)

1. ☐ Build interactive prototype (flat-list beat editor with core features)
2. ☐ Run 7 testing tasks with Savannah
3. ☐ Validate intuitive-ness of reorganization
4. ☐ Iterate based on feedback
5. ☐ Build pet component with positive feedback
6. ☐ Test with real manuscript during drafting/editing

---

## First Principles Refinement Session (2026-02-11)

### Core Insights from Clarification

Through rigorous first-principles questioning and deep clarification, several assumptions were validated OR fundamentally shifted:

#### **VALIDATED - Non-Negotiable Elements:**
- ✅ **Pet is the differentiating feature** - Not just gamification, but digital body doubling for ADHD support
- ✅ **Inline annotations are essential** - Sidebar breaks cognitive continuity; brain needs instant context
- ✅ **Continuous document view is PRIMARY** - Flow state preservation is critical
- ✅ **Atomic beats (no sub-structure)** - Prevents over-engineering, allows emergent organization

#### **REVISED - Annotation System Architecture:**
- ❌ **Removed:** Preset annotation types (@, >>, $$, //)
- ✅ **New:** Freeform user-defined prefixes (defined globally in settings, not per-project)
- ✅ **Dynamic:** @ tags created inline on-the-fly (no preset list)
- ✅ **Three-state annotation display:**
  1. **Show Annotations** - Full visibility of inline annotations
  2. **Minimize Annotations** - Faintly colored underlines show annotated text (visual indicator without clutter)
  3. **Hide Annotations** - Complete invisibility (no visual indicator)
- ✅ **Smart creation:** When hidden, new annotations auto-hide immediately after creation/escape

#### **REFINED - Pet Gamification (ADHD Body Doubling):**
The pet serves 4 simultaneous functions:
1. **Body Doubling** - Provides accountability presence for ADHD writers
2. **Progress Visualization** - Concrete micro-rewards for visible output
3. **Motivational Scaffolding** - Celebrates process, not just completion
4. **Dopamine Support** - Active typing animation + partial progress celebration

#### **NEW - Reward System Architecture:**
**Reward Triggers (In Priority Order):**
1. **Active Typing** → Pet happy animation (immediate, micro-reward)
2. **Partial Progress** → Pet celebration/encouragement (milestone feedback)
3. **Daily Goal Met** → Session completed, major pet celebration
4. **Idle > 5 minutes** → Pet takes a nap (context-aware rest, wakes on typing only)

**Goal System:**
- **Daily Word Count Goal:** User sets as percentage of total manuscript goal
- **Total Manuscript Goal:** User selects genre from dropdown (auto-calculates average for genre) OR sets custom value
- **Defaults Provided:** Short Story, Novella, Novel, Novella+, Epic
- **Goals Editable Anytime** - Can adjust during project

#### **CRITICAL - Word Count Calculation:**
- **Counts toward goals:** Text outside annotation markers ONLY
- **Example:** "Annie looked at her hands >>>fear of fire<<<. She gasped." = **7 words** (prose only)
- **Excludes:** All annotation markers, prefixes, and annotation content

#### **DEFERRED - Corkboard View (Phase 2):**
- Card-based view ideal for outlining phase, but not MVP critical
- Will implement after core editor + pet + continuous view validated

### Revised MVP Scope (Validated)

**Must-Have for MVP (Week 1-2):**

**Editor Core:**
- [ ] Flat-list beat editor (create, edit, delete beats)
- [ ] Continuous document view with all beats rendered
- [ ] Drag-and-drop beat reordering
- [ ] Up/down arrow buttons for micro-reorganization
- [ ] Real-time word count (manuscript words only)

**Annotation System:**
- [ ] Global settings for annotation prefixes (user-defined)
- [ ] @ tags created inline on-the-fly with autocomplete
- [ ] Three-state annotation display (Show/Minimize/Hide)
- [ ] Auto-hide new annotations when in hidden mode
- [ ] Faint underlines for minimized annotations

**Pet Gamification:**
- [ ] Pet sprite with happy/napping animations
- [ ] Active typing → happy animation
- [ ] Partial progress celebration (e.g., 50% daily goal)
- [ ] Daily goal met → major celebration
- [ ] Idle nap detection (> 5 min typing idle, wake on typing only)
- [ ] Visual progress indicator (daily/total word count toward goals)

**Goal Management:**
- [ ] Genre-based total manuscript goal (dropdown selection)
- [ ] Daily goal as percentage of total
- [ ] Settings to customize goals anytime

**Persistence:**
- [ ] localStorage for beats, annotations, word counts
- [ ] Auto-save on content changes (debounced)

**Nice-to-Have (If Time in MVP Window):**
- [ ] Beat splitting/merging
- [ ] Basic beat metadata (created date, last edited, word count)
- [ ] Session history (daily streak, total words written)

### Data Model (Refined)

```javascript
// Global Settings (localStorage: "writersSuite_globalSettings")
{
  annotationPrefixes: [
    { prefix: ">>", label: "Research Notes", color: "#FFA500" },
    { prefix: "##", label: "Character Notes", color: "#9370DB" },
    { prefix: "!!", label: "Plot Points", color: "#FF6B6B" }
    // User can add/edit/delete prefixes
  ],
  tagColor: "#FFD700" // @ tag color (globally customizable)
}

// Project (localStorage: "writersSuite_projects_{projectId}")
{
  id: "project-uuid",
  title: "My Novel",
  genre: "Science Fiction",
  totalManuscriptGoal: 90000, // From genre or custom
  dailyWordCountGoal: 1800, // As percentage (2% of 90k)
  createdAt: "ISO-8601",
  lastEditedAt: "ISO-8601"
}

// Beats (localStorage: "writersSuite_beats_{projectId}")
[
  {
    id: "beat-uuid",
    projectId: "project-uuid",
    title: "Scene: Annie's Discovery",
    content: "Annie looked at her hands >>>fear of fire<<<. She gasped.",
    annotations: [
      {
        prefix: ">>",
        startIndex: 30,
        endIndex: 44,
        content: "fear of fire"
      }
    ],
    manuscriptWordCount: 7, // Calculated, excluding annotation markers
    totalWordCount: 12, // Including annotations
    status: "draft", // outline | draft | editing | done
    createdAt: "ISO-8601",
    lastEditedAt: "ISO-8601"
  }
]

// Pet State (localStorage: "writersSuite_petState_{projectId}")
{
  projectId: "project-uuid",
  lastSessionDate: "2026-02-11",
  totalSessionsCompleted: 0,
  totalManuscriptWordsWritten: 0,
  currentDayWordsWritten: 0,
  streak: 0,
  lastActivityTime: "ISO-8601",
  isNapping: false,
  mood: "happy" // happy | napping | excited
}

// Session Tracking (localStorage: "writersSuite_sessions_{projectId}")
[
  {
    date: "2026-02-11",
    wordsWritten: 1250,
    goalMet: true,
    sessionsCompleted: 1,
    celebrationTriggered: true
  }
]
```

### Implementation Priority

**PHASE 1A (Days 1-3): Foundation**
- React scaffold + TypeScript setup
- localStorage persistence layer
- Global settings UI (annotation prefixes, @ tag color)
- Beat CRUD operations

**PHASE 1B (Days 4-6): Editor + Display**
- Beat list rendering (continuous view)
- Content editing with annotation parsing
- Annotation display with three-state toggle
- Word count calculation (manuscript vs. total)

**PHASE 1C (Days 7-9): Reorganization**
- Drag-and-drop beat reordering
- Up/down arrow buttons
- Instant feedback animations (< 0.5s snap)

**PHASE 1D (Days 10-12): Pet + Gamification**
- Pet sprite/animation component
- Reward trigger system (typing, partial progress, goals met)
- Idle detection and napping
- Goal setup and tracking UI

**PHASE 1E (Days 13-14): Polish + Testing**
- Use with real manuscript excerpt
- Iterate based on UX feedback
- Bug fixes and refinement

### Critical Decisions (Finalized)

1. ✅ **Editor:** Custom React component (more control than Slate/Prosemirror for annotation handling)
2. ✅ **Annotation Prefixes:** Global settings, user-defined, freeform
3. ✅ **@ Tags:** Dynamically created inline, always customizable globally
4. ✅ **Initial Scope:** Beats only (no Acts/Chapters/Scenes nesting in MVP)
5. ✅ **Pet Evolution:** Static for MVP; visual growth as feature in Phase 2
6. ✅ **Persistence:** localStorage for MVP; Firebase/sync in Phase 2+
7. ✅ **Corkboard View:** Phase 2 (after core validated)
8. ✅ **Word Count:** Manuscript words only (excludes all annotation content/markers)
9. ✅ **Daily/Total Goals:** User-configurable with genre defaults
10. ✅ **Reward Triggers:** Typing animation + partial progress + goal completion + idle nap

---

## Role Playing Method Analysis (2026-02-12)

### Stakeholder Perspectives Explored

Using the Role Playing brainstorming method, five key personas were analyzed to identify hidden priorities, tensions, and requirements:

#### **1. The Professional Editor**
- **Initial Concern:** Gamification might trivialize professional work
- **Resolution:** Export-to-Word with toggle for annotation visibility addresses this
- **Key Insight:** Editors need clean manuscripts for collaboration; annotations are research tools for writers, not editorial inputs
- **Validation:** .docx export (with/without annotations) aligns with professional workflows

#### **2. The Frustrated Writer**
- **Initial Concern:** Flat beats might feel limiting vs. Scrivener's hierarchy
- **Resolution:** Hierarchical organization (Acts > Chapters > Scenes) with drag-and-drop grouping
- **Key Insight:** Writers think hierarchically even if UI presentation is continuous; nesting enables intuitive reorganization
- **Validation:** Moving entire chapters with contained scenes requires true hierarchical nesting

#### **3. The ADHD Creator**
- **Initial Concern:** Static pet animations become invisible after first week
- **Resolution:** Variability-rich pet with micro-rewards for small progress
- **Key Insight:** Dopamine requires unpredictability; rewarding "wrote 50 words" is as valuable as "completed daily goal"
- **Validation:** Pet should celebrate progress continuously, not just milestones

#### **4. The Commercial Product Manager**
- **Initial Concern:** Need analytics to understand user retention and differentiation
- **Resolution:** Analytics deferred to Phase 2; focus on building the engagement loop itself in MVP
- **Key Insight:** Data collection can wait; validating the core behavioral loop is Phase 1
- **Validation:** Ship the product, gather usage data naturally, iterate in Phase 2

#### **5. The Developer (Savannah)**
- **Initial Concern:** Scope creep from multiple stakeholder demands
- **Resolution:** Clear MVP definition with deferred features (sharing, advanced analytics, multi-device sync)
- **Key Insight:** Joy and momentum matter more than feature completeness
- **Validation:** Focus on building an editor YOU love first; others follow

### Resolved Tensions

| Point | Previous Assumption | New Clarity |
|-------|-------------------|------------|
| **Pet Philosophy** | Simple animations | Variability-rich + customizable; micro-rewards over milestones |
| **Hierarchy** | Flat beats only | Acts > Chapters > Scenes (true nesting for grouping/reorganization) |
| **Export** | Phase 2 feature | Must-have MVP (with annotation toggle for clean exports) |
| **Annotations** | Visible or invisible | Toggle for writers' research view; clean export for editors |
| **Scope** | Multiple features | Focused MVP: editor + hierarchy + annotations + pet + export |
| **Editing Workflow** | Generic export | Professional .docx export for editor collaboration |
| **Analytics** | Required for V1 | Phase 2 (gather usage data organically) |
| **Sharing** | Out of scope | Future phase (beta reading / peer editing, not professional) |

### MVP Redefined Through Clarification

**Must-Have for MVP:**

**Editor Core**
- [ ] Hierarchical beat organization (Acts > Chapters > Scenes)
- [ ] Continuous document view (all scenes rendered continuously)
- [ ] Drag-and-drop scene reordering within chapters
- [ ] Drag-and-drop chapter reordering within acts
- [ ] Up/down arrow buttons for micro-reorganization
- [ ] Real-time manuscript word count (excludes annotations)

**Annotation System**
- [ ] Global settings for annotation prefixes (user-defined)
- [ ] @ tags created inline with autocomplete
- [ ] Three-state annotation display (Show/Minimize/Hide)
- [ ] Auto-hide new annotations when in hidden mode

**Export Functionality (CRITICAL MVP)**
- [ ] Export to .docx with clean formatting
- [ ] Toggle: Include annotations or clean manuscript only
- [ ] Preserve hierarchy in export (acts, chapters visible in document structure)
- [ ] Annotation content stripped from "clean" export

**Pet Gamification (ADHD-Focused)**
- [ ] Pet sprite with varied celebration animations (not repetitive)
- [ ] Micro-rewards for small progress (50 words = celebration, not just daily goals)
- [ ] Active typing → happy animation (immediate feedback)
- [ ] Variability in reward triggers (celebrate every 100 words, then 250, then 500 in session)
- [ ] Daily goal met → major celebration
- [ ] Idle nap detection (> 5 min, wakes on typing only)
- [ ] Visual progress toward daily/total goals
- [ ] Customizable pet behaviors/appearance (Phase 2)

**Goal Management**
- [ ] Genre-based total manuscript goal selection
- [ ] Daily goal as percentage of total (customizable)
- [ ] Settings UI for goal adjustments anytime

**Persistence**
- [ ] localStorage for all data (Acts, Chapters, Scenes, Annotations, Goals, Pet State)
- [ ] Auto-save on content changes (debounced)

### Deferred Features (Phase 2+)

- ❌ Multi-device cloud sync
- ❌ Real-time collaborative editing
- ❌ Share links with commenting permissions
- ❌ Advanced analytics dashboard
- ❌ Pet evolution/customization
- ❌ Beta reader/peer editing features
- ❌ Publishing/submission workflows

### Key Insights from Role Playing

1. **Neurodivergent Writers as Beachhead:** ADHD creators are your ideal first users. They'll adopt tools that provide behavioral scaffolding (like your pet + micro-rewards). This segment is underserved and highly engaged.

2. **Export ≠ Betrayal of Vision:** Professional export isn't surrendering to "traditional tools"—it's enabling writers to use your tool for their creative process, then hand off clean work to editors who use Word. You don't compete with Word; you become the "before Word" tool.

3. **Hierarchy is Essential for Workflow:** True nesting (Acts > Chapters > Scenes) isn't overengineering—it's a core requirement for your own use case. Moving chapters with all scenes intact is fundamental to non-linear writing.

4. **Pet Variability is Non-Negotiable:** For ADHD users, predictable rewards stop working within days. Variable, frequent micro-rewards (celebrate every X words, where X changes) create sustainable engagement without guilt.

5. **Annotations as Discovery Tool:** Annotations aren't just metadata—they're how writers think through problems while drafting. Toggling them off for export respects both the creative process and the professional handoff.

### Next Steps from Role Playing

1. ✅ **Clarify MVP Scope**: Hierarchy + Export + Variability-Rich Pet = Core Value
2. ✅ **Validate Technical Approach**: Decide between custom editor (more control) vs. Slate/ProseMirror (faster build)
3. ✅ **Design Reward Variability**: Create algorithm for unpredictable but frequent pet celebrations
4. ✅ **Plan Export Architecture**: .docx generation with conditional annotation stripping

---

