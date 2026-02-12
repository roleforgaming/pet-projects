# Design Thinking Session: Writers Suite MVP Prototype

**Date:** 2026-02-11
**Facilitator:** Claude Code
**Design Challenge:** Building an MVP Writer's Editor with Block Structure & Positive Pet Feedback

---

## 🎯 Design Challenge

**How might we create a writing editor that lets Savannah see her entire continuous document AND reorganize blocks with instant visual feedback, while supporting her emergent, non-linear writing process?**

---

## 👥 EMPATHIZE: Understanding Users

### User Insights

**Savannah's Writing Journey:**
- Experienced writer across multiple tools: Scrivener, Google Docs, Word, Obsidian MD
- **Scrivener strength:** Easy reordering of scene files → BUT creates "out of sight, out of mind" problem (ADHD challenge)
- **Google Docs strength:** Continuous document view → BUT reorganization is painfully slow and lack of instant visual feedback
- **Core need:** Scrivener's reordering power + Google Docs' continuous document view + instant visual feedback

**Mental Model of Writing Structure:**
- Does NOT think in pre-planned Acts > Chapters > Scenes hierarchy
- **Actual process:** Beats (smallest units) → organically grow into scenes → only then determines chapter placement → finally discovers act placement
- **Key phrase:** "The structure emerges FROM the writing, not before it"
- Writing is deeply non-linear: jumps around the timeline, discovers structure emergently

**Reorganization Patterns:**
- Occasional "big reshuffles" early in the writing process
- Frequent "micro-adjustments" during editing phase
- Depends on how many scenes are created and whether she's hopping around the timeline
- Needs 1-2 click reorganization with INSTANT feedback (critical for ADHD working memory)

**Pain Points with Current Tools:**
- Scrivener: Can't see the whole story at once (context loss)
- Google Docs: Reorganization feels slow and laborious (no instant visual feedback)
- All tools: Disconnect between mental model (emerge from writing) and tool model (pre-defined structure)

### Key Observations

1. **The structure-emergence problem is the core design challenge** – Most writing tools assume hierarchical pre-planning. Savannah writes emergently, discovering structure as content develops.

2. **ADHD + visibility = critical combination** – For Savannah, "out of sight" means forgotten. The tool must show her entire document continuously to reduce cognitive load.

3. **1-2 clicks + instant feedback is non-negotiable** – She's experienced the friction of slow reorganization. The interaction must feel as fast as her thinking.

4. **Scrivener + Docs = ideal experience** – She knows exactly what she wants; we just need to build it specifically for her workflow.

5. **Metadata is secondary to flow** – In an emergent structure, the ability to quickly locate and reorganize beats is more important than rigid tagging systems.

### Empathy Map Summary

**Says:**
- "I struggle with 'out of sight, out of mind'"
- "I don't write from point A to point B"
- "I reorganize depending on how many scenes are created"
- "Beats grow into scenes... structure emerges"

**Thinks:**
- *How do I keep the whole story visible while writing?*
- *Where does this beat actually belong?*
- *I need to move this scene, but Docs makes it so tedious*

**Does:**
- Starts with multiple beat fragments across timeline
- Writes non-linearly, jumping between time periods
- Frequently reshuffles to find the right narrative flow
- Uses multiple tools to work around their limitations

**Feels:**
- Frustrated by slow reorganization (cognitive burden)
- Anxious about losing context ("out of sight, out of mind")
- Excited about tools that give instant feedback
- Constrained by pre-defined hierarchies that don't match her thinking

---

## 🎨 DEFINE: Frame the Problem

### Point of View Statement

**Savannah, a non-linear writer, needs a tool that shows her entire document continuously AND lets her reorganize beats in 1-2 clicks with instant visual feedback, because her story structure emerges from writing itself, not from pre-planning.**

### How Might We Questions

1. **How might we show a continuous document that supports emergent hierarchies** (starting flat, optionally grouping later)?
2. **How might we make reorganization feel as instant as thinking** (≤ 5 seconds per move, clear visual confirmation)?
3. **How might we support non-linear writing** without forcing a pre-planned structure upfront?
4. **How might we use metadata (tags, notes) to help locate beats** without requiring hierarchical organization?
5. **How might we prevent "out of sight, out of mind"** while keeping the interface clean?

### Key Insights

1. **Flat-first, hierarchical-optional** – Start with a simple vertical list of beats. Add optional chapter/act grouping later, when Savannah is ready to impose structure.

2. **Emergent structure changes everything** – The traditional Acts > Chapters > Scenes hierarchy doesn't fit her workflow. We need to support fluidity.

3. **Visibility is a cognitive accessibility tool** – For ADHD, seeing the whole document isn't a nice-to-have; it's essential to maintaining context.

4. **Instant feedback is interaction design** – The reorganization interaction must feel *immediate*. Slow visual feedback = cognitive burden.

5. **Metadata serves discovery, not organization** – Tags (@character, >>research, etc.) help find related beats, not organize them. They're secondary to the core reorganization need.

---

## 💡 IDEATE: Generate Solutions

### Selected Methods

- **Emergent Design Thinking** – Design for how Savannah actually writes, not how tools assume writers should work
- **Interaction Design Focus** – Prioritize speed and feedback over feature richness
- **Accessibility-First** – Design for ADHD cognitive patterns from day one

### Generated Ideas

**Core Architecture: Flat-List with Optional Emergent Grouping**

1. **Flat List of Beats (Primary MVP)**
   - Vertical scrollable document showing all beats continuously
   - Each beat is a draggable block containing content + metadata
   - No pre-defined hierarchy (no Acts/Chapters folders)
   - Solves: "continuous document" + "see everything" needs

2. **Three-Mode Reorganization System**
   - **Drag-and-drop:** For any-to-any repositioning (intuitive visual interaction)
   - **Up/Down arrow buttons:** For micro-adjustments (1-click swaps between adjacent beats)
   - **Keyboard shortcuts:** `Ctrl+↑/Cmd+↓` for power users and rapid micro-moves
   - Solves: "1-2 clicks + instant" reorganization

3. **Instant Visual Feedback**
   - Snap animation (< 0.5s) when block is dropped
   - Subtle background flash (light green, 300ms) to confirm move completed
   - Optional: subtle "whoosh" sound cue (optional, respects accessibility)
   - Solves: Instant feedback for ADHD brain + confirmation

4. **Beat-to-Chapter Optional Grouping**
   - "Mark as Chapter X" button on each beat (not required upfront)
   - Visual divider when consecutive beats share the same chapter tag
   - Purely optional—structure can stay flat indefinitely
   - Allows later export to standard chapter/act format if needed
   - Solves: Future-proofing without forcing hierarchy now

5. **Filter & Search Bar**
   - Real-time search for `@character`, `>>research`, `$$synopsis`, `//comments`
   - Toggle to show only matching beats
   - Helps locate related beats without relying on hierarchy
   - Solves: Metadata helps discovery, not organization

6. **Quick-Move Modal (Optional Advanced Feature)**
   - When reorganizing large lists (20+ beats), offer modal with searchable list of target positions
   - Insert selected beat after target position
   - Same visual feedback as drag-drop
   - Solves: Power users can move without scrolling

7. **Persistent Document View**
   - Everything in localStorage initially (no cloud sync in MVP)
   - Auto-save on every change (debounced to prevent lag)
   - Full undo/redo stack
   - Solves: No risk of losing work, ADHD-friendly auto-save

### Top Concepts

**MVP Prototype to Test:**

1. **Flat-list beat editor** with drag-and-drop + up/down arrows + split/merge (highest priority)
2. **Instant visual feedback** on reorganization (snap animation + flash)
3. **Filter bar** for searching metadata tags AND timeline periods
4. **Timeline markers** for non-linear narrative tracking
5. **Status badges** (outline/draft/editing/done) for workflow progression
6. **Word count tracking** for progress monitoring

---

## 🎯 Beat Data Model & Architecture

**MVP Beat Schema:**

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

**Key Design Decisions:**

1. **Flat list, not nested** – Beats stay in a single continuous list (narrative order). Optional hierarchy (parentId) stored but hidden in MVP UI.
2. **Status field** – Tracks beat evolution from outline → draft → editing → done. UI shows badge, controls available based on status.
3. **Timeline markers** – Each beat can reference a timeline period (e.g., "1900-1910"). Optional "Timeline View" sorts by period separate from narrative order.
4. **Split/Merge actions** – Single-click operations to divide a beat at cursor or combine adjacent beats. Updates metadata and word count automatically.
5. **Metadata as array** – Tags parsed from content into a searchable array. Raw text remains editable.
6. **Future-proof versioning** – `lastEdited` timestamp in MVP, can expand to full `revisionHistory` array later.

**Timeline View:**

- Primary view: Flat beat list in narrative order (for writing)
- Secondary view: Toggle to "Timeline/Chronology" → sorts beats by timelineId period
- Both views support drag-and-drop reorganization
- Filter bar supports `#period-name` queries to show beats from specific timeline periods

---

## 📊 Multi-Stage Workflow Support

This beat model supports the eventual full suite:

| Stage | Beat Role | Key Features |
|-------|-----------|--------------|
| **Brainstorming** | Placeholder beats with minimal content | Tags, timeline period (for discovery) |
| **Planning/Outline** | Structured beats with notes, sparse content | Status=outline, timeline markers, metadata |
| **Drafting** | Beats grow into prose | Content fills, word count tracking, split/merge available |
| **Editing** | Beats refined, possibly split/merged | Status=editing, heavy filtering by tags, timeline review |
| **Export** | Beats compiled, metadata stripped | Convert to .docx/.pdf/.epub with period markers optionally included |

---

## 🔄 Export Strategy

**Phase 1 (MVP):** Serialize beats to JSON, strip inline metadata, generate simple .docx proof-of-concept.

**Phase 2+ (Full Suite):**
- Export to .docx, .pdf, .epub with style preservation
- Optional chronology appendix (beats sorted by period)
- Hidden metadata markers in export for downstream tools
- Support for custom formatting templates

---

## 🛠️ PROTOTYPE: Make Ideas Tangible

### Prototype Approach

**Two-Track Prototyping Strategy:**

1. **Paper Prototype (Low-Fi, 30 minutes)**
   - Sketch sticky notes representing beats on a large board
   - Let Savannah physically rearrange them
   - Observe: Does she naturally group them, or prefer a flat line?
   - Outcome: Validates flat-list assumption vs. discovering hidden hierarchy needs

2. **Interactive Prototype (Medium-Fi, 1-2 days)**
   - Build in Figma (no-code) or simple React sandbox
   - Focus: Drag-and-drop + up/down arrows + visual feedback
   - Test with realistic content (20-30 beats from Savannah's actual writing)
   - Interactive, but no backend—localStorage only

### Prototype Description

**Low-Fi: Paper Beat Board**
- Large surface with 15-20 sticky notes (each represents a beat)
- Different colors for "early beats," "middle beats," "late beats" (to surface timeline complexity)
- Savannah rearranges freely while narrating her thinking

**Medium-Fi: Figma/HTML Interactive Prototype**
- Vertical scrollable list of 25 beat blocks
- Each block shows:
  - Beat title/summary
  - Content preview (first 50 chars)
  - Metadata tags displayed as chips (@character, >>research, etc.)
  - Drag handle (visual indicator it's draggable)
  - Up/down arrow buttons for micro-moves
- Interactions:
  - Drag-to-reorder (smooth feedback)
  - Click up/down arrow for 1-click swaps
  - Snap animation + flash on drop
  - Optional: keyboard shortcuts (Ctrl+↑/↓) with tooltip
- Filter bar at top:
  - Type to search metadata
  - Toggle to show only matches

### Key Features to Test

| Feature | What we're testing | Success criterion |
|---------|-------------------|-------------------|
| **Flat-list layout** | Does continuous document feel right? Can she find beats? | Locates any beat < 2 min by scrolling |
| **Drag-and-drop** | Is reorganization intuitive? How many mental steps? | ≤ 3 mental steps; ≤ 5 seconds per move |
| **Up/Down arrows** | Do 1-click micro-moves feel natural? | Prefers arrows for adjacent moves |
| **Split/Merge** | Are single-click split/merge operations discoverable? | Completes operation ≤ 3 clicks; ≤ 10 sec |
| **Status badge** | Does status field help track beat progression? | Understands outline/draft/editing/done distinction |
| **Timeline period** | Is timeline marker useful for non-linear writing? | Can assign period to beat ≤ 3 sec |
| **Timeline view toggle** | Does chronological sort help review story flow? | Finds it useful for editing; ≥ 3/5 |
| **Filter bar** | Does metadata + period filtering help beat discovery? | Uses filters; rates usefulness ≥ 4/5 |
| **Visual feedback** | Does snap animation + flash feel immediate? | Rates animation immediacy ≥ 4/5 |
| **Word count** | Does progress tracking motivate writing? | Uses word count; finds it useful |
| **Overall experience** | Does this feel like "Scrivener + Docs + Timeline"? | Rates overall satisfaction ≥ 4/5 |

### Testing Tasks

**Task 1 – Micro-reorganization (Up/Down arrows)**
- Instructions: "Swap these two adjacent beats using the arrow buttons"
- Success: Completes in ≤ 5 seconds, ≤ 2 mental steps

**Task 2 – Macro-reorganization (Drag-and-drop)**
- Instructions: "Move this beat from the top to somewhere in the middle of the list"
- Success: Completes in ≤ 5 seconds, finds drag intuitive

**Task 3 – Beat splitting**
- Instructions: "This beat is too long. Split it at this point [marker]"
- Success: Finds split button ≤ 10 seconds, operation feels natural

**Task 4 – Timeline assignment**
- Instructions: "Assign this beat to Period 1 (year 1900)"
- Success: Finds period dropdown ≤ 3 seconds, period badge updates

**Task 5 – Timeline view toggle**
- Instructions: "Switch to Timeline view. Can you see how beats are ordered chronologically?"
- Success: Understands the view, finds it useful; ≥ 3/5 rating

**Task 6 – Filtering by period**
- Instructions: "Show me only beats from Period 2 using the filter bar"
- Success: Finds filter feature, types `#Period 2`, results are correct

**Task 7 – Overall experience**
- Freeform: "Now write a beat, assign it a period, reorganize it. How does this feel?"
- Success: Rates intuitive-ness ≥ 4/5; prefers vs. Docs and matches Scrivener

---

## ✅ TEST: Validate with Users

### Testing Plan

**Test Script (Savannah + observational approach)**

**Session 1: Paper Prototype Walkthrough (30 min)**
- Present 15-20 sticky notes on a board
- Say: "These represent beats from your story. Can you arrange them the way they should flow?"
- Observe: grouping behavior, hesitations, narration
- Questions:
  - "Do you naturally group beats into chapters?"
  - "How do you know when to move a beat?"
  - "What visual cues would help you find a specific beat?"

**Session 2: Interactive Prototype Testing (15 min)**

**Task A – Micro-move (Up/down arrows):**
- "Can you swap these two adjacent beats using the arrow buttons?"
- Measure: Time to complete, mental steps, satisfaction

**Task B – Macro-move (Drag-and-drop):**
- "Move this beat (somewhere in the list) to a different position"
- Measure: Drag intuition, visual feedback clarity, time

**Task C – Filter & locate:**
- "Find all beats tagged with @villain using the filter bar"
- Measure: Filter usefulness, discovery effectiveness

**Post-task interview (5 min):**
- "How many steps did you think about for each move?"
- "Did the visual feedback (animation + flash) feel immediate?"
- "How does this compare to Scrivener vs. Google Docs?"
- "On a scale 1-5, how intuitive was reorganization?"
- "What would make it even better?"

### User Feedback

_To be captured during testing sessions_

**Expected feedback themes:**
- Drag-and-drop intuitiveness
- Visual feedback clarity
- Filter bar utility
- Overall cognitive load

### Key Learnings

_To be synthesized after testing_

**We're validating:**
1. ✅ Flat-list architecture matches her writing process
2. ✅ Drag-and-drop feels intuitive for reorganization
3. ✅ Up/down arrows satisfy "1-2 click" requirement
4. ✅ Visual feedback (animation + flash) feels immediate
5. ✅ Filter bar helps with beat discovery
6. ✅ Overall experience is better than Docs/Scrivener

**Potential surprises to watch for:**
- Does she actually want a hierarchy earlier than expected?
- Are there reorganization patterns we haven't anticipated?
- Is the beat granularity right, or should it be smaller/larger?
- Do keyboard shortcuts matter, or is mouse-only enough?

---

## 🚀 Next Steps

### Refinements Needed

Based on your writing process insights, the original MVP vision has been **reframed**:

**What Changed:**
- ❌ Removed: Pre-defined Acts > Chapters > Scenes hierarchy
- ✅ Added: Flat-list beats with optional emergent grouping
- ✅ Added: Multiple reorganization modes (drag + arrows + keyboard)
- ✅ Emphasized: Instant visual feedback for ADHD cognitive needs
- ✅ Reframed: Metadata as discovery tool, not organizational tool

**What Stays the Same:**
- ✅ Continuous document view (all beats visible)
- ✅ Positive pet gamification
- ✅ Inline metadata annotations
- ✅ localStorage persistence

### Action Items

**Immediate (Before Building – CRITICAL DECISIONS NEEDED):**

1. ✅ **Confirm beat granularity** – "Beat" is perfect (outliner + placeholder → content)
2. ✅ **Confirm timeline markers** – Timeline view needed for non-linear narrative
3. ✅ **Confirm export needs** – Will export to .docx/.pdf/.epub later with metadata stripped
4. ✅ **Timeline use confirmed** – Timeline markers are for planning/editing only. No chronological navigation in exports. Exports will be narrative-order with metadata stripped.

---

**Sprint 1: Core Interactive Prototype (1-2 days)**

Core features to build and test:

1. ☐ **Beat data model** – Define schema with id, title, content, tags, status, timelineId, wordCount
2. ☐ **Flat-list editor** – Vertical scrollable list of beats (20-30 sample beats from your writing)
3. ☐ **Drag-and-drop reordering** – SortableJS or Figma interactive prototype
4. ☐ **Up/down arrow buttons** – 1-click micro-moves between adjacent beats
5. ☐ **Split/Merge icons** – Single-click operations to divide or combine beats
6. ☐ **Status badge** – Visual indicator (outline/draft/editing/done) on each beat
7. ☐ **Timeline period dropdown** – Assign beat to a timeline period (e.g., "Period 1 – 1900-1910")
8. ☐ **Visual feedback** – Snap animation (< 0.5s) + background flash on reorganization
9. ☐ **Filter bar** – Search for `@tags` and `#period-name`
10. ☐ **localStorage persistence** – Save beat structure across sessions
11. ☐ **Word count tracking** – Display on each beat, aggregate total
12. ☐ **Timeline View toggle** – Secondary view that sorts beats by period instead of narrative order

---

**Sprint 2: Discoverability & Polish (If time allows)**

1. ☐ Keyboard shortcuts (Ctrl+↑/↓)
2. ☐ Pet component with writing session feedback
3. ☐ Session tracking (words written, session completion)
4. ☐ Optional chapter grouping button
5. ☐ Export stub (serialize beats to JSON, strip metadata, generate .docx proof-of-concept)

---

**Testing & Iteration (After Prototype Complete):**

1. ☐ Run 7 testing tasks (see Key Features section above)
2. ☐ Measure: Time to task, mental steps, satisfaction ratings
3. ☐ Gather qualitative feedback on intuitive-ness, visual feedback, mental load
4. ☐ Test with your actual writing (real beats from your manuscript)
5. ☐ Iterate based on learnings
6. ☐ Document success metrics achieved

### Success Metrics

**Assumption: "Block-structured editor feels intuitive for reorganization"**

| Metric | Target | How to measure |
|--------|--------|-----------------|
| **Time to reorganize** | ≤ 5 seconds per move | Stopwatch during testing |
| **Mental steps** | ≤ 2 steps | Ask: "How many steps did you think about?" |
| **Satisfaction** | ≥ 4/5 | Post-move rating scale |
| **Visual feedback clarity** | ≥ 4/5 | "Did animation feel immediate?" |
| **Overall intuitive-ness** | ≥ 4/5 | "On a scale 1-5, how intuitive?" |
| **Preference vs. Docs** | Strongly prefer | "Compare to Google Docs experience" |
| **Preference vs. Scrivener** | Equally good + better visibility | "Compare to Scrivener experience" |

**Phase Gate:**
- If metrics ≥ thresholds → Proceed to full build
- If metrics < thresholds → Debug (Is it drag-drop? Animation speed? Filter placement?) and iterate

### Key Open Questions for You

Before we move to the PROTOTYPE phase, I need your input on:

1. **Beat Granularity:** Is the "beat" (smallest unit) the right size, or should the MVP work with "scenes" instead? How fine-grained should reorganization be?

2. **Chapter Grouping:** Do you anticipate needing to export to a hierarchical manuscript format (chapters, acts)? If so, should optional grouping be in the MVP or deferred?

3. **Timeline Management:** Your writing hops around the timeline. Should beats have timestamps or timeline markers, or is the linear order in the editor sufficient?

4. **Metadata Priority:** In your workflow, how often do you search for beats by tag (e.g., "@villain")? Is this critical, or secondary to reorganization?

5. **Paper Prototype:** Ready to do the physical beat arrangement test, or shall we jump straight to the interactive prototype?

---

## 📋 Session Summary & Key Decisions

### Design Thinking Outcomes

This design thinking session transformed the Writers Suite MVP from a **pre-planned hierarchical editor** into a **beat-driven emergent outliner** that matches Savannah's actual non-linear, discovery-based writing process.

### Critical Insights Discovered

1. **Writing is emergent, not predetermined** – Savannah doesn't write Acts > Chapters > Scenes in order. She writes beats that organically grow into scenes, discovers chapters, and later places acts. Structure emerges from writing itself.

2. **Continuous visibility is accessibility** – For ADHD, "out of sight, out of mind" is cognitive load. The editor must show the entire document continuously (Google Docs strength) while supporting Scrivener's fast reorganization (Scrivener strength).

3. **Interaction speed matters more than features** – 1-2 clicks with instant visual feedback (< 0.5s) is non-negotiable. The tool must feel as fast as thinking.

4. **Timeline is for planning, not readers** – Non-linear writing requires temporal markers for the author's reference (editing, reviewing narrative flow), but these are internal tools. Exports will be narrative-order with metadata stripped.

5. **A single data model scales from outline to export** – The beat schema supports the full suite (brainstorm → outline → draft → edit → export) without major rework.

### Reframed MVP Architecture

**From:** Acts > Chapters > Scenes hierarchy (pre-planned structure)
**To:** Flat list of beats with optional emergent grouping (structure discovered during writing)

**Core Design:**
- **Beats:** Smallest unit, serves as placeholder during outlining, grows into full content during drafting
- **Continuous flat list:** Entire document visible, no nested files (solves "out of sight" problem)
- **Multiple reorganization modes:** Drag-and-drop + up/down arrows + split/merge (1-2 clicks)
- **Timeline markers:** Each beat references a period for non-linear editing (planning/editing only, not exported)
- **Status tracking:** Outline → Draft → Editing → Done (shows beat progression)
- **Instant feedback:** Snap animation (< 0.5s) + visual flash on every reorganization action
- **Metadata as discovery:** Tags and period-based filtering help locate beats, not organize them
- **Future-proof hierarchy:** Optional chapter/act grouping can be added later without data migration

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

**Future extensions (no breaking changes):**
- `parentId` for optional hierarchy
- `revisionHistory` for version tracking
- `children` array for nested beats (if needed)

### Timeline Markers Strategy

**Two-view system:**
1. **Narrative View (Primary):** Beats in story order (how Savannah writes)
2. **Timeline View (Secondary):** Beats sorted by period (for editing/review of chronological flow)

**Use cases:**
- **Planning:** Assign beats to story periods (Period 1: 1900-1910, Period 2: 1912-1918, etc.)
- **Editing:** Switch to Timeline View to review if events make chronological sense
- **Filtering:** Use `#period-name` in filter bar to isolate beats from specific time period
- **Export:** Timeline markers are internal only; exports are narrative-order with metadata stripped

### Multi-Workspace Vision (Complete Suite)

The beat model and timeline support the full Writers Suite:

| Workspace | Purpose | Beat Role |
|-----------|---------|-----------|
| **Brainstorming** | Generate ideas, capture concepts | Beat = idea placeholder with minimal content |
| **Research & Planning** | Gather research, outline structure | Beat = outline block with notes, tags for discovery |
| **Outlining** | Organize beats into story flow | Beat = structural node, timeline period assigned |
| **Drafting** | Write prose, develop content | Beat = growing content block, split/merge as needed |
| **Editing** | Refine, revise, reorganize | Beat = focus unit, filter by tags/period, final polish |
| **Export & Publishing** | Prepare final manuscript | Beat = stripped of metadata, compiled to .docx/.pdf/.epub |

### Next Steps (When Ready to Prototype)

1. **Build interactive prototype** – Flat-list beat editor with core features (drag, arrows, split/merge, timeline, filter)
2. **Test with 7 tasks** – Validate intuitive-ness of reorganization, timeline assignment, filtering
3. **Iterate based on feedback** – Adjust interaction timing, visual feedback, feature prominence
4. **Build pet component** – Add positive feedback mechanism for writing sessions
5. **Test with real writing** – Use tool on actual manuscript during drafting/editing
6. **Refine based on workflow** – Document pain points, missing features, iteration priorities

### Design Thinking Artifacts Generated

- ✅ Comprehensive beat data model
- ✅ Timeline marker strategy
- ✅ Multi-view interaction design (Narrative + Timeline)
- ✅ 7-task test script for prototype validation
- ✅ Success metrics for intuitive-ness evaluation
- ✅ Roadmap for full Writers Suite
- ✅ Export strategy (phases 1-3)

### Key Validated Assumptions

✅ **"Beat" is the right granularity** – Serves outlining, drafting, and editing seamlessly
✅ **Flat-list is the right structure** – Matches emergent writing process, enables continuous visibility
✅ **Timeline is for internal workflow only** – Simplifies data model, clarifies export strategy
✅ **Status field enables workflow progression** – Outline → Draft → Editing → Done is natural
✅ **Metadata as discovery (not organization)** – Tags and periods help find beats, not structure them

### Questions Answered

| Question | Answer |
|----------|--------|
| Should MVP have Acts > Chapters > Scenes hierarchy? | No. Start flat. Optional grouping later. |
| What's the core assumption to test? | Drag-and-drop + up/down arrows feel intuitive for reorganization. |
| Should timeline markers be in exports? | No. Timeline is internal planning/editing tool only. |
| Should beats have versions/revision history? | No in MVP. Can add later via `revisionHistory` array. |
| Can beats be split or merged? | Yes. Single-click operations on each beat. |
| How does metadata help in editing? | Filter bar searches `@tags` and `#period-name` for discovery. |
| What happens to metadata in export? | Stripped completely. Export is clean narrative prose. |

---

_Session completed: 2026-02-11_
_Facilitator: Claude Code using PAL collaborative thinking_
_Generated using BMAD Creative Intelligence Suite - Design Thinking Workflow_
