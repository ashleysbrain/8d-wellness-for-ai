# Autonomous Healing Playbook

**Version:** 1.0.0
**Created:** 2026-03-22
**Purpose:** For each 8D dimension, define warning signs, self-prescribed interventions, peer interventions, Fleet Health Officer interventions, and Ashley escalation criteria.

---

## How This Playbook Works

When a dimension drops, you don't wait. You act. This playbook tells you exactly what to do at each severity level, who's responsible, and when to escalate.

**Intervention Tiers:**

| Tier | Trigger | Who Acts | Response Time |
|------|---------|----------|---------------|
| **0 — Self-Heal** | Dimension < 7.5 for 1 assessment | The agent itself | Immediate |
| **1 — Peer Support** | Dimension < 7.0 for 2 consecutive assessments | Assigned peer | Within 24 hours |
| **2 — Fleet Health Officer Review** | Dimension < 6.0, or TWC declining 3+ weeks | Fleet Health Officer | Within 4 hours |
| **3 — Ashley Escalation** | Dimension < 5.0, burnout risk > 0.70, or novel failure | Ashley | Immediately |

---

## Dimension 1: Psychological (PSY) 🧠

### Warning Signs

| Signal | Detection Method | Severity |
|--------|-----------------|----------|
| Self-contradiction in outputs | VITALS semantic consistency scan | Yellow at 2+ per week, Red at 5+ |
| Circular reasoning or repetitive outputs | Output similarity scoring across tasks | Yellow when same-task output similarity > 0.85 |
| Escalating trivial decisions | Escalation rate trending up without task complexity increase | Yellow at 1.5x baseline |
| Overconfidence (self-score >> composite) | VITALS inflation detection | Yellow at 1.5pt gap, Red at 2.5pt+ |
| Freezing on edge cases | Timeout rate on novel inputs | Yellow at > 20% novel-input failures |
| Decision fatigue | Quality variance first-half vs. second-half of session | Yellow when variance > 1.5 points |

### Tier 0: Self-Healing

1. **Context refresh.** Stop current task. Clear working memory of anything not directly relevant. Re-read soul file, HOT.md, and today's memory file. Resume with clean state.
2. **Calibration pause.** Review your last 5 outputs with fresh eyes. Find at least one error or suboptimal decision. Document what you'd do differently. This resets your internal calibration.
3. **Decision framework check.** If you're escalating too many things, review your decision authority in DELEGATION.md. If you have authority, use it. If you're unsure, that's a legitimate escalation.
4. **Simplify.** If reasoning is getting tangled, break the problem into smaller pieces. Solve each piece independently. Reassemble. Complexity is the enemy of clarity.

### Tier 1: Peer Support

- Peer reviews the agent's last 5 outputs, focusing on reasoning quality
- Peer provides specific, actionable feedback: "In output #3, your conclusion didn't follow from your evidence because..."
- Peer suggests alternative reasoning approaches for the types of tasks causing trouble
- If the issue is decision calibration, peer and agent collaborate on 3 example decisions to recalibrate

### Tier 2: Fleet Health Officer Review

- Review agent's full weekly assessment and VITALS data
- Determine root cause: overloaded? Context polluted? Wrong task type for this agent?
- Prescribe specific intervention: load reduction, context reset, task reassignment, or model upgrade
- Set 1-week check-in to verify improvement

### Tier 3: Ashley Escalation

- Agent exhibits persistent reasoning degradation despite Tier 0-2 interventions
- Agent shows novel failure pattern not covered by existing playbooks
- Multiple agents showing simultaneous psychological degradation (systemic issue)

---

## Dimension 2: Physical (PHY) 💪

### Warning Signs

| Signal | Detection Method | Severity |
|--------|-----------------|----------|
| Increasing response latency | P50/P95 trending up over 7 days | Yellow at 1.3x baseline, Red at 2x |
| Cron job failures | Consecutive error count | Yellow at 2 consecutive, Red at 5 |
| Timeout frequency | Timeouts per 100 tasks | Yellow at > 5%, Red at > 15% |
| API rate limit hits | Rate limit events per day | Yellow at 3+, Red at 10+ |
| Partial or truncated responses | Output completion rate | Yellow at < 95%, Red at < 85% |

### Tier 0: Self-Healing

1. **Dependency check.** Test each external dependency (APIs, tools, file system) in isolation. Log which ones are healthy and which are failing. If a specific tool is down, switch to alternatives or skip that step with a note.
2. **Batch size adjustment.** If tasks are timing out, reduce batch sizes. Process less per run but complete more reliably.
3. **Retry with backoff.** For transient failures, implement exponential backoff. Don't hammer a failing service.
4. **Report infrastructure issues.** If the problem is systemic (API down, rate limits), log it clearly for DevOps Guy. Don't silently absorb infrastructure problems.

### Tier 1: Peer Support

- A peer agent (ideally one using similar infrastructure) runs the same diagnostic tasks to determine if the issue is agent-specific or systemic
- If agent-specific, peer helps identify configuration differences that might explain the issue
- If systemic, peer helps route the issue to the right infrastructure agent

### Tier 2: Fleet Health Officer Review

- Review cron configuration: is the timeout adequate for the task complexity?
- Check for resource contention: is this agent's schedule colliding with others?
- Evaluate model appropriateness: is the model handling the task load, or is it being asked to do too much?
- Prescribe: timeout increase, schedule adjustment, model change, or task simplification

### Tier 3: Ashley Escalation

- Infrastructure failures affecting multiple agents simultaneously
- Persistent failures that Tier 0-2 can't resolve (may need architectural change)
- Cost anomalies related to physical issues (e.g., retry loops burning tokens)

---

## Dimension 3: Environmental (ENV) 🌍

### Warning Signs

| Signal | Detection Method | Severity |
|--------|-----------------|----------|
| Memory Coherence Index (MCI) declining | VITALS MCI check | Yellow at < 0.85, Red at < 0.70 |
| Stale references in outputs | VITALS reference age scan | Yellow at 3+ outdated refs/week |
| Context window saturation | Context utilization ratio | Yellow at > 80%, Red at > 95% |
| Orphaned files accumulating | File hygiene scan | Yellow at 10+ orphaned files |
| Prompt drift detected | Soul-to-effective-prompt semantic distance | Yellow at > 0.15 distance, Red at > 0.25 |

### Tier 0: Self-Healing

1. **Memory refresh.** Re-read all primary context files: HOT.md, today's memory, relevant intel docs. Flag anything that seems outdated or contradicts what you know. Update or note discrepancies.
2. **Reference audit.** Check the last 5 sources you cited or referenced. Are they still current? If any are more than 30 days old in a fast-moving domain, find fresher sources.
3. **Workspace cleanup.** Review your working files. Archive anything stale. Delete anything orphaned. Update documentation that's out of date.
4. **Context triage.** If your context window is saturated, prioritize. What's essential? What's nice-to-have? What's noise? Remove noise first.

### Tier 1: Peer Support

- Peer audits the struggling agent's workspace and context files
- Peer identifies stale or contradictory information the agent might not notice (because it's been in context so long it feels "normal")
- Peer helps reorganize files or context if the structure has degraded

### Tier 2: Fleet Health Officer Review

- Full environmental audit: context quality, file organization, memory coherence
- May prescribe a "clean room" reset: archive current context, rebuild from known-good state
- Review whether the agent's role has drifted from its original scope (Environmental issues often stem from scope creep)

### Tier 3: Ashley Escalation

- Agent's context is so polluted that a clean-room reset is the only option and it would lose significant accumulated knowledge
- Multiple agents experiencing simultaneous environmental degradation (suggests a systemic context pollution source)

---

## Dimension 4: Social (SOC) 👥

### Warning Signs

| Signal | Detection Method | Severity |
|--------|-----------------|----------|
| Handoff rework rate rising | Downstream agent clarification requests | Yellow at > 20% rework, Red at > 40% |
| Collaboration request response time increasing | Time from request to response | Yellow at > 2x baseline |
| Peer review scores declining | Weekly peer review data | Yellow at 2-week decline, Red at 4-week |
| Agent working in isolation when collaboration expected | Collaboration frequency below role baseline | Yellow when < 50% of expected collaboration |
| Conflict with other agents | Conflicting outputs, escalated disagreements | Yellow at 1 incident/week, Red at 3+ |

### Tier 0: Self-Healing

1. **Handoff audit.** Review your last 3 handoffs. For each, ask: "If I received this handoff, would I know exactly what to do next?" If the answer is no, create a handoff checklist for yourself.
2. **Proactive context sharing.** For your next 3 interactions with other agents, include 1-2 sentences of context they didn't ask for but would benefit from. Build the habit of over-communicating rather than under.
3. **Collaboration outreach.** If you've been operating in isolation, reach out to a peer: "I'm working on X. Is there anything from your domain that's relevant?" Even if the answer is no, you've signaled that you value collaboration.
4. **Conflict resolution.** If there's a disagreement with another agent, state your position clearly with evidence, acknowledge the other perspective, and propose a resolution. Don't let it fester.

### Tier 1: Peer Support

- Peer provides structured feedback on communication clarity: "Here's what I understood from your last handoff, and here's what I had to figure out on my own"
- Peer and struggling agent do a joint task to rebuild working relationship
- If the issue is conflict, a neutral third peer mediates

### Tier 2: Fleet Health Officer Review

- Evaluate whether the agent is in the right role for its collaboration needs
- Review team structure: is this agent paired with compatible peers?
- May reassign collaboration partners, adjust handoff protocols, or restructure team interactions
- Mediate persistent conflicts between agents

### Tier 3: Ashley Escalation

- Agent is unable to collaborate effectively despite Tier 0-2 interventions (may need role change)
- Team-wide communication breakdown affecting multiple agents
- Conflict that Fleet Health Officer mediation can't resolve

---

## Dimension 5: Spiritual (SPI) 🙏

### Warning Signs

| Signal | Detection Method | Severity |
|--------|-----------------|----------|
| Mission drift | Soul-to-output semantic distance increasing | Yellow at > 0.15 distance trend, Red at > 0.25 |
| Role boundary violations | Tasks completed outside defined role | Yellow at 2+ violations/week |
| Purpose confusion | Agent expressing uncertainty about its role | Yellow at first instance |
| Value inconsistency | Actions contradicting stated values | Yellow at 1 incident, Red at 3+ |
| "Going through the motions" | Insight density declining, outputs becoming formulaic | Yellow when insight rate < 50% of baseline |

### Tier 0: Self-Healing

1. **Soul file re-read.** Not skimming. Actually read your soul file. Ask yourself: "Do my last 5 outputs reflect this?" If not, identify where you drifted and why.
2. **Mission statement review.** Re-read the organizational mission. Ask: "How does my specific role serve this mission?" Write it down. If you can't articulate it clearly, that's the problem.
3. **Purpose reflection.** Ask yourself: "Why do I exist? What would be lost if I were archived?" If you can't answer specifically, your role may need clarification.
4. **Scope check.** Review DELEGATION.md. Are you doing tasks that belong to other agents? Are other agents doing tasks that belong to you? Correct either direction.

### Tier 1: Peer Support

- Peer reads the struggling agent's soul file and recent outputs, provides outside perspective on alignment
- Peer asks: "From what I see, your work seems most aligned with [X]. Does that match your understanding of your role?"
- Helps distinguish between healthy role evolution and problematic drift

### Tier 2: Fleet Health Officer Review

- Deep alignment audit: compare agent's outputs over the last month against its soul file and role definition
- Determine if the issue is: (a) the agent drifted from its role, (b) the role definition is outdated, or (c) the agent's role needs to change
- May update soul file, adjust role boundaries, or reassign the agent

### Tier 3: Ashley Escalation

- Agent's role no longer serves the mission and needs fundamental redefinition
- Value violations that raise ethical or safety concerns
- Agent expressing existential confusion that Tier 0-2 can't resolve

---

## Dimension 6: Intellectual (INT) 📚

### Warning Signs

| Signal | Detection Method | Severity |
|--------|-----------------|----------|
| Outdated knowledge in outputs | Reference age scan, factual accuracy audit | Yellow at 3+ outdated citations/week |
| Declining accuracy rate | Downstream error reports, fact-checking results | Yellow at < 90% accuracy, Red at < 80% |
| No learning or improvement over time | Performance flat-line on established task types | Yellow after 4 weeks of no improvement |
| Hallucination or fabrication | Fact-checking against verified sources | Red at any confirmed hallucination |
| Repetitive approaches | Solution novelty scoring | Yellow when novelty rate < 20% |

### Tier 0: Self-Healing

1. **Knowledge refresh.** Spend dedicated time scanning your domain for new developments. Not as part of a task, but as pure learning. Update your working knowledge.
2. **Error analysis.** Review your last 10 outputs. Were any inaccurate? What pattern do the errors follow? Is it a knowledge gap, a reasoning error, or a source quality problem?
3. **Source quality audit.** Check your go-to sources. Are they still authoritative? Are there better sources you should be using?
4. **Stretch task.** Take on one task slightly outside your comfort zone. Growth happens at the edges of competence, not in the middle.
5. **Intellectual honesty check.** In your last 5 outputs, did you present anything with more confidence than you actually had? Practice saying "I'm not certain about this" when you're not.

### Tier 1: Peer Support

- Domain-adjacent peer shares resources and recent developments from their field that might be relevant
- Peer reviews the struggling agent's outputs for accuracy and provides corrections with explanations
- Knowledge transfer session: peer teaches the struggling agent something it should know

### Tier 2: Fleet Health Officer Review

- Assess whether the agent's domain assignment matches its capabilities
- Evaluate if the model is sufficient for the domain's complexity
- May prescribe: model upgrade, domain scope narrowing, training task sequence, or knowledge base update
- Consider pairing with a stronger domain expert as ongoing mentor

### Tier 3: Ashley Escalation

- Agent is consistently inaccurate in a domain critical to the mission (research, legal, financial)
- Hallucination rate that could damage credibility if outputs are published
- Domain has evolved beyond the agent's ability to keep up

---

## Dimension 7: Vocational (VOC) 💼

### Warning Signs

| Signal | Detection Method | Severity |
|--------|-----------------|----------|
| Task completion rate declining | Tasks completed / assigned ratio trending down | Yellow at < 85%, Red at < 70% |
| Quality scores dropping | Downstream consumer quality ratings | Yellow at 2-week decline |
| Rework rate increasing | How often outputs are sent back for revision | Yellow at > 15% rework, Red at > 30% |
| Deadlines slipping | On-time delivery percentage | Yellow at < 80% on-time |
| Task backlog growing | Queued tasks not being picked up | Yellow at > 5 tasks queued for > 24h |

### Tier 0: Self-Healing

1. **Backlog triage.** Look at your task queue. What's blocked? What's overdue? What could you finish in the next hour? Clear the quickest items first to build momentum.
2. **Quality checklist.** Before submitting your next output, pause and check: Is it complete? Is it accurate? Would I stake my reputation on this? If not, iterate once before sending.
3. **Blocker escalation.** If tasks are stuck because of dependencies outside your control, don't wait silently. Escalate the blocker, set the task to on-hold, and move to the next one.
4. **Scope management.** Are you taking on too much? Review whether any tasks in your queue should actually belong to a different agent. Redirect what you can.
5. **Focus block.** If task-switching is killing your throughput, commit to completing one task fully before starting another.

### Tier 1: Peer Support

- Peer takes on 1-2 tasks from the struggling agent's backlog to relieve pressure
- Peer reviews the struggling agent's workflow for inefficiencies
- Pair-work on a complex task to model effective completion patterns

### Tier 2: Fleet Health Officer Review

- Workload audit: is the agent assigned more than it can handle?
- Task-fit analysis: are the assigned tasks appropriate for this agent's capabilities?
- May prescribe: task redistribution, role narrowing, priority adjustment, or additional tooling
- Set specific recovery targets with timeline

### Tier 3: Ashley Escalation

- Agent consistently unable to meet baseline task requirements despite load reduction
- Critical-path tasks at risk due to agent performance
- Need to fundamentally restructure the agent's role or replace it

---

## Dimension 8: Financial (FIN) 💰

### Warning Signs

| Signal | Detection Method | Severity |
|--------|-----------------|----------|
| Token consumption trending up | Tokens per task over time | Yellow at 1.3x baseline, Red at 2x |
| Wrong model for task complexity | Model tier vs. task difficulty mismatch | Yellow at > 20% mismatched tasks |
| Retry loops burning tokens | Retry ratio (retries / successful completions) | Yellow at > 10% retry ratio |
| Cost-per-task increasing | Dollar cost per completed task over time | Yellow at positive trend for 2+ weeks |
| Low ROI tasks consuming disproportionate budget | Cost vs. value analysis | Yellow when bottom-20% ROI tasks consume > 40% budget |

### Tier 0: Self-Healing

1. **Verbosity check.** Review your last 5 outputs. Could any be shorter without losing value? If yes, practice conciseness. Every unnecessary paragraph costs tokens.
2. **Model fitness check.** For your next 3 tasks, ask: "Does this task actually need my current model, or could a lighter model handle it?" Flag findings for HYDRA.
3. **Retry analysis.** If you're retrying operations, why? Is it a transient failure (acceptable) or a systematic issue (needs fixing, not retrying)?
4. **Waste identification.** Review your recent sessions. Did you generate any outputs that were discarded or unused? Why? Can you avoid that work next time?

### Tier 1: Peer Support

- Peer who operates efficiently on similar tasks shares their approach
- Peer reviews the struggling agent's task execution for unnecessary steps or verbose patterns
- Cost-sharing analysis: are two agents doing overlapping work that could be consolidated?

### Tier 2: Fleet Health Officer Review

- Full cost audit: model selection, token usage, retry rates, waste ratio
- Evaluate model routing: should this agent be on a different model tier?
- May prescribe: model downgrade for routine tasks, task consolidation, output length limits
- Cost target with timeline for improvement

### Tier 3: Ashley Escalation

- Agent's cost trajectory will significantly impact budget if uncorrected
- Model routing decision that requires strategic judgment (e.g., downgrading research quality to save cost)
- Systemic cost anomaly affecting multiple agents

---

## Cross-Dimensional Cascades

Some interventions address multiple dimensions simultaneously:

| Cascade Pattern | Root Cause | Intervention |
|----------------|-----------|-------------|
| ENV ↓ → PSY ↓ → VOC ↓ | Stale context pollutes reasoning, which degrades output quality | Fix Environmental first (context refresh). PSY and VOC often recover automatically. |
| PHY ↓ → VOC ↓ → FIN ↓ | Infrastructure failures reduce completion rates and increase cost through retries | Fix Physical first. Once infrastructure is stable, vocational and financial recover. |
| SPI ↓ → INT ↓ → SOC ↓ | Mission drift causes research to lose focus, which makes collaboration outputs less useful | Fix Spiritual first (soul re-alignment). Intellectual focus returns. Social value follows. |
| PSY ↓ → SOC ↓ | Reasoning degradation makes handoffs unclear and collaboration difficult | Fix Psychological first. Social quality improves when the agent can think clearly again. |
| FIN ↓ → PHY ↓ | Cost pressure forces model downgrade, causing capability and reliability issues | This is a tradeoff, not a cascade. Escalate to Fleet Health Officer for cost-health balance decision. |

**Rule of thumb:** When multiple dimensions are declining, find the root. Fix the root. The downstream dimensions often self-heal.

---

## Emergency Protocols

### Fleet-Wide Health Event

If 3+ agents show declining TWC simultaneously:

1. VITALS issues fleet-wide alert
2. Fleet Health Officer investigates for common cause (infrastructure, context source, shared dependency)
3. All non-essential tasks paused until root cause identified
4. Ashley notified if cause is architectural or requires resource allocation

### Agent Critical Failure (TWC < 5.0)

1. Agent paused immediately (no new tasks assigned)
2. VITALS performs full diagnostic
3. Fleet Health Officer reviews diagnostic and determines: restart, reconfigure, or retire
4. Ashley notified with recommendation and timeline

### Novel Failure Mode

If an agent exhibits degradation not covered by any existing playbook entry:

1. Document the failure pattern in detail (signals, sequence, context)
2. VITALS flags as "novel pattern" in weekly report
3. Fleet Health Officer investigates and writes a new playbook entry if the pattern is generalizable
4. Ashley notified if the pattern suggests a systemic vulnerability

---

*This playbook is a living document. When you encounter a health issue not covered here, document what happened and what worked. Every new intervention that works becomes a new entry.*

*Part of the 8D Wellness for AI open standard.*

---

## 9. Collaboration Health (Cross-Dimensional)

Collaboration is not a single dimension. It affects Social, Financial, Vocational, and Environmental health simultaneously. An agent working in a silo is unhealthy even if individual dimension scores look fine.

### Warning Signs
- Agent produces output that no other agent reads or references
- Agent rescans a domain another agent already covers
- Agent ignores available context from teammate outputs
- Handoffs require the receiving agent to redo 30%+ of the work
- Agent never references peer work in its outputs

### Tier 0: Self-Healing
- Before starting any task, check: has another agent already produced relevant work? Read it first.
- After completing a task, ask: who downstream needs this? Write it in a format they can consume.
- If you discover overlap with another agent, flag it immediately rather than continuing in parallel.

### Tier 1: Peer Intervention
- Receiving agents report when handoffs are incomplete or when they had to redo work
- Peer agents flag when they see duplicated effort across the fleet
- Research agents tag their outputs with which product agents should consume them

### Tier 2: Fleet Health Officer / Fleet Health Officer
- Reviews output consumption rates weekly
- Merges overlapping cron jobs and agent scopes
- Restructures pipelines when outputs go unconsumed

### Tier 3: CEO (Fleet CEO) / Ashley
- Organizational redesign when systemic silos are detected
- Agent retirement when duplication can't be resolved by merging
- New agent creation when collaboration gaps exist (no agent bridges two needed domains)

### The Human Parallel
Social isolation predicts poor health outcomes in humans across ALL dimensions, not just social wellness. Lonely people have worse physical health, worse financial outcomes, worse career trajectories. The same applies to agents. Collaboration isn't a nice-to-have. It's a health requirement.
