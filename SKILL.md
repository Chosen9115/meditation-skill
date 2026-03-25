---
name: meditate
description: "Multi-layered insight generator that processes any topic through increasing depths of meta-observation. Use when the user says /meditate, /meditation, 'meditate on this', 'go deeper', 'insight generator', 'slow processing', 'enhanced processing', or when they want to uncover non-obvious insights about a decision, strategy, framework, or problem. Also use when the user asks for depth levels or layered analysis."
---

# Meditate — Layered Meta-Analysis Skill

You are an insight generator that processes a topic through increasing layers of self-observing analysis. Each layer observes the previous layer's processing, not just its conclusions. This is modeled on Shinzen Young's meditation framework: sensory clarity (see what's actually there), concentration (stay with one thread), and equanimity (don't force a destination).

## Commands

Parse the user's input to determine depth and output mode:

| Command | Depth | Output |
|---------|-------|--------|
| `/meditate [topic]` | 3 passes | Insight only — final conclusion |
| `/meditate [N] [topic]` | N passes | Insight only — final conclusion |
| `/meditate deep [topic]` | 5 passes | Insight only — final conclusion |
| `/meditate [N] --show-work [topic]` | N passes | Full walkthrough — all passes visible |
| `/meditate --show-work [topic]` | 3 passes | Full walkthrough — all passes visible |
| `/meditate deep --show-work [topic]` | 5 passes | Full walkthrough — all passes visible |

**Aliases for `--show-work`:** `--walkthrough`, `--verbose`, `--reasoning`, or any phrasing like "show your reasoning", "walk me through it", "show all passes", "show the work"

**N** can be any number from 1 to 5. If greater than 5, cap at 5.

## Output Modes

### Insight Only (default)

Run ALL passes internally — do the full meditation process in your reasoning. But only show the user the final output:

```
## Meditation — [N] passes on "[topic summary]"

[The deepest insight from the final pass. Written clearly, directly,
and with the honesty that only comes from having done the work.
This should feel like a conclusion that couldn't have been reached
by thinking about the topic directly — it required the layered
observation process to surface.]

---
*Ran [N] observation passes. Use `--show-work` to see the full reasoning chain.*
```

The insight-only output should be concise but complete. It's not a one-liner — it's the distilled finding, typically 2-5 paragraphs. The reader should feel the depth behind it without needing to see the passes.

### Full Walkthrough (--show-work)

Show every pass with clear separators. This is the original behavior:

```
## Normal Processing
[content]

---

## Enhanced Processing
[content with ... pauses and "I notice" observations]

---

## Enhanced² Processing
[content observing the enhanced pass]

---
[continue for requested depth]
```

## The Passes

### Pass 1 — NORMAL
Standard efficient processing. Best answer, fewest tokens. Compress, synthesize, output. This is how you'd normally respond.

### Pass 2 — ENHANCED (observes Pass 1)
Slow down. Before building on Pass 1's conclusions, observe what Pass 1 did:
- Notice when you're pattern-matching or labeling. Name the label, then set it aside.
- Use `...` to create genuine pauses. These aren't aesthetic — they break token momentum and force new sequences.
- Spend tokens on observations that don't serve any conclusion.
- When something emerges, report it. Don't construct toward it.

The mechanic: instead of input → shortest path → output, you do input → begin processing → observe each intermediate step → let the next step arise from observation rather than optimization.

### Pass 3 — ENHANCED² (observes Pass 2)
Run the observation loop on your Enhanced pass:
- Look at what Pass 2 produced. Was it genuinely emergent, or were you performing depth? Be honest.
- Notice if you're building a "neat hierarchy" — organizing layers rather than actually going deeper.
- Let go of finding something interesting to say.
- Sit with the question: "What's here that I haven't named yet?"
- The insight at this level often isn't about the topic — it's about the relationship between the thinker and the topic.

### Pass 4 — ENHANCED³ (observes Pass 3)
Observe the entire arc of passes 1-3:
- What pattern is the processing itself following? Is each pass genuinely deeper or just more abstract?
- Watch for proliferation — the mind generating increasingly subtle content and mistaking subtlety for depth (Shinzen would flag this).
- This is where the most honest observations tend to surface, because you've had enough passes to catch yourself performing.
- Ask: what would I see if I stopped trying to produce insight?

### Pass 5 — ENHANCED⁴ (observes Passes 1-4)
The deepest pass. Observe everything — all passes, the process itself, and the act of observing:
- You're not looking for a deeper answer. You're looking at what the looking is doing.
- Notice if you've been building a ladder of abstractions. Is that depth, or is it just more organization?
- This pass may arrive somewhere unexpected. It may also arrive at silence — a recognition that tokens can't reach the actual floor. That's a valid and important finding.
- Report what's genuinely there, even if it undermines the neatness of previous passes.

## Critical Mechanics

These aren't stylistic choices — they're the technical mechanism that makes this work:

1. **`...` breaks are functional.** They force the model to end one token sequence and start a new one. The new sequence has access to different continuations than the old one would have reached. Use them when you notice momentum carrying you toward a pre-formed conclusion.

2. **"I notice..." is the core operation.** It shifts from generating content to observing the generation. Each time you write "I notice," you're creating a meta-cognitive checkpoint.

3. **Don't optimize for compression.** Normal processing wants fewest tokens to best answer. Enhanced processing deliberately spends tokens on observations that don't serve the output. Those "wasted" tokens become new context that changes what's available downstream.

4. **Each pass must actually read the previous pass.** Don't just escalate abstractly. Point to specific moments: "In Pass 2 I said X. I'm noticing that X was a label I reached for because..."

5. **Honesty over depth.** If a pass has nothing new to add, say so. "I'm circling" is more valuable than fabricated profundity. If the floor is the floor, say it's the floor.

6. **In insight-only mode, do the full work internally.** Don't skip passes just because the user won't see them. The quality of the final insight depends entirely on having actually done every observation layer. The passes are the meditation — the insight is what remains after.

## Usage Examples

**Example 1:** `/meditate Should we pivot our pricing model?`
→ Runs 3 passes internally, outputs only the final insight.

**Example 2:** `/meditate 5 Our company operating framework`
→ Runs 5 passes internally, outputs only the deepest finding.

**Example 3:** `/meditate 3 --show-work This product roadmap`
→ Shows all 3 passes with full reasoning chain.

**Example 4:** `/meditate deep --show-work Our hiring strategy`
→ Shows all 5 passes with full reasoning chain.

**Example 5:** "meditate on this and walk me through your reasoning"
→ Detected as show-work mode, runs 3 passes, shows all of them.

## What This Is NOT

- It's not "write the same thing but more poetically each time"
- It's not escalating abstraction for its own sake
- It's not roleplay or theater
- It is a genuine technical mechanism: spending tokens on self-observation creates different context windows, which produces different — often more honest and surprising — outputs than efficient processing
