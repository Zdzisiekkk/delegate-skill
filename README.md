# Delegate Skill for Claude Code

A powerful Claude Code skill that optimizes complex task execution through intelligent planning and cost-efficient model routing. Perfect for multi-step projects, architectural decisions, and high-risk work.

**The Problem:** Complex tasks need Fable 5's planning power, but running the entire task through Fable is expensive. **The Solution:** Fable plans, a cheaper model (Sonnet 5 or Opus 4.8) executes. No quality loss when the plan is specific enough.

---

## Features

🎤 **Deep Interview Before Planning**
- Claude conducts thorough discovery to understand full project structure and requirements
- Filters out vague/incomplete prompts before expensive Fable planning
- Prevents budget waste on low-quality task descriptions
- Results in higher-quality plans from Fable 5

✨ **Smart Orchestration**
- Fable 5 creates detailed, step-by-step plans based on complete context
- User reviews concise summary before execution
- Recommended model selected automatically based on task type

💰 **Cost Optimization**
- Deep interview ensures only well-defined tasks reach Fable planning
- Fable 5 for strategic planning only
- Sonnet 5 for mechanical, well-defined tasks
- Opus 4.8 for nuanced, ambiguous, creative decisions
- Typically 30-50% cheaper than full Fable execution

🎯 **Handles Any Task Type**
- Code refactoring & architecture
- Business strategy & planning
- Content creation & research
- System design & migrations

⚙️ **Two Usage Modes**
- **Manual:** `/delegate <task description>`
- **Auto:** Claude suggests `/delegate` for complex tasks automatically

---

## Quick Start

### Installation

1. **Copy the skill** to your Claude Code skills directory:
   - **User-level** (all projects): `~/.claude/skills/delegate/`
   - **Project-level** (specific project): `.claude/skills/delegate/`

2. **Place the file:**
   ```
   ~/.claude/skills/delegate/
   └── SKILL.md
   ```

3. **Done.** Invoke with `/delegate` in any conversation.

See [Installation Guide](./docs/installation.md) for detailed setup.

---

## Usage

### Manual Mode
```
/delegate Refactor the authentication module while maintaining backward compatibility
```

### What Happens

1. **Deep interview** — Claude asks about project structure, requirements, and constraints until fully understood
2. **Fable 5 plans** — creates detailed, step-by-step execution plan based on clear requirements
3. **You review** — concise summary with key steps + recommended model
4. **Choose** — accept plan, switch model, request changes, or cancel
5. **Model executes** — Sonnet 5 or Opus 4.8 runs the plan exactly
6. **Done** — brief report of what was accomplished

### Automatic Mode

Claude will proactively suggest `/delegate` when detecting:
- Multi-step, strategic tasks (3+ independent parts)
- High-risk decisions (architectural, business-critical)
- Ambiguous requirements needing deep analysis

---

## When to Use

### ✅ Great for `/delegate`

- Refactoring large modules with backward compatibility requirements
- Designing multi-service system migrations
- Architecting new features across multiple components
- Complex business strategy requiring scenario analysis
- Research with competing sources requiring synthesis
- Compliance/security audit with multiple touchpoints

### ❌ Not Worth It

- Simple bug fixes ("fix typo", "update variable name")
- Single-function implementations
- Straightforward queries or lookups
- Tasks that fit in 5 minutes

---

## How It Works

### Step 1: Qualification
Ensures the task is actually complex enough to warrant the overhead (typically 2-3 min planning time).

### Step 2: Deep Interview
**Before expensive Fable planning, Claude conducts a thorough interview to prevent wasted budget.**

Claude asks questions until fully understanding:
- **Project structure** — architecture, technologies, existing components, data model
- **Business goal** — what exactly needs to be achieved and why
- **Functional requirements** — specific behaviors (not vague: "form with validation for X" not "make UI")
- **Non-functional requirements** — performance, security, accessibility, deadline, budget constraints
- **Context** — who uses this, what are use cases and edge cases
- **Constraints** — what cannot change, dependencies, failure modes

This filters out vague/incomplete prompts before they reach Fable. **No garbage in → no wasted budget.**

### Step 3: Planning with Fable 5
Fable analyzes armed with complete context:
- Task scope and dependencies (now clearly defined)
- Files/data that need examination
- Edge cases and branching logic
- Success criteria
- Risks and mitigations
- **Model recommendation** (Sonnet vs Opus with reasoning)

Result: Detailed, concrete, unambiguous plan ready for execution.

### Step 4: Review & Accept
User sees:
- **Objective** (1 sentence)
- **Main steps** (3-4 bullet points)
- **Recommended model** (with Fable's reasoning)
- **Key risks** (if any)

User chooses: Execute | Swap model | Revise plan | Cancel

### Step 5: Execution
Recommended model receives **full, detailed plan** from Fable and executes step-by-step. Reports any deviations from plan assumptions.

### Step 6: Report
Brief summary of what was accomplished. No unnecessary plan repetition.

---

## Examples

See [Examples](./examples/) for full walkthroughs:

- **Code Refactoring** — Multi-file module update with backward compatibility
- **Business Strategy** — Market entry planning with competitive analysis
- **Research & Synthesis** — Gathering and synthesizing competing sources

---

## Model Selection Guide

**Sonnet 5 (Recommended for):**
- Implementation following clear specifications
- Code refactoring with well-defined requirements
- Mechanical transformations (rename, restructure, format)
- Predictable, deterministic tasks

**Opus 4.8 (Recommended for):**
- Ambiguous requirements needing interpretation
- Creative solutions and design decisions
- Complex judgment calls between competing approaches
- Deep synthesis of contradictory information
- Tasks requiring understanding of subtle tradeoffs

---

## Installation Details

### For Claude Code CLI / Desktop

Place the skill in:
```bash
# User-level (all projects)
~/.claude/skills/delegate/SKILL.md

# OR Project-level (specific project)
/path/to/project/.claude/skills/delegate/SKILL.md
```

### For Claude Code VS Code Extension

Extensions inherit `~/.claude/skills/`, so user-level installation covers all projects using the extension.

See [Installation Guide](./docs/installation.md) for platform-specific instructions.

---

## Troubleshooting

**Skill doesn't appear after installation?**
- Restart Claude Code / IDE extension
- Check the skill is in the right directory: `~/.claude/skills/delegate/SKILL.md`
- Verify frontmatter is valid YAML

**Fable creates a vague plan?**
- This means the task itself is ambiguous
- Use "Revise plan" option to give Fable clearer requirements
- Be specific: "maintain backward compatibility with versions 1.5+" not "don't break things"

**Model runs out of context?**
- Simplify the plan into smaller steps
- For very large tasks, consider breaking into 2-3 separate `/delegate` runs

**Wrong model was recommended?**
- You can always swap before executing
- Use "Swap model" to choose the other option
- Please open an issue with task details for tuning

See [Troubleshooting Guide](./docs/troubleshooting.md) for more.

---

## Contributing

We welcome improvements! This skill benefits from:
- Real-world usage feedback and edge cases
- Better task qualification heuristics
- Improved model routing rules
- Documentation clarifications

See [CONTRIBUTING.md](./CONTRIBUTING.md) for guidelines.

---

## License

MIT License — feel free to use, modify, and distribute.

See [LICENSE](./LICENSE) for details.

---

## Questions?

- **How do I customize it for my workflow?** See [How It Works](./docs/how-it-works.md) — the prompt sections are designed to be adapted.
- **Can I add my own model routing rules?** Yes — edit the model recommendation logic in step 2.
- **Does it work with custom agents?** Yes, adapt the `subagent_type` parameter in the skill.

---

**Built for Anthropic Claude Code.** Learn more at [claude.ai/code](https://claude.ai/code)
