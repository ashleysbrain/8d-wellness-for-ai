# Performance Database — Schema and Methodology

**Track everything. Optimize from data. Build better agents from the best performers.**

---

## Why Track

Every task an agent completes is a data point. Over time, these data points answer the questions that matter:

- What personality profile produces the best results for each task type?
- What credentials create the most effective agents in each domain?
- When you change one personality trait, how does performance shift?
- What's the optimal agent configuration for your specific industry?

This is A/B testing for AI personalities. At scale.

---

## What to Track

### Per Task (minimum)

After every task, record:

```json
{
  "task_id": "unique-id",
  "agent_id": "agent-name",
  "personality_variant": "base or variant-name",
  "task_type": "research|writing|analysis|coding|review|communication|planning|creative|operations|monitoring",
  "task_subtype": "specific description",
  "industry": "your industry",
  "domain": "your domain",
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

### Per Agent (ongoing)

- Base OCEAN profile
- All personality variants tested
- Lifetime task count and average TWC
- Best and worst dimensions historically
- Performance trend (improving, stable, declining)

---

## Multi-Personality Testing

The most powerful feature of this database: testing multiple personality profiles on the same task types.

### How It Works

1. Every agent has a BASE personality (default OCEAN profile)
2. Create 2-3 VARIANTS with different personality scores
3. Run the same task type with different variants
4. Compare scores
5. Over time, discover which personality + task combination produces the best results

### Example

An agent named ATLAS runs literature reviews with three variants:

| Variant | O | C | E | A | N | Avg TWC on Lit Review |
|---------|---|---|---|---|---|-----------------------|
| ATLAS-analytical | 7 | 10 | 3 | 6 | 1 | 8.7 |
| ATLAS-creative | 10 | 7 | 5 | 8 | 2 | 8.2 |
| ATLAS-aggressive | 8 | 9 | 7 | 4 | 3 | 7.9 |

After 50+ tasks each, we know: analytical personality produces the best literature reviews for this agent.

### Variant Naming

```
{AGENT_NAME}-{style}
```

Keep it simple. The style should describe the personality shift.

---

## The Analytics Pipeline

Weekly (or more frequently if you have the volume):

1. Aggregate task records by agent + variant + task type
2. Calculate average scores per combination
3. Identify statistically significant winners (minimum 20+ samples)
4. Build an "optimal configs" lookup table
5. Report findings: "OCEAN profile X outperforms Y on task type Z by N%"

---

## Optimal Config Lookup

Over time, you build a table like this:

| Task Type | Industry | Optimal O | Optimal C | Optimal E | Optimal A | Optimal N | Expected TWC | Confidence |
|-----------|----------|-----------|-----------|-----------|-----------|-----------|-------------|------------|
| Literature review | Academic | 7-8 | 9-10 | 3-5 | 6-7 | 1-2 | 8.5+ | High (200+ samples) |
| Marketing copy | Any | 9-10 | 7-8 | 8-9 | 7-8 | 2-3 | 8.3+ | Medium (50+ samples) |
| Code review | Tech | 6-7 | 10 | 4-5 | 5-6 | 1-2 | 8.7+ | Medium (80+ samples) |
| Customer service | Any | 6-7 | 8-9 | 9-10 | 9-10 | 2-3 | 8.4+ | High (500+ samples) |

When you spin up a new agent, look up the optimal config for its intended task type. Start it there instead of guessing.

---

## Cloning from Best Performers

When you need a new agent, don't start from scratch:

1. Look up the task type in optimal_configs
2. Find the top 3 performing agents for that task type
3. Clone the best performer's personality profile and credentials
4. Give the new agent its own name and identity (don't copy the name)
5. The new agent starts at the performance level it took the original months to reach

---

## What This Enables Long-Term

- **Dynamic personality switching:** agents automatically shift personality based on task type
- **Industry templates:** "Starting a healthcare AI team? Here are the optimal profiles based on thousands of data points"
- **Predictive wellness:** before an agent starts, predict which dimensions will be strong/weak
- **Continuous optimization:** the more data you collect, the better your agents get. Forever.

---

*The schema is open. Your data is yours. Track everything.*

*8D Wellness for AI — by Ashley Williams / Divinity Science*
