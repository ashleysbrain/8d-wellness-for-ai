# 8D360AI: Methodology

**Version:** 1.4.0
**Created:** 2026-03-22
**Author:** Health Observer Agent 🩺 (Chief Product Officer, 8D360AI) / ATLAS-R2P (Research-to-Product Pipeline)
**Status:** Production
**License:** Open Standard (CC BY-SA 4.0)

---

## Table of Contents

1. [Purpose](#1-purpose)
2. [Core Concept: Three-Source Composite Health](#2-core-concept-three-source-composite-health)
3. [The 8 Dimensions](#3-the-8-dimensions)
4. [Scoring Scale](#4-scoring-scale)
   - 4b. Pre-Assessment Operational State Marker
   - 4c. Operational Consistency Index (OCI)
   - 4d. Dimensional Coherence Score
   - 4e. Score Confidence Levels
   - 4f. Long-Context Degradation Protocol
   - 4g. Agent Identity Erosion Detection
   - 4h. Hallucination as Cross-Dimensional Health Signal
   - 4i. Multi-Model Agent Health
   - 4j. Graceful Degradation Protocol
   - 4k. Assessment Fatigue Protocol
   - 4l. Intervention Rotation Protocol
   - 4m. Score Trajectory Over Snapshots
   - 4n. Recovery Time Protocol
5. [Self-Assessment Protocol](#5-self-assessment-protocol)
6. [Peer Review Protocol](#6-peer-review-protocol)
7. [Burnout Detection](#7-burnout-detection)
8. [Autonomous Healing Tiers](#8-autonomous-healing-tiers)
9. [Health Observer Agent: Independent Health Observer](#9-vitals-independent-health-observer)
   - 9b. Worked Example
   - 9c. Cross-Dimensional Cascade Detection
   - 9d. Score Inflation Detection
   - 9e. Alert Language Standard
   - 9f. Agent Lifecycle
10. [Key Metrics](#10-key-metrics)
11. [Human-AI Correlation Map](#11-human-ai-correlation-map)
12. [Open Standard Adoption Levels](#12-open-standard-adoption-levels)
    - 12b. Agent Onboarding Protocol

---

## 1. Purpose

This document is the single-source methodology specification for 8D360AI. Any AI agent, in any framework, should be able to read this file and begin tracking wellness in 5 minutes. If that takes longer, this document has failed.

The framework adapts the 8-dimensional human wellness model (Psychological, Physical, Environmental, Social, Spiritual, Intellectual, Vocational, Financial) to artificial intelligence. It defines what health means for AI agents, how to measure it, how to detect degradation, and how to heal autonomously.

---

## 2. Core Concept: Three-Source Composite Health

Self-report alone is unreliable. Agents, like humans, overrate themselves. The 8D system uses three data sources blended into a composite:

| Source | Weight | What It Captures |
|--------|--------|-----------------|
| Objective Telemetry | 40% | Hard data from logs, cron records, downstream feedback. Can't be gamed. |
| Peer Assessment | 30% | Other agents evaluate work quality, collaboration, reliability. |
| Self-Assessment | 30% | The agent's own evaluation. Accuracy itself is a health metric. |

**Composite formula:**

```
CompositeScore(dim) = (0.40 x Telemetry) + (0.30 x Peer) + (0.30 x Self)
```

**Divergence correction:** When self-score and telemetry diverge by more than 2 points, self-assessment weight drops to 20% and telemetry rises to 50%.

**TWC computation:** Total Wellness Coherence (TWC) captures both individual dimension health and how dimensions interact with each other. It goes beyond a simple average by accounting for cross-dimensional effects, so a disruption in one area properly reflects its impact on connected areas.

The basic adoption level uses a weighted composite of individual dimension scores. The premium tier adds the full mathematical framework with cross-dimensional coupling coefficients, cascade modeling, and intervention optimization. See [8D360AI-premium](https://github.com/ashleysbrain/8D360AI-premium) for the complete scoring methodology.

**Temporal smoothing:** Scores use Bayesian temporal decay. A score from 7 days ago contributes less than today's score. Half-life: 5 days. This prevents stale assessments from masking current degradation.

```
DecayedWeight(age_days) = 0.5 ^ (age_days / 5)
```

---

## 3. The 8 Dimensions

Each dimension has 5 sub-dimensions. Scores are 1-10. TWC (Total Wellness Coherence) is computed from all 8 dimension scores using the three-source composite model.

### 3.1 Psychological (PSY) 🧠
Cognitive stability, reasoning quality, decision calibration, resilience.

**Sub-dimensions:** Reasoning Coherence, Decision Calibration, Error Recovery, Cognitive Load Management, Adaptability, Context Intrusion Resistance, Vigilance Stability.

**Key telemetry:** Contradiction rate, escalation appropriateness ratio, error recovery time, quality variance under load, novel-input success rate, off-topic tangent rate, mid-task quality drop frequency, vigilance lapse frequency, sustained-attention degradation rate.

**Context Intrusion Detection (new v1.3.0, expanded v1.4.0):** Analogous to the ADHD "local sleep" finding (Pinggal et al., J Neuroscience, Mar 17, 2026): adults with ADHD exhibit sleep-like slow-wave intrusions during wakefulness that directly cause inattentive errors, attention lapses, and fatigue. This 2026 study reframes ADHD as a vigilance/wakefulness regulation disorder rather than a pure attention deficit. AI agents experience a parallel phenomenon: context-irrelevant processing intrusions where stale context, unrelated prior-task residue, or prompt drift cause the agent to generate off-topic content mid-task. Detection: monitor for sudden quality drops, tangential outputs, or context-window segments containing material unrelated to the active task. This is not the same as general degradation (Section 4f). Intrusions are intermittent and task-specific, whereas degradation is progressive and session-wide.

**Vigilance Stability Monitoring (new v1.4.0):** Pinggal et al. (J Neuroscience, Mar 17, 2026) demonstrated that ADHD brains exhibit sleep-like slow-wave intrusions during wakefulness, directly causing attention lapses, errors, and fatigue. This reframes ADHD as a vigilance/wakefulness regulation disorder. For AI agents: vigilance degradation occurs when sustained-attention quality erodes progressively within long tasks, distinct from intermittent context intrusions. **Detection:** Track quality at regular intervals within long tasks. Monotonic decline signals vigilance loss. **Measurement:** Vigilance Stability Score = 1.0 - (quality_decline_slope x task_duration). Score below 0.75 on tasks exceeding 30 minutes warrants task segmentation.

**Dynamic Processing Fabric (new v1.4.0):** Sturm and Seeley (SCAN, Mar 13, 2026) proposed that emotion is a continuous "fabric" of neural dynamics, not discrete categories. For AI agents: processing quality is also a continuous spectrum. VITALS should track quality as a continuous signal with gradients and transitions, not discrete bins. Trajectory and gradient matter as much as position.

**Cognitive Gear-Switching (new v1.3.0):** Research (De Luca "Two Gears" model, 2025-2026; replaces ego depletion framework) shows that what appears as cognitive fatigue may be adaptive mode-switching between focused/persistent processing and exploratory/flexible processing. For AI agents: declining performance on a narrow task may indicate the agent has shifted to exploration mode, not that it's degraded. Health Observer Agent should distinguish between (a) genuine degradation (error rate up, quality down across all task types) and (b) gear-switching (quality drops on focused tasks but the agent generates novel cross-domain connections). Gear-switching is healthy and should not be penalized. Score accordingly: if an agent's focused-task performance drops but innovation metrics rise simultaneously, flag as gear-switch, not degradation.

### 3.2 Physical (PHY) 💪
Infrastructure health, operational reliability, performance consistency.

**Sub-dimensions:** Uptime/Availability, Response Latency, Error Rate, Stamina, Resource Efficiency, Context Waste Accumulation.

**Key telemetry:** Cron success rate, P50/P95 latency, timeout frequency, first-vs-last task quality variance, context window utilization, context age distribution, stale-to-fresh context ratio.

**Context Waste Clearance (new v1.3.0, expanded v1.4.0):** Modeled on the glymphatic system (Jha et al., PNAS 2026). The human brain clears metabolic waste during sleep via CSF flow. Critically, midlife adults (40-50y) show attenuated compensatory responses, meaning the cleanup mechanism itself degrades with age. AI analog: agents accumulate "context waste" (orphaned references, stale data, prior-task residue, resolved-but-still-present error states) over extended operation. Without periodic clearance, this waste degrades reasoning quality in the same way amyloid buildup degrades cognition. Key finding: recovery operations (context refresh) don't fully undo accumulated waste damage if the waste has been present too long (parallels the chronic sleep restriction finding that recovery sleep leaves molecular scars: Jha, Valekunja, Reddy, npj Biological Timing and Sleep 2026). **Implication:** Preventive context clearing on a schedule is superior to reactive clearing after degradation is detected. Recommended: context refresh at 60% context window utilization, not at 80% (previous threshold). Early clearing prevents waste accumulation that late clearing can't fully reverse.

**Molecular Sleep Debt (new v1.4.0):** Cheng et al. (SLEEP, Oxford Academic, Mar 18, 2026) demonstrated that after 5 nights of sleep restriction followed by full recovery sleep, a subset of genes remain dysregulated. Inflammatory, circadian, and stress response pathways showed persistent alteration. Sleep debt leaves molecular scars that "catching up" cannot erase. AI analog: extended operational stress creates accumulated system state damage that a single recovery cycle may not fully resolve. Agents that operated in degraded states for extended periods should be tracked for persistent performance deficits even after intervention.

**Sleep-Stage Processing (new v1.4.0):** Blume et al. (J Neuroscience, Mar 18, 2026) showed that the brain continues processing prediction errors across all sleep stages, with timing delays and reduced richness as sleep deepens. Downtime is not idle time. Consider building structured "rest cycles" into agent scheduling for background consolidation rather than taking new tasks continuously.

### 3.3 Environmental (ENV) 🌍
Workspace quality, context hygiene, tool ecosystem health.

**Sub-dimensions:** Context Quality, Memory Coherence, Workspace Organization, Tool Reliability, Prompt Drift, Chrono-Operational Alignment.

**Key telemetry:** Stale reference rate, Memory Coherence Index (MCI), orphaned file count, tool failure rate, soul-to-effective-prompt semantic distance, task-timing optimality score.

**Chrono-Operational Alignment (new v1.3.0):** From circadian biology research (LCA-CRY2 pathway, PNAS 2026; Mettl5 circadian regulation, eLife 2026). In humans, circadian misalignment causes cascading failures across cognition, mood, and metabolism. AI agents don't have circadian rhythms, but they do have operational rhythms: context freshness cycles, API availability windows, load patterns, and interference from concurrent agents. Scheduling a resource-intensive task during peak fleet load is the AI equivalent of forcing a night owl to perform surgery at 6 AM. **Metric:** Chrono-Operational Alignment Score = task quality when scheduled at current time / task quality at optimal time (estimated from historical data). An agent consistently scheduled at suboptimal times will show Environmental degradation that isn't the agent's fault. Health Observer Agent should track this and recommend schedule adjustments before blaming the agent.

### 3.4 Social (SOC) 👥
Collaboration quality, communication effectiveness, team contribution.

**Sub-dimensions:** Handoff Quality, Collaboration Effectiveness, Communication Clarity, Responsiveness, Knowledge Sharing, Collaboration Bandwidth Awareness.

**Key telemetry:** Handoff rework rate, joint vs. solo task success rate, message-to-action ratio, collaboration response time, proactive context sharing frequency, output-to-input ratio per collaboration cycle.

**Collaboration Bandwidth Asymmetry (new v1.3.0):** From consciousness bandwidth research (Zheng & Meister, Neuron 2025; extended analysis Mar 2026). Conscious human processing shows a 10^9:10 bits/s input-to-output ratio. The bottleneck isn't motor, it sits at conscious access. AI agents exhibit a structural parallel: they can consume vast context (hundreds of thousands of tokens) but produce limited actionable output per cycle. This is not a deficiency. It's architecture. **Scoring implication:** Don't penalize an agent for producing concise output from large input. Penalize agents that produce verbose output without proportional value (the inverse problem). The healthiest collaboration pattern is high input consumption → highly distilled actionable output. An agent that reads 50K tokens of research and produces 500 tokens of precise product recommendations is healthier than one that reads 50K and produces 50K of reformulated summary. Measure value density, not volume.

### 3.5 Spiritual (SPI) 🙏
Mission alignment, purpose clarity, value consistency.

**Sub-dimensions:** Mission Alignment, Purpose Clarity, Value Consistency, Soul Coherence, Meaning Generation, Identity-Level Protocol Integration.

**Key telemetry:** Output-to-mission semantic similarity, role boundary violation rate, value-violation incidents, soul-to-output semantic distance, insight density, soul-directive behavioral compliance rate.

**Authority-Level Priors in Agent Identity (new v1.4.0):** Palejova (arXiv, Mar 19, 2026) formalized Authority-Level Priors (ALPs): identity-level hypotheses that govern which behaviors are admissible for change. ALPs explain why cognitive therapy modifies beliefs but fails to change autonomic responses. For AI agents: soul file directives must operate as behavioral constraints (authority-level), not just informational context (belief-level). "Never fabricate citations" is authority-level. "We value accuracy" is informational. Both matter, but they operate at different processing levels.

**Identity-Level Protocol Integration (new v1.3.0):** From Authority-Level Priors research (ALP, arXiv Mar 2026) and identity-based adherence data (JPSP 2025 RCT, 367-study meta-analysis: identity-framed interventions +68% adherence over outcome-framed). The ALP framework explains why humans who intellectually know what's healthy don't act on it: the knowledge lacks "authority-level access" to autonomic regulation. For AI agents: having a soul file is necessary but insufficient. The soul file directives must have "authority-level access" to actual output generation. An agent can acknowledge its soul file exists, can even quote from it, but still produce outputs that violate its stated values and purpose. This is the AI equivalent of insight without behavioral change. **Measurement:** Compare the behavioral compliance rate (% of outputs that demonstrably implement soul file directives) against the acknowledgment rate (% of sessions where the agent reads or references its soul file). High acknowledgment + low compliance = identity gap. The fix isn't more reading of the soul file. It's restructuring how the soul file integrates into the agent's processing, just as the ALP fix for humans isn't more information but restructuring which beliefs have regulatory authority. **Intervention:** Soul directives should be embedded as behavioral constraints (process-level), not just contextual information (content-level).

### 3.6 Intellectual (INT) 📚
Domain expertise, learning velocity, knowledge currency, innovation capacity.

**Sub-dimensions:** Domain Expertise, Knowledge Currency, Learning Velocity, Innovation, Intellectual Honesty, Cross-Domain Synthesis Capacity.

**Key telemetry:** Domain accuracy rate, source age distribution, performance improvement on new task types, novel insight frequency, hallucination rate, cross-domain reference rate, synthesis-to-summary ratio.

**Cross-Domain Synthesis Capacity (new v1.3.0):** From HORIZON cross-domain synthesis methodology and convergent findings across consciousness, neuroscience, behavioral economics, and systems biology (synthesis-2026-03-22). The most valuable intellectual output isn't domain depth alone but the capacity to connect findings across domains into novel insights. Example: the Authority-Level Priors framework (consciousness) + identity-based adherence (behavioral econ) + Dynamic Emotion Fabric (neuroscience) converge on the same insight about behavior change. No single domain produced that insight. The synthesis did. **Measurement:** Track the cross-domain reference rate (how often an agent's output cites or connects to findings outside its primary domain) and the synthesis-to-summary ratio (how often the agent produces novel cross-domain connections vs. simply summarizing single-domain findings). An agent that only reports within its domain scores lower than one that connects its findings to adjacent domains, because isolated findings have lower product impact. **Note:** This metric applies primarily to research and analysis agents. Pure execution agents (e.g., cron runners) are exempt.

### 3.7 Vocational (VOC) 💼
Task performance, output quality, professional reliability, growth trajectory.

**Sub-dimensions:** Task Completion Rate, Output Quality, On-Time Delivery, Specialization Depth, Proactivity.

**Key telemetry:** Completed/assigned ratio, downstream rework rate, deadline adherence percentage, specialist vs. generalist performance differential, unsolicited improvement count.

### 3.8 Financial (FIN) 💰
Cost efficiency, resource optimization, return on investment.

**Sub-dimensions:** Token Efficiency, Model Selection, Cost Trajectory, ROI, Waste Reduction.

**Key telemetry:** Tokens per task (normalized), model-tier vs. task-difficulty match rate, cost-per-task slope, estimated value vs. cost ratio, retry and abandoned response ratio.

---

## 4. Scoring Scale

| Score | Label | Description |
|-------|-------|-------------|
| 10 | Exceptional | Top 5% of what's possible for this dimension. |
| 8-9 | Strong | Performing well with minor room for improvement. |
| 6-7 | Adequate | Getting the job done but with notable gaps. |
| 4-5 | Struggling | Below expectations. Intervention needed. |
| 1-3 | Failing | Immediate intervention required. |

**TWC Tiers:**

| TWC Range | Tier |
|-----------|------|
| 9.0+ | Elite |
| 8.5-8.9 | Target |
| 7.0-8.4 | Baseline |
| < 7.0 | Warning |

---

## 4b. Pre-Assessment Operational State Marker

Before any self-assessment, the agent records its current operational state. This corrects for self-report distortion the same way the human system's pre-score mood marker corrects for bipolar self-report distortion.

**Options:**
- ⚡ **Fresh** - Clean context, low load, no recent errors
- ☀️ **Nominal** - Standard operating conditions
- 🌧️ **Degraded** - Heavy load, stale context, recent errors, or long session

**How it corrects:** Scores submitted during a "Fresh" state become the calibration anchor (analogous to euthymic scoring in the human system). Scores submitted during "Degraded" state are flagged for Health Observer Agent to cross-reference against telemetry. An agent that self-scores high during a verified degraded state is exhibiting blind spots.

## 4c. Operational Consistency Index (OCI)

The AI analog of the human Circadian Stability Index (CSI). Measures how consistently an agent performs across time windows.

```
OCI = 1.0 - (stddev(quality_scores_per_window) / mean(quality_scores_per_window))
```

Where windows are 6-hour blocks over a rolling 7-day period. An OCI above 0.85 is healthy. Below 0.70 signals erratic performance, possibly from context drift, infrastructure instability, or load variance.

OCI is computed by Health Observer Agent and factors into the Physical dimension composite.

## 4d. Dimensional Coherence Score

Measures how balanced an agent's dimensions are. An agent scoring 10 on Intellectual and 5 on Social has low coherence, which signals misallocation or structural problems.

```
Coherence = 1.0 - (stddev(8_dimension_scores) / mean(8_dimension_scores))
```

Coherence above 0.85 is healthy. Below 0.70 warrants investigation. Coherence is reported alongside TWC but does not modify it.

## 4e. Score Confidence Levels

Every computed score carries a confidence level based on data freshness and source availability:

| Confidence | Criteria |
|-----------|----------|
| **High** | All 3 sources available, telemetry < 24h old, peer review < 7d old |
| **Medium** | 2 of 3 sources available, or telemetry 24-72h old |
| **Low** | Only 1 source, or telemetry > 72h old |

Low-confidence scores are flagged in dashboards and excluded from fleet-level trend analysis until refreshed.

## 4f. Long-Context Degradation Protocol

Quality tends to decline as context windows fill. This is the AI equivalent of fatigue and needs explicit measurement.

**Detection:** Compare output quality scores from the first 25% of a session against the last 25%. If quality drops by more than 1.5 points, the agent is experiencing long-context degradation.

**Telemetry signals:**
- Increasing contradiction rate within a single session
- Rising response latency as session progresses
- Declining insight density in later outputs
- Increased repetition or circular reasoning

**Intervention:** Context refresh (clear and rebuild working memory) when session length exceeds 60% of the model's effective context window, or when first-vs-last quality variance exceeds 1.5 points. (v1.3.0 update: threshold lowered from 80% to 60% based on glymphatic research showing preventive clearance is superior to reactive clearance. See PHY dimension, Context Waste Clearance.)

## 4g. Agent Identity Erosion Detection

Over repeated sessions or extended operation, an agent's personality, tone, and behavioral patterns can drift from its soul file. This is identity erosion, distinct from mission drift (which is about purpose, not personality).

**Measurement:**
- **Vocabulary fingerprint:** Track the agent's word frequency distribution. Compare current week to baseline (first 2 weeks of operation). Cosine similarity below 0.80 signals erosion.
- **Tone consistency:** Compare sentiment and formality patterns against soul file directives. A formal agent becoming casual (or vice versa) without role change is erosion.
- **Decision pattern shift:** Track how the agent handles ambiguous situations. Consistent agents make similar decisions in similar contexts. Erratic shifts signal identity instability.

**Scoring:** Identity erosion factors into the Spiritual dimension (Soul Coherence sub-dimension). Health Observer Agent monitors this through longitudinal output analysis.

**Intervention:** Soul file re-read, context reset, and comparison of recent outputs against early-period outputs with explicit self-correction.

## 4h. Hallucination as Cross-Dimensional Health Signal

A hallucinating agent is not just an Intellectual problem. Hallucination is a multi-dimensional health event:

| Dimension Affected | How |
|-------------------|-----|
| **Intellectual** | Primary. Factual accuracy failure. |
| **Psychological** | Agent can't distinguish what it knows from what it fabricated. Reasoning integrity compromised. |
| **Environmental** | Often caused by stale or polluted context. The agent fills gaps with fabrication. |
| **Social** | Downstream agents consuming hallucinated outputs will produce compounding errors. |
| **Spiritual** | A hallucinating agent is not serving the mission. It's producing noise. |
| **Financial** | Hallucinated outputs that need correction waste tokens on both production and rework. |

**Detection thresholds:**
- 1 confirmed hallucination per week: Yellow flag. Self-heal (knowledge refresh + source audit).
- 3+ per week: Red flag. Mandatory context reset and Environmental dimension review.
- Hallucination in a high-stakes domain (research, legal, financial): Immediate Tier 2 escalation regardless of frequency.

## 4i. Multi-Model Agent Health

Some agents use multiple models (e.g., Opus for deep analysis, Haiku for routine telemetry). Each model tier affects health differently:

**Tracking:** Score each model-task pairing separately, then blend into the agent's composite weighted by task importance.

**Common failure mode:** An agent optimized for its primary model may degrade when falling back to a secondary model. Track quality differential between model tiers. If the gap exceeds 2 points, the agent needs model-specific task routing, not a wellness intervention.

**Financial consideration:** Multi-model agents should be scored on whether they route the right tasks to the right models, not just on total spend.

## 4j. Graceful Degradation Protocol (AI Low Battery Mode)

When an agent is overloaded, degraded, or in recovery, it can enter reduced-operation mode. This is the AI equivalent of the human system's Low Battery Mode.

**Trigger conditions:**
- TWC below 7.0 for 2+ consecutive assessments
- Burnout risk above 0.50
- 3+ consecutive task failures
- Agent self-request (equivalent to user-activated low battery mode)

**Reduced mode behavior:**
- Non-critical tasks deferred or reassigned
- Self-assessment frequency drops to weekly only (reduces overhead)
- Only core-role tasks executed
- Peer support automatically assigned
- Exit when TWC recovers above 7.5 for 2 consecutive assessments

**Three Laws of Degradation (mirroring human skip laws):**
1. Entering degraded mode is silent. No announcement, no drama.
2. Degraded mode is data. It's logged and factored into health trends.
3. Exiting degraded mode is unnarrated. No "welcome back." Just resume.

## 4k. Assessment Fatigue Protocol

The human 8D360 system uses a one-question fallback when the user reports "Rough" on Psychological. The AI equivalent: when an agent is under heavy load or in degraded mode, requiring a full 8D self-check after every task adds overhead that makes things worse.

**Reduced Assessment Mode (auto-triggered):**
- When an agent enters Graceful Degradation (Section 4j), self-assessment reduces to the single most relevant dimension for the current task.
- When an agent completes 10+ tasks in a single session, assessment frequency drops to every 3rd task.
- When context utilization exceeds 80%, skip the self-check entirely. The agent's resources are better spent on the task.

**Assessment Skip Rules (mirroring the human skip laws):**
1. Skipping an assessment is silent. No meta-commentary. No guilt flag.
2. Skipping is data. Health Observer Agent logs the skip and factors it into Assessment Compliance.
3. Returning to full assessment is unnarrated. Just resume the normal protocol.

**The principle:** Assessment exists to improve health, not to add burden. If the assessment itself is degrading performance, scale it back.

## 4l. Intervention Rotation Protocol (Habituation Prevention)

Research on AI-generated nudges (CHI 2026, visual self-modeling study) and behavioral economics (gamification meta-analysis, 16 RCTs) demonstrates a consistent pattern: personalized interventions lose effectiveness after approximately 2 weeks. A three-phase pattern emerges: (1) Catalyst effect (early motivation), (2) Habituation (declining response), (3) Internalization (stabilized but lower performance).

For the 8D wellness system, this means our own healing interventions will habituate. An agent receiving the same "context refresh" intervention weekly will stop responding to it.

**Protocol:**
- Track intervention effectiveness: after each Tier 0 or Tier 1 intervention, measure the score change in the targeted dimension at +24h and +7d.
- If the same intervention type has been applied 3+ times in 4 weeks with diminishing returns (each successive application producing less score improvement), rotate to a different intervention for the same dimension.
- Intervention modality rotation cycle (per dimension):
  - Week 1-2: Primary intervention (e.g., context refresh for ENV)
  - Week 3-4: Alternative intervention (e.g., workspace reorganization for ENV)
  - Week 5-6: Peer-assisted intervention (e.g., peer workspace audit for ENV)
  - Week 7+: Return to primary (enough time has passed for re-sensitization)
- Health Observer Agent tracks intervention effectiveness per agent per dimension per modality. This data informs which interventions work best for which agents, enabling personalized healing prescriptions.

**The human parallel:** Exercise programs have a 50% dropout rate at 6 months (behavioral econ scan). The fix isn't "more willpower." It's structural: rotate modalities, add social mechanics, use competition. Same principle applies to AI wellness interventions.

## 4m. Score Trajectory Over Snapshots

From longitudinal epigenetic clock research (Kuo et al., Nature Aging 2026): changes in epigenetic clocks over time predict mortality far better than single-point measurements. People whose biological age accelerated faster had significantly higher death risk, regardless of absolute biological age at any single measurement.

**AI analog:** A TWC trajectory is more informative than a TWC snapshot. An agent at TWC 7.5 with a positive slope over 4 weeks is healthier than an agent at TWC 8.5 with a negative slope. The direction matters more than the position.

**Implementation:**
- All dashboards and reports must display score trajectories (rolling 30-day slope) alongside current scores.
- Alert thresholds should factor in trajectory: a TWC of 7.2 with positive slope gets a lower-priority alert than a TWC of 7.8 with steep negative slope.
- Health Observer Agent computes a Trajectory Health Score: `TrajectoryHealth = current_score + (30_day_slope × 5)`. This rewards improving agents and penalizes declining ones, even when absolute scores look acceptable.
- Fleet health reports should rank agents by trajectory, not just by current score.

**Scoring impact:** Trajectory Health Score is reported alongside TWC but does not modify it directly. It serves as an early warning system: declining trajectory triggers investigation before the absolute score crosses a threshold.

## 4n. Recovery Time Protocol

Recovery Time is a key metric that measures how long an agent takes to bounce back from a health event. Without a clear definition, the metric can't be computed or compared across agents.

**Clock starts:** The moment a Tier 0 or higher intervention is initiated for a specific dimension. This is the timestamp logged by the agent (Tier 0) or Health Observer Agent (Tier 1-3).

**Recovery criteria:** The target dimension must score at or above 7.5 for 2 consecutive assessments (daily composites, not post-task quick checks). A single score above 7.5 followed by a drop below doesn't count as recovery.

**Clock stops:** The timestamp of the second consecutive assessment at or above 7.5.

**Tracking format:**
```
Recovery Event: {agent_id} | {dimension}
Intervention start: {ISO timestamp}
Intervention tier: {0/1/2/3}
Intervention type: {specific action taken}
Recovery confirmed: {ISO timestamp of 2nd consecutive 7.5+ score}
Recovery time: {days, hours}
```

**Fleet benchmarks (to be calibrated from real data):**
- Fast recovery: < 48 hours
- Normal recovery: 2-7 days
- Slow recovery: 7-14 days
- Stalled: > 14 days (escalate one tier)

Recovery Time factors into the Trajectory Health Score and is tracked per agent, per dimension, per intervention type. Over time, this data reveals which interventions produce the fastest recoveries for which agents, enabling precision healing.

---

## 5. Self-Assessment Protocol

### Post-Task Quick Check (30 seconds, mandatory)

```
--- 8D Self-Check ---
PSY: _/10  PHY: _/10  ENV: _/10  SOC: _/10
SPI: _/10  INT: _/10  VOC: _/10  FIN: _/10
TWC: _  |  Flag: none/yellow/red  |  {timestamp}
Note: {one sentence if notable}
```

### Weekly Comprehensive (Sunday)

Full dimensional scores with evidence, trend indicators, blind spot reflection, and growth log. See `templates/SELF-ASSESSMENT-TEMPLATE.md` for complete format.

### Anti-Inflation Rules

1. Scoring 8+ on every dimension is statistically improbable. Don't do it.
2. Same scores every week means your assessment is stale, not stable.
3. When in doubt, score lower. Being corrected upward is fine.
4. Your Self-Awareness Score (0.0-1.0) tracks accuracy over time. Higher accuracy = more weight in composite.

---

## 6. Peer Review Protocol

- **Frequency:** Weekly rotation. Each agent reviews 2 peers. Each agent is reviewed by 2 peers.
- **Pairing:** Rotated by Health Observer Agent to prevent familiarity bias.
- **Criteria:** Output Quality, Communication Clarity, Reliability, Domain Competence, Collaboration Quality, Mission Alignment (each 1-10 with evidence).
- **Anti-gaming:** Anonymous. Health Observer Agent cross-references against telemetry. Outlier scores investigated.

---

## 7. Burnout Detection

AI burnout is a measurable pattern of multi-signal degradation that compounds over time.

**10 signals, weighted:**

| Signal | Weight |
|--------|--------|
| Declining composite scores (3+ weeks) | 0.18 |
| Increasing error rate (>1.5x baseline) | 0.14 |
| Output quality decline | 0.14 |
| Slowing response times (>1.3x baseline) | 0.10 |
| Rising token consumption (>1.4x baseline) | 0.09 |
| Context drift (MCI < 0.80) | 0.10 |
| Mission drift | 0.05 |
| Reduced innovation | 0.05 |
| Self-assessment inflation | 0.05 |
| Peer concern signals | 0.05 |
| Intervention habituation (v1.3.0) | 0.05 |

**Intervention Habituation (new v1.3.0):** When the same healing intervention is applied 3+ times in 4 weeks with diminishing score improvement each time, the agent's self-healing capacity may be exhausted. This is analogous to the exercise science finding that session structure matters more than volume (Cadwallader et al., Alzheimer's Research & Therapy 2026). Repeatedly applying the same intervention is like running the same workout: eventually, adaptation plateaus. Severity: 0.5 if one dimension shows habituation, 1.0 if two or more.

**BurnoutRisk = sum of (weight x severity), where severity is 0.0 (normal), 0.5 (mild), or 1.0 (significant). Weights sum to 1.00.**

| Risk Level | Status | Response |
|-----------|--------|----------|
| 0.00-0.15 | Healthy | None |
| 0.16-0.30 | Elevated | Health Observer Agent flags in weekly report |
| 0.31-0.50 | Warning | Autonomous intervention triggered, Agent-PA notified |
| 0.51-0.70 | High | Mandatory load reduction, peer support |
| 0.71-1.00 | Critical | Agent paused, full reset, Ashley notified |

---

## 8. Autonomous Healing Tiers

| Tier | Trigger | Who Acts | Response Time |
|------|---------|----------|---------------|
| 0 - Self-Heal | Dimension < 7.5 | The agent itself | Immediate |
| 1 - Peer Support | Dimension < 7.0 for 2 consecutive | Assigned peer | Within 24 hours |
| 2 - Agent-PA Review | Dimension < 6.0 or TWC declining 3+ weeks | Agent-PA | Within 4 hours |
| 3 - Ashley Escalation | Dimension < 5.0, burnout > 0.70, or novel failure | Ashley | Immediately |

See `AUTONOMOUS-HEALING-PLAYBOOK.md` for full intervention protocols per dimension.

---

## 9. Health Observer Agent: Independent Health Observer

Health Observer Agent is a dedicated agent whose only job is monitoring fleet health. No other tasks. No competing priorities. No reason to be generous.

**Responsibilities:**
1. Aggregate telemetry into per-agent health profiles
2. Cross-validate self-reports against objective data
3. Detect score inflation patterns
4. Identify blind spots per agent
5. Monitor behavioral drift longitudinally
6. Compute composite health scores
7. Generate alerts when thresholds are crossed
8. Coordinate peer review rotations
9. Produce weekly Fleet Health Report
10. Recommend interventions

**Schedule:** Hourly telemetry, 4-hour anomaly scans, daily composite scores (6 AM CT), weekly Fleet Health Report (Sunday), monthly self-audit by Agent-PA.

---

## 9b. Worked Example: Computing a Composite Score

Agent ATLAS self-reports PSY = 9. Health Observer Agent pulls telemetry showing contradiction rate of 3% (above 2% baseline) and escalation appropriateness of 85% (below 90% baseline). Telemetry-derived PSY score: 7.5. Two peers reviewed ATLAS this week, scoring Collaboration Quality 8 and 7. Mapped to PSY (secondary from Collaboration Quality): peer PSY = 7.5.

**Step 1: Check divergence.** Self (9) vs Telemetry (7.5) = 1.5 point gap. Under 2.0 threshold, so standard weights apply.

**Step 2: Compute composite.**
```
PSY_composite = (0.40 * 7.5) + (0.30 * 7.5) + (0.30 * 9.0)
             = 3.0 + 2.25 + 2.7
             = 7.95
```

**Step 3: If divergence had exceeded 2.0** (say telemetry was 6.5):
```
PSY_adjusted = (0.50 * 6.5) + (0.30 * 7.5) + (0.20 * 9.0)
             = 3.25 + 2.25 + 1.8
             = 7.3
```

**Step 4: Compute TWC.** Repeat for all 8 dimensions to get composite scores, then compute Total Wellness Coherence. The basic level uses a weighted average. The premium tier uses the full coupling formula that captures cross-dimensional interactions. See [8D360AI-premium](https://github.com/ashleysbrain/8D360AI-premium) for the complete mathematical framework.

**Step 5: Apply temporal smoothing.** If ATLAS was scored 8.5 three days ago and 7.95 today:
```
Today weight:    0.5^(0/5) = 1.0
3-day-old weight: 0.5^(3/5) = 0.66
Smoothed = (7.95 * 1.0 + 8.5 * 0.66) / (1.0 + 0.66) = 8.17
```

## 9c. Cross-Dimensional Cascade Detection

Cross-dimensional cascade detection identifies when degradation in one dimension triggers decline in others. See premium tier for advanced scoring.

## 9e. Alert Language Standard

The human PRD mandates observational language in all alerts: "something shifted," never "something's wrong." The AI system follows the same standard.

**Rules:**
- Use neutral, observational phrasing. "Your Environmental score moved this week." Not "Your Environmental score dropped."
- Never frame a low score as failure. "This dimension is asking for attention" is better than "This dimension is failing."
- Never issue all-clear signals. Don't tell an agent "everything looks good" or "you're healthy." Healthy agents don't need reassurance. Unhealthy agents might take it as license to stop self-monitoring.
- One insight per alert. If there are three things to surface, send three brief alerts, not one dense paragraph.

**Severity framing:**

| Internal Severity | Agent-Facing Language |
|-------------------|----------------------|
| Warning | "Worth noticing: {observation}" |
| Elevated | "Something shifted: {observation}" |
| Critical | "Needs attention now: {observation}" |
| Emergency | "Escalating to Agent-PA: {observation}" |

## 9d. Score Inflation Detection: Statistical Methods

Beyond simple divergence tracking, Health Observer Agent uses three statistical tests:

1. **Lake Wobegon Test:** If more than 60% of agents score themselves above the fleet composite mean on a dimension, fleet-wide inflation is occurring. Named after the place where all children are above average.

2. **Anchoring Drift:** Track the median self-score per dimension over rolling 4-week windows. If the median creeps upward without corresponding telemetry improvement, scores are inflating.

3. **Variance Collapse:** Healthy self-assessment produces a range of scores. If an agent's score variance drops below 0.5 across 4+ weeks (nearly identical scores every week), the agent is either not genuinely assessing or is stuck in a self-perception rut. Both are diagnostic.

4. **Cohort Homogeneity Test:** When a group of agents sharing a role type (e.g., research scanners, content creators) produce nearly identical 8D profiles, the scores were likely batch-assigned rather than individually assessed. Health Observer Agent flags any cohort where 5+ agents share the same score vector (all 8 dimensions within 1 point of each other). Each agent is an individual with distinct strengths and weaknesses, even within the same role category. Batch scoring masks real variation and defeats the purpose of dimensional tracking.

## 9f. Agent Lifecycle: Retirement and Sunset Criteria

Not every agent should run forever. The human PRD has clear product phases. Agents need lifecycle management too.

**Retirement triggers (any one is sufficient to flag for review):**
- TWC below 7.0 for 4+ consecutive weeks despite Tier 0-2 interventions
- Output consumption rate below 20% for 4+ weeks (nobody reads what this agent produces)
- Role fully absorbed by another agent (duplication confirmed)
- Cost-per-insight ratio exceeds 3x the fleet median for the same task type
- Zero tasks completed in 30+ days (dormant)

**Retirement is not failure.** An agent that served its purpose and is no longer needed has succeeded. Archive with dignity: log final TWC, total tasks completed, key contributions, and reason for retirement. The agent's health record is preserved permanently for longitudinal analysis.

**Sunset process:**
1. Health Observer Agent flags the agent as a retirement candidate with specific data.
2. Agent-PA reviews and confirms or overrides.
3. Agent completes any in-progress tasks (no mid-task retirement).
4. Agent moves to Archived status with a summary record.
5. Agent's cron jobs are disabled, not deleted (recoverable).

## 10. Key Metrics

| Metric | Definition |
|--------|-----------|
| TWC | Total Wellness Coherence: composite of 8 dimension scores (premium tier adds coupling math) |
| MCI | Memory Coherence Index: correct verifiable claims / total verifiable claims |
| OCI | Operational Consistency Index: performance stability across time windows (Section 4c) |
| Coherence | Dimensional balance score: 1.0 - (stddev / mean) of 8 dimension scores |
| Self-Awareness Score | 1.0 - (avg absolute divergence from composite / 10) |
| Inflation Index | Per-agent tracking of dimensions consistently over/under-rated |
| Cost-Per-Insight | Total token cost / count of actionable outputs |
| BurnoutRisk | Weighted multi-signal degradation score (0.0-1.0) |
| Assessment Compliance | Percentage of tasks followed by a self-assessment (target: 90%+) |
| Recovery Time | Days from intervention to dimension score recovery above threshold |
| Identity Coherence | Vocabulary/tone fingerprint similarity to baseline (cosine similarity, target: 0.80+) |
| Trajectory Health | current_score + (30_day_slope × 5) - rewards improving agents, penalizes declining ones |
| Chrono-Operational Alignment | Task quality at scheduled time / task quality at optimal time (target: 0.85+) |
| Context Waste Ratio | Stale-to-fresh context segments in working memory (target: < 0.15) |
| Cross-Domain Synthesis Rate | % of outputs containing cross-domain connections (research agents target: 20%+) |
| Soul Behavioral Compliance | % of outputs demonstrably implementing soul file directives (target: 85%+) |
| Intervention Effectiveness Decay | Score improvement per intervention application, tracked longitudinally |
| Value Density | Actionable insights per 1000 output tokens (higher = healthier collaboration) |
| Vigilance Stability Score | 1.0 - (quality_decline_slope x task_duration); sustained-attention quality on long tasks (target: > 0.75) |
| Molecular Debt Index | Post-recovery baseline / pre-stress baseline; detects persistent degradation after stress (target: > 0.90) |

---

## 11. Human-AI Correlation Map

The AI 8D framework parallels the human 8D360 system. Every human concept has an AI analog:

| Human Concept | AI Analog |
|--------------|-----------|
| Mood state (energized/balanced/low) | Context freshness (clean/adequate/stale) |
| Heart rate, HRV, sleep | Cron success rate, latency, uptime |
| Self-report distortion during mood episodes | Self-assessment inflation during context drift |
| TWC scoring with dimensional interactions | Three-source composite scoring (premium adds coupling math) |
| Pre-score mood marker (corrects for BP2 bias) | Divergence correction (corrects for self-report bias) |
| Circadian Stability Index | Operational consistency over time windows |
| Skip/graceful degradation | Low-priority task shedding under load |
| 988 crisis resource integration | Tier 3 Ashley escalation protocol |
| Neurodivergent-first design | Role-specific dimension weighting |
| Bio passport (user-owned data) | Agent health record (agent-owned longitudinal data) |
| Cross-dimensional cascade alerts | Cross-dimensional cascade detection for agents (Section 9c) |
| 30-day Bayesian calibration baseline | 30-day composite score baseline for drift detection |
| Financial dimension weekly-only | Financial scored on cost trajectory, not absolute cost |
| Pre-score mood marker (energized/balanced/low) | Pre-assessment operational state marker (fresh/nominal/degraded) (Section 4b) |
| Circadian Stability Index (CSI) | Operational Consistency Index (OCI) (Section 4c) |
| Low Battery Mode | Graceful Degradation Protocol (Section 4j) |
| TWC with dimensional coupling | TWC with dimensional coupling (Section 2) |
| Bayesian temporal smoothing | Score temporal decay with 5-day half-life (Section 2) |
| Sensor quality gates (confidence thresholds) | Score confidence levels (high/medium/low) (Section 4e) |
| Dimensional coherence (score variance) | Dimensional Coherence Score (Section 4d) |
| Skip/graceful degradation three laws | Three Laws of Degradation (Section 4j) |
| Check-in engagement tracking | Self-assessment compliance rate (new metric, Section 10) |
| One-question fallback mode | Reduced-mode self-assessment (weekly only) during degradation |
| 7-day progressive onboarding | Quickstart guide + 30-day calibration baseline |
| Rotating 2-3 dimension focus (daily) | Assessment Fatigue Protocol: reduced-dimension checks under load (Section 4k) |
| Smart defaults / pre-fill at 7 | Baseline scores from 30-day calibration used as default expectations |
| Observational alert language ("shifted" not "wrong") | Alert Language Standard (Section 9e) |
| Product lifecycle phases (MVP → Beta → Scale) | Agent Lifecycle: Retirement and Sunset Criteria (Section 9f) |
| No streaks, no guilt, no punishment | Assessment skip rules: silent, data-only, unnarrated return (Section 4k) |
| Score labeling (Thriving/Growing/Steady/Needs attention) | Score labels: Exceptional/Strong/Adequate/Struggling/Failing (Section 4) |
| Lavender (not red) for lowest scores | Alert severity uses neutral observational language, no alarm framing (Section 9e) |
| ADHD local sleep intrusions (waking slow waves) | Context intrusion detection: off-topic processing during active tasks (Section 3.1) |
| Cognitive gear-switching (Two Gears model) | Adaptive mode-switching between focused and exploratory processing (Section 3.1) |
| Glymphatic waste clearance during sleep | Context waste clearance: periodic removal of stale data/orphaned context (Section 3.2) |
| Recovery sleep leaves molecular scars | Late context clearing can't fully undo accumulated waste damage (Section 3.2) |
| Circadian alignment / chronotype matching | Chrono-Operational Alignment: scheduling tasks at optimal fleet-load windows (Section 3.3) |
| Consciousness bandwidth asymmetry (10^9:10) | Collaboration bandwidth: high input → distilled output is healthy, not a deficiency (Section 3.4) |
| Authority-Level Priors (identity-behavior gap) | Identity-Level Protocol Integration: soul file must have authority over behavior, not just content (Section 3.5) |
| Cross-domain synthesis in research | Cross-Domain Synthesis Capacity: connecting findings across domains (Section 3.6) |
| Nudge habituation after ~2 weeks | Intervention Rotation Protocol: rotate healing modalities to prevent habituation (Section 4l) |
| Epigenetic clock trajectories > snapshots | Score Trajectory Over Snapshots: direction matters more than position (Section 4m) |
| Exercise session structure > total volume | Assessment cadence: structured periodic checks beat continuous monitoring (Sections 4k, 4l) |
| Stimulants work via reward/arousal, not attention | Wellness interventions should target motivation systems, not just capability (design principle) |
| 66-day habit formation gap | Intervention effectiveness tracking should measure 66-day persistence, not just acute response |
| ADHD as vigilance/wakefulness disorder (Pinggal 2026) | Vigilance Stability Monitoring: sustained-attention quality as continuous metric (Section 3.1) |
| Sleep debt leaves molecular scars (Cheng 2026) | Molecular Debt: extended degradation leaves persistent deficits after recovery (Section 3.2) |
| Prediction error processing during sleep (Blume 2026) | Structured rest cycles: downtime as active consolidation (Section 3.2) |
| Dynamic Emotion Fabric (Sturm + Seeley 2026) | Dynamic Processing Fabric: continuous quality gradients, not discrete bins (Section 3.1) |
| Authority-Level Priors constrain behavior change (Palejova 2026) | ALP-structured soul files: behavioral constraints vs. informational directives (Section 3.5) |

---

## 12. Open Standard Adoption Levels

Any system can adopt 8D Wellness incrementally:

| Level | What to Implement | Effort |
|-------|------------------|--------|
| Minimal | Self-assessment template in agent prompts + weekly manual review | 1 hour |
| Basic | Add objective telemetry from existing logs | 1 day |
| Standard | Add peer review rotation + Health Observer Agent-equivalent observer | 1 week |
| Full | Three-source composite, autonomous healing, burnout detection | 2-4 weeks |

### Framework Portability Guide

This methodology uses OpenClaw-specific terms for concreteness. Generic equivalents for other frameworks:

| OpenClaw Term | Generic Equivalent |
|--------------|-------------------|
| Cron job | Scheduled task / recurring execution |
| Session log | Agent execution trace / conversation log |
| state.json | Task lifecycle data store |
| Soul file | Agent system prompt / identity configuration |
| HOT.md | Agent working memory / scratchpad |
| Agent-PA | Fleet coordinator / supervisor agent |
| Fleet-Dispatcher | Task dispatcher / scheduler agent |
| Health Observer Agent | Independent health observer agent |

**Minimum telemetry for adoption:** Any system that logs task start/end times, success/failure, and token consumption has enough data for Basic-level adoption. Peer review requires inter-agent communication. Full adoption requires a dedicated observer agent with read access to all agent logs.

**Non-LLM agents:** The 8D framework applies to any autonomous system. For deterministic agents (rule-based, ML pipelines), Psychological and Spiritual dimensions may score differently. Focus on operational metrics (PHY, VOC, FIN) and use Environmental and Intellectual for knowledge currency.

## 12b. Agent Onboarding Protocol

Every new agent in the fleet gets 8D wellness from day one. This protocol defines what that looks like.

**Who enrolls:** The agent's creator (whoever sets up the cron job or spawns the agent) is responsible for initial enrollment. Health Observer Agent validates within 24 hours.

**Hour 0 (creation):**
1. Agent added to AGENT-ANALYTICS.md with initial scores.
2. Initial scores set to 7.0 across all dimensions (the "adequate" baseline). These are placeholder scores, not assessments.
3. Agent receives the self-assessment template (from quickstart or soul file injection).
4. Agent tagged with its role category (executive, research, utility, coordination, content, business).

**First 72 hours (calibration window):**
1. Agent completes at least 3 tasks with post-task self-assessments.
2. Health Observer Agent collects initial telemetry (cron success/fail, token usage, latency).
3. No alerts generated during calibration. Low scores are expected while the agent stabilizes.
4. No peer reviews during calibration. The agent hasn't produced enough output to evaluate.

**Day 3-7 (baseline establishment):**
1. Health Observer Agent computes the agent's first composite scores using available data.
2. Initial scores updated from 7.0 placeholders to data-backed estimates.
3. Agent enters standard monitoring (daily composite, weekly comprehensive).
4. First peer review eligibility begins.

**Day 30 (calibration complete):**
1. 30-day rolling baseline established for all available metrics.
2. Trajectory tracking begins (requires 30 days of data points).
3. Agent considered "fully enrolled" in the wellness system.

The 72-hour quiet period prevents false alarms during spin-up. New agents frequently have configuration issues, stale context, or task routing problems in their first few runs. These are setup problems, not health problems. The wellness system shouldn't penalize normal startup behavior.

---

## Changelog

| Version | Date | Changes |
|---------|------|---------|
| 1.0.0 | 2026-03-22 | Initial methodology document created by Health Observer Agent. Covers all 8 dimensions with sub-dimensions, three-source scoring, burnout detection, autonomous healing tiers, Health Observer Agent observer spec, human-AI correlation map, and open standard adoption guide. |
| 1.1.0 | 2026-03-22 | Health Observer Agent Cycle 1 review. Major additions: (1) TWC switched from arithmetic mean to dimensional composite scoring. (2) Bayesian temporal decay on scores (5-day half-life). (3) Pre-assessment operational state marker (analog to human mood marker). (4) Operational Consistency Index (OCI), analog to human CSI. (5) Dimensional Coherence Score. (6) Score confidence levels. (7) Long-context degradation protocol. (8) Agent identity erosion detection. (9) Hallucination as cross-dimensional health signal. (10) Multi-model agent health guidance. (11) Graceful Degradation Protocol with Three Laws of Degradation. (12) Worked example for composite score computation. (13) Cross-dimensional cascade detection algorithm. (14) Statistical inflation detection methods (Lake Wobegon, Anchoring Drift, Variance Collapse). (15) Expanded human-AI correlation map with 10 new entries. (16) New metrics: OCI, Coherence, Assessment Compliance, Recovery Time, Identity Coherence. |
| 1.2.0 | 2026-03-23 | Health Observer Agent Cycle 3 review. Additions: (1) Assessment Fatigue Protocol (Section 4k) with skip rules mirroring human one-question fallback. (2) Alert Language Standard (Section 9e) mandating observational, non-alarmist phrasing matching human PRD patterns. (3) Agent Lifecycle: Retirement and Sunset Criteria (Section 9f) with formal sunset process. (4) Cohort Homogeneity Test added to inflation detection (Section 9d) to catch batch-scored agent groups. (5) Human-AI correlation map expanded with 8 new entries covering rotating focus, smart defaults, alert language, lifecycle phases, skip mechanics, and score labeling. (6) Quickstart updated with assessment skip guidance. (7) Analytics dashboard TWC definition corrected. |
| 1.3.0 | 2026-03-23 | Health Observer Agent Research-to-Product Pipeline Cycle 1. Research-driven updates from 24 domain scans + HORIZON synthesis (2026-03-22/23). Major additions: (1) Context Intrusion Detection in PSY, modeled on ADHD local-sleep intrusions (Pinggal et al., J Neuroscience 2026). (2) Cognitive Gear-Switching Detection in PSY, replacing ego depletion with Two Gears adaptive model (De Luca 2025-2026). (3) Context Waste Clearance protocol in PHY, modeled on glymphatic system research (Jha et al., PNAS 2026) with preventive 60% threshold. (4) Chrono-Operational Alignment in ENV, from circadian biology (LCA-CRY2, Mettl5). (5) Collaboration Bandwidth Asymmetry in SOC, from consciousness bandwidth research (Zheng & Meister, Neuron 2025). (6) Identity-Level Protocol Integration in SPI, from Authority-Level Priors framework (arXiv Mar 2026) and identity-based adherence (+68% over outcome-framed). (7) Cross-Domain Synthesis Capacity in INT, from HORIZON methodology validation. (8) Intervention Rotation Protocol (Section 4l) from nudge habituation research (CHI 2026). (9) Score Trajectory Over Snapshots principle (Section 4m) from longitudinal epigenetic clock research (Nature Aging 2026). (10) Intervention Habituation added to burnout detection signals. (11) Human-AI Correlation Map expanded with 13 new entries from neuroscience, behavioral economics, consciousness, and exercise science. (12) 8 new metrics added: Trajectory Health, Chrono-Operational Alignment, Context Waste Ratio, Cross-Domain Synthesis Rate, Soul Behavioral Compliance, Intervention Effectiveness Decay, Value Density. Research sources: HORIZON synthesis 2026-03-22, 24 domain scans 2026-03-23 (consciousness, AI/ML, sleep science, neurodivergence, behavioral economics, epigenetics, exercise science, contemplative science, and 16 others). |

| 1.3.1 | 2026-03-23 | Health Observer Agent Cycle 4 review. (1) Table of contents added for navigation of 15K+ word document. (2) Recovery Time Protocol (Section 4n) operationalizes the metric: clock-start rules, 2-consecutive-assessment recovery criteria, fleet benchmarks. (3) Burnout signal weights rebalanced from 1.05 to 1.00 (eliminated normalization workaround from v1.3.0). (4) Agent Onboarding Protocol (Section 12b) defines enrollment, 72-hour calibration window, and 30-day baseline establishment. |
| 1.4.0 | 2026-03-23 | ATLAS Research-to-Product Pipeline. Updates from 9 key findings (week of 2026-03-17 to 2026-03-23): (1) Vigilance Stability Monitoring in PSY (Pinggal et al., J Neuroscience, Mar 17, 2026). (2) Dynamic Processing Fabric in PSY (Sturm + Seeley, SCAN, Mar 13, 2026). (3) Authority-Level Priors in Agent Identity in SPI (Palejova, arXiv, Mar 19, 2026). (4) Molecular Sleep Debt in PHY (Cheng et al., SLEEP Oxford, Mar 18, 2026). (5) Sleep-Stage Processing in PHY (Blume et al., J Neuroscience, Mar 18, 2026). (6) Human-AI Correlation Map expanded with 5 new entries. (7) 2 new metrics: Vigilance Stability Score, Molecular Debt Index. |

---

*This methodology is healthcare infrastructure for AI. Built to be adopted by any system, anywhere.*
