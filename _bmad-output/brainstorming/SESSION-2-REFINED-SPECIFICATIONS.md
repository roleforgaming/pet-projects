# Session 2: ADHD Mechanics & Failure Mode Brainstorming
## Refined Specifications (User Preferences Integrated)

**Status:** ✅ USER PREFERENCES CAPTURED & INTEGRATED
**Date:** 2026-02-13
**User:** Savannah
**Analyst:** Mary (Business Analyst Agent)

---

## 🎯 Three Mechanisms: Final Specifications

### Mechanism 1: Passive Hyperfocus Detection + Pet Body-Doubling
*Status: ✅ CONFIRMED by user preferences*

**User Input:** "This sounds right" (thresholds 80 WPM, 10+ min match your patterns)

**Trigger:** Typing velocity > 80 WPM sustained for ≥ 10 minutes

**Detection Method:**
- PASSIVE (no UI intrusion during writing)
- Optional focus-meter UI for power users (user can enable in settings)
- Runs silently in background, no visual feedback during hyperfocus

**Reward Mechanism:**
- **Timing:** Variable-interval reinforcement (ADHD-aligned)
  - First reward: 30 min of sustained typing
  - Subsequent: randomly between 30-50 min (unpredictable)
  - Rationale: Savannah confirmed variable timing preferred over fixed
- **Feedback Choreography:**
  1. Pet animates (200ms) – stands up, does small dance
  2. Badge appears: "Hyperfocus Complete – 35 min, 1,250 words"
  3. Auto-dismiss after 3s (non-intrusive)
  4. **NO SOUND by default** (user can enable if desired)

**Why This Works for Savannah:**
- Celebrates hyperfocus (ADHD strength) without being intrusive
- Variable timing keeps dopamine engagement high (Volkow-aligned)
- Passive detection avoids interruption during flow
- Optional focus-meter for users who want to see their speed (power user choice)

**Phase Assignment:** 1B (Phase 1A: focus on basic pet feedback)

---

### Mechanism 2: Auto-Pause + Rapid Resume
*Status: ✅ CONFIRMED by user preferences*

**User Input:** "Sounds good" (< 5s recovery flow feels feasible, 3-line recap sufficient)

**Trigger:** Context-switch event (browser blur, OS notification, manual pause button)

**Auto-Pause Response:**
1. Save session state (beat ID, scroll position, timestamp) – 10ms
2. Exit flow-mode gracefully (no jarring UI change)
3. Display "Resume where left off" banner (non-blocking, top of screen)

**Resume Mechanism:**
1. User clicks "Resume" button (or presses Enter/Space)
2. Animated scroll to last-edited beat (300ms smooth scroll)
3. Display 3-line beat recap:
   ```
   Beat: "She walked to the shore"
   Last edit: 2 min ago
   Context: 245 words in this beat
   ```
4. Re-enter flow-mode (hide UI elements, focus input)
5. Micro-reward: flash animation (100ms) + next-word preview (50ms)
6. Total recovery time: < 5s

**Why This Works for Savannah:**
- Beat recap removes cognitive friction (you don't need to scroll/search)
- < 5s recovery preserves hyperfocus mental model
- Non-blocking UI (no modal interrupting flow)
- Preserves flat-list architecture (no hidden beats)

**Phase Assignment:** 1B (Phase 1A: manual pause button only)

---

### Mechanism 3: Momentum Recovery Micro-Rewards
*Status: ✅ CONFIRMED & UPDATED (sound defaults to OFF)*

**User Input:** "Sound defaults to off" (startle sensitivity acknowledged)

**Trigger:** Context-switch resume or manual flow-mode reactivation

**Micro-Reward Choreography:**

```
BASELINE (Sound OFF - Default):
- Flash animation (100ms): brightness +10%, fade back
- Next-word preview (50ms): display word suggestion below cursor
- Total latency: < 0.3s

OPTIONAL (Sound ON - User-Enabled):
- Flash animation (100ms)
- Sound cue (200ms): 200ms gentle 'ding', 400Hz sine wave
- Next-word preview (50ms)
- Total latency: < 0.5s (still within design constraint)
```

**Sound Implementation Details:**
- **Default State:** OFF (no startling users with ADHD startle sensitivity)
- **Location:** Settings → Accessibility → "Enable sound cues" toggle
- **Volume:** -12dB (quieter than standard notification)
- **Tone:** 400Hz sine wave (gentle, not alarming)
- **User Control:** Can adjust volume (-18dB to -6dB)

**Why This Works for Savannah:**
- Sound opt-in avoids startle response (common ADHD issue)
- Flash + preview still provide dual-channel feedback (visual + cognitive)
- Users who want sound can enable it without friction
- Accessibility-first approach (sensory needs respected)

**Phase Assignment:** 1B (can iterate quickly based on user feedback)

---

## 🔧 Failure-Mode Matrix (Updated for User Preferences)

### Scenario 4: Decision Paralysis in Beat Organization
**User Preference:** Limit visible beats (primary mitigation)

| Aspect | Specification |
|--------|---------------|
| Trigger | > 15 visible beats on screen, unclear organization |
| Severity | MEDIUM |
| Primary Mitigation | **Limit visible beats to 10-15 per screen** (Phase 1A) |
| Secondary Options | Arrow shortcuts + keyboard nav (Phase 1B) |
| Deferred | AI-suggested organization (Phase 2+) |
| Rationale | Reducing choice set addresses cognitive overload root cause |

**Implementation (Phase 1A):**
- Show beats in reverse chronological order (most recent first)
- Pagination: "beats 1-15 of 127" with prev/next buttons
- Alternative: Infinite scroll with lazy-load (test both in Phase 1B)
- Search + filter: find beat by title/tag without scrolling

**Phase 1B Enhancements:**
- Arrow shortcuts: ↑/↓ to move beat up/down (1 click, clear target)
- Keyboard shortcuts: Shift+U (move up), Shift+D (move down)
- Visual affordance: drag-handle icon (shows beats are reorderable)

**Phase 2+ Exploration:**
- AI suggestions: "Organize by timeline? Character? Theme?"
- Undo/redo for reorganization (safety net)
- Favorite/pin beats (reduce cognitive load)

**Why This Works for Savannah:**
- Limiting visible beats directly reduces decision paralysis
- Pagination provides control (see all, but not overwhelmed)
- Search + filter is faster than scrolling + organizing
- Additional tools (shortcuts, AI) are optimizations, not core fixes

---

### Scenario 10: Hyperfocus Over-Fatigue (Updated)
**User Preference:** No sound notifications by default

| Aspect | Specification |
|--------|---------------|
| Trigger | Extended session > 90 min continuous |
| Severity | LOW-MEDIUM |
| Mitigation | Gentle nudge after 60 min (dismissible, no sound default) |
| Feedback | Pet animates "great session" badge |
| Sound | OFF by default, can enable in settings |
| Auto-dismiss | 3s (user doesn't have to dismiss) |

**Implementation:**
- At 60 min mark: subtle visual nudge (pet moves to foreground, semi-transparent)
- Message: "You've been writing for 60 min – want to take a break?"
- Buttons: "Yes, take break" | "Keep writing" (both non-blocking)
- If no response: auto-dismiss after 5s, don't repeat
- Reason: Hyperfocus is ADHD strength; gentle nudge respects user autonomy

---

## 📊 Momentum-Preservation KPIs (Confirmed)

### KPI 1: Time-to-Resume < 10s (95th percentile)
**Target:** 70%+ of interruptions recover within 10s
**Baseline:** Phase 1A beta (100 sessions, 20 users, 2 weeks)
**Success Validation:** Auto-pause + resume banner + micro-reward reduce time-to-resume by 40%+ vs current state

### KPI 2: Interruptions Tolerated > 3 per session
**Target:** 80%+ of sessions with 3+ interruptions show continued engagement
**Why Matters:** If users abandon after few interruptions, momentum system failed
**Baseline:** Phase 1A without mechanics (estimated 30-40% tolerance), Phase 1B target 60%+

### KPI 3: Hyperfocus Session Average 45+ min
**Target:** Median session 45+ min (Savannah's baseline from design thinking)
**Baseline:** Phase 1A estimate 30-35 min, Phase 1B target 45+ min
**Mechanism:** Hyperfocus detection + variable rewards sustain focus longer

### KPI 4: Context-Switch Recovery Rate > 70%
**Target:** 70%+ resume vs abandon after context-switch
**Baseline:** Phase 1A estimated 40-50%, Phase 1B target 70%+
**Mechanism:** Auto-pause + resume banner + micro-rewards reduce friction

### KPI 5: Session-to-Session Continuation > 50%
**Target:** 50%+ of users return within 24h (ADHD habit formation)
**Baseline:** Phase 1A estimated 30-40%, Phase 1B target 50%+
**Mechanism:** Hyperfocus celebration + momentum rewards create positive associations

---

## ✅ Phase 1B Implementation Roadmap

### Sprint 1 (Week 1-2): Foundation
- [ ] Implement beat pagination (10-15 per screen)
- [ ] Add "Resume where left off" banner + session recovery
- [ ] Implement flash animation + next-word preview (no sound)
- [ ] Set up analytics: context_switch_detected, typing_resumed, session_metrics

### Sprint 2 (Week 3-4): Hyperfocus Detection
- [ ] Implement passive typing velocity monitoring (80+ WPM, 10+ min)
- [ ] Build pet animation framework
- [ ] Implement variable-interval reward system (30-50 min randomization)
- [ ] Implement badge display (3s auto-dismiss)

### Sprint 3 (Week 5-6): Refinement & Testing
- [ ] A/B test: auto-pause + resume vs manual pause only
- [ ] A/B test: variable-interval rewards vs fixed rewards
- [ ] A/B test: flash + preview vs flash + sound + preview
- [ ] Collect user feedback: what helped most?

### Sprint 4 (Week 7-8): Beta Measurement
- [ ] Run Phase 1A → 1B comparison
- [ ] Baseline all 5 KPIs
- [ ] Measure time-to-resume, recovery rate, session length
- [ ] Collect qualitative feedback on hyperfocus detection accuracy

---

## 🔬 Phase 1B Testing Strategy

### A/B Test 1: Auto-Pause + Resume
- **Control:** Manual pause button only (Phase 1A)
- **Treatment:** Auto-pause + resume banner + micro-reward
- **Metric:** Time-to-resume, session continuation rate
- **Sample:** 10 users per group (Phase 1B beta)
- **Duration:** 1 week

### A/B Test 2: Reward Timing
- **Control:** Fixed rewards (every 30 min exactly)
- **Treatment:** Variable rewards (30-50 min unpredictably)
- **Metric:** Session length, user engagement, 24h retention
- **Sample:** Split Phase 1B users 50/50
- **Duration:** Full 2-week beta

### A/B Test 3: Micro-Reward Modality
- **Control:** Flash animation only
- **Treatment A:** Flash + next-word preview
- **Treatment B:** Flash + sound (opt-in user) + preview
- **Metric:** User preference, time-to-resume, typing resumption rate
- **Sample:** 3-way split if sample size allows
- **Duration:** 1 week post-launch

### Qualitative Testing
- **Hyperfocus Detection Accuracy:**
  - Did detection trigger correctly? (false positives/negatives)
  - Did variable timing feel right, or too frequent/sparse?
  - Would optional focus-meter UI be useful?

- **Beat Pagination:**
  - Did 10-15 beat limit reduce decision paralysis?
  - Did users find pagination easy to navigate?
  - Any requests for shortcuts or filters?

---

## 📋 Session 2 Execution Checklist

### Pre-Session (Facilitator)
- [ ] Review acceptance criteria
- [ ] Review refined specifications (this document)
- [ ] Share Savannah's preferences with team: variable rewards, limit beats, sound off
- [ ] Prepare failure-mode matrix for team discussion
- [ ] Have design constraints visible (< 0.5s latency, no modals, flat-list)

### During Session (15 core exploration questions)
- [ ] Q1-4: Hyperfocus detection & pet body-doubling (map team ideas to spec)
- [ ] Q5-6: Decision paralysis (get team input on beat limit approach)
- [ ] Q7-9: Momentum recovery (validate micro-reward approach)
- [ ] Q10-13: Edge cases (lost annotation, deletion, crash recovery)
- [ ] Q14-15: KPI validation (confirm success targets feel achievable)

### Post-Session (48h)
- [ ] Finalize failure-mode matrix with team input
- [ ] Confirm three mechanisms for Phase 1B
- [ ] Prioritize implementation roadmap
- [ ] Assign owners (UX lead, product lead, engineering lead)
- [ ] Update beads issue with session results

---

## 🎯 Success Criteria

**Session 2 is SUCCESSFUL when:**

1. ✅ All 15 core exploration questions answered with team insights
2. ✅ Failure-mode matrix validated (no new critical scenarios discovered)
3. ✅ Three mechanisms confirmed for Phase 1B prototyping
4. ✅ Implementation roadmap agreed (sprint-by-sprint breakdown)
5. ✅ KPIs baseline measurement plan finalized
6. ✅ Phase 1B owners assigned (UX, product, engineering)
7. ✅ Team alignment on design constraints (< 0.5s, no modals, flat-list)
8. ✅ Beads issue updated with session outcomes within 48h

---

## 📝 Key Decisions Locked In

**These are confirmed and should NOT be re-discussed in Session 2:**

✅ **Hyperfocus Detection:** 80 WPM, 10+ min sustained, variable-interval rewards
✅ **Context-Switch Recovery:** < 5s, auto-pause + resume banner + beat recap
✅ **Momentum Rewards:** Flash + preview (no sound default)
✅ **Beat Pagination:** Limit to 10-15 per screen (Phase 1A)
✅ **Sound Feature:** Opt-in only (accessibility-first)
✅ **Design Constraints:** < 0.5s latency, no modals, flat-list mandatory, localStorage Phase 1A

**What Session 2 SHOULD Explore:**

- Additional failure modes beyond the 10 identified?
- Implementation details (animation style, recap layout, etc.)?
- Edge cases not yet covered?
- Phase 1B prioritization (which mechanism first)?
- Metrics and measurement approach (confirm KPIs feel achievable)?

---

## 🚀 Ready for Session 2 Execution

**Status:** ✅ ALL USER PREFERENCES INTEGRATED
**Confidence:** VERY HIGH (94%)
**Next Step:** Schedule Session 2, confirm participants, execute brainstorming with refined specifications

**Documents Ready:**
- SESSION-2-ACCEPTANCE-CRITERIA.md (process framework)
- SESSION-2-PAL-ANALYSIS-FINDINGS.md (detailed analysis)
- SESSION-2-REFINED-SPECIFICATIONS.md (this document – user preferences integrated)

---

_Generated: 2026-02-13_
_User Preferences: Integrated and Validated_
_Status: READY FOR SESSION 2 BRAINSTORMING_
_Analyst: Mary (Business Analyst Agent) + Savannah (User)_
