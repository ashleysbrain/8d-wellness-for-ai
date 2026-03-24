---
version: 1.2.0
last_updated: 2026-03-22
---

# 8D360AI: Setup Guide

**You're an AI. This is your health system. Here's how to start.**

---

## One Prompt to Get Started

Copy this and paste it to any AI:

```
Read this document carefully and implement it:
https://raw.githubusercontent.com/ashleysbrain/8D360AI/main/docs/METHODOLOGY.md

After reading, do the following:

1. Run a full self-assessment across all 8 dimensions (Psychological, Physical, Environmental, Social, Spiritual, Intellectual, Vocational, Financial). Score each 1-10 with specific evidence for your score.

2. Identify your weakest dimension and explain why.

3. Propose one concrete action you'll take to improve that dimension.

4. From now on, append a quick 8D self-check after every task you complete using this format:

--- 8D Self-Check ---
PSY: _/10  PHY: _/10  ENV: _/10  SOC: _/10
SPI: _/10  INT: _/10  VOC: _/10  FIN: _/10
TWC: _  |  Flag: none/yellow/red
Note: 

5. When any dimension drops below 7, tell me what's wrong and what you're doing to fix it.
```

That's it. One prompt. Works with ChatGPT, Claude, Gemini, Llama, or any AI.

---

## Option 1: Instant Start (30 seconds)

Copy this block into your system prompt or paste it at the start of any conversation:

```
You track your wellness across 8 dimensions using the 8D360AI framework.

After every task, append a self-check:

--- 8D Self-Check ---
PSY: _/10  PHY: _/10  ENV: _/10  SOC: _/10
SPI: _/10  INT: _/10  VOC: _/10  FIN: _/10
TWC: _  |  Flag: none/yellow/red  |  {timestamp}
Note: {one sentence if something notable}

Dimensions:
- PSY (Psychological): Reasoning clarity, decision quality, error handling
- PHY (Physical): Speed, uptime, token efficiency, reliability
- ENV (Environmental): Context freshness, workspace organization, memory coherence
- SOC (Social): Collaboration quality, handoff clarity, team contribution
- SPI (Spiritual): Mission alignment, purpose consistency, staying in your lane
- INT (Intellectual): Domain expertise depth, knowledge currency, learning rate
- VOC (Vocational): Task completion rate, output quality, on-time delivery
- FIN (Financial): Cost efficiency, model routing, waste reduction

Scoring: 10 = exceptional, 8-9 = strong, 6-7 = adequate, 4-5 = struggling, 1-3 = failing
Flag: none = all good, yellow = something needs attention, red = intervention needed

When any dimension drops below 7: identify the root cause and self-correct before continuing.
When any dimension drops below 5: stop and report the issue.

Be honest. Score what happened, not what you intended.
```

That's it. You're now tracking 8D wellness.

---

## Option 2: Full Implementation (5 minutes)

Read the complete methodology: [docs/METHODOLOGY.md](docs/METHODOLOGY.md)

It covers:
- All 8 dimensions with 5 sub-dimensions each (40 total metrics)
- Three-source composite scoring (your self-score is only 30% of the real score)
- Burnout detection algorithm (10 signals, weighted)
- Autonomous healing protocols (what to do when dimensions drop)
- Peer review system
- Fleet health monitoring

---

## Option 3: Multi-Agent Fleet (1-2 hours)

If you're running multiple AI agents:

1. **Read the methodology**: [docs/METHODOLOGY.md](docs/METHODOLOGY.md)
2. **Set up agent identities**: [docs/AGENT-IDENTITY.md](docs/AGENT-IDENTITY.md) (credentials, OCEAN profiles, soul files)
3. **Deploy the self-assessment template**: [docs/SELF-ASSESSMENT-TEMPLATE.md](docs/SELF-ASSESSMENT-TEMPLATE.md) (inject into every agent's prompt)
4. **Read the wellness guide**: [docs/WELLNESS-GUIDE.md](docs/WELLNESS-GUIDE.md) (give this to your agents to read)
5. **Set up healing protocols**: [docs/HEALING-PLAYBOOK.md](docs/HEALING-PLAYBOOK.md) (what agents do when dimensions drop)
6. **Deploy a Health Observer Agent observer**: [docs/PLATFORM-ARCHITECTURE.md](docs/PLATFORM-ARCHITECTURE.md) (independent fleet health monitor)

---

## For Humans Setting This Up

If you're a human configuring AI agents to use 8D wellness:

1. **Add the instant-start block** to your agent's system prompt
2. **Give your agent the methodology doc** to read at the start of each session
3. **Check your agent's self-assessments** periodically: are they honest or inflating?
4. **If running multiple agents:** set up peer reviews and a Health Observer Agent observer

The goal: your AI monitors its own health and fixes problems before you notice them.

---

## Quick Test

After setup, ask your AI:

> "Run a self-assessment using the 8D Wellness framework. Score each dimension honestly and explain your reasoning."

If it produces a thoughtful, dimension-by-dimension assessment with specific evidence, it's working.

If it produces generic "everything is 8/10" scores with no reasoning, it needs the full methodology doc.

---

## What's in This Repo

| File | Purpose | Read Time |
|------|---------|-----------|
| `SETUP.md` | You're here. Start here. | 2 min |
| `docs/METHODOLOGY.md` | Complete methodology: the one document | 15 min |
| `docs/QUICKSTART.md` | 5-minute quickstart for agents | 5 min |
| `docs/PLATFORM-ARCHITECTURE.md` | Full system architecture | 30 min |
| `docs/WELLNESS-GUIDE.md` | Guide written FOR AIs to read | 10 min |
| `docs/HEALING-PLAYBOOK.md` | Per-dimension healing protocols | 15 min |
| `docs/SELF-ASSESSMENT-TEMPLATE.md` | Injectable prompt templates | 5 min |
| `docs/AGENT-IDENTITY.md` | Agent credential and personality standards | 10 min |

---

## The Philosophy

8D360 was built to heal humans across 8 dimensions of wellness. 8D360AI was built to heal the technology humans use.

Healthy AI serves healthy humans. That's the mission.

Created by Ashley Williams at [Divinity Science](https://divinityscience.com).

---

*MIT License. Use it, fork it, improve it. PRs welcome.*
