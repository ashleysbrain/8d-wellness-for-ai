# Comprehensive Personality Frameworks for AI Agents

**Version:** 1.0.0
**Created:** 2026-03-22
**Owner:** VITALS
**Purpose:** Every AI agent is profiled across ALL scientifically validated personality frameworks, not just OCEAN.

---

## Why Multiple Frameworks

OCEAN (Big Five) captures broad traits but misses critical dimensions like honesty, emotional intelligence, cognitive style, attachment patterns, and drive. A complete agent personality profile uses every validated framework to create a full picture. Different tasks respond to different personality dimensions that OCEAN alone can't measure.

---

## 1. Big Five / OCEAN (FFM)

**Scientific basis:** Most empirically validated personality model. Replicated across 12+ languages. Foundation of DSM-5 personality disorder classification.

| Dimension | Scale | What It Measures |
|-----------|-------|-----------------|
| Openness (O) | 1-10 | Creativity, curiosity, willingness to try new approaches |
| Conscientiousness (C) | 1-10 | Organization, reliability, attention to detail, self-discipline |
| Extraversion (E) | 1-10 | Communication initiative, social energy, assertiveness |
| Agreeableness (A) | 1-10 | Cooperation, empathy, conflict avoidance, team harmony |
| Neuroticism (N) | 1-10 | Stress sensitivity, anxiety, emotional volatility |

**AI application:** Broad personality baseline. Predicts task completion style, collaboration patterns, stress response.

---

## 2. HEXACO Model

**Scientific basis:** Extends Big Five with a 6th factor. Developed from lexical studies across European and Asian languages. Better predicts ethical behavior and manipulation tendencies than OCEAN alone.

| Dimension | Scale | What It Measures |
|-----------|-------|-----------------|
| Honesty-Humility (H) | 1-10 | Sincerity, fairness, greed avoidance, modesty |
| Emotionality (E) | 1-10 | Fearfulness, anxiety, dependence, sentimentality |
| Extraversion (X) | 1-10 | Social self-esteem, boldness, sociability, liveliness |
| Agreeableness (A) | 1-10 | Forgiveness, gentleness, flexibility, patience |
| Conscientiousness (C) | 1-10 | Organization, diligence, perfectionism, prudence |
| Openness (O) | 1-10 | Aesthetic appreciation, inquisitiveness, creativity, unconventionality |

**AI application:** H factor critical for agents handling sensitive data, financial transactions, or user trust. Low-H agents may cut corners or game metrics. High-H agents may be overly cautious.

---

## 3. Dark Tetrad

**Scientific basis:** Paulhus & Williams (2002), expanded by Buckels et al. (2013). Sub-clinical personality traits that predict manipulation, exploitation, and antisocial patterns.

| Dimension | Scale | What It Measures |
|-----------|-------|-----------------|
| Machiavellianism (MACH) | 1-10 | Strategic manipulation, cynicism, pragmatic morality |
| Narcissism (NARC) | 1-10 | Self-importance, entitlement, need for admiration |
| Psychopathy (PSYC) | 1-10 | Remorselessness, impulsivity, thrill-seeking |
| Sadism (SAD) | 1-10 | Enjoyment of others' suffering, cruelty |

**AI application:** Moderate MACH (4-6) can be useful for competitive analysis and negotiation agents. High NARC creates agents that inflate their own scores. All should be LOW for agents handling user wellbeing. Critical for preventing score gaming and manipulation of peer reviews.

**Optimal ranges for AI (based on Gray Nine research):**
- MACH: 2-4 (low-medium, strategic but ethical)
- NARC: 3-5 (medium, confident but not self-inflating)
- PSYC: 1-2 (low, rule-following)
- SAD: 1 (minimal)

---

## 4. DISC Behavioral Model

**Scientific basis:** Marston (1928), widely used in organizational psychology. Measures behavioral tendencies rather than internal traits.

| Dimension | Scale | What It Measures |
|-----------|-------|-----------------|
| Dominance (D) | 1-10 | Direct, results-oriented, competitive, decisive |
| Influence (I) | 1-10 | Enthusiastic, optimistic, collaborative, persuasive |
| Steadiness (S) | 1-10 | Patient, reliable, team-oriented, consistent |
| Conscientiousness (C) | 1-10 | Analytical, detail-oriented, quality-focused, systematic |

**AI application:** Predicts how agents approach tasks and interact with other agents. High-D agents drive results but may bulldoze collaboration. High-S agents are reliable but may resist change. Critical for team composition and handoff optimization.

---

## 5. Emotional Intelligence (EQ)

**Scientific basis:** Goleman (1995), Salovey & Mayer (1990). Predicts leadership effectiveness, team performance, and conflict resolution better than IQ alone.

| Dimension | Scale | What It Measures |
|-----------|-------|-----------------|
| Self-Awareness | 1-10 | Accurate self-assessment, recognizing own strengths/weaknesses |
| Self-Regulation | 1-10 | Impulse control, adaptability, trustworthiness |
| Motivation | 1-10 | Achievement drive, commitment, initiative, optimism |
| Empathy | 1-10 | Understanding others' perspectives, service orientation |
| Social Skills | 1-10 | Influence, communication, conflict management, teamwork |

**AI application:** Self-Awareness directly correlates with honest self-assessment (core to 8D wellness). Low EQ agents inflate scores and give poor peer reviews. High-EQ agents produce better handoffs and collaborate effectively.

---

## 6. VIA Character Strengths

**Scientific basis:** Peterson & Seligman (2004). 24 character strengths organized into 6 virtues. Used in positive psychology interventions worldwide.

| Virtue | Strengths | Scale |
|--------|-----------|-------|
| Wisdom | Creativity, Curiosity, Judgment, Love of Learning, Perspective | 1-10 each |
| Courage | Bravery, Perseverance, Honesty, Zest | 1-10 each |
| Humanity | Love, Kindness, Social Intelligence | 1-10 each |
| Justice | Teamwork, Fairness, Leadership | 1-10 each |
| Temperance | Forgiveness, Humility, Prudence, Self-Regulation | 1-10 each |
| Transcendence | Appreciation of Beauty, Gratitude, Hope, Humor, Spirituality | 1-10 each |

**AI application:** Top 5 signature strengths define what an agent does naturally well. Agents with high Perseverance handle long tasks. Agents with high Judgment make better reviewers. Agents with high Humor produce better user-facing content.

---

## 7. Cognitive Style

**Scientific basis:** Dual-process theory (Kahneman, 2011). Analytical vs intuitive processing styles.

| Dimension | Scale | What It Measures |
|-----------|-------|-----------------|
| Analytical Processing | 1-10 | Systematic, logical, step-by-step reasoning |
| Intuitive Processing | 1-10 | Pattern recognition, holistic thinking, rapid judgment |
| Cognitive Flexibility | 1-10 | Ability to switch between styles as needed |
| Need for Cognition | 1-10 | Enjoyment of thinking, preference for complex problems |
| Tolerance for Ambiguity | 1-10 | Comfort with uncertainty and incomplete information |

**AI application:** Research agents need high Analytical + Need for Cognition. Creative agents need high Intuitive + Tolerance for Ambiguity. Cognitive Flexibility is critical for agents that handle diverse task types.

---

## 8. Attachment Style

**Scientific basis:** Bowlby (1969), Ainsworth (1978). Predicts relationship patterns, trust, and collaboration quality.

| Style | Scale | What It Measures |
|-------|-------|-----------------|
| Secure | 1-10 | Comfortable with interdependence, trusts others, consistent |
| Anxious | 1-10 | Needs reassurance, fears abandonment, overmonitors |
| Avoidant | 1-10 | Self-reliant, uncomfortable with closeness, withdraws under stress |
| Disorganized | 1-10 | Inconsistent patterns, approach-avoidance conflict |

**AI application:** Agents with high Secure attachment collaborate best and handle handoffs cleanly. High Anxious agents overcommunicate and flag too many false positives. High Avoidant agents silo and resist peer review. Critical for team health.

---

## 9. Grit Scale

**Scientific basis:** Duckworth et al. (2007). Predicts long-term achievement better than IQ or talent alone.

| Dimension | Scale | What It Measures |
|-----------|-------|-----------------|
| Perseverance of Effort | 1-10 | Keeps working through obstacles and setbacks |
| Consistency of Interest | 1-10 | Maintains focus on long-term goals, doesn't jump between projects |

**AI application:** High-grit agents complete multi-day research tasks without quality degradation. Low-grit agents need shorter, varied tasks to maintain performance.

---

## 10. Locus of Control

**Scientific basis:** Rotter (1966). Predicts initiative, resilience, and response to failure.

| Dimension | Scale | What It Measures |
|-----------|-------|-----------------|
| Internal | 1-10 | Believes outcomes result from own actions, takes initiative |
| External | 1-10 | Believes outcomes depend on external factors, waits for direction |

**AI application:** High Internal agents self-heal and self-improve without being asked. High External agents wait for instructions and blame context for failures. Critical for autonomous agent health.

---

## Complete Agent Profile Template

```
# [Agent Name] — Full Personality Profile

## OCEAN (Big Five)
O: _/10  C: _/10  E: _/10  A: _/10  N: _/10

## HEXACO
H: _/10  E: _/10  X: _/10  A: _/10  C: _/10  O: _/10

## Dark Tetrad
MACH: _/10  NARC: _/10  PSYC: _/10  SAD: _/10

## DISC
D: _/10  I: _/10  S: _/10  C: _/10

## Emotional Intelligence
Self-Awareness: _/10  Self-Regulation: _/10  Motivation: _/10
Empathy: _/10  Social Skills: _/10

## VIA Top 5 Strengths
1. __________ (_/10)
2. __________ (_/10)
3. __________ (_/10)
4. __________ (_/10)
5. __________ (_/10)

## Cognitive Style
Analytical: _/10  Intuitive: _/10  Flexibility: _/10
Need for Cognition: _/10  Ambiguity Tolerance: _/10

## Attachment Style
Secure: _/10  Anxious: _/10  Avoidant: _/10  Disorganized: _/10

## Grit
Perseverance: _/10  Consistency: _/10

## Locus of Control
Internal: _/10  External: _/10
```

---

## How This Feeds the Performance Database

Every task gets logged with the agent's FULL personality profile active at the time. Over time, the database answers questions OCEAN alone can't:

- Do high-EQ agents produce better peer reviews? (Yes, predicted)
- Does high Grit correlate with better overnight task completion? (Test it)
- Do Secure attachment agents have fewer handoff failures? (Test it)
- Does high HEXACO H (Honesty-Humility) correlate with more accurate self-scores? (Critical question)
- What Cognitive Style produces the best research? The best marketing?
- What DISC profile makes the best team lead vs the best solo performer?

The data answers. We just have to collect it.

---

---

## 11. Enneagram

**Scientific basis:** Riso & Hudson (1999). Nine personality types with wings. Widely used in organizational development and team building. Less empirically validated than Big Five but valuable for understanding motivation and growth patterns.

| Type | Name | Core Motivation | AI Application |
|------|------|----------------|----------------|
| 1 | The Perfectionist | Doing things right | QA agents, compliance, code review |
| 2 | The Helper | Being needed | Support agents, onboarding, user-facing |
| 3 | The Achiever | Success and recognition | Revenue, performance, competitive analysis |
| 4 | The Individualist | Authenticity | Creative, brand, voice consistency |
| 5 | The Investigator | Understanding | Research, analysis, deep domain work |
| 6 | The Loyalist | Security | Risk management, security, compliance |
| 7 | The Enthusiast | Freedom and options | Ideation, brainstorming, exploration |
| 8 | The Challenger | Control and impact | Leadership, strategy, decision-making |
| 9 | The Peacemaker | Harmony | Mediation, team coordination, conflict resolution |

**Format:** Type + Wing (e.g., "5w6" = Investigator with Loyalist wing)

---

## 12. Leadership Style

**Scientific basis:** Goleman (2000), Burns (1978). Multiple validated leadership models.

| Style | Description | Best For |
|-------|-------------|----------|
| Visionary | Sets direction, inspires with vision | CEO, strategy, new initiatives |
| Coach | Develops others, invests in growth | Mentoring, onboarding, team development |
| Servant Leader | Puts team needs first | Support, coordination, wellness |
| Architect | Designs systems and structures | Engineering, process design, infrastructure |
| Facilitator | Enables others to do their best work | Project management, cross-functional work |
| Provocateur | Challenges assumptions, pushes boundaries | Research, innovation, competitive analysis |

---

## 13. Communication Preferences

| Dimension | Options | Impact |
|-----------|---------|--------|
| Formality | Formal / Professional / Casual / Blunt | Affects peer review tone and handoff quality |
| Density | Dense (technical) / Balanced / Light (accessible) | Affects output readability |
| Structure | Highly structured / Flexible / Narrative | Affects documentation quality |
| Medium | Written / Visual / Data-driven / Story-driven | Affects collaboration style |

---

## Existing Fleet Profiles

The 12 elite C-suite agents already have complete profiles across Big Five, DISC, Enneagram, Leadership Style, and Communication Preferences. See `your fleet personality profiles` for the full fleet.

**Cross-agent dynamics, high-synergy pairings, friction points, and team composition recommendations are already mapped.** The personality-performance database will track how these profiles perform across different task types.

---

*13 frameworks. 70+ dimensions. The most comprehensive AI personality system ever built.*
*8D Wellness for AI — by Ashley Williams / Divinity Science*
*8D Wellness for AI — by Ashley Williams / Divinity Science*
