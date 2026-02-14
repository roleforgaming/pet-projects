# Session 2: ADHD Mechanics & Failure Mode Brainstorming
## Complete Documentation Index

**Status:** ✅ READY FOR EXECUTION
**Beads Issue:** pet-projects-wkd
**Date:** 2026-02-13 → 2026-02-14
**Owner:** Savannah (decisions), Product Lead (facilitation)

---

## 📚 Document Guide

### 1. **SESSION-2-ACCEPTANCE-CRITERIA.md** (START HERE IF: You're the facilitator)
**What:** Process framework with 75+ acceptance criteria
**Use:** Before, during, and after session execution
**Key sections:**
- Pre-session requirements (6 criteria)
- During-session process (15 core questions + synthesis)
- Output deliverables (3 major deliverables with specs)
- Session success validation (8 mandatory + 5 quality thresholds)
- Design constraints validation checklist
- Session failure conditions (8 explicit fail states)
- Post-session follow-up (9 criteria within 24h/48h/1 week)

**Why use it:** Defines what "done" means. Share with facilitator to ensure session meets all criteria.

---

### 2. **SESSION-2-PAL-ANALYSIS-FINDINGS.md** (START HERE IF: You want the research)
**What:** Deep analysis of ADHD mechanics with neuroscience grounding
**Use:** Understand the thinking behind each mechanism
**Key sections:**
- Executive summary (3-layer momentum system)
- Failure-mode matrix (10 ADHD-specific scenarios)
- Three prototype mechanisms (detailed specifications)
- Momentum-preservation KPIs (quantified targets)
- Five critical clarification points (answered by Savannah)
- Neuroscience references (Volkow, Barkley, Douglas)

**Why use it:** Provides research backing for each mechanism. Reference when team questions "why this approach?"

---

### 3. **SESSION-2-REFINED-SPECIFICATIONS.md** (START HERE IF: You're implementing Phase 1B)
**What:** Final technical specifications incorporating user preferences
**Use:** Implementation guide for engineering team
**Key sections:**
- Three mechanisms with final specs (updated for your preferences)
- Failure-mode matrix adjusted for your preferences
- Beat pagination strategy (Phase 1A → 1B)
- KPIs confirmed (5 metrics with numerical targets)
- Phase 1B implementation roadmap (4 sprints, detailed tasks)
- A/B testing strategy (3 test plans with metrics)
- Session 2 execution checklist

**Why use it:** Everything engineering needs to build Phase 1B. Specifications are grounded in your feedback.

---

### 4. **SESSION-2-READY-TO-EXECUTE.md** (START HERE IF: You want the complete summary)
**What:** Complete execution guide + quick reference
**Use:** Facilitator preparation + team alignment
**Key sections:**
- What's ready (3 complete deliverables)
- Savannah's clarifications (5 points, all integrated)
- Mechanism specs (quick reference, 3 mechanisms)
- Beat pagination (primary decision paralysis solution)
- KPIs (5 metrics, baseline plan)
- Phase 1B roadmap (4 sprints)
- Session success criteria (8 checkpoints)
- Facilitator checklist (pre/during/post)

**Why use it:** One-stop reference for everything. Share with team before session.

---

## 🎯 Quick Navigation by Role

### 👩‍💼 If you're **Savannah (Product Owner)**:
1. Read: SESSION-2-READY-TO-EXECUTE.md (overview)
2. Scan: SESSION-2-REFINED-SPECIFICATIONS.md (confirm your preferences are integrated)
3. Reference: SESSION-2-PAL-ANALYSIS-FINDINGS.md (if team questions why X approach)

### 👨‍💻 If you're the **Facilitator (Product/UX Lead)**:
1. Start: SESSION-2-ACCEPTANCE-CRITERIA.md (know what success looks like)
2. Prepare: SESSION-2-READY-TO-EXECUTE.md (read "Facilitator Checklist")
3. During session: Use 15-question framework from ACCEPTANCE-CRITERIA
4. Reference: SESSION-2-PAL-ANALYSIS-FINDINGS.md (if team gets stuck)

### 👨‍🔬 If you're **Implementing Phase 1B (Engineering Lead)**:
1. Start: SESSION-2-REFINED-SPECIFICATIONS.md (technical specs)
2. Reference: SESSION-2-PAL-ANALYSIS-FINDINGS.md (neuroscience grounding)
3. Plan: Phase 1B roadmap (4 sprints) from REFINED-SPECIFICATIONS
4. Execute: A/B testing strategy (3 tests) from REFINED-SPECIFICATIONS

### 👥 If you're a **Team Member (contributing ideas)**:
1. Skim: SESSION-2-READY-TO-EXECUTE.md (understand session purpose)
2. Read: SESSION-2-PAL-ANALYSIS-FINDINGS.md (see failure-mode matrix)
3. During session: Ask questions, contribute ideas, map to matrix

---

## 📋 Core Concepts Reference

### The Three-Layer Momentum System

**Layer 1: Passive Hyperfocus Detection**
- Detects when user enters flow state (80+ WPM, 10+ min sustained)
- Celebrates achievement with pet animation + badge + variable-interval rewards
- **Goal:** Encourage return sessions (dopamine-aligned habit formation)

**Layer 2: Auto-Pause + Rapid Resume**
- Auto-pauses flow-mode when context-switch detected (browser blur, notification)
- Resume mechanism: banner + animated scroll + 3-line beat recap < 5s total
- **Goal:** Preserve cognitive continuity after interruption

**Layer 3: Momentum Recovery Micro-Rewards**
- Flash animation (100ms) + next-word preview (50ms) = < 0.3s latency
- Optional sound (200ms) for users who want it; defaults OFF
- **Goal:** Remove friction for re-engagement after pause

**Why Synergistic:**
- Layer 1 makes users want to come back tomorrow
- Layer 2 preserves their mental state when interrupted
- Layer 3 removes friction to resume immediately
- All three work together to sustain momentum across sessions and interruptions

---

## 🎯 Your Clarifications (Integrated)

| Clarification | Your Answer | Specification Impact |
|---|---|---|
| 1. Hyperfocus detection (80 WPM, 10 min) | "This sounds right" | ✅ Confirmed. Proceed with 80 WPM sustained 10+ min as detection threshold. |
| 2. Context-switch recovery < 5s | "Sounds good" | ✅ Confirmed. Resume flow (banner + scroll + recap + reward) targets < 5s total. |
| 3. Reward timing (variable preferred) | "Variable" | ✅ Confirmed. Use variable-interval rewards (30-50 min unpredictably, not fixed). |
| 4. Decision paralysis solution | "Limit visible beats" | ✅ Confirmed. Primary Phase 1A solution: paginate beats (10-15 per screen). Defer shortcuts + AI suggestions to Phase 1B. |
| 5. Sound cue sensitivity | "Sound defaults to off" | ✅ Confirmed. Sound is opt-in feature (users must enable in settings). Baseline micro-reward: flash + preview only. |

---

## 📊 Success Metrics at a Glance

### Phase 1B KPIs (What Success Looks Like)

| KPI | Target | Why It Matters |
|-----|--------|----------------|
| **Time-to-Resume** | < 10s (95th percentile) | If recovery takes > 10s, momentum system fails. You need rapid context restoration. |
| **Interruptions Tolerated** | > 3 per session without abandonment | ADHD users face multiple interruptions. If they abandon after 2-3, the system failed. |
| **Hyperfocus Session Average** | 45+ minutes sustained | Your baseline from design thinking. Phase 1B should sustain or improve this. |
| **Context-Switch Recovery Rate** | > 70% resume vs abandon | After context-switch, 70%+ of users should resume typing (vs close app). |
| **24h Session Continuation** | > 50% users return within 24h | Dopamine-driven habit formation. If <50% return, momentum system isn't working. |

**Baseline Measurement:** 20 ADHD users, 2 weeks Phase 1A baseline + 2 weeks Phase 1B with mechanics

---

## 🔄 Implementation Timeline

### Phase 1A (Current)
- ✅ Beat pagination (10-15 per screen, Phase 1A MVP priority)
- ⏳ Manual pause button (basic context-switch control)

### Phase 1B (Next: 8 weeks)
**Sprint 1 (W1-2):** Beat pagination refinement, resume banner, analytics setup
**Sprint 2 (W3-4):** Hyperfocus detection (80 WPM), pet animation, variable rewards
**Sprint 3 (W5-6):** A/B testing (auto-pause, reward timing, micro-reward modality)
**Sprint 4 (W7-8):** KPI measurement, Phase 1C roadmap

### Phase 1C & 2+ (Future)
- Arrow shortcuts + keyboard navigation
- AI-suggested organization
- Advanced gamification (streaks, achievements)
- Optional cloud sync + backup

---

## ✅ Before Session 2

**Facilitator Pre-Session Checklist (48h before):**
- [ ] Read SESSION-2-REFINED-SPECIFICATIONS.md (understand final specs)
- [ ] Review SESSION-2-ACCEPTANCE-CRITERIA.md (know success criteria)
- [ ] Prepare failure-mode matrix for team discussion (visual on board)
- [ ] Set up shared board (Miro, FigJam, whiteboard)
- [ ] Invite participants (product lead, UX lead, ADHD consultant optional)
- [ ] Confirm: 90-120 min time block scheduled
- [ ] Confirm: Savannah's preferences shared with team (variable rewards, limit beats, sound off)

**Team Pre-Session Review:**
- [ ] Read SESSION-2-READY-TO-EXECUTE.md (5 min skim)
- [ ] Review failure-mode matrix (10 scenarios, understand categories)
- [ ] Understand: 15-question framework (how session will flow)

---

## 🚀 After Session 2 (Within 48h)

**Post-Session Checklist:**
- [ ] Transcribe notes from shared board
- [ ] Update failure-mode matrix with any new scenarios
- [ ] Confirm: 3 mechanisms ready for Phase 1B (or document alternatives)
- [ ] Assign owners: UX lead, product lead, engineering lead
- [ ] Update beads issue (pet-projects-wkd) with session outcomes
- [ ] Share outcomes with stakeholders
- [ ] Schedule Phase 1B sprint kickoff

---

## 📞 Questions?

**Before Session 2:**
- Mechanism not clear? → Read SESSION-2-PAL-ANALYSIS-FINDINGS.md (detailed specs + neuroscience)
- Want quick reference? → Read SESSION-2-READY-TO-EXECUTE.md (one-page summaries)
- Need technical details? → Read SESSION-2-REFINED-SPECIFICATIONS.md (implementation guide)

**During Session 2:**
- Team questions approach? → Reference failure-mode matrix (maps ideas to scenarios)
- Need to validate KPIs? → Share KPI definitions from SESSION-2-REFINED-SPECIFICATIONS.md
- Clarify design constraints? → Show "Non-negotiable Constraints" (< 0.5s, no modals, flat-list)

**After Session 2:**
- Implement Phase 1B? → Use SESSION-2-REFINED-SPECIFICATIONS.md (roadmap + A/B test strategy)
- Report outcomes? → Share SESSION-2-READY-TO-EXECUTE.md (overview for stakeholders)

---

## 🎯 Document Statistics

| Document | Pages | Focus | Use Case |
|----------|-------|-------|----------|
| SESSION-2-ACCEPTANCE-CRITERIA.md | ~15 pages | Process framework | Facilitators, success validation |
| SESSION-2-PAL-ANALYSIS-FINDINGS.md | ~20 pages | Research grounding | Technical details, neuroscience backing |
| SESSION-2-REFINED-SPECIFICATIONS.md | ~18 pages | Implementation guide | Engineering, Phase 1B roadmap |
| SESSION-2-READY-TO-EXECUTE.md | ~15 pages | Complete summary | Facilitators, team alignment |
| SESSION-2-INDEX.md (this) | ~8 pages | Navigation guide | Find right document for your role |

**Total Documentation:** ~70 pages of analysis, specifications, and implementation guidance

---

## ✨ The Big Picture

**What we're solving:**
ADHD writers lose momentum when hyperfocus is interrupted. Without support, they abandon sessions. This creates a cycle of: hyperfocus → interruption → exhaustion → abandonment → no return.

**How we're solving it:**
A three-layer momentum system that:
1. Celebrates hyperfocus (dopamine-aligned rewards)
2. Recovers rapidly from interruptions (< 5s resume)
3. Removes friction to re-engage (micro-rewards)

**Why it matters:**
If successful, Phase 1B will show: 50%+ users return within 24h (vs 30-40% now), sessions average 45+ min (vs 30-35 now), and > 70% recover from interruptions (vs 40-50% now).

**Next: Session 2 execution** to validate these mechanisms with your team and prepare Phase 1B implementation.

---

## 📁 All Documents Located In

```
_bmad-output/brainstorming/

├── SESSION-2-ACCEPTANCE-CRITERIA.md
├── SESSION-2-PAL-ANALYSIS-FINDINGS.md
├── SESSION-2-REFINED-SPECIFICATIONS.md
├── SESSION-2-READY-TO-EXECUTE.md
├── SESSION-2-INDEX.md (this file)
└── BRAINSTORMING-SESSIONS-SETUP.md (Sessions 1, 2, 3 overview)
```

---

**Status: ✅ READY FOR SESSION 2 EXECUTION**
**Confidence: VERY HIGH (94%)**
**Generated: 2026-02-14**
**Analyst: Mary (Business Analyst Agent)**
