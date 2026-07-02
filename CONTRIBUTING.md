# Contributing to Delegate

Thanks for interest in improving Delegate! This skill is for everyone, and improvements come from real-world usage.

## Ways to Contribute

### 1. Report Issues

Found a bug or something confusing?

**Open an issue** on GitHub with:
- What you tried (the task you gave Delegate)
- What you expected to happen
- What actually happened
- Your OS and Claude Code version
- Error messages (if any)

Example:
```
Title: Fable plan too vague for database migration task

Description:
Task: Migrate our PostgreSQL schema to add new columns and migrate data
Fable created plan with generic steps ("update schema", "backfill data")
Expected: Concrete steps like "alter table users add column..., update users set..."
Actual: Had to revise plan 3 times to get concrete enough for execution

OS: macOS 14.4, Claude Code CLI 1.2.0
```

### 2. Suggest Improvements

Ideas for making the skill better?

**Open an issue with label `enhancement`:**
- Better model routing rules (when to recommend Sonnet vs. Opus)
- Improved qualification criteria (should simpler tasks qualify?)
- New workflow steps
- Better documentation

Example:
```
Title: Auto-suggest smaller tasks when current task is too large

Idea: If Fable detects that a task exceeds token budget or has 
10+ steps, proactively suggest breaking into 2-3 smaller /delegate runs.
This would help prevent mid-execution failures.
```

### 3. Share Real-World Usage

Used `/delegate` successfully? Tell us!

**Open an issue with label `feedback`:**
- What task did you use it for?
- Which models (Fable + Sonnet/Opus)?
- Did the output meet expectations?
- What surprised you?
- Would you use it again?

Real feedback helps us understand what works and what doesn't.

### 4. Improve Documentation

See unclear sections in the docs? Help clarify!

**Options:**
- Small fixes (typos, clarifications): Open a PR directly
- Large rewrites (restructuring sections): Open an issue first to discuss

Documentation lives in `docs/` and examples in `examples/`.

### 5. Add Examples

Have a great use case for `/delegate`?

**Contribute an example:** Create a new markdown file in `examples/`:

```markdown
# Example N: [Task Type]

## Scenario
[What problem this solves]

## The Ask
[Example /delegate input]

## Results
[What output you got, what you learned]

## Why This Worked
[Key insights for others]
```

See existing examples for format.

---

## Development & Testing

If you want to modify the skill itself:

### Local Testing

1. **Edit `skill/SKILL.md`** with your changes

2. **Copy to your Claude Code:**
   ```bash
   cp skill/SKILL.md ~/.claude/skills/delegate/SKILL.md
   ```

3. **Restart Claude Code** and test

4. **Test a real task** with your changes to verify it still works

### Things to Test

- Does Fable create plans (not execute)?
- Do plan summaries fit in 5-10 lines?
- Do user options make sense (accept, swap model, revise, cancel)?
- Does recommended model make sense based on task?

### Pull Request Process

1. **Fork the repo** and create a branch:
   ```bash
   git checkout -b improve/better-model-routing
   ```

2. **Make your changes** (skill + tests + docs)

3. **Test locally** (copy to `~/.claude/skills/delegate/` and verify)

4. **Write clear commit message:**
   ```
   Improve model selection logic for code tasks
   
   Previously recommended Opus for all refactoring tasks.
   Now distinguishes between:
   - Mechanical refactoring (well-defined) → Sonnet
   - Complex refactoring (ambiguous requirements) → Opus
   
   Tested with: payment module refactor, API consolidation
   ```

5. **Push and open a PR** with:
   - Clear title
   - Description of changes
   - Why this improves Delegate
   - Test results

6. **Respond to feedback** and iterate

### Code Style

- **Skill prompt (SKILL.md):** Clear, concise instructions. Polish for readability.
- **Documentation:** Plain English, analogies > jargon, examples > theory
- **Examples:** Real, not contrived. Show where Delegate shines AND when it doesn't.

---

## Guidelines

### What We Welcome

✅ Bug reports with details  
✅ Documentation improvements  
✅ Real-world examples  
✅ Model routing enhancements based on usage data  
✅ Workflow improvements grounded in actual use  

### What We Avoid

❌ Over-engineering (Delegate should stay simple)  
❌ Adding features for hypothetical use cases  
❌ Changing model recommendations without testing  
❌ PRs that assume one "right way" to use agents  

---

## Discussion

Have thoughts but not quite a bug or feature?

**Start a Discussion** on GitHub (Discussions tab) to chat about:
- Whether Delegate should work for X type of task
- Best practices you've discovered
- Questions about how Delegate works
- Ideas for improving something

Discussions are lower-friction than issues and great for brainstorming.

---

## Credit

All contributors will be credited in:
- `CHANGELOG.md` (if we add one)
- README acknowledgments section

If you prefer not to be credited, just mention in your PR.

---

## Questions?

- **How do I...?** — Check [Installation](./docs/installation.md) or [How It Works](./docs/how-it-works.md)
- **Is this a bug?** — See [Troubleshooting](./docs/troubleshooting.md)
- **Something else?** — Open a Discussion or issue

---

## Thank You

Delegate works better because people like you use it, find edge cases, suggest improvements, and share what works.

That's how skills get better. Thanks for being part of it.
