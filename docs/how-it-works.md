# How Delegate Works

## The Problem It Solves

When tackling complex tasks, you need a powerful model like Fable 5:
- To think through architecture and planning
- To understand nuanced requirements
- To reason about edge cases and risks

**But:** Running the entire task through Fable 5 is expensive. And often, the actual execution doesn't need all of Fable's reasoning power—it just needs to follow a clear plan.

**The cost:** 2-3x more expensive than necessary for the execution phase.

## The Solution

1. **Deep interview** — Claude asks questions to understand full project structure and requirements
2. **Fable 5 plans** (expensive but necessary) — creates detailed, step-by-step plan based on complete context
3. **User reviews** — brief summary, accepts/rejects/modifies
4. **Cheaper model executes** (Sonnet 5 or Opus 4.8) — follows plan precisely
5. **You get results** — same quality, 30-50% lower cost, no wasted budget on vague prompts

---

## Step-by-Step Workflow

### Phase 1: Qualification (< 1 min)

**What happens:** Claude evaluates if the task is actually complex enough for this workflow.

**Is the task complex enough?**
- ✅ Multi-step with dependencies (3+ independent parts)
- ✅ Requires architecture or strategic decisions
- ✅ High risk (mistakes would be costly)
- ✅ Needs investigation (reading files, analyzing data)
- ❌ Single-function implementation
- ❌ Simple bug fix
- ❌ Straightforward query

**If too simple:** Claude will tell you and just do the task normally.

**If complex:** Continue to Phase 2.

---

### Phase 2: Deep Interview (2-5 minutes)

**What happens:** Claude conducts a structured interview to fully understand the project before expensive Fable planning.

**Claude will ask about:**
- 🏗️ **Project structure** — architecture, technologies, existing components, data model
- 🎯 **Business goal** — what exactly needs to be achieved and why
- ✅ **Functional requirements** — specific behaviors (be concrete: "form with email validation for signup" not "make a form")
- ⚙️ **Non-functional requirements** — performance targets, security constraints, accessibility needs, deadline, budget
- 👥 **Context** — who will use this, what are realistic use cases, what are edge cases
- 🚫 **Constraints** — what absolutely cannot change, what are dependencies, failure modes

**Why this matters:** Filters out vague or incomplete prompts before they reach Fable 5. No garbage in = no wasted budget on bad plans.

**What you do:** Answer questions honestly and specifically. If asked "what's the scope?"—don't say "make a dashboard", say "render real-time metrics from PostgreSQL for 50K users with <500ms load time".

**If requirements are unclear:** Claude will keep asking until they're not.

**Output:** Complete, structured understanding of what needs to be done.

---

### Phase 3: Planning with Fable 5 (2-5 minutes)

**What happens:** Fable 5 analyzes the task deeply and creates a detailed execution plan.

**Fable will:**
- Understand requirements and constraints
- Identify what needs to be examined (files, data, specs)
- Create concrete, step-by-step plan
- Anticipate edge cases and branching logic
- Identify success criteria
- Flag risks and mitigations
- **Recommend which model should execute** (based on complexity analysis)

**What Fable will NOT do:** Actually execute the task. Just plan it.

**Output:** Detailed plan with:
```
1. Understanding (what, why)
2. Context (files/data needed)
3. Step-by-step plan (concrete, not vague)
   - Branch logic for edge cases
   - Specific file changes, not general ideas
4. Success criteria (how to verify it worked)
5. Risks and mitigation strategies
6. Model recommendation (Sonnet 5 vs Opus 4.8)
```

---

### Phase 4: Review & Accept (1-2 minutes)

**What happens:** You see a brief summary and decide whether to proceed.

**You see:**
- ✏️ **Objective** — what will be done (1 sentence)
- 📋 **Main steps** — 3-4 major phases (high level)
- 🎯 **Recommended model** — Sonnet 5 or Opus 4.8, with Fable's reasoning
- ⚠️ **Key risks** — if any significant ones exist

**You choose:**
- ✅ **Accept** — Execute with recommended model
- 🔄 **Swap model** — Use Opus instead of Sonnet (or vice versa)
- ✏️ **Revise** — Send feedback to Fable for plan improvements
- ❌ **Cancel** — Don't proceed

---

### Phase 5: Execution (5-30 minutes depending on task)

**What happens:** Selected model (Sonnet 5 or Opus 4.8) receives the full detailed plan and executes it step-by-step.

**The model will:**
- Follow the plan exactly
- Report any deviations from plan assumptions (e.g., "file structure different than expected")
- Handle edge cases per the plan's branching logic
- Verify success criteria as it goes
- Output results with links to modified files

**Why this works:** The plan is concrete enough that the model doesn't need to re-strategize—it just executes.

---

### Phase 6: Report (< 1 min)

**What you get:**
- Brief summary of what was accomplished
- Key files modified with links
- Whether plan was followed or if deviations occurred
- Any blockers or unexpected challenges

**What you DON'T get:** Entire plan repeated (you already saw the summary)

---

## Model Selection: Sonnet 5 vs Opus 4.8

Fable makes the recommendation based on task complexity. You can override.

### Sonnet 5 — Recommended for:
- ✅ Code refactoring with clear requirements
- ✅ Implementation from detailed specs
- ✅ Mechanical transformations (rename, restructure, format)
- ✅ Well-defined, deterministic tasks
- **Cost:** Lower (~60% of Opus cost)
- **Speed:** Faster

**Example:** "Refactor module A into smaller functions per this architecture diagram"

### Opus 4.8 — Recommended for:
- ✅ Ambiguous requirements needing interpretation
- ✅ Creative solution design
- ✅ Complex judgment calls between approaches
- ✅ Synthesizing contradictory information
- **Cost:** Higher (~160% of Sonnet cost)
- **Flexibility:** Better with ambiguity

**Example:** "Decide how to migrate our auth system while minimizing downtime and risk"

---

## Cost Analysis Example

### Task: Refactor authentication module (well-defined requirements)

**Old approach (Fable does everything):**
- Fable planning: 5 min
- Fable execution: 20 min
- Total: Fable 5 (most expensive)

**Delegate approach:**
- Fable planning: 5 min
- You review: 1 min
- Sonnet 5 execution: 20 min
- Total: Fable (planning) + Sonnet 5 (execution)

**Savings:** ~40% on execution phase

### Task: Design new API with competing requirements (ambiguous)

**Delegate approach:**
- Fable planning: 5 min (understand tradeoffs)
- You review: 2 min
- Opus 4.8 execution: 15 min (make nuanced decisions)
- Total: Fable (planning) + Opus 4.8 (execution)

**Why Opus here:** Needs strategic decision-making during execution, not just plan-following

---

## When NOT to Use `/delegate`

- **Simple task** — "add a button that logs user out"
- **Quick fix** — "fix this typo"
- **Lookups** — "what files handle routing?"
- **Single-function** — "write a function that validates email"
- **Anything < 5 min work** — overhead not worth it

In these cases, just use Claude directly or a simpler tool.

---

## Customizing the Skill

### Changing Model Routing Logic

Edit `skill/SKILL.md` step 3 (Planning phase). Fable's prompt includes:

```
6. **Rekomendacja modelu**:
   - Sonnet 5 (tańszy): jeśli zadanie jest MECHANICZNE...
   - Opus 4.8 (droższy): jeśli wymaga NIUANSU...
```

Modify the criteria based on your preferences. Example:

> Always recommend Opus for security-related tasks, even if mechanical.

### Adjusting Qualification Criteria

Edit step 1 if you want looser/stricter qualification. Example:

> Currently requires 3+ independent steps. Change to 2+ for more aggressive use.

### Adding Auto-Invocation Rules

The skill auto-proposes when detecting "very complex" tasks. Edit the guideline in "Przewodnik do Auto-Invokacji" to tune when it triggers.

---

## Performance & Limits

| Metric | Typical | Range |
|--------|---------|-------|
| Planning time (Fable) | 3-5 min | 2-15 min |
| Execution time | Task-dependent | 5-60+ min |
| Total overhead | ~10-15% | Can vary |
| Token context per step | Reasonable | Splits on very large tasks |

### Large Tasks

If the plan is very large (1000+ steps):
- Fable may split it
- Or break into 2-3 smaller `/delegate` runs
- Monitor token usage

---

## FAQ

**Q: Can I provide feedback to Fable mid-plan?**  
A: Yes—use "Revise plan" option. Fable rewrites with your feedback.

**Q: What if the executing model hits a blocker?**  
A: It reports the issue. You can revise the plan or manually fix it.

**Q: Can I use this with custom agents?**  
A: Yes—edit `subagent_type` in the skill to route to your agent.

**Q: Does it work with other Claude models?**  
A: Edit the skill's model names. Fable 5 / Sonnet 5 / Opus 4.8 are recommended for cost/quality, but you can use others.

**Q: What if I want to override the recommended model?**  
A: You can choose in step 3. Just note the cost difference.

---

Next: See [Examples](../examples/) for real-world walkthroughs.
