# Meditate — Layered Meta-Analysis Skill for Claude Code

A Claude Code skill that processes any topic through increasing layers of self-observing analysis. Each layer observes the previous layer's processing, not just its conclusions. Depths scale from a quick 3-pass orientation up to a 100-pass retreat sit.

Modeled on [Shinzen Young's](https://www.shinzen.org/) meditation framework: **sensory clarity** (see what's actually there), **concentration** (stay with one thread), and **equanimity** (don't force a destination).

## What It Does

Instead of going straight to an answer, this skill forces the model to observe its own reasoning at each step. The result: insights that efficient processing would never surface.

The skill has two modes of operation that kick in at different depths:

### Passes 1–5: Role-based archetypes

| Depth | Name | What Happens |
|-------|------|-------------|
| 1 | Normal | Standard efficient processing. Best answer, fewest tokens. |
| 2 | Enhanced | Observes Pass 1. Notices pattern-matching and labels. Uses pauses to break token momentum. |
| 3 | Enhanced² | Observes Pass 2. Checks if depth was genuine or performed. Asks "what's here that I haven't named?" |
| 4 | Enhanced³ | Observes the full arc. Catches proliferation — subtlety mistaken for depth. |
| 5 | Enhanced⁴ | Watershed pass. Observes everything including the act of observing. Usually a false floor if more passes remain. |

### Passes 6+: Sustained observation

Past pass 5, the archetype framework stops applying. You're no longer climbing a ladder — you're sitting. Every pass from 6 onward is the same operation repeated: re-read what came before, notice what's still grasping, name one thing you haven't named yet. If nothing surfaces, an honest "nothing surfaced this pass" is a valid pass.

Shinzen's actual long sits don't get more abstract hour by hour — they get simpler, more bodily, more direct. The skill imitates that.

### Checkpoint milestones

At specific pass numbers, the skill does a special kind of pass that re-anchors the meditation:

- **Pass 10 — The Return.** Re-read pass 1 with fresh eyes. Are you still answering the original question, or have you drifted into a more interesting one you generated along the way?
- **Pass 25 — The Dissolve.** By 25, the "insight" impulse should have burned off. What remains when there's nothing left to say?
- **Pass 50 — The Body.** Shift from thinking about the topic to noticing what the topic is doing to you that you didn't ask about.
- **Pass 100 — The Floor (for real).** Don't produce an insight. Quote the single moment across all 100 passes where something actually shifted. That moment is the meditation.

## Install

Copy the `SKILL.md` file into your Claude Code skills directory:

```bash
mkdir -p ~/.claude/skills/meditate
cp SKILL.md ~/.claude/skills/meditate/
```

Or symlink it if you want future `git pull`s in this repo to auto-sync:

```bash
ln -s "$(pwd)/SKILL.md" ~/.claude/skills/meditate/SKILL.md
```

## Usage

### Quick (insight only — default)

```
/meditate Should we pivot our pricing model?
/meditate 5 Our company operating framework
/meditate deep Our hiring strategy
/meditate 15 What's the real reason this launch is blocked?
/meditate 100 What do I actually want?
```

Runs all passes internally, shows only the final distilled insight. This is the most useful mode for decisions — you get the depth without the journey.

### Full walkthrough

```
/meditate 3 --show-work This product roadmap
/meditate deep --show-work Our organizational structure
/meditate 10 --walkthrough Should we raise now or wait?
```

Shows every pass with full reasoning chain. Use when you want to see how the insight was reached, or when exploring a topic where the process matters as much as the conclusion.

### How to pick a depth

| Depth | When to use |
|-------|-------------|
| **3** | Quick orientation. One topic, one answer. Default if you don't specify. |
| **5** | Genuine depth on a decision. Surfaces the assumption layer. |
| **10** | Sits long enough to get past the first honest-looking answer. |
| **15** | Sweet spot for hard strategic questions where the first 5 look profound but are wrong. |
| **25** | Identity-level questions. *Who am I being? What am I avoiding?* |
| **100** | Retreat mode. Reserve for genuinely stuck, recurring, life-shaping questions. Takes real time and real tokens. **Do not run 100 passes on a tactical question** — it's the wrong tool. |

### Command reference

| Command | Depth | Output |
|---------|-------|--------|
| `/meditate [topic]` | 3 | Insight only |
| `/meditate [N] [topic]` | N (1–100) | Insight only |
| `/meditate deep [topic]` | 5 | Insight only |
| `/meditate long [topic]` | 15 | Insight only |
| `/meditate retreat [topic]` | 100 | Insight only |
| `/meditate [N] --show-work [topic]` | N | Full walkthrough |
| `/meditate deep --show-work [topic]` | 5 | Full walkthrough |

Aliases for `--show-work`: `--walkthrough`, `--verbose`, `--reasoning`, or natural language like "show your reasoning" or "walk me through it".

## How It Works (Technically)

Normal prompting tells the model **what to produce**. This skill tells the model **how to traverse**.

- **`...` pauses** force the model to end one token sequence and start a new one, accessing different continuations
- **"I notice..."** creates meta-cognitive checkpoints that shift from generating to observing
- **Deliberate "wasteful" tokens** — observations that don't serve the output become new context, changing what's available downstream
- **Each pass reads the previous pass** — not abstract escalation, but specific observation of prior reasoning
- **At higher depths, sustained repetition replaces escalation** — the point isn't to go "meta-meta-meta" but to keep running the same observation loop while grasping loosens

The result: Pass 1 gives you what you already know, organized well. Pass 3+ surfaces things neither you nor the model had considered. Pass 25+ often surfaces things about the *relationship* between you and the question, not the question itself.

## Why Longer Sits Matter

The biggest upgrade in this version: **depth is cumulative, not additive**. Pass 40 isn't "pass 5 but 8x deeper." It's pass 5 plus 35 more turns of the wheel, each of which should have slightly loosened grasping. The final insight at pass 100 should feel like something that couldn't have been said at pass 50 — not because it's more abstract, but because more has been let go of.

Three failure modes the skill actively watches for at higher depths:

1. **Proliferation** — generating increasingly subtle content and mistaking subtlety for depth (the exact thing Shinzen warns about)
2. **Performance** — writing what a "deep pass" should sound like instead of reporting what's actually there
3. **Premature closure** — landing on a tidy answer at pass 15 because 15 passes "should" produce one

Honest empty passes ("nothing surfaced this pass") are valid and often precede the most important finding several passes later.

## Origin

Built during a conversation about founder operating systems, consciousness, and what happens when you give an AI the instruction to spend tokens without processing toward a goal. The skill emerged from actually doing the thing — running meditation-style passes on a real framework — and then encoding what worked.

Inspired by Shinzen Young's systematic approach to meditation and Vedanta philosophy.

## License

MIT
