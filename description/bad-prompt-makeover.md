# Bad Prompt Makeover: Description Competency Exercise

This document captures a prompt improvement exercise applying the Description core competency from the AI Fluency Framework.

## Reference: Description Principles

From `description/key-takeaways.md`:

1. **Collaborative Environment** — Description creates productive collaboration, not commands
2. **Product Description** — Define outputs, format, audience, and style
3. **Process Description** — Guide how the AI approaches the request
4. **Performance Description** — Define behavioral aspects (concise/detailed, challenging/supportive)
5. **Interactive Partners** — AI systems are partners, not databases or vending machines
6. **Clear Communication** — Upfront clarity saves time and improves results

---

## Exercise 1: User Improves Bad Prompts

### Round 1 Results

| Original | Improved |
|----------|----------|
| "Make this better." | Improve this product summary. Follow the prose format from other product summaries in the same document. Identify the most optimal audience from the buyer persona definitions. Use the product summary skill. Be concise. |
| "Write something about climate change." | Write a concise analysis about climate change effects in the southern region of Mexico. Prioritize findings from scientific reports and government issued alerts from the past 2 years. Format the content for young elementary school students. Follow a 3 step process. Step 1 gather data. Step 2 synthesize data. Step 3 write analysis. Present each step for evaluation where I will compare against my own findings. |
| "Help me with my code." | Improve this bash function following bash scripting best practices. Document variables, comments and function description for infrastructure engineers. The output should align with existing bash functions in the codebase in terms of spacing, length, function naming and unit testing. Approach function creation from a ralph loop perspective. Where each iteration addresses a specific part of the function, for example iteration 1 function naming, iteration 2 variable naming, iteration 3 main logic, iteration 4 unit testing. Be concise, and follow do not repeat yourself patterns. |

### Round 1 Analysis

| Principle | Prompt 1 | Prompt 2 | Prompt 3 |
|-----------|----------|----------|----------|
| Product Description | Strong — format reference, audience, skill | Strong — output type, audience, geographic scope | Strong — artifact type, documentation needs, codebase alignment |
| Process Description | Partial — skill invocation | Strong — 3-step process with checkpoints | Strong — iteration breakdown |
| Performance Description | Present — "be concise" | Present — "concise analysis" | Present — "be concise", DRY |
| Collaborative Environment | Weak — no review points | Strong — evaluation at each step | Moderate — iterations imply review |

**Strengths demonstrated:**
- Consistent addition of specific subjects
- Style/format references to existing artifacts
- Audience specification
- Process structure (steps, iterations)

**Gap identified:** Prompt 2 stood out for explicitly creating collaboration checkpoints ("present each step for evaluation"). Prompts 1 and 3 could benefit from similar patterns.

---

## Exercise 2: Claude Improves Bad Prompts

### Round 2 Results

| Original | Improved |
|----------|----------|
| "Create an summary of last month's infra incident." | Create a postmortem summary for the database failover incident (`<INCIDENT-ID>`). Source details from the incident channel (`<#your-incident-channel>`) and the PagerDuty timeline. Format for the engineering leadership audience using our postmortem template in `<path/to/template.md>`. Include: timeline, root cause, customer impact metrics, and remediation status. Keep it under 500 words. |
| "Configure claude with personal credentials." | Configure my GitHub personal access token for Claude Code. Add it to user-level settings (~/.claude.json) using environment variable expansion so the token isn't hardcoded. The token is stored in my password manager as `<your-vault-entry-name>`. Verify the configuration works by listing available MCP tools after setup. |
| "Fix the error in the pipeline." | Fix the failing GitHub Actions workflow in `<path/to/workflow.yml>`. The error occurs at the "Build Docker image" step with: `ERROR: failed to solve: image:version: not found`. The workflow passed on the previous commit (`<last-passing-commit>`). Preserve the existing caching strategy. Run the workflow locally with `act` to verify the fix before pushing. |

### Round 2 Self-Critique

| Principle | Prompt 1 (Postmortem) | Prompt 2 (Credentials) | Prompt 3 (Pipeline) |
|-----------|----------------------|------------------------|---------------------|
| Product Description | Strong | Strong | Strong |
| Process Description | Weak | Partial | Partial |
| Performance Description | Weak | Weak | Weak |
| Collaborative Environment | Weak | Weak | Weak |

**Pattern identified:** Heavy emphasis on Product Description, neglecting Process, Performance, and Collaboration.

---

## Gap Analysis: Which Principles Are We Overlooking?

### Primary Gap: Collaborative Environment

Both exercise rounds revealed a tendency to treat prompts as **task orders** rather than **collaboration invitations**. The key-takeaways principle states:

> "AI systems are interactive partners, not databases or vending machines"

**Symptoms of this gap:**
- One-shot requests expecting complete deliverables
- No checkpoints for review or course correction
- No invitation for Claude to ask clarifying questions
- No acknowledgment that Claude might identify issues with the request itself

### Secondary Gap: Performance Description

Neither round consistently specified behavioral expectations:
- Verbosity level (explain reasoning or just execute?)
- Confidence signaling (flag uncertainty or proceed silently?)
- Tone (formal, conversational, challenging?)
- Interaction style (ask questions or make assumptions?)

### Tertiary Gap: Process Description

While some prompts included process elements (steps, iterations), most focused on **what** rather than **how**:
- Missing: "Diagnose before fixing"
- Missing: "Present hypothesis before implementing"
- Missing: "Ask clarifying questions if scope is unclear"

---

## Addressing the Gaps

### Pattern 1: Add Collaboration Checkpoints

**Before:**
> Fix the failing pipeline. The error is X. Preserve caching.

**After:**
> Fix the failing pipeline. The error is X. Preserve caching.
> 
> **Approach:** First explain your diagnosis. Wait for my confirmation before implementing changes.

### Pattern 2: Specify Performance Expectations

**Before:**
> Create a postmortem summary for `<INCIDENT-ID>`.

**After:**
> Create a postmortem summary for `<INCIDENT-ID>`.
> 
> **Behavior:** Be concise. Use blameless language. If you're missing context from the sources, flag it rather than inferring.

### Pattern 3: Guide the Process Explicitly

**Before:**
> Configure my GitHub PAT for Claude Code.

**After:**
> Configure my GitHub PAT for Claude Code.
> 
> **Process:** First confirm the current state of my Claude configuration. Then propose changes before applying them.

---

## Revised Prompt Template

Based on this exercise, a well-described prompt includes:

```
[Task statement with specific artifact/subject]

**Product:** [Output format, audience, style references]

**Process:** [How to approach — checkpoints, sequence, diagnostic steps]

**Performance:** [Behavioral expectations — verbosity, tone, uncertainty handling]

**Collaboration:** [Review points, questions welcome, confirmation gates]
```

---

## Key Learnings

1. **Product Description is the easy part** — both participants naturally specified outputs, formats, and audiences.

2. **Collaboration is the overlooked principle** — prompts defaulted to vending-machine mode ("input request, output result") rather than partner mode ("let's work through this together").

3. **Process and Performance require deliberate effort** — these don't emerge naturally and must be consciously added.

4. **The user's Prompt 2 was the gold standard** — the 3-step process with evaluation checkpoints exemplified all four Description principles working together.

5. **One-shot prompts waste iteration potential** — by not building in review points, we lose the opportunity to course-correct before Claude produces a complete (but potentially misaligned) deliverable.

---

## Quick Reference: Description Checklist

Before submitting a prompt, verify:

- [ ] **Product:** Is the output clearly defined (format, audience, style)?
- [ ] **Process:** Does Claude know how to approach this (sequence, diagnosis, research)?
- [ ] **Performance:** Are behavioral expectations set (verbosity, tone, uncertainty)?
- [ ] **Collaboration:** Are there checkpoints for review or invitation to clarify?

If any box is unchecked, the prompt may produce technically correct but misaligned results.
