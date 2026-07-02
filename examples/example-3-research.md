# Example 3: Research & Synthesis (Content Context)

## Scenario

You're writing a technical deep-dive article: "AI Agents in Production: What Actually Works?"

This needs:
- Research across competing frameworks, companies, approaches
- Synthesizing contradictory information (Crew.ai vs. LangGraph vs. hand-rolled agents)
- Cost analysis (when to buy vs. build)
- Real production examples
- Your unique take, not just regurgitation

`/delegate` shines here: Fable plans the research structure, Opus does deep synthesis across competing sources.

## The Ask

```
/delegate

I'm writing a technical article: "AI Agents in Production: What Actually Works?"

Goal: 4000-word article with original insights on when to use 
agents, which framework/approach, cost analysis, and real examples.

Target audience: Engineering leaders deciding whether to build agents 
into their product.

Research needs:
1. Compare agent frameworks: Crew.ai, LangGraph, AutoGPT, hand-rolled
2. Production costs: framework vs. hand-rolled, including inference costs
3. Real production deployments: examples from startups/enterprises
4. Common failure modes: what breaks in production
5. When to use agents vs. prompt engineering vs. traditional code
6. Future of agents (14-month horizon)

Angle: Practical and cost-focused, not hype-driven. 
Real tradeoffs, not cheerleading for one framework.

Sources to check:
- Crew.ai and LangGraph GitHub discussions/issues
- ProdSec/HN discussions from past 6 months
- Papers/articles by Anthropic, Mistral, others
- Company blogs (Stripe, Figma, others with public agent work)

Timeline: Need first draft by Friday. Need solid research by tomorrow.

Constraints: Article should be 4000 words max, original insights, 
but synthesize all the competing claims into coherent story.
```

## Step 1: Fable Plans Research

Fable creates a research plan:

```
## Understanding

Article requires synthesizing agent frameworks and production insights 
into narrative that guides reader decisions. Not survey (just list options), 
but argument (here's what actually works and when).

Core tension to resolve: Hype (agents are magic) vs. Reality 
(agents work well for specific tasks, not universal).

## Research Structure

**Section 1: Framework Comparison**
Research: Crew.ai, LangGraph, AutoGPT, hand-rolled patterns
Sources: GitHub repos, docs, HN/Reddit discussions, product diffs
Extract: Architecture, learning curve, production support, cost
Synthesis: Trade-off matrix (simplicity vs. flexibility vs. cost)

**Section 2: Production Costs**
Research: Pricing models, inference cost per call, framework overhead
Sources: Documentation, user reports, benchmarks where available
Calculation: Total cost of ownership for small/medium/large deployments
Synthesis: Break-even point between frameworks

**Section 3: Real Examples**
Research: Find 3-4 companies publicly discussing agent deployments
Sources: Company blogs, conference talks, GitHub projects (look for case studies)
Extract: What problem they solved, which framework, how it performs
Synthesis: Common patterns in successful deployments

**Section 4: Failure Modes**
Research: What breaks in production (costs, hallucinations, latency, reliability)
Sources: GitHub issues, HN discussions, technical blog posts
Extract: Specific failure scenarios and their fixes
Synthesis: Proactive checklist for builders

**Section 5: When NOT to Use Agents**
Research: When prompt engineering or traditional code is better
Sources: Framework docs (they acknowledge limits!), HN debates
Extract: Decision criteria (task type, latency requirements, cost sensitivity)
Synthesis: Decision tree for framework choice

**Section 6: Future (14-month view)**
Research: Roadmaps, announcements, emerging approaches
Sources: Framework docs, CEO interviews, research papers
Synthesis: What's changing and why it matters

## Success Criteria

- Article grounded in real data (cost numbers, actual deployments)
- Multiple frameworks considered fairly (no cherry-picking failures)
- Clear decision framework for reader (when to use which approach)
- Original synthesis, not rehash of existing articles
- Sources cited, verifiable

## Research Challenges

- **Hype vs. Reality gap:** Many articles oversell agents
  → Mitigation: Prioritize technical discussions (GitHub, HN) over marketing

- **Limited public data:** Some companies don't publicize deployments
  → Mitigation: Use patterns from 2-3 solid examples + extrapolate

- **Frameworks evolving fast:** Prices/features changing month-to-month
  → Mitigation: Document dates, note deprecations, focus on structure not specifics

## Model Recommendation

**Opus 4.8** — This task requires:
- Synthesizing contradictory information across competing frameworks
- Identifying patterns in 50+ data points (not just listing them)
- Making judgment calls about what's important vs. hype
- Writing with original voice (not just summarizing)
- Identifying gaps and explaining implications
- Balancing technical depth with accessibility

This isn't just data gathering—it's thinking about the data.
```

## Step 2: You Review & Accept

Claude summarizes:

```
📋 RESEARCH & ARTICLE OUTLINE

Objective: Research AI agents in production (frameworks, costs, examples, 
failures, decision criteria) and synthesize into coherent 4000-word article.

Main Steps:
1. Compare frameworks: architecture, cost, production readiness
2. Analyze production costs: framework vs. hand-rolled, per-call economics
3. Find and analyze 3-4 real production deployments
4. Research common failure modes and solutions
5. Synthesize decision framework: when to use agents
6. Analyze 14-month outlook for agent tooling
7. Draft article with original synthesis, not just summary

Recommended Model: Opus 4.8
Reason: Requires synthesizing competing information, identifying patterns 
in contradictory claims, and writing original perspective. Not just data 
gathering—strategic thinking about what the data means.

⚠️ Risks:
- Some frameworks don't publicize production metrics (private data)
- Prices/features changing fast (will need update notes)
- Risk of missing emerging startups with novel approaches
```

**You choose:** "Execute with Opus 4.8 — excited to see the synthesis"

## Step 3: Opus Researches & Synthesizes

```
### Research Phase 1: Framework Comparison

Crew.ai analysis:
- Architecture: Agentic loop with tool calling, built on LangChain
- Production readiness: Mature (1.0+ released), commercial support available
- Cost: ~$0.002-0.01 per agent call (varies by model)
- Trade-off: User-friendly vs. less flexible than hand-rolled
- Source: GitHub, pricing page, HN discussion 2024-11

LangGraph analysis:
- Architecture: Graph-based workflow (more flexible than Crew)
- Production readiness: Production-ready, maintained by Anthropic
- Cost: Depends on underlying LLM; framework overhead minimal
- Trade-off: More control, steeper learning curve
- Source: Anthropic docs, LangGraph examples, tech Twitter

AutoGPT analysis:
- Architecture: Monolithic agent (older pattern)
- Production readiness: Legacy, not recommended for new builds
- Cost: High (inefficient loops, expensive model calls)
- Status: Essentially replaced by Crew/LangGraph patterns
- Source: GitHub discussions, framework comparisons

Hand-rolled patterns:
- Architecture: Custom loop, tool discovery, error handling
- Production readiness: Depends on implementation (varies widely)
- Cost: Very low framework overhead, but high dev time
- Trade-off: Full control, massive dev effort
- Source: GitHub repos, engineering blog posts, case studies

[Opus continues with detailed framework analysis...]

### Research Phase 2: Production Costs

Cost breakdown for typical deployment (1M calls/month):

Crew.ai:
- Framework overhead: ~$200/month
- LLM calls (Claude): ~$800/month (typical)
- Total: ~$1000/month (cost per call: ~$0.001)

Hand-rolled + Claude:
- Framework overhead: ~$50/month (minimal)
- LLM calls: ~$800/month (same workload)
- Total: ~$850/month (cost per call: ~$0.000085)
- Dev cost amortized: ~$5000/month (engineer time)

Finding: For high-volume (1M+ calls), cost gap small. 
For low-volume, dev time matters more than runtime cost.

Break-even: ~50k calls/month (where dev time becomes significant factor)

[Opus continues with cost modeling...]

### Research Phase 3: Real Production Examples

Example 1: Stripe (public via blog post)
- Problem: Routing customer support queries to right team
- Approach: Agent with tools for ticket search, precedent lookup
- Framework: Custom (not Crew/LangGraph)
- Results: 60% automated routing, 40% edge cases to humans
- Cost: Not disclosed, but implies ~$0.01-0.05 per call infrastructure

Example 2: Figma (from engineering blog, 2024)
- Problem: Design file analysis and suggestion generation
- Approach: Agent with vision tools for image understanding
- Framework: LangChain-based (similar to Crew architecture)
- Results: Works well for common patterns, hallucinations on novel designs
- Cost: Running inference on-device to save API costs

Example 3: Anthropic (documented in docs)
- Problem: Code generation with file modification (Claude Coder pattern)
- Approach: Agent with access to file tools, git diff tools
- Framework: LangGraph
- Results: High success rate for straightforward changes; struggles with large refactors
- Learning: Agent needs context about what's already tried (memory)

[Opus continues with synthesis of patterns...]

### Research Phase 4: Failure Modes

Common failure mode 1: Hallucinated tool calls
- What: Agent calls a tool that doesn't exist / with wrong parameters
- Cause: Model doesn't understand tool schema well enough
- Impact: Wasted tokens, broken UX, user sees error
- Fix: Stricter schema validation, simpler tool names, schema examples in prompt

Common failure mode 2: Cost spiral
- What: Agent looping, calling expensive LLM repeatedly
- Cause: No exit condition, agent doesn't realize it's stuck
- Impact: $100s per user in bad cases
- Fix: Token budgets, call limits, "give up" logic after N attempts

Common failure mode 3: Latency (agent too slow for real-time)
- What: Agent taking 5-30 seconds per call (multiple LLM round-trips)
- Cause: Each tool call needs new LLM inference
- Impact: Bad UX for synchronous queries (search, chat, suggestions)
- Fix: Batch tool calls, cache intermediate results, hybrid approach (agent for planning, traditional code for execution)

Common failure mode 4: Hallucinations in reasoning
- What: Agent makes false assumptions, reasons incorrectly
- Cause: LLM's tendency to confabulate when uncertain
- Impact: Wrong decisions, cascading errors
- Fix: Add verification steps, use tools to ground reasoning, don't trust agent output directly

[Opus continues with more failures and solutions...]

### Synthesis: Decision Framework

After analyzing all data, Opus creates decision tree:

**Use agents when:**
- Task has 3+ decision points (where reasoning helps)
- Tools are well-defined and reliable
- Some latency acceptable (seconds, not ms)
- Cost per call isn't critical
- Examples: Customer support routing, code generation, research synthesis

**DON'T use agents when:**
- Task is straightforward (just prompt engineering sufficient)
- Latency is critical (< 1 second response needed)
- Cost per call matters (millions of calls, tight budget)
- Tools are unreliable or hard to define
- Examples: Real-time chat, high-volume categorization, simple retrieval

**Hybrid approach:**
- Use agent for reasoning + planning
- Use traditional code for fast execution
- Best of both: LLMs for thinking, code for doing
```

## Step 4: Output — Research & Article Outline

Opus delivers comprehensive research + draft outline:

```
AI AGENTS IN PRODUCTION: WHAT ACTUALLY WORKS

Research Summary (for you):

Total frameworks analyzed: 6
Companies/deployments studied: 3 major + 12 HN examples
Papers/blog posts reviewed: 24
GitHub issues analyzed: 50+
Pricing models compared: 4 major frameworks

## Article Outline (4000 words)

### 1. Introduction (400 words)
- Hype vs. Reality: agents aren't magic, but specific approaches work well
- Article's angle: practical decision framework, cost analysis, real examples

### 2. What Are Agents & Why Now? (500 words)
- Definition: LLM + tools in a loop
- Why it works: LLMs are good at reasoning + planning
- Why it's hard: coordination, reliability, cost
- Competing approaches: Crew vs. LangGraph vs. hand-rolled patterns

### 3. Framework Comparison (1000 words)
- Crew.ai: Easiest, most opinionated, moderate control
- LangGraph: More flexible, from Anthropic, steeper learning curve
- Hand-rolled: Full control, expensive dev time
- Cost/complexity trade-off matrix
- Recommendation: Crew for MVP, LangGraph for production, hand-rolled for complex cases

### 4. Production Costs (500 words)
- Per-call economics: $0.0001 to $0.01 depending on approach
- Infrastructure costs: usually < 10% of LLM costs
- Break-even: hand-rolled pays off after 50k+ calls/month
- Hidden cost: operational/monitoring overhead (agents need babysitting)
- Real numbers from Stripe, Figma examples

### 5. Common Failure Modes (600 words)
- Hallucinated tools & parameters
- Cost spirals (agents looping)
- Latency (real-time requirements break agents)
- Hallucinations in reasoning
- Solutions for each

### 6. When to Use Agents (400 words)
- Decision tree: Does task fit agent profile?
- Sweet spot: 3+ decision points, well-defined tools, latency OK
- Not agents: Real-time, cost-critical, simple tasks

### 7. What's Next (14 months) (300 words)
- Agent frameworks consolidating around LLMs (Crew, LangGraph)
- Cost dropping 50% (better models, efficiency)
- Agents becoming infrastructure, not novel
- Rise of hybrid approaches (agent planning + traditional code execution)

### 8. Conclusion (200 words)
- Agents work. Specific problems, not universal.
- Pick framework based on your constraints (dev time, latency, cost).
- Monitor production closely (they fail in unexpected ways).

## Key Insights (Original Contribution)

1. **Agents are not a fundamentally new capability** — they're an interface pattern for existing LLM abilities (tool use + reasoning). The innovation is engineering, not science.

2. **The cost argument is weaker than it seems** — Per-call overhead is small enough that framework choice (Crew vs. LangGraph) matters more than "custom vs. off-shelf."

3. **Latency is the real constraint** — Agents don't work for real-time applications. Every tool call is an LLM round-trip. This is physics, not solvable by better frameworks.

4. **Hybrid is the future** — Agents for planning/reasoning (where LLMs are good), traditional code for execution (where code is fast). This pattern appears in Figma, Stripe work.

5. **Operational complexity is underestimated** — Agents need monitoring, error handling, fallbacks. Dev time increases 2-3x vs. simple prompting.

## Article Strengths

✅ Grounded in real data (cost numbers, deployments, code)
✅ Balances frameworks fairly (no picking winners)
✅ Original synthesis (not regurgitated opinions)
✅ Practical decision framework (reader can apply)
✅ Honest about limitations (when agents don't work)

## Next Steps for You

- Take outline, write sections (or assign to writer)
- Verify specific numbers if you want (I can provide sources)
- Add examples from your own work if relevant
- Article ready by Friday with this foundation
```

## Step 5: You Have the Research

Unlike business strategy (where Opus recommends decisions), this is pure research output.

**Your next move:** 
- ✅ Use the outline to write article (or delegate to writer)
- ✅ Fact-check specific numbers if needed
- ✅ Adapt tone to your publication
- ✅ Add any examples from your own work

Research is done. Writing is yours.

---

## Why This Worked

✅ **Fable planned the research** (what to look for, how to structure findings)
✅ **Opus synthesized deeply** (not just listing frameworks, but identifying patterns)
✅ **Output is actionable** (ready to write article, specific outline, original insights)
✅ **Cost-efficient** — Opus's thinking for a 4000-word piece that will reach thousands

---

## Follow-Up Tasks

After publishing, you might `/delegate`:

```
/delegate

Article got 50k views. Now I want to create a video explainer 
(10 minutes) covering the same content. Research what video 
structures work for technical content, what tools to use, 
what's the realistic production timeline for high-quality output.

Audience: Same (engineering leaders)
Constraint: Budget ~$5k for production
```

Same skill, different output type.
