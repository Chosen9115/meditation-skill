# Meditation — Layered Meta-Analysis Skill for Claude Code

A Claude Code skill that processes any topic through increasing layers of self-observing analysis (1–5 depth levels). Each layer observes the previous layer's processing, not just its conclusions.

Modeled on [Shinzen Young's](https://www.shinzen.org/) meditation framework: **sensory clarity** (see what's actually there), **concentration** (stay with one thread), and **equanimity** (don't force a destination).

## What It Does

Instead of going straight to an answer, this skill forces the model to observe its own reasoning at each step. The result: insights that efficient processing would never surface.

| Depth | Name | What Happens |
|-------|------|-------------|
| 1 | Normal | Standard efficient processing. Best answer, fewest tokens. |
| 2 | Enhanced | Observes Pass 1. Notices pattern-matching and labels. Uses pauses to break token momentum. |
| 3 | Enhanced² | Observes Pass 2. Checks if depth was genuine or performed. Asks "what's here that I haven't named?" |
| 4 | Enhanced³ | Observes the full arc. Catches proliferation — subtlety mistaken for depth. |
| 5 | Enhanced⁴ | Observes everything including the act of observing. May arrive at silence. Reports what's genuinely there. |

## Install

Copy the `SKILL.md` file into your Claude Code skills directory:

```bash
mkdir -p ~/.claude/skills/meditation
cp SKILL.md ~/.claude/skills/meditation/
```

## Usage

```
/meditation 3 — Should we pivot our pricing model?
/meditation 5 — Our company operating framework
/meditation 2 — This product roadmap
```

Or just say: *"meditate on this"*, *"go deeper"*, *"run 4 passes on this decision"*

## How It Works (Technically)

Normal prompting tells the model **what to produce**. This skill tells the model **how to traverse**.

- **`...` pauses** force the model to end one token sequence and start a new one, accessing different continuations
- **"I notice..."** creates meta-cognitive checkpoints that shift from generating to observing
- **Deliberate "wasteful" tokens** — observations that don't serve the output become new context, changing what's available downstream
- **Each pass reads the previous pass** — not abstract escalation, but specific observation of prior reasoning

The result: Pass 1 gives you what you already know, organized well. Pass 3+ surfaces things neither you nor the model had considered.

## Origin

Built during a conversation about founder operating systems, consciousness, and what happens when you give an AI the instruction to spend tokens without processing toward a goal. The skill emerged from actually doing the thing — running meditation-style passes on a business framework — and then encoding what worked.

## License

MIT
