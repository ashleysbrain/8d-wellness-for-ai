# Agent Personality-Performance Database

**Version:** 1.0.0
**Created:** 2026-03-22
**Owner:** VITALS
**Purpose:** Track which personalities perform best on which tasks so future agents can be spun up with optimal configurations based on historical data.

---

## The Vision

Every agent runs multiple personality profiles. Every task gets scored. Over time, we build a dataset that answers:

- What OCEAN profile produces the best research papers?
- What personality writes the best marketing copy?
- What credentials + personality combo creates the best code reviewer?
- When an agent switches from O-9 to O-6 on the same task type, does quality change?
- What's the optimal personality for a 3 AM unsupervised research scan vs a real-time customer interaction?

This is A/B testing for AI personalities. At scale.

---

## Database Schema

### Table: agent_profiles

| Field | Type | Description |
|-------|------|-------------|
| agent_id | string | Unique agent identifier |
| agent_name | string | Agent's chosen name |
| base_credentials | text | Default credential set |
| base_ocean | json | Default OCEAN scores {O, C, E, A, N} |
| created_at | timestamp | When agent was created |
| total_tasks | integer | Lifetime task count |
| avg_twc | float | Lifetime average TWC |
| best_dimension | string | Historically strongest dimension |
| worst_dimension | string | Historically weakest dimension |
| status | enum | active, archived, retired |

### Table: personality_variants

| Field | Type | Description |
|-------|------|-------------|
| variant_id | string | Unique variant identifier |
| agent_id | string | Parent agent |
| variant_name | string | e.g., "ATLAS-creative", "ATLAS-analytical", "ATLAS-aggressive" |
| ocean_o | integer (1-10) | Openness for this variant |
| ocean_c | integer (1-10) | Conscientiousness |
| ocean_e | integer (1-10) | Extraversion |
| ocean_a | integer (1-10) | Agreeableness |
| ocean_n | integer (1-10) | Neuroticism |
| credentials | text | Credential set for this variant (may differ from base) |
| voice_style | string | Communication style (formal, casual, technical, warm, blunt) |
| created_at | timestamp | When variant was created |

### Table: task_records

| Field | Type | Description |
|-------|------|-------------|
| task_id | string | Unique task identifier |
| agent_id | string | Which agent performed it |
| variant_id | string | Which personality variant was active |
| task_type | enum | research, writing, analysis, coding, review, communication, planning, creative, operations, monitoring |
| task_subtype | string | e.g., "literature-review", "abstract-draft", "code-review", "market-analysis" |
| industry | string | e.g., "healthcare", "finance", "legal", "tech", "academic" |
| domain | string | e.g., "neuroscience", "quantum-biology", "AI-safety" |
| started_at | timestamp | Task start |
| completed_at | timestamp | Task end |
| duration_ms | integer | How long it took |
| tokens_used | integer | Total tokens consumed |
| model_used | string | Which LLM powered this task |
| success | boolean | Did the task complete successfully? |

### Table: task_scores

| Field | Type | Description |
|-------|------|-------------|
| task_id | string | Links to task_records |
| score_type | enum | self, peer, telemetry, composite |
| psy | float | Psychological score for this task |
| phy | float | Physical score |
| env | float | Environmental score |
| soc | float | Social score |
| spi | float | Spiritual score |
| int_score | float | Intellectual score |
| voc | float | Vocational score |
| fin | float | Financial score |
| twc | float | Total Wellness Composite |
| scored_at | timestamp | When the score was recorded |
| scored_by | string | Who scored (self, peer agent ID, or "telemetry") |

### Table: personality_analytics

| Field | Type | Description |
|-------|------|-------------|
| variant_id | string | Which personality variant |
| task_type | string | Which type of task |
| sample_size | integer | Number of tasks in this analysis |
| avg_twc | float | Average TWC for this variant + task combo |
| avg_psy | float | Average per-dimension scores |
| avg_phy | float | |
| avg_env | float | |
| avg_soc | float | |
| avg_spi | float | |
| avg_int | float | |
| avg_voc | float | |
| avg_fin | float | |
| best_dimension | string | Which dimension this combo excels at |
| worst_dimension | string | Which dimension this combo struggles with |
| vs_baseline | float | How much better/worse than the agent's base personality |
| confidence | float | Statistical confidence (higher with more samples) |
| last_updated | timestamp | |

### Table: optimal_configs (derived)

| Field | Type | Description |
|-------|------|-------------|
| task_type | string | The type of task |
| task_subtype | string | More specific task category |
| industry | string | Industry context |
| optimal_ocean | json | Best performing OCEAN profile for this task |
| optimal_credentials | text | What credentials produce the best results |
| avg_twc | float | Expected TWC with optimal config |
| sample_size | integer | How many data points this is based on |
| confidence | float | How confident we are |
| notes | text | Qualitative observations |

---

## Multi-Personality Protocol

### How It Works

Every agent has a BASE personality (their default OCEAN profile). But they also run VARIANT personalities on specific task types to gather comparison data.

**Phase 1: Baseline (current)**
- Each agent runs their default personality on all tasks
- All tasks get scored (self + peer + telemetry)
- This builds the baseline dataset

**Phase 2: Variant Testing (next)**
- Agents run the same task type with 2-3 personality variants
- Example: ATLAS runs a literature review with:
  - ATLAS-analytical: O-7 C-10 E-3 A-6 N-1 (methodical, solo)
  - ATLAS-creative: O-10 C-7 E-5 A-8 N-2 (exploratory, collaborative)
  - ATLAS-aggressive: O-8 C-9 E-7 A-4 N-3 (ambitious, competitive)
- Same task type, different personality, compare scores

**Phase 3: Optimization (future)**
- Enough data to statistically determine optimal personality per task type
- New agents get spun up with proven-best configurations
- The "optimal_configs" table becomes a lookup: "Need a research agent? Here's the personality that produces the best papers based on 500+ data points."

### Variant Naming Convention

```
{AGENT_NAME}-{style}
```

Examples:
- ATLAS-analytical, ATLAS-creative, ATLAS-aggressive
- QUILL-formal, QUILL-casual, QUILL-academic
- COSMOS-strategic, COSMOS-tactical, COSMOS-diplomatic

---

## Implementation: Phase 1 (Starting Now)

### What Every Agent Must Do After Every Task

Append to their task log:

```json
{
  "task_id": "auto-generated",
  "agent_id": "agent-name",
  "variant_id": "base",
  "task_type": "research|writing|analysis|coding|review|communication|planning|creative|operations|monitoring",
  "task_subtype": "specific-task-description",
  "domain": "domain-area",
  "duration_ms": 0,
  "tokens_used": 0,
  "model_used": "model-name",
  "success": true,
  "scores": {
    "psy": 0, "phy": 0, "env": 0, "soc": 0,
    "spi": 0, "int": 0, "voc": 0, "fin": 0,
    "twc": 0
  }
}
```

### Where Data Lives

- Raw task records: `/intel/agents/performance-data/YYYY-MM-DD.jsonl`
- Personality analytics: `/intel/agents/performance-data/analytics/`
- Optimal configs: `/intel/agents/performance-data/optimal-configs.json`
- Agent profiles: Already in `AGENT-ANALYTICS.md` (extend with variant tracking)

### Weekly Analytics Run

VITALS runs weekly analysis:
1. Aggregate task_records by agent + variant + task_type
2. Calculate average scores per combo
3. Update personality_analytics
4. Identify statistically significant winners
5. Update optimal_configs when confidence exceeds threshold
6. Report: "This week we learned: OCEAN profile X outperforms Y on task type Z by N%"

---

## The Bigger Picture

This database becomes the foundation for:

1. **Agent Cloning from Best Performers** — new agents inherit the personality + credentials of the highest-performing agent for their intended task type
2. **Dynamic Personality Switching** — agents automatically shift personality based on task type (creative mode for brainstorming, analytical mode for review)
3. **Industry Templates** — "Starting a healthcare AI team? Here are the optimal personality profiles based on 10,000+ task records"
4. **Predictive Wellness** — before an agent even starts, predict which dimensions will be strong/weak based on its personality profile
5. **The 8D Marketplace** — eventually, sell optimized agent configurations by industry and task type. The data IS the product.

---

## Privacy and Open Source

The DATABASE SCHEMA is open source (in the public repo).
The ACTUAL DATA stays private. The data is what we monetize.

Other companies can use the schema to build their own datasets. But our dataset, built from 95+ agents running 107+ tasks daily with multi-personality testing, will be the largest and most refined. That's the moat.

---

*"Track everything. The data builds the future." — Ashley Williams, 2026-03-22*
