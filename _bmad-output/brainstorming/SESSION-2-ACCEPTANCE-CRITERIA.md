# Session 2: ADHD Mechanics & Failure Mode Brainstorming
## Acceptance Criteria

**Issue:** `pet-projects-wkd`
**Session Goal:** Deep dive into ADHD-specific workflows; ground pet mechanics and flow mode in neuroscience-backed principles
**Duration:** 90-120 minutes
**Date Created:** 2026-02-13
**Analyst:** Mary (Business Analyst Agent)

---

## 🎯 Session Completion Criteria

### Pre-Session Requirements
**Status: MUST BE MET BEFORE SESSION START**

- [ ] **AC-PS1:** Session scheduled with 90-120 minute block (NO interruptions)
- [ ] **AC-PS2:** Facilitator has read full beads issue (`bd show pet-projects-wkd`)
- [ ] **AC-PS3:** "Already Decided" section reviewed - team acknowledges no re-hashing of:
  - Pet-style gamification (virtual companion)
  - Flat-list architecture
  - Timeline markers (internal only)
  - localStorage Phase 1A scope
- [ ] **AC-PS4:** Shared collaboration space prepared (Miro/FigJam/physical whiteboard)
- [ ] **AC-PS5:** Reference materials gathered:
  - ADHD research papers on dopamine reward pathways
  - Competitor ADHD tools (Bear, Notion templates, distraction blockers)
  - Existing design thinking doc (2026-02-11) loaded
- [ ] **AC-PS6:** Participants confirmed (min 2: product lead + UX; optional: ADHD-experience consultant)

---

## 📋 During-Session Process Criteria

### Warm-up Phase (10 minutes)
**Status: MUST BE COMPLETED BEFORE CORE EXPLORATION**

- [ ] **AC-W1:** All 3 warm-up questions asked and discussed
- [ ] **AC-W2:** Each participant shares personal ADHD/focus experience (psychological safety established)
- [ ] **AC-W3:** Key terms defined and shared (hyperfocus, context-switch, decision paralysis, momentum loss)

### Core Exploration Phase (60-90 minutes)
**Status: MUST ADDRESS ALL 15 CORE QUESTIONS**

#### Hyperfocus & Pet Mechanics
- [ ] **AC-CE1:** Question 1 explored - Hyperfocus detection mechanism proposed (typing speed, idle-time, focus-meter UI options documented)
- [ ] **AC-CE2:** Question 2 explored - Pet body-doubling actions defined (≥3 specific actions: prompts, nudges, progress bar, voice encouragement)
- [ ] **AC-CE3:** Question 3 explored - Context-switch triggers identified (browser visibility, OS notification, manual pause documented)
- [ ] **AC-CE4:** Question 4 explored - Recovery mechanisms specified with time constraints (resume banner, animated scroll, beat recap with < 5s target)

#### Decision Paralysis
- [ ] **AC-CE5:** Question 5 explored - Beat organization freeze causes identified (too many beats, unclear hierarchy, ambiguous drag target)
- [ ] **AC-CE6:** Question 6 explored - Annotation typing friction points mapped (keyboard focus loss, modal overlay, missing quick-add shortcut)

#### Momentum & Recovery
- [ ] **AC-CE7:** Question 7 explored - Micro-rewards for 5s momentum recovery defined (flash animation, sound cue, next-word preview)
- [ ] **AC-CE8:** Question 8 explored - External distraction stimuli catalogued (notifications, email, phone, social media)
- [ ] **AC-CE9:** Question 9 explored - Flow-mode auto-pause behavior decided (auto-pause + resume vs soft-pause)

#### Neuroscience & Dopamine
- [ ] **AC-CE10:** Question 10 explored - Dopamine reward signals aligned with ADHD research (variable reward, streaks, surprise animation referenced to peer-reviewed studies)

#### Edge Cases & Failure Modes
- [ ] **AC-CE11:** Question 11 explored - Lost annotation recovery specified (inline 'saving…' indicator, auto-retry, local draft fallback)
- [ ] **AC-CE12:** Question 12 explored - Rapid beat deletion prevention designed (undo toast, confirm delete after 2s inactivity)
- [ ] **AC-CE13:** Question 13 explored - Emotional friction 'stuck' UI affordance defined ('Stuck? Try prompt' button, AI-suggested ideas)

#### Progress & Visualization
- [ ] **AC-CE14:** Question 14 explored - Progress visualization mechanism designed (filling bubbles per word, disappear timing)
- [ ] **AC-CE15:** Question 15 explored - Hyperfocus crash recovery flow documented ('You were in flow-mode, X words in – resume?' prompt)

### Synthesis Phase (10-20 minutes)
**Status: MUST PRODUCE ACTIONABLE NEXT STEPS**

- [ ] **AC-S1:** Synthesis Question 1 answered - Top 3 mechanisms prioritized for prototyping (pet-doubling, dopamine reward, auto-pause ranked)
- [ ] **AC-S2:** Synthesis Question 2 answered - Non-negotiable MVP failure-mode mitigations identified (minimum 3 high-priority items)
- [ ] **AC-S3:** Synthesis Question 3 answered - Momentum-preservation KPIs defined with measurable thresholds (time-to-resume < Xs, interruptions tolerated > Y)
- [ ] **AC-S4:** All ideas documented on shared board with owner assignments
- [ ] **AC-S5:** Top ideas voted on and ranked (min 5, max 10 ideas for prototyping)

---

## 📊 Output Deliverables Criteria

### 1. Failure-Mode Matrix (REQUIRED)
**Status: MUST BE DELIVERED WITHIN 48 HOURS POST-SESSION**

- [ ] **AC-O1:** Matrix includes minimum 10 ADHD-specific failure scenarios
- [ ] **AC-O2:** Each scenario has:
  - [ ] Trigger description (what causes failure)
  - [ ] User impact assessment (severity: critical/high/medium/low)
  - [ ] Mitigation strategy (specific UX/technical solution)
  - [ ] Owner assigned (who implements)
  - [ ] Phase assignment (1A, 1B, 1C, 2+)
- [ ] **AC-O3:** High-severity scenarios (critical/high) have concrete mitigation plans (not "TBD")
- [ ] **AC-O4:** Matrix cross-references design constraints:
  - All visual feedback < 0.5s
  - No modal overlays during flow-mode
  - Micro-interactions reinforce momentum
- [ ] **AC-O5:** Matrix exported as structured doc (Markdown table or spreadsheet)

**Example Failure-Mode Entries:**
| Scenario | Trigger | Impact | Mitigation | Owner | Phase |
|----------|---------|--------|------------|-------|-------|
| Lost annotation mid-typing | Browser crash, network loss | High - User loses work, trust broken | Inline 'saving…' indicator + auto-retry + localStorage draft fallback | UX Lead | 1A |
| Context-switch during hyperfocus | OS notification, browser tab switch | Medium - Momentum broken, 30s+ to recover | Auto-pause flow-mode + 'Resume where left off' banner with one-click restore | Product Lead | 1B |

### 2. ADHD-Mechanics Prototype List (REQUIRED)
**Status: MUST BE DELIVERED WITHIN 48 HOURS POST-SESSION**

- [ ] **AC-O6:** Minimum 2 mechanisms specified and ready for Phase 1B testing
- [ ] **AC-O7:** Each mechanism includes:
  - [ ] Name & description (clear, concise)
  - [ ] User trigger (when mechanism activates)
  - [ ] Visual/auditory/haptic feedback spec
  - [ ] Success metric (how measure effectiveness)
  - [ ] Neuroscience rationale (ADHD dopamine alignment referenced)
  - [ ] Implementation complexity estimate (low/medium/high)
  - [ ] Phase assignment (1B, 1C, 2+)
- [ ] **AC-O8:** At least 1 mechanism targets hyperfocus support
- [ ] **AC-O9:** At least 1 mechanism targets momentum recovery (< 5s post-interruption)
- [ ] **AC-O10:** All mechanisms comply with:
  - No modal overlays during flow-mode
  - Visual feedback < 0.5s
  - Minimal decision friction

**Example Prototype Entry:**
```
MECHANISM: Pet Body-Doubling Progress Nudge
- Trigger: User completes 30 min uninterrupted typing (500+ words)
- Feedback: Pet animates with 'Great session!' + subtle sound cue + 'Session Complete' badge (auto-dismiss 3s)
- Success Metric: Users who see badge write 20%+ longer in next session (A/B test)
- Neuroscience: Variable reward timing aligns with ADHD dopamine pathways (reference: Volkow et al., 2009)
- Complexity: Medium (animation + badge system)
- Phase: 1B
```

### 3. Momentum-Preservation KPI Definition (REQUIRED)
**Status: MUST BE DELIVERED WITHIN 48 HOURS POST-SESSION**

- [ ] **AC-O11:** KPIs defined with specific numerical thresholds:
  - [ ] Time-to-resume (target: < Xs after interruption)
  - [ ] Interruptions tolerated per session (target: > Y without session abandonment)
  - [ ] Hyperfocus session length (target: avg Zm minutes sustained typing)
  - [ ] Context-switch recovery rate (% users who resume vs abandon)
- [ ] **AC-O12:** Baseline measurement plan specified:
  - [ ] Data collection method (analytics events, user survey, session replay)
  - [ ] Sample size (minimum N users)
  - [ ] Timeframe (X days/weeks of beta testing)
- [ ] **AC-O13:** KPIs aligned with ADHD-specific success criteria:
  - 30-day retention ≥ 45% (from Session 3 context)
  - ADHD-user % ≥ 30% (market fit validation)

**Example KPI Specification:**
```
TIME-TO-RESUME KPI:
- Definition: Seconds elapsed from context-switch trigger to user resuming typing
- Target: < 10s (95th percentile)
- Baseline: Measure in Phase 1A beta (100 sessions, 20 users)
- Data Collection: Analytics event 'context_switch_detected' → 'typing_resumed'
- Success Threshold: 70%+ of interruptions recover within 10s
```

---

## ✅ Session Success Validation

### Mandatory Success Criteria (ALL MUST BE MET)

- [ ] **AC-SV1:** All 15 core exploration questions answered with documented ideas
- [ ] **AC-SV2:** Failure-mode matrix delivered with ≥10 scenarios (≥3 high-severity with concrete mitigation)
- [ ] **AC-SV3:** ≥2 ADHD-mechanics mechanisms ready for Phase 1B testing with full specs
- [ ] **AC-SV4:** Momentum-preservation KPIs defined with numerical thresholds + baseline plan
- [ ] **AC-SV5:** All outputs cross-reference design constraints (0.5s feedback, no modals, momentum-first)
- [ ] **AC-SV6:** Every output artifact has assigned owner + phase assignment (1A/1B/1C/2+)
- [ ] **AC-SV7:** Beads issue `pet-projects-wkd` updated with session results within 48 hours
- [ ] **AC-SV8:** Next steps identified (specific actions, owners, deadlines)

### Quality Thresholds

- [ ] **AC-QT1:** Psychological safety maintained - all participants contributed ideas (no single-voice domination)
- [ ] **AC-QT2:** Ideas grounded in evidence - neuroscience references cited for dopamine/reward claims
- [ ] **AC-QT3:** No re-hashing - session stayed focused on gaps (didn't redesign flat-list, localStorage scope, pet gamification philosophy)
- [ ] **AC-QT4:** Divergent thinking preserved - ideas captured before judging (no premature "that won't work" dismissals)
- [ ] **AC-QT5:** Convergent prioritization clear - voting/ranking used to identify top mechanisms

---

## 🚫 Session Failure Conditions

**Session FAILS if any of these occur:**

- [ ] **FC1:** Session runs < 60 minutes (insufficient time for 15 core questions)
- [ ] **FC2:** < 10 core exploration questions addressed (incomplete exploration)
- [ ] **FC3:** Failure-mode matrix has < 3 high-severity scenarios with mitigation
- [ ] **FC4:** < 2 ADHD-mechanics mechanisms ready for prototyping
- [ ] **FC5:** Momentum KPIs lack numerical thresholds (vague "improve retention" instead of "< 10s time-to-resume")
- [ ] **FC6:** Team re-hashes already-decided architecture (wastes time on flat-list debate, localStorage scope)
- [ ] **FC7:** Outputs not documented within 48 hours (knowledge loss, participant memory fades)
- [ ] **FC8:** No owner assigned to outputs (ideas die in limbo)

---

## 📐 Design Constraints Validation Checklist

**Every output MUST comply with these constraints:**

### Non-Negotiable Constraints (CRITICAL)
- [ ] **DC1:** All visual feedback mechanisms < 0.5s latency
- [ ] **DC2:** No modal overlays during flow-mode (non-blocking UI only)
- [ ] **DC3:** Micro-interactions reinforce momentum (not interrupt)
- [ ] **DC4:** ADHD reward mechanics aligned with dopamine pathways (research-backed)

### Phase 1A Scope Constraints
- [ ] **DC5:** localStorage persistence only (no backend/cloud)
- [ ] **DC6:** Flat-list architecture preserved (no hidden panels, nested folders)
- [ ] **DC7:** Single-user, self-directed scope (no collaboration features)

### UX Constraints
- [ ] **DC8:** 1-2 clicks maximum for core actions (beat creation, editing, annotation)
- [ ] **DC9:** Continuous flat-list document view (ADHD accessibility)
- [ ] **DC10:** Instant status feedback for beat progression (Outline → Draft → Editing → Done)

---

## 🔄 Post-Session Follow-Up Criteria

### Within 24 Hours
- [ ] **AC-PF1:** Session notes transcribed and uploaded to shared board
- [ ] **AC-PF2:** Photos/recordings archived (if applicable)
- [ ] **AC-PF3:** Participants thanked (email/Slack message)

### Within 48 Hours
- [ ] **AC-PF4:** All 3 output deliverables finalized and shared:
  - Failure-mode matrix
  - ADHD-mechanics prototype list
  - Momentum-preservation KPI definition
- [ ] **AC-PF5:** Beads issue `pet-projects-wkd` updated with:
  - Session date completed
  - Output deliverables linked
  - Next steps added to notes
  - Status updated to `in_progress` or `completed`

### Within 1 Week
- [ ] **AC-PF6:** Cross-session synthesis begun (Session 1 + Session 2 findings merged)
- [ ] **AC-PF7:** MVP spec updated with ADHD-mechanics insights
- [ ] **AC-PF8:** Implementation roadmap adjusted based on failure-mode priorities
- [ ] **AC-PF9:** Session 3 (Competitive Positioning) scheduled with Session 2 insights as input

---

## 📚 Reference Materials Checklist

**Facilitator should have these materials ready:**

### ADHD Research
- [ ] Peer-reviewed papers on ADHD dopamine reward pathways
- [ ] Hyperfocus triggers and detection studies
- [ ] Context-switching cognitive load research

### Competitor Analysis
- [ ] Bear app - distraction-free writing features
- [ ] Notion - ADHD templates and workflow examples
- [ ] Scrivener - focus mode analysis
- [ ] Cold Turkey/Freedom - distraction blocker patterns
- [ ] Flowtime/Forest - gamified focus apps

### Internal Docs
- [ ] Design thinking doc (2026-02-11) - emergent structure philosophy
- [ ] Session 1 outputs (if completed) - UX flow findings
- [ ] Existing wireframes/prototypes (if any)

---

## ✨ Success Indicators (Beyond Minimum Criteria)

**Session EXCEEDS expectations if:**

- [ ] **SI1:** ≥3 mechanisms ready for Phase 1B testing (exceeds minimum 2)
- [ ] **SI2:** Failure-mode matrix includes ≥5 high-severity scenarios with mitigation
- [ ] **SI3:** Neuroscience references cited for ≥50% of dopamine/reward mechanisms
- [ ] **SI4:** User testing plan drafted for top 3 mechanisms (not just specs)
- [ ] **SI5:** Cross-functional collaboration - UX, product, engineering all contributed ideas
- [ ] **SI6:** ADHD-experience consultant participated and validated approaches
- [ ] **SI7:** Momentum KPIs include both quantitative (time-to-resume) and qualitative (user sentiment) measures

---

## 🎯 Acceptance Criteria Summary

**Session is ACCEPTED when:**

1. ✅ All 15 core exploration questions addressed
2. ✅ Failure-mode matrix delivered (≥10 scenarios, ≥3 high-severity with mitigation)
3. ✅ ≥2 ADHD-mechanics mechanisms ready for Phase 1B testing
4. ✅ Momentum KPIs defined with numerical thresholds + baseline plan
5. ✅ All outputs cross-reference design constraints
6. ✅ Outputs delivered within 48 hours with owners assigned
7. ✅ Beads issue updated
8. ✅ No failure conditions triggered

**Status:** Ready for execution
**Next Step:** Schedule session, confirm participants, prepare materials
**Owner:** Product Lead (session facilitation)
**Analyst:** Mary (Business Analyst Agent)

---

_Generated: 2026-02-13_
_Status: READY FOR SESSION EXECUTION_
_PAL Analysis: Acceptance criteria grounded in ADHD research, design constraints, and failure-mode analysis_
