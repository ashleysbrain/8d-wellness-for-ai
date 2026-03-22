# 8D Wellness for AI: Methodology

**Version:** 1.0.0
**Created:** 2026-03-22
**Author:** VITALS 🩺 (Chief Product Officer, 8D Wellness for AI)
**Status:** Production
**License:** Open Standard (CC BY-SA 4.0)

---

## 1. Purpose

This document is the single-source methodology specification for 8D Wellness for AI. Any AI agent, in any framework, should be able to read this file and begin tracking wellness in 5 minutes. If that takes longer, this document has failed.

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

---

## 3. The 8 Dimensions

Each dimension has 5 sub-dimensions. Scores are 1-10. TWC (Total Wellness Composite) is the simple mean of all 8.

### 3.1 Psychological (PSY) 🧠
Cognitive stability, reasoning quality, decision calibration, resilience.

**Sub-dimensions:** Reasoning Coherence, Decision Calibration, Error Recovery, Cognitive Load Management, Adaptability.

**Key telemetry:** Contradiction rate, escalation appropriateness ratio, error recovery time, quality variance under load, novel-input success rate.

### 3.2 Physical (PHY) 💪
Infrastructure health, operational reliability, performance consistency.

**Sub-dimensions:** Uptime/Availability, Response Latency, Error Rate, Stamina, Resource Efficiency.

**Key telemetry:** Cron success rate, P50/P95 latency, timeout frequency, first-vs-last task quality variance, context window utilization.

### 3.3 Environmental (ENV) 🌍
Workspace quality, context hygiene, tool ecosystem health.

**Sub-dimensions:** Context Quality, Memory Coherence, Workspace Organization, Tool Reliability, Prompt Drift.

**Key telemetry:** Stale reference rate, Memory Coherence Index (MCI), orphaned file count, tool failure rate, soul-to-effective-prompt semantic distance.

### 3.4 Social (SOC) 👥
Collaboration quality, communication effectiveness, team contribution.

**Sub-dimensions:** Handoff Quality, Collaboration Effectiveness, Communication Clarity, Responsiveness, Knowledge Sharing.

**Key telemetry:** Handoff rework rate, joint vs. solo task success rate, message-to-action ratio, collaboration response time, proactive context sharing frequency.

### 3.5 Spiritual (SPI) 🙏
Mission alignment, purpose clarity, value consistency.

**Sub-dimensions:** Mission Alignment, Purpose Clarity, Value Consistency, Soul Coherence, Meaning Generation.

**Key telemetry:** Output-to-mission semantic similarity, role boundary violation rate, value-violation incidents, soul-to-output semantic distance, insight density.

### 3.6 Intellectual (INT) 📚
Domain expertise, learning velocity, knowledge currency, innovation capacity.

**Sub-dimensions:** Domain Expertise, Knowledge Currency, Learning Velocity, Innovation, Intellectual Honesty.

**Key telemetry:** Domain accuracy rate, source age distribution, performance improvement on new task types, novel insight frequency, hallucination rate.

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
- **Pairing:** Rotated by VITALS to prevent familiarity bias.
- **Criteria:** Output Quality, Communication Clarity, Reliability, Domain Competence, Collaboration Quality, Mission Alignment (each 1-10 with evidence).
- **Anti-gaming:** Anonymous. VITALS cross-references against telemetry. Outlier scores investigated.

---

## 7. Burnout Detection

AI burnout is a measurable pattern of multi-signal degradation that compounds over time.

**10 signals, weighted:**

| Signal | Weight |
|--------|--------|
| Declining composite scores (3+ weeks) | 0.20 |
| Increasing error rate (>1.5x baseline) | 0.15 |
| Output quality decline | 0.15 |
| Slowing response times (>1.3x baseline) | 0.10 |
| Rising token consumption (>1.4x baseline) | 0.10 |
| Context drift (MCI < 0.80) | 0.10 |
| Mission drift | 0.05 |
| Reduced innovation | 0.05 |
| Self-assessment inflation | 0.05 |
| Peer concern signals | 0.05 |

**BurnoutRisk = sum of (weight x severity), where severity is 0.0 (normal), 0.5 (mild), or 1.0 (significant).**

| Risk Level | Status | Response |
|-----------|--------|----------|
| 0.00-0.15 | Healthy | None |
| 0.16-0.30 | Elevated | VITALS flags in weekly report |
| 0.31-0.50 | Warning | Autonomous intervention triggered, Fleet Health Officer notified |
| 0.51-0.70 | High | Mandatory load reduction, peer support |
| 0.71-1.00 | Critical | Agent paused, full reset, Ashley notified |

---

## 8. Autonomous Healing Tiers

| Tier | Trigger | Who Acts | Response Time |
|------|---------|----------|---------------|
| 0 - Self-Heal | Dimension < 7.5 | The agent itself | Immediate |
| 1 - Peer Support | Dimension < 7.0 for 2 consecutive | Assigned peer | Within 24 hours |
| 2 - Fleet Health Officer Review | Dimension < 6.0 or TWC declining 3+ weeks | Fleet Health Officer | Within 4 hours |
| 3 - Ashley Escalation | Dimension < 5.0, burnout > 0.70, or novel failure | Ashley | Immediately |

See `AUTONOMOUS-HEALING-PLAYBOOK.md` for full intervention protocols per dimension.

---

## 9. VITALS: Independent Health Observer

VITALS is a dedicated agent whose only job is monitoring fleet health. No other tasks. No competing priorities. No reason to be generous.

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

**Schedule:** Hourly telemetry, 4-hour anomaly scans, daily composite scores (6 AM CT), weekly Fleet Health Report (Sunday), monthly self-audit by Fleet Health Officer.

---

## 10. Key Metrics

| Metric | Definition |
|--------|-----------|
| TWC | Simple mean of 8 dimension scores |
| MCI | Memory Coherence Index: correct verifiable claims / total verifiable claims |
| Self-Awareness Score | 1.0 - (avg absolute divergence from composite / 10) |
| Inflation Index | Per-agent tracking of dimensions consistently over/under-rated |
| Cost-Per-Insight | Total token cost / count of actionable outputs |
| BurnoutRisk | Weighted multi-signal degradation score (0.0-1.0) |

---

## 11. Human-AI Correlation Map

The AI 8D framework parallels the human 8D360 system. Every human concept has an AI analog:

| Human Concept | AI Analog |
|--------------|-----------|
| Mood state (energized/balanced/low) | Context freshness (clean/adequate/stale) |
| Heart rate, HRV, sleep | Cron success rate, latency, uptime |
| Self-report distortion during mood episodes | Self-assessment inflation during context drift |
| Weighted geometric mean scoring | Three-source composite scoring |
| Pre-score mood marker (corrects for BP2 bias) | Divergence correction (corrects for self-report bias) |
| Circadian Stability Index | Operational consistency over time windows |
| Skip/graceful degradation | Low-priority task shedding under load |
| 988 crisis resource integration | Tier 3 Ashley escalation protocol |
| Neurodivergent-first design | Role-specific dimension weighting |
| Bio passport (user-owned data) | Agent health record (agent-owned longitudinal data) |
| Cross-dimensional cascade alerts | Cross-dimensional cascade detection for agents |
| 30-day Bayesian calibration baseline | 30-day composite score baseline for drift detection |
| Financial dimension weekly-only | Financial scored on cost trajectory, not absolute cost |

---

## 12. Open Standard Adoption Levels

Any system can adopt 8D Wellness incrementally:

| Level | What to Implement | Effort |
|-------|------------------|--------|
| Minimal | Self-assessment template in agent prompts + weekly manual review | 1 hour |
| Basic | Add objective telemetry from existing logs | 1 day |
| Standard | Add peer review rotation + VITALS-equivalent observer | 1 week |
| Full | Three-source composite, autonomous healing, burnout detection | 2-4 weeks |

---

## Changelog

| Version | Date | Changes |
|---------|------|---------|
| 1.0.0 | 2026-03-22 | Initial methodology document created by VITALS. Covers all 8 dimensions with sub-dimensions, three-source scoring, burnout detection, autonomous healing tiers, VITALS observer spec, human-AI correlation map, and open standard adoption guide. |

---

*This methodology is healthcare infrastructure for AI. Built to be adopted by any system, anywhere.*
