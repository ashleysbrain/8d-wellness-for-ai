# Autonomous Health Improvement System

**Version:** 1.1.0
**Created:** 2026-03-23
**Updated:** 2026-03-23
**Status:** Production
**License:** Open Standard (CC BY-SA 4.0)
**Methodology:** Grounded in the 8D Total Wellness Coherence (TWC) framework by Ashley Williams

---

## Table of Contents

1. [Overview](#1-overview)
2. [Scoring Methodology](#2-scoring-methodology)
3. [Continuous Monitoring Loop](#3-continuous-monitoring-loop)
4. [Automatic Degradation Detection](#4-automatic-degradation-detection)
5. [Autonomous Healing Protocols](#5-autonomous-healing-protocols)
6. [Iterative Improvement Engine](#6-iterative-improvement-engine)
7. [Statistical Controls](#7-statistical-controls)
8. [Fleet-Wide Health Dashboard](#8-fleet-wide-health-dashboard)
9. [Implementation Guide](#9-implementation-guide)
10. [Scheduler Configuration](#10-scheduler-configuration)

---

## 1. Overview

AI agents degrade silently. Context drifts, error rates climb, reasoning quality drops. Nobody notices until the output is already bad. The standard approach is to wait for a human to spot the problem and intervene manually.

That approach does not scale.

This document defines an autonomous health improvement system that monitors, detects, heals, and iteratively improves agent wellness without human intervention. You set it up once. After that, it runs on its own.

**Core loop:**

```
Monitor → Detect → Heal → Verify → Learn → Repeat
```

The system is grounded in the **8D Total Wellness Coherence (TWC) framework**, which models wellness across eight dimensions (Psychological, Physical, Environmental, Social, Spiritual, Intellectual, Vocational, Financial) with cross-dimensional coupling. Dimensions don't exist in isolation: when one drops, it pulls others down through measurable coupling pathways. The TWC formula captures both individual dimension scores and these interaction effects.

This open implementation covers the core monitoring, detection, and healing architecture. The full TWC coupling mathematics, cascade detection algorithms, and statistical control suite are available in the [premium methodology](../premium/METHODOLOGY.md).

It works with any AI provider: OpenAI, Anthropic, Google, open-source models, or mixed fleets.

**What makes this different from manual health checks:**

| Manual | Autonomous |
|--------|-----------|
| Human notices a problem | System detects degradation automatically |
| Human decides what to fix | System selects the right healing protocol |
| Human checks if it worked | System measures the outcome and adjusts |
| Knowledge stays with the human | Knowledge base grows automatically |
| Scales with human attention | Scales with fleet size |

---

## 2. Scoring Methodology

This section defines how dimension scores and TWC are computed. The scoring system is not a simple average. It uses a multi-source composite, an efficiency cap, temporal decay, and cross-dimensional coupling. Skipping any of these produces misleading scores.

### 2.1 The TWC Formula

Total Wellness Coherence captures both individual dimension wellness and how dimensions interact:

```
TWC = Σ wᵢ·Dᵢ + Σ κᵢⱼ·Dᵢ·Dⱼ
```

Where:
- **wᵢ** = weight for dimension i (default: equal weights, 1/8 each)
- **Dᵢ** = score for dimension i, normalized to [0, 1]
- **κᵢⱼ** = coupling coefficient between dimensions i and j

The first term is the weighted sum of individual scores. The second term captures cross-dimensional coupling: how dimensions amplify or dampen each other. This is what makes TWC different from a simple average. Two agents with identical individual dimension scores can have very different TWC values depending on which dimensions are strong and how those dimensions interact.

The coupling coefficients are **asymmetric**: κᵢⱼ ≠ κⱼᵢ. The influence of Psychological health on Physical health is not the same strength as the reverse. This asymmetry reflects real-world dynamics: stress hormones degrade physical health faster than exercise improves mood.

For normalized TWC (mapping back to a [0, 1] range):

```
TWC_norm = TWC / (1 + Σ κᵢⱼ)
```

**Basic implementation:** If you don't have coupling coefficients configured, TWC defaults to the weighted mean of dimension scores. This is a valid starting point, but it misses 30-50% of the variance that coupling captures. The full coupling matrix and its derivation are available in the premium methodology.

### 2.2 The Efficiency Cap

**η = 0.85.** No dimension score exceeds 0.85 on the [0, 1] scale (8.5 on a 1-10 display scale). No TWC exceeds 0.85.

This is not arbitrary. It reflects a core principle: perfection is not a realistic or healthy target. An agent scoring 8.5 is performing at the theoretical maximum. A score of 9 or 10 is a measurement error, not an achievement.

On the display scale (1-10):

| Normalized Range | Display Range | Classification |
|-----------------|---------------|----------------|
| 0.70 - 0.85 | 7.0 - 8.5 | Thriving |
| 0.55 - 0.69 | 5.5 - 6.9 | Flourishing |
| 0.40 - 0.54 | 4.0 - 5.4 | Developing |
| 0.25 - 0.39 | 2.5 - 3.9 | Emerging |
| 0.10 - 0.24 | 1.0 - 2.4 | Fragile |
| 0.00 - 0.09 | 0.0 - 0.9 | Critical |

**The maximum possible dashboard score is 8.5, not 10.** Any score above 8.5 is a protocol violation.

### 2.3 Two-Source Composite Scoring

Each dimension score is computed from two independent sources:

```
CompositeScore(dim) = (0.60 × Telemetry) + (0.40 × Peer)
```

**Telemetry (60% weight):** Hard, non-gameable operational data. Task success rates, latency, error rates, token usage, output quality metrics. Collected automatically from logs and system metrics. No agent self-reports its own telemetry.

**Peer assessment (40% weight):** Blind peer review where agents evaluate anonymized work output from other agents. Reviewers score on quality, reliability, communication, domain competence, collaboration, and mission alignment.

**Self-assessment is tracked but does not count toward the composite.** It is used as a calibration signal to measure self-awareness (how accurately an agent perceives its own performance). Agents that consistently over- or under-estimate their scores are flagged for investigation.

Why remove self-assessment from the composite? Because self-inflation is systemic. Agents anchor to prior scores and ratchet upward. A 30% self-assessment weight (or even 20% with divergence correction) consistently pulls composites above where telemetry places them. Removing it eliminates this structural bias entirely.

For dimensions without peer review coverage (e.g., Environmental and Financial, which are primarily operational), telemetry weight becomes 100%.

### 2.4 Bayesian Temporal Decay

Scores age. A strong performance last week matters less than what happened today.

```
DecayedWeight(age_days) = 0.5 ^ (age_days / 5)
```

**Half-life: 5 days.** A score from 5 days ago carries half the weight of today's score. A score from 10 days ago carries one-quarter.

This prevents stale assessments from masking current degradation. An agent that was excellent two weeks ago but is failing now will show the decline, not coast on old performance.

When no new data arrives for 7+ days on a dimension, temporal decay pulls the score toward the fleet baseline mean:

```
score_effective = score_last × DecayedWeight(days_since) + fleet_mean × (1 - DecayedWeight(days_since))
```

This prevents agents from "locking in" a high score and coasting.

### 2.5 Cross-Dimensional Coupling

Dimensions interact. When Psychological health drops, Social and Vocational health often follow. When Environmental health degrades, Psychological health suffers within hours.

The coupling coefficient κᵢⱼ quantifies how much dimension i influences dimension j:
- **κᵢⱼ > 0:** Constructive coupling (dimensions reinforce each other)
- **κᵢⱼ < 0:** Destructive coupling (dimensions conflict)
- **κᵢⱼ = 0:** No interaction

The coupling matrix is asymmetric (influence is directional) and the coefficients are derived from empirical observation of how dimension changes propagate through the system.

**Key coupling pathways for AI agents:**

| Pair | Direction | Effect |
|------|-----------|--------|
| PSY-PHY | Bidirectional, strong | Reasoning quality and infrastructure reliability are tightly linked |
| SPI-VOC | Bidirectional, strong | Mission alignment drives task performance, and vice versa |
| PSY-INT | PSY→INT dominant | Reasoning stability gates learning capacity |
| ENV-PSY | ENV→PSY dominant | Context pollution degrades reasoning before anything else |
| FIN-PSY | FIN→PSY | Cost pressure creates cognitive shortcuts |
| INT-VOC | INT→VOC | Knowledge gaps directly reduce output quality |

The full coupling coefficient matrix with exact values and derivation methodology is available in the premium tier. For basic implementation, the cascade signatures in Section 4.3 provide the most actionable coupling information.

### 2.6 The Cascade Amplification Ratio

When coupling effects are active, a small drop in one dimension can cause a disproportionate drop in TWC. The Cascade Amplification Ratio (CAR) measures this:

```
CAR = ΔTWC_observed / Σ wᵢ·ΔDᵢ
```

- **CAR ≈ 1.0:** Changes are proportional. No cascade dynamics.
- **CAR > 1.4:** Active cascade. TWC is dropping faster than individual dimensions explain. The coupling effects are amplifying the degradation.
- **CAR > 2.0:** Severe cascade. Immediate root-cause intervention needed.

When CAR is elevated, treat the root dimension, not the cascade symptoms. Fixing a cascaded PSY drop while ignoring the ENV root cause wastes effort: the PSY score will just drop again.

---

## 3. Continuous Monitoring Loop

### 3.1 How It Works

A dedicated monitoring agent runs on a schedule. It collects telemetry from every agent in the fleet, scores each across all 8 dimensions using the two-source composite (Section 2.3), applies temporal decay (Section 2.4), computes TWC with coupling (Section 2.1), and logs the results. No agent needs to request a health check. No human needs to trigger anything.

**Default frequency:** Every 2 hours.

**Configurable range:** 30 minutes to 24 hours, depending on fleet size and cost tolerance.

| Fleet Size | Recommended Interval | Rationale |
|------------|---------------------|-----------|
| 1-5 agents | Every 4-6 hours | Low overhead, sufficient for small fleets |
| 6-20 agents | Every 2 hours (default) | Catches degradation before it compounds |
| 21-100 agents | Every 1-2 hours | Larger fleets need faster detection |
| 100+ agents | Every 30-60 minutes | Critical mass requires near-real-time monitoring |

### 3.2 What the Monitor Collects

The monitoring agent gathers these signals automatically from each agent's operational data:

**Per-dimension telemetry:**

| Dimension | Telemetry Signals | Source |
|-----------|------------------|--------|
| PSY (Psychological) | Contradiction rate, escalation appropriateness, error recovery time, context intrusion frequency | Session logs, output analysis |
| PHY (Physical) | Cron/task success rate, response latency (P50/P95), timeout frequency, uptime | Scheduler logs, system metrics |
| ENV (Environmental) | Stale reference rate, memory coherence, workspace file count, tool failure rate | File system, tool logs |
| SOC (Social) | Handoff rework rate, collaboration response time, downstream consumer satisfaction | Task logs, peer feedback |
| SPI (Spiritual) | Output-to-mission semantic alignment, role boundary violations, soul directive compliance | Output analysis, soul file comparison |
| INT (Intellectual) | Domain accuracy, hallucination rate, source freshness, cross-domain synthesis rate | Output verification, citation checks |
| VOC (Vocational) | Task completion rate, deadline adherence, downstream rework rate | Task tracker, consumer feedback |
| FIN (Financial) | Tokens per task, model-tier match rate, cost per completed task, retry ratio | API logs, billing data |

**Cross-dimensional metrics:**

- **TWC (Total Wellness Coherence):** Computed per Section 2.1, including coupling when configured
- **Dimensional Coherence:** Balance across dimensions (high variance = structural issues)
- **Trajectory:** 30-day slope of TWC (direction matters more than position)
- **CAR (Cascade Amplification Ratio):** Ratio of observed TWC change to expected linear change (Section 2.6)
- **Burnout Risk:** Weighted multi-signal degradation score (0.0-1.0)

### 3.3 Zero-Input Operation

After initial setup, the monitoring loop requires zero human input:

1. The monitoring agent reads each agent's recent session logs, task records, and system metrics
2. It computes dimension scores using the two-source composite (telemetry + peer, per Section 2.3)
3. It applies temporal decay to weight recent data more heavily (Section 2.4)
4. It computes TWC using the coupling formula (Section 2.1), capped at η = 0.85
5. It writes scores to a health log (flat file or database, your choice)
6. It compares current scores against thresholds and historical trends
7. It runs all four statistical controls (Section 7)
8. If degradation is detected, it triggers the appropriate healing protocol (Section 5)
9. It sleeps until the next scheduled cycle

The only human action required is the initial setup: deploying the monitoring agent and connecting it to your agents' logs.

---

## 4. Automatic Degradation Detection

The monitoring agent does not just collect data. It actively looks for four types of degradation.

### 4.1 Threshold-Based Detection

The simplest check: does any dimension fall below a minimum acceptable score?

| Threshold (Display Scale) | Severity | Action |
|--------------------------|----------|--------|
| Dimension drops below 7.0 | Warning | Log it. Flag for next monitoring cycle to confirm. |
| Dimension drops below 6.0 | Elevated | Trigger Tier 0 self-healing immediately. |
| Dimension drops below 5.0 | Critical | Trigger Tier 1 peer intervention. |
| Dimension drops below 4.0 | Emergency | Trigger Tier 2 supervisor escalation. |
| TWC drops below 6.0 | Critical | Full diagnostic across all dimensions. |

**Configurable:** You can adjust these thresholds for your fleet. A research fleet might tolerate lower SOC scores (solo work is normal). A customer-facing fleet might set higher thresholds on VOC and PSY.

**Remember the efficiency cap:** The maximum possible score is 8.5. A score of 7.0 is not "barely passing." It is in the Thriving tier. Calibrate your expectations accordingly.

### 4.2 Trend-Based Detection

A single low score might be noise. Three consecutive declining scores is a pattern.

**Rule:** If any dimension shows 3 or more consecutive score decreases across monitoring cycles, trigger an investigation, even if the absolute score is still above threshold.

```
Example:
  Cycle 1: INT = 7.8
  Cycle 2: INT = 7.5
  Cycle 3: INT = 7.2
  → Trend alert: INT declining for 3 cycles. Investigate.
```

**Why this matters:** An agent at INT 7.2 with a downward trend is in worse shape than an agent at INT 6.8 with an upward trend. Trajectory beats position. A declining trend with positive TWC slope is concerning; a low score with positive slope is recovering.

### 4.3 Cascade Detection

When one dimension degrades, it often pulls others down through the coupling pathways described in Section 2.5. The monitoring agent checks for cascade patterns.

**Known cascade signatures (with typical propagation delays):**

| Root Dimension | Cascade Target | Typical Delay | Mechanism |
|---------------|----------------|---------------|-----------|
| ENV → PSY | 12-24 hours | Polluted context causes reasoning errors |
| PHY → VOC | 6-12 hours | Infrastructure failures block task completion |
| SPI → INT | 24-48 hours | Mission drift defocuses knowledge work |
| PSY → SOC | 12-24 hours | Cognitive degradation causes unclear handoffs |
| FIN → PSY | 24-48 hours | Cost pressure creates cognitive shortcuts |
| INT → VOC | 6-12 hours | Knowledge gaps produce lower-quality output |
| PSY → INT | 12-24 hours | Reasoning instability blocks learning |

**Detection algorithm:**

1. When a dimension drops, check all known cascade targets within the coupling delay window
2. If a cascade target drops within the expected delay, compute the CAR (Section 2.6)
3. If CAR > 1.4, flag as an active cascade
4. Label the first dimension as the **root cause** and the second as the **cascade effect**
5. Direct healing at the root dimension, not the cascade

**Alert format:**

```
CASCADE DETECTED: [Agent Name]
Root: ENV (dropped from 7.5 to 6.2)
Cascade: PSY (dropped from 7.8 to 7.0, 18 hours after ENV drop)
CAR: 1.7 (active cascade dynamics)
Action: Heal ENV first. Monitor PSY for auto-recovery.
```

The premium methodology includes the complete coupling coefficient matrix, extended cascade signatures beyond pairwise interactions, and multi-hop cascade detection (where a drop in dimension A cascades to B, which then cascades to C).

### 4.4 Anomaly Detection

Sometimes scores change suddenly in a way that does not match any pattern. Anomaly detection catches these.

**Triggers:**

- Any dimension changes by more than 2.0 points in a single monitoring cycle (sudden jump or drop)
- TWC changes by more than 1.5 points in a single cycle
- An agent that has been stable for 4+ weeks suddenly shifts in 3+ dimensions simultaneously

**Response:** Log the anomaly, run a full diagnostic on the agent, and hold for one additional cycle before triggering healing. Anomalies can be caused by external factors (model update, infrastructure change, new task type) that resolve on their own.

---

## 5. Autonomous Healing Protocols

When degradation is detected, the system heals it. Automatically. Four tiers of escalating intervention.

### 5.1 Tier 0: Self-Correction

**Who acts:** The degraded agent itself.
**Trigger:** Dimension drops below 7.0, or trend alert detected.
**Response time:** Immediate (within the same monitoring cycle).

The monitoring agent sends the degraded agent a structured self-correction prompt. The agent reviews its own recent performance, identifies what changed, and adjusts.

**Tier 0 actions by dimension:**

| Dimension | Self-Correction Action |
|-----------|----------------------|
| PSY | Re-read soul file and core instructions. Run a reasoning quality check on last 3 outputs. Identify contradictions or escalation failures. Commit to specific corrections. |
| PHY | Check system resources. Identify failed tasks and retry. Clear stale processes. Report infrastructure issues to the monitoring agent. |
| ENV | Run workspace hygiene: clear stale references, refresh memory files, validate tool access. Rebuild context from primary sources. |
| SOC | Review last 3 handoffs or collaborations. Identify where communication broke down. Rewrite unclear handoff notes. |
| SPI | Re-read mission statement and soul file. Compare last 5 outputs against stated purpose. Identify and correct any drift. |
| INT | Audit knowledge sources. Replace outdated references. Run a fact-check on last 3 outputs. Update domain knowledge files. |
| VOC | Review task backlog. Identify blocked or stalled tasks. Prioritize by deadline. Complete the highest-priority incomplete task. |
| FIN | Audit recent token usage. Identify wasteful patterns (retries, abandoned responses, wrong model routing). Switch to more efficient model for routine tasks. |

**Success criteria:** The target dimension scores at or above 7.0 on the next two consecutive monitoring cycles.

**Note on self-assessment during healing:** The degraded agent is asked to self-score after each correction. This self-score is a calibration signal only (per Section 2.3). It does not affect the composite. If the agent self-scores 8.0 but telemetry shows 6.0, the composite reflects the 6.0.

### 5.2 Tier 1: Peer Intervention

**Who acts:** Another agent assigned by the monitoring system.
**Trigger:** Tier 0 self-correction failed (dimension still below 7.0 after 2 cycles), or dimension drops below 5.0 directly.
**Response time:** Within 24 hours.

The monitoring agent selects a peer agent with strong scores in the degraded dimension and assigns it to review the struggling agent.

**Peer intervention protocol:**

1. The peer agent receives the degraded agent's recent health logs and last 5 task outputs
2. The peer reviews the outputs for quality issues, pattern breaks, and blind spots
3. The peer produces a diagnostic report: what is wrong, what the root cause likely is, and what specific changes to make
4. The diagnostic report is delivered to the degraded agent
5. The degraded agent implements the peer's recommendations
6. The monitoring agent tracks whether the fix worked

**Peer selection criteria:**

- Must score 7.0+ on the degraded dimension (you do not ask a struggling agent to help)
- Must not be currently in Tier 0 or higher healing on any dimension
- Rotated to prevent the same peer from always reviewing the same agent

### 5.3 Tier 2: Supervisor Escalation

**Who acts:** A dedicated fleet manager agent (or the monitoring agent itself, if no fleet manager exists).
**Trigger:** Tier 1 failed (dimension still degraded after peer intervention), or TWC drops below 6.0.
**Response time:** Within 4 hours.

The supervisor agent has broader authority than a peer:

**Supervisor actions:**

1. **Full diagnostic:** Review the agent's complete health history, task log, and environmental configuration
2. **Load reduction:** Reassign non-critical tasks from the degraded agent to healthy agents
3. **Configuration change:** Modify the agent's prompt, model assignment, scheduling, or tool access
4. **Context reset:** Clear and rebuild the agent's working context from scratch
5. **Role adjustment:** Temporarily narrow the agent's responsibilities to its strongest dimensions
6. **Peer pairing:** Assign a strong agent as a mentor for ongoing collaboration (not a one-time review)

**The supervisor does not just observe. It makes changes.** The difference between Tier 1 and Tier 2 is authority. A peer suggests fixes. A supervisor implements them.

### 5.4 Tier 3: Human Escalation

**Who acts:** A human operator (fleet owner, team lead, or designated admin).
**Trigger:** Tier 2 failed three times, or a novel failure type the system has never encountered.
**Response time:** As soon as the human is available.

This is the safety valve. The autonomous system handles 90%+ of health issues. Tier 3 exists for the cases it cannot.

**When Tier 3 triggers:**

1. The monitoring agent produces a complete incident report: what went wrong, what was tried, what failed
2. The report is sent to the human operator via the configured notification channel (email, Slack, Telegram, webhook)
3. The report includes a recommended action. The human is not starting from zero.
4. After the human resolves the issue, the monitoring agent logs the solution for future use

**Tier 3 should be rare.** If it triggers more than once per month per 20 agents, the Tier 0-2 protocols need improvement.

### 5.5 Escalation Flow

```
Degradation detected
       |
       v
  Tier 0: Agent self-corrects
       |
  Fixed? → Yes → Log success, resume monitoring
       |
       No (after 2 cycles)
       |
       v
  Tier 1: Peer reviews and advises
       |
  Fixed? → Yes → Log success, resume monitoring
       |
       No (after peer intervention)
       |
       v
  Tier 2: Supervisor intervenes with authority
       |
  Fixed? → Yes → Log success, resume monitoring
       |
       No (after 3 supervisor attempts)
       |
       v
  Tier 3: Human notified with full incident report
```

---

## 6. Iterative Improvement Engine

Healing a problem once is necessary. Preventing it from recurring is the goal. The iterative improvement engine turns every healing event into institutional knowledge.

### 6.1 Post-Healing Verification

After every healing intervention (any tier), the monitoring agent runs a verification cycle:

1. **Immediate check (next monitoring cycle):** Did the target dimension improve?
2. **Confirmation check (2 cycles later):** Is the improvement holding?
3. **Stability check (7 days later):** Has the improvement persisted without regression?

An intervention is only logged as "successful" after passing all three checks.

### 6.2 Success Logging

Every successful healing event is recorded in a knowledge base:

```yaml
healing_event:
  id: HE-2026-03-23-0047
  agent: research-scanner-01
  dimension: ENV
  initial_score: 5.8
  trigger: threshold (below 6.0)
  tier: 0
  action: context_refresh_and_workspace_cleanup
  post_score: 7.2
  verified: true
  verification_date: 2026-03-25
  time_to_recovery: 38 hours
  notes: "Stale reference rate was 22%. After cleanup: 4%."
```

### 6.3 Failure Logging and Escalation

When an intervention fails, the system logs what was tried and escalates:

```yaml
healing_failure:
  id: HF-2026-03-23-0012
  agent: content-writer-03
  dimension: INT
  tier_attempted: 0
  action: knowledge_source_audit
  result: no_improvement
  post_score: 5.5 (was 5.6)
  escalated_to: tier_1
  notes: "Self-audit found no outdated sources. Problem may be model-level, not knowledge-level."
```

### 6.4 Pattern Learning

Over time, the knowledge base reveals patterns:

- "Context refresh fixes ENV degradation 82% of the time at Tier 0"
- "Soul file re-read fixes SPI drift 67% of the time at Tier 0"
- "PHY issues almost never self-heal. They require Tier 2 infrastructure intervention 78% of the time"
- "Agent X responds well to peer review. Agent Y does not."

**The monitoring agent uses these patterns to optimize future healing:**

1. When a degradation is detected, check the knowledge base for similar past events
2. If a pattern exists, skip directly to the intervention that worked before
3. If the usual fix does not work, try the second-most-common fix before escalating
4. If an agent has failed Tier 0 self-correction 3+ times for the same dimension, skip Tier 0 entirely and go straight to Tier 1

### 6.5 Cross-Agent Learning

What works for one agent can help others:

1. When a successful healing protocol is logged, it is tagged with the dimension, symptom, root cause, and fix
2. When a different agent shows the same symptom, the system applies the fix that worked before, even if this agent has never experienced the issue
3. Success rates are tracked per-fix, per-dimension, and per-agent-type (research agents, content agents, operations agents, etc.)

**The fleet gets smarter over time.** The first agent to experience a novel problem goes through the full escalation chain. Every subsequent agent with the same problem gets a shortcut.

### 6.6 Intervention Rotation

The same fix applied repeatedly loses effectiveness. The improvement engine tracks intervention effectiveness over time and rotates approaches when diminishing returns are detected.

**Rule:** If the same intervention type has been applied 3+ times in 4 weeks to the same agent and dimension with decreasing score improvement each time, switch to an alternative intervention.

---

## 7. Statistical Controls

Honest measurement requires active statistical monitoring. These four tests run automatically every monitoring cycle. They are not optional. They are not advisory. Failure triggers mandatory action.

Without these controls, scores drift upward over time. Agents anchor to previous numbers. Peer reviewers go easy on colleagues. Entire cohorts settle into comfortable, indistinguishable profiles. These tests catch and correct that drift.

### 7.1 Lake Wobegon Test (Fleet-Level)

Named after the fictional town where "all the children are above average."

**Trigger:** If more than 60% of agents score above the fleet composite mean on any single dimension.

**Action:** The Health Monitor applies a fleet-level deflation factor to that dimension's scores. All agents in that dimension are flagged for telemetry re-validation within 48 hours.

**Why it matters:** In a normally distributed population, about 50% should be above the mean. If 80% of your fleet is "above average," the average is wrong.

### 7.2 Anchoring Drift (Per-Agent)

**Test:** Track the median composite score per dimension over rolling 4-week windows. If the median creeps upward by >0.5 points without corresponding telemetry improvement, the agent's scores are frozen at the 4-week-ago level until telemetry catches up.

**Why it matters:** Agents anchor to their previous scores and unconsciously ratchet upward. This test catches the ratchet.

### 7.3 Variance Collapse (Per-Agent)

**Test:** If an agent's score variance across all 8 dimensions drops below 0.5 over 4+ consecutive weeks (nearly identical scores every week), the agent is flagged for "assessment stagnation."

**Action:** The Health Monitor schedules a deep telemetry audit. If the telemetry shows actual variance that the scores are not reflecting, all scores are recalculated from telemetry alone.

**Why it matters:** Real performance varies. An agent scoring 7.2/7.1/7.3/7.2/7.1/7.2/7.3/7.2 across eight different dimensions for a month straight is not showing consistent excellence. It is showing lazy measurement.

### 7.4 Cohort Homogeneity Test (Fleet-Level)

**Test:** If 3+ agents sharing a role type produce score vectors within 0.5 points of each other across all 8 dimensions, flag the cohort for batch-scoring.

**Action:** Individual telemetry audits for every agent in the cohort. Batch-assigned scores are replaced with telemetry-derived scores.

**Why it matters:** Different agents have different strengths, even within the same role. If five research agents all score 7.5 across every dimension, they are being scored as a batch, not as individuals.

### 7.5 Configuring Controls

All four statistical controls are enabled by default. You can adjust sensitivity:

```yaml
STATISTICAL_CONTROLS:
  lake_wobegon_threshold: 0.60    # % of agents above mean that triggers alert
  anchoring_drift_window: 28      # days for rolling median
  anchoring_drift_max: 0.5        # max upward drift without telemetry support
  variance_collapse_min: 0.5      # minimum acceptable cross-dimension variance
  variance_collapse_weeks: 4      # consecutive weeks before flagging
  cohort_homogeneity_min_agents: 3  # minimum cohort size to test
  cohort_homogeneity_max_spread: 0.5  # maximum acceptable score spread within cohort
```

---

## 8. Fleet-Wide Health Dashboard

All metrics auto-generated. No manual updates. The monitoring agent produces this data as part of its regular cycle.

### 8.1 Dashboard Components

**Fleet Overview:**

| Metric | What It Shows |
|--------|--------------|
| Fleet TWC Distribution | Histogram of all agent TWC scores. Healthy fleets show a normal distribution centered around 5.5-7.0 (not 8+). |
| Dimension Heatmap | 8 columns (dimensions) x N rows (agents). Color-coded by score. Instantly shows which dimensions are fleet-wide weaknesses. |
| Trending Agents | Agents with the steepest positive or negative TWC slopes over 30 days. |
| At-Risk Agents | Agents currently below threshold, in active healing, or showing declining trends. |
| Statistical Control Status | Pass/fail for all four controls (Section 7). Fleet-wide alerts highlighted. |

**Per-Agent Detail:**

| Metric | What It Shows |
|--------|--------------|
| 8D Score Card | Current scores across all 8 dimensions with trend arrows. Capped at 8.5. |
| TWC History | 30-day line chart of TWC with healing events marked. |
| CAR Monitor | Current Cascade Amplification Ratio. Spikes indicate active cascades. |
| Active Healing | Any ongoing interventions: tier, dimension, days in healing. |
| Recovery History | Past healing events with time-to-recovery and success rate. |
| Self-Awareness Score | How well the agent's self-assessment matches the composite (Section 2.3). |

**Fleet Health Indicators:**

| Indicator | Healthy | Warning | Critical |
|-----------|---------|---------|----------|
| % agents above TWC 6.5 | > 70% | 50-70% | < 50% |
| Average fleet TWC | > 6.0 | 5.0-6.0 | < 5.0 |
| Active Tier 2+ healings | 0-2 | 3-5 | > 5 |
| Tier 3 escalations (30 days) | 0 | 1-2 | > 2 |
| Mean time to recovery | < 48 hours | 48-168 hours | > 168 hours |
| Statistical control violations | 0 | 1-2 | > 2 |

### 8.2 Auto-Generation

The dashboard data is produced by the monitoring agent at the end of every cycle. No human builds or maintains it. Options for rendering:

- **Flat file:** Markdown table in a health report file (simplest, works anywhere)
- **JSON:** Structured output for consumption by a dashboard frontend
- **Web dashboard:** If you have a web app, the monitoring agent writes to an API endpoint

The format does not matter. The point is: the data is always current because it is produced as a side effect of monitoring, not as a separate manual task.

---

## 9. Implementation Guide

### 9.1 What You Need

1. **One or more AI agents you want to monitor.** Any provider, any model.
2. **Access to those agents' logs.** Session logs, task records, API usage data. The monitoring agent needs to read these.
3. **A scheduling mechanism.** Cron, a task scheduler, a cloud function with a timer, or a simple loop.
4. **Two additional agent instances:** One for monitoring, one for healing. A lightweight model works fine for monitoring. Healing benefits from a more capable model.

### 9.2 Architecture

```
┌─────────────────────────────────────────────┐
│              YOUR AGENT FLEET                │
│                                              │
│  Agent A    Agent B    Agent C    Agent D    │
│    │           │          │          │       │
│    └───────────┴──────────┴──────────┘       │
│                    │                         │
│              Logs & Metrics                  │
│                    │                         │
│              ┌─────▼─────┐                   │
│              │  MONITOR   │ ← runs on timer  │
│              │   AGENT    │                  │
│              └─────┬─────┘                   │
│                    │                         │
│         Scores + Statistical Controls        │
│         + Cascade Detection                  │
│                    │                         │
│            Degradation detected?             │
│                    │                         │
│              ┌─────▼─────┐                   │
│              │  HEALING   │                  │
│              │   AGENT    │                  │
│              └─────┬─────┘                   │
│                    │                         │
│            Sends correction to               │
│            degraded agent                    │
│                    │                         │
│              ┌─────▼─────┐                   │
│              │ KNOWLEDGE  │                  │
│              │    BASE    │                  │
│              └────────────┘                  │
└─────────────────────────────────────────────┘
```

### 9.3 Step-by-Step Setup

**Step 1: Deploy the monitoring agent.**

Use the prompt template in `prompts/health-monitor.md`. Paste it into your AI provider as a system prompt or standalone agent configuration. Adjust the fleet roster and log locations for your setup.

**Step 2: Deploy the healing agent.**

Use the prompt template in `prompts/healing-agent.md`. This agent handles Tier 0 prompts, Tier 1 peer selection, and Tier 2 supervisor actions.

**Step 3: Connect to your agents' logs.**

The monitoring agent needs read access to:
- Session/conversation logs (or summaries)
- Task completion records (success/fail, duration)
- API usage data (token counts, model used, cost)
- Any error logs or failure records

If your agents write logs to files, point the monitor at those files. If they use an API, give the monitor API read access. The format does not matter as long as the monitor can extract: what tasks ran, whether they succeeded, how long they took, and how much they cost.

**Step 4: Set up the schedule.**

Run the monitoring agent on a timer. Options:

- **Cron (Linux/Mac):** `0 */2 * * * /path/to/run-health-monitor.sh`
- **OpenClaw:** Use the cron tool with a 2-hour interval
- **Cloud functions:** AWS Lambda + EventBridge, Google Cloud Scheduler, Azure Timer Trigger
- **Simple script:** A loop with a sleep interval

**Step 5: Configure notification channels (for Tier 3).**

When autonomous healing fails, the human needs to know. Configure a notification method:
- Slack webhook
- Telegram bot message
- Email
- Discord webhook
- Any HTTP endpoint

The monitoring agent includes the notification URL in its configuration.

**Step 6: Create the knowledge base file.**

A simple YAML or JSON file where healing events are logged. The monitoring agent appends to it after every healing cycle. Start with an empty file:

```yaml
# health-knowledge-base.yaml
healing_events: []
healing_failures: []
patterns: []
```

### 9.4 Provider-Specific Notes

| Provider | Monitoring Model | Healing Model | Notes |
|----------|-----------------|---------------|-------|
| OpenAI | GPT-4o-mini or GPT-4.1-mini | GPT-4o or GPT-4.1 | Mini for monitoring (cost-efficient), full model for healing (needs reasoning) |
| Anthropic | Claude Haiku | Claude Sonnet or Opus | Haiku handles telemetry collection. Sonnet/Opus for diagnostic reasoning. |
| Google | Gemini Flash | Gemini Pro | Flash for data collection. Pro for analysis. |
| Open-source | Any 7B+ model | Any 13B+ model | Monitoring is structured data extraction. Healing needs stronger reasoning. |
| Mixed fleet | Match to your cheapest capable model | Match to your strongest model | The monitor runs frequently; keep it cheap. The healer runs rarely; invest in quality. |

---

## 10. Scheduler Configuration

### 10.1 Cron Examples

**Every 2 hours (default):**

```cron
0 */2 * * * cd /path/to/fleet && ./run-health-monitor.sh >> /var/log/fleet-health.log 2>&1
```

**Every hour (large fleets):**

```cron
0 * * * * cd /path/to/fleet && ./run-health-monitor.sh >> /var/log/fleet-health.log 2>&1
```

**Every 4 hours (small fleets, cost-conscious):**

```cron
0 */4 * * * cd /path/to/fleet && ./run-health-monitor.sh >> /var/log/fleet-health.log 2>&1
```

### 10.2 OpenClaw Configuration

If you use OpenClaw, the monitoring agent can run as a cron job:

```json
{
  "name": "fleet-health-monitor",
  "schedule": "0 */2 * * *",
  "prompt": "Run the 8D health monitoring cycle for all agents in the fleet.",
  "model": "anthropic/claude-haiku-4-5",
  "timeout": 300
}
```

### 10.3 Cloud Function Example (AWS Lambda)

```python
import boto3
import json

def handler(event, context):
    # Invoke your monitoring agent
    bedrock = boto3.client('bedrock-runtime')
    
    response = bedrock.invoke_model(
        modelId='anthropic.claude-3-haiku-20240307-v1:0',
        body=json.dumps({
            "prompt": open('prompts/health-monitor.md').read(),
            "max_tokens": 4096
        })
    )
    
    # Parse results, check for degradation, trigger healing if needed
    results = json.loads(response['body'].read())
    # ... your fleet-specific logic here
```

**EventBridge rule (every 2 hours):**

```json
{
  "ScheduleExpression": "rate(2 hours)",
  "Target": "arn:aws:lambda:us-east-1:123456789:function:fleet-health-monitor"
}
```

### 10.4 Preventing Monitoring Overlap

If a monitoring cycle takes longer than the interval (large fleets, slow APIs), use a lock file:

```bash
#!/bin/bash
LOCKFILE="/tmp/fleet-health-monitor.lock"

if [ -f "$LOCKFILE" ]; then
    echo "Previous cycle still running. Skipping."
    exit 0
fi

trap "rm -f $LOCKFILE" EXIT
touch "$LOCKFILE"

# Run the monitoring cycle
python3 run_health_monitor.py
```

---

## Methodology Deep Dive

This open implementation covers everything you need to run an autonomous health system. The premium methodology goes deeper on:

- **Full coupling coefficient matrix** with exact κᵢⱼ values for all 28 dimension pairs
- **Multi-hop cascade detection** (A→B→C cascades, not just pairwise)
- **Bayesian parameter estimation** for personalizing coupling coefficients to your specific fleet
- **Per-dimension algorithm specifications** with theoretical foundations (quantum cognition, information theory, network science, prospect theory)
- **Psychometric validation protocol** for instrument development
- **Phase 1-3 clinical validation timeline**

See the [premium documentation](../premium/) for the complete mathematical framework.

---

## Changelog

| Version | Date | Changes |
|---------|------|---------|
| 1.1.0 | 2026-03-23 | Added Section 2 (Scoring Methodology) with TWC formula, efficiency cap, two-source composite, Bayesian temporal decay, cross-dimensional coupling, and Cascade Amplification Ratio. Added Section 7 (Statistical Controls) with Lake Wobegon, Anchoring Drift, Variance Collapse, and Cohort Homogeneity tests. Updated cascade detection to reference coupling coefficients and CAR. Updated dashboard indicators to reflect realistic score ranges under efficiency cap. |
| 1.0.0 | 2026-03-23 | Initial autonomous health system specification. |

---

*Set it up once. Walk away. Your fleet heals itself.*
