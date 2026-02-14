# Project Learnings: Writers Suite MVP - ADHD-First Design

**Last Updated:** 2026-02-14
**Focus:** Session 2 ADHD Mechanics & Failure Mode Analysis

---

## ADHD-First Momentum System (Core Innovation)

### Three-Layer Architecture (Synergistic)

The most effective momentum system for ADHD writers combines three interdependent mechanisms:

1. **Passive Hyperfocus Detection** (Layer 1)
   - Detects flow state: typing velocity > 80 WPM sustained 10+ min
   - Non-intrusive (passive monitoring, optional UI for power users)
   - Variable-interval rewards (30-50 min unpredictably) more effective than fixed
   - Neuroscience: Volkow et al. research shows ADHD dopamine responds to variable schedules
   - User preference: Savannah confirmed 80 WPM/10 min thresholds match her writing patterns

2. **Auto-Pause + Rapid Resume** (Layer 2)
   - Context-switch auto-pause (browser blur, notifications, manual pause)
   - Recovery < 5s: Resume banner → animated scroll → 3-line beat recap → micro-reward
   - Preserves cognitive continuity (critical for ADHD context-switch recovery)
   - Reduces cognitive load of "getting back into it" after interruption

3. **Momentum Recovery Micro-Rewards** (Layer 3)
   - Flash animation (100ms) + next-word preview (50ms) = < 0.3s baseline latency
   - Sound cue (200ms) optional, defaults OFF (accessibility: ADHD startle sensitivity)
   - Multi-modal feedback removes friction to resume typing
   - All within < 0.5s design constraint (non-negotiable)

**Why Synergistic:**
- Layer 1 makes users *want* to return tomorrow (dopamine memory)
- Layer 2 *preserves* mental state when interrupted (cognitive continuity)
- Layer 3 *removes friction* to resume immediately (micro-engagement)
- Together = resilient momentum system that prevents session abandonment

---

## Failure-Mode Thinking Applied to ADHD UX

### Critical Pattern: Map Failure Modes Before Building

Don't design features in isolation. Instead:
1. Identify specific ADHD failure modes (where users abandon)
2. Map each to severity (high/medium/low based on user impact)
3. Design concrete mitigations for each
4. Validate mitigations comply with design constraints

### 10 ADHD-Specific Failure Modes Identified

| Severity | Failure Mode | Root Cause | Mitigation |
|----------|--------------|-----------|-----------|
| **HIGH** | Lost annotation mid-typing | Browser crash, network loss | Inline 'saving…' (50ms) + auto-retry + localStorage fallback |
| **HIGH** | Hyperfocus crash recovery | Session interruption without recovery path | Recovery prompt: "You were in flow, 250 words in – resume?" (one-click restore) |
| **MEDIUM** | Context-switch active typing | Interruption with no rapid resume | Auto-pause + resume banner < 5s + beat recap |
| **MEDIUM** | Beat organization paralysis | > 15 visible beats (cognitive overload) | **Limit visible beats (10-15/screen)** – PRIMARY Phase 1A solution |
| **MEDIUM** | Annotation typing paralysis | Modal overlay, slow feedback | Inline editing (no modal) + Ctrl+K quick-add |
| **MEDIUM** | Accidental beat deletion | No confirmation, undo takes effort | Undo toast (3s auto-dismiss) + soft-confirm (2s inactivity) |
| **MEDIUM** | Momentum loss post-interrupt | > 10s recovery time, lost context | Flash + sound + preview < 0.5s total |
| **LOW-MED** | Distraction pull-out | Notifications, email, social media | Optional Do Not Disturb mode + focus-meter UI |
| **LOW** | Beat merge/split confusion | Unclear UI affordance | Contextual menu + keyboard shortcuts (Shift+S/M) + animated feedback |
| **LOW-MED** | Hyperfocus over-fatigue | Extended session > 90 min | Gentle nudge at 60 min (dismissible, no sound default) |

**Key Insight:** Decision paralysis has TWO separate causes (beat org vs annotation typing). Each needs different mitigation. Don't conflate them.

---

## Design Constraints: Non-Negotiable, Always Validate

### Critical Constraints (Must Never Violate)

1. **< 0.5s Latency for All Visual Feedback**
   - Not aspirational, not "try to be fast"
   - Measured at 95th percentile of user's system
   - ADHD users experience > 0.5s as broken/unresponsive
   - Affects: all animations, micro-interactions, UI updates

2. **No Modal Overlays During Flow-Mode**
   - Modals interrupt hyperfocus state catastrophically
   - Use non-blocking banners, toast notifications, inline editing instead
   - Even "small" modals violate ADHD momentum preservation

3. **Flat-List Architecture Mandatory**
   - ADHD "out of sight, out of mind" pattern
   - All beats visible in continuous list (pagination OK, nesting NOT OK)
   - Hidden beats = forgotten beats = lost work anxiety

4. **localStorage Phase 1A Only** (No Backend)
   - Simplifies scope, reduces complexity
   - Auto-save locally, no sync delays
   - Phase 2+ can add cloud, but MVP is single-device

5. **1-2 Clicks Maximum for Core Actions**
   - Beat creation, editing, annotation, reordering
   - Deeper actions OK (find, search), but primary workflows must be minimal
   - ADHD decision fatigue compounds with multiple steps

**Validation Pattern:** Before implementing any feature, check:
- [ ] Will this latency stay < 0.5s on lower-end hardware?
- [ ] Does this require a modal? (If yes, redesign it away)
- [ ] Is this beat hidden from the flat list? (If yes, make it visible)
- [ ] Does this require backend sync? (Phase 1A only = no)
- [ ] How many clicks to complete? (> 2 = redesign)

---

## Decision Paralysis Has Multiple Root Causes

### Critical Realization: Don't Over-Engineer the Solution

We identified decision paralysis in two places:
1. **Beat organization:** Too many visible beats (cognitive overload)
2. **Annotation typing:** Missing quick-add shortcut (friction in workflow)

**Wrong Approach:** Throw all solutions at it (AI suggestions, complex shortcuts, drag-drop)
**Right Approach:** Limit choice set first (pagination), add tools only if needed in Phase 1B

**Why This Matters for ADHD:**
- Cognitive resources are limited
- Adding "helpful" UI tools can paradoxically increase paralysis
- Start with removing/limiting the problem source
- Optimization tools are Phase 1B, not Phase 1A

**Lesson:** Simplicity compounds. Each added feature increases decision surface. For ADHD, reducing choices beats adding features.

---

## Neuroscience-Backed ADHD Design Principles

### Dopamine Pathways (Volkow et al., 2009)

**Key Finding:** ADHD brains have lower baseline dopamine, requiring:
- External reward signals (pet celebration, badges)
- Variable-interval reinforcement (unpredictable timing sustains attention better than fixed)
- Positive feedback only (celebrating wins, not shaming failures)

**Implementation Implications:**
- Fixed rewards (every 30 min) → habituation, loses effect
- Variable rewards (30-50 min unpredictably) → sustained dopamine engagement
- Celebrating hyperfocus (strength) vs penalizing breaks (shame) → engagement differences measurable in A/B tests

**Savannah Confirmed:** Variable rewards preferred over fixed or milestone-based (500 words)

### Context-Switch Cognitive Load

ADHD brains experience higher cognitive load during context-switches:
- Baseline context-switch cost: 10-15 min to fully re-engage
- With recovery mechanics: target < 5s to restore mental state
- This is not optimization, it's accommodation

**Why 5s Target Matters:**
- Below this: cognitive continuity maintained (feels like brief interruption)
- Above 10s: ADHD user forgets where they were (re-engagement effort increases exponentially)
- Sweet spot: 5s keeps user's "mental model" intact

### Startle Sensitivity

ADHD users often have heightened startle response to:
- Loud notification sounds
- Sudden visual changes
- Abrupt visual contrasts

**Implementation:**
- Sound cues: Optional, OFF by default (Savannah's preference)
- Flash animations: Gentle brightness change (10%), not sudden
- Visual feedback: Gradual (fade-in), not instant

---

## Acceptance Criteria as Process Framework

### Lesson: Write ACs BEFORE Brainstorming

We created 75+ acceptance criteria before Session 2 execution. This prevented:
- Session drift (questions stayed focused)
- Unclear success conditions (everyone knew "done")
- Wasted discussion time (framework kept us organized)
- Scope creep (ACs defined what's in scope vs out)

### AC Structure That Works

1. **Pre-Session Requirements** (6 criteria)
   - Preparation, participants, materials
   - If ANY missing, session is invalid

2. **During-Session Process** (15 core questions + synthesis)
   - Specific questions mapped to deliverables
   - Synthesis questions for prioritization

3. **Output Deliverables** (3 major with specific specs)
   - Failure-mode matrix (≥10 scenarios, ≥3 high-severity)
   - ADHD-mechanics prototypes (≥2 mechanisms ready)
   - Momentum-preservation KPIs (numerical targets)

4. **Session Success Validation** (8 mandatory + quality thresholds)
   - If ANY mandatory fails, session fails
   - Quality thresholds show "exceeds expectations"

5. **Design Constraints Validation** (10 critical constraints)
   - Every output must comply
   - No exceptions (these are non-negotiable)

6. **Post-Session Follow-Up** (9 criteria within 24h/48h/1 week)
   - Who does what, by when
   - Prevents "great session" → no follow-up

**Key Insight:** ACs are not bureaucratic overhead. They're a communication tool that prevents misalignment and wasted effort.

---

## User Preferences Drive Design Decisions

### Five Critical Clarification Points (Integrate Early)

Rather than guess, we asked Savannah directly:

| Question | Answer | Design Impact |
|----------|--------|---------------|
| Hyperfocus thresholds (80 WPM, 10 min)? | "This sounds right" | Locked into specifications |
| Context-switch < 5s feasible? | "Sounds good" | Confirmed target, proceed with confidence |
| Reward timing preference? | "Variable" | Use 30-50 min unpredictable, not fixed |
| Decision paralysis solution? | "Limit visible beats" | Pagination (10-15/screen) Phase 1A priority |
| Sound sensitivity? | "Sound defaults to off" | Micro-rewards use flash+preview, sound opt-in |

**Outcome:** Specifications updated to reflect user preferences, not designer guesses.

**Lesson:** One 15-minute clarification call prevents weeks of building wrong features. Ask users directly about thresholds, targets, and preferences. Don't assume.

---

## Phase 1B Implementation Roadmap (4 Sprints)

### Sprint Structure That Works for ADHD Features

**Sprint 1 (W1-2): Foundation**
- Beat pagination (10-15/screen) — PRIMARY Phase 1A achievement unlocked
- Resume banner framework
- Analytics setup
- Goal: Enable rapid iteration without performance overhead

**Sprint 2 (W3-4): Hyperfocus Detection + Rewards**
- Typing velocity monitoring (80+ WPM algorithm)
- Pet animation system
- Variable-interval reward scheduler
- Badge display (3s auto-dismiss)
- Goal: Core mechanism working end-to-end

**Sprint 3 (W5-6): A/B Testing + Iteration**
- Test: auto-pause vs manual pause only
- Test: variable vs fixed reward timing
- Test: micro-reward modalities (flash+preview vs flash+sound)
- Goal: Validate which approach works for real users

**Sprint 4 (W7-8): Measurement**
- Baseline all 5 KPIs (Phase 1A → 1B comparison)
- Collect user feedback (interviews, preferences)
- Prepare Phase 1C roadmap
- Goal: Data-driven decisions for next phase

**Why This Order:**
- S1 unblocks S2 (foundation first)
- S2 delivers core value (hyperfocus celebration)
- S3 validates assumptions (don't blindly ship)
- S4 measures impact (prove it works)

---

## KPI Definition: Momentum Preservation Metrics

### Five KPIs That Matter for ADHD Writers

1. **Time-to-Resume** (Primary Metric)
   - Definition: Seconds from context-switch to typing resumed
   - Target: < 10s (95th percentile)
   - Success: 70%+ of interruptions recover within target
   - Why: Cognitive continuity depends on speed

2. **Interruptions Tolerated Per Session**
   - Definition: Context-switches user tolerates before abandonment
   - Target: > 3 interruptions without session end
   - Success: 80%+ of sessions with 3+ interruptions show continued engagement
   - Why: ADHD users face many interruptions; system must tolerate multiple

3. **Hyperfocus Session Average Duration**
   - Definition: Minutes of uninterrupted typing (zero context-switches)
   - Target: 45+ min median (Savannah's design thinking baseline)
   - Success: Median > 40 min (accounting for variability)
   - Why: Shows momentum system sustains focus longer

4. **Context-Switch Recovery Rate**
   - Definition: % of users who resume vs abandon after context-switch
   - Target: > 70% resume rate
   - Success: 70%+ of context-switches lead to typing resumption
   - Why: If recovery rate drops, system not working

5. **24h Session Continuation Rate**
   - Definition: % users returning within 24h (ADHD habit formation proxy)
   - Target: > 50% daily return rate
   - Success: 50%+ of Phase 1B users return within 24h
   - Why: Dopamine-aligned mechanics should encourage habit formation

### Baseline Measurement (Phase 1A → 1B)

- **Sample:** 20 ADHD-diagnosed users
- **Duration:** 2 weeks Phase 1A (baseline) + 2 weeks Phase 1B (with mechanics)
- **Method:** localStorage event logging (privacy-first, no server)
- **Analysis:** Percentiles, cohort comparison, A/B test results

---

## Windows Learning Hook: Platform Compatibility Matters

### Lesson: Know Your Dependencies Early

**Original Hook:** Python script using `fcntl` (Unix file locking)
**Problem:** fcntl doesn't exist on Windows → hook crashes
**Solution:** Created PowerShell equivalent (533 lines, Windows-native)

**Key Takeaway:** Test on target platform early. Dependencies matter.

**What We Learned:**
- Python cross-platform claims ≠ all libraries are cross-platform
- Windows has native APIs (System.IO.File) that replace Unix patterns
- Retryable locking is better than immediate failure
- Platform-native usually beats "general" cross-platform

---

## Documentation as Design Artifact

### Why We Created Multiple Documents (Not Overkill)

1. **SESSION-2-ACCEPTANCE-CRITERIA.md**
   - Process framework (who does what)
   - Success validation (how to know when done)
   - Failure conditions (explicit "invalid" states)

2. **SESSION-2-PAL-ANALYSIS-FINDINGS.md**
   - Research grounding (why this approach)
   - Detailed specifications (what exactly to build)
   - Neuroscience references (academic backing)

3. **SESSION-2-REFINED-SPECIFICATIONS.md**
   - Final specs + user preferences
   - Implementation roadmap (4 sprints, tasks)
   - A/B test strategy (how to validate)

4. **SESSION-2-READY-TO-EXECUTE.md**
   - Quick reference (one-page summaries)
   - Facilitator checklist (pre/during/post)
   - Success criteria (clear definition)

5. **SESSION-2-INDEX.md**
   - Navigation guide (which doc for which role)
   - Quick reference by topic
   - Role-based reading paths

**Why Multiple Documents:**
- Different audiences (facilitator, engineer, product owner, team member)
- Different use cases (research, implementation, execution, reference)
- Searchability (can find specific info faster)
- Persistent knowledge (shared with team, lasts beyond session)

---

## Session 2 Analysis Summary

### What We Accomplished

✅ Analyzed Unix Python learning hook (problem: fcntl dependency)
✅ Created Windows-native PowerShell equivalent (533 lines)
✅ Designed three-layer momentum system for ADHD writers
✅ Identified 10 ADHD-specific failure modes with mitigations
✅ Defined 5 momentum-preservation KPIs with numerical targets
✅ Created 75+ acceptance criteria for Session 2 execution
✅ Integrated Savannah's 5 clarification preferences into specs
✅ Drafted 4-sprint Phase 1B implementation roadmap
✅ Created A/B test strategy for validating mechanics
✅ Documented everything for team reference

### Key Principles Applied

1. **Failure-mode thinking:** Identify where users abandon, mitigate each
2. **Design constraints first:** Non-negotiable boundaries protect quality
3. **Synergistic systems:** Three mechanisms work together (not alone)
4. **Neuroscience grounding:** Back up claims with research (Volkow, Barkley)
5. **User preferences drive design:** Ask directly, don't assume
6. **Acceptance criteria before execution:** Define success before starting
7. **Multiple documents for different roles:** One doc can't serve everyone
8. **Platform compatibility matters:** Test on target platform early
9. **Simplicity compounds:** Limit choices before adding features
10. **Data-driven validation:** A/B test mechanisms in Phase 1B, don't guess

---

**Next Session:** Execute Session 2 brainstorming with team using acceptance criteria framework. Gather additional failure modes and insights. Validate three mechanisms for Phase 1B prototyping.

**Team Share:** All Session 2 documents shared with Product Lead, UX Lead. Ready for 90-min brainstorming session.

---

*Generated: 2026-02-14*
*Session: 2 - ADHD Mechanics & Failure Mode Analysis*
*Analyst: Mary (Business Analyst Agent) + Savannah (Product Owner)*
*Status: Ready for Session 2 Execution*
