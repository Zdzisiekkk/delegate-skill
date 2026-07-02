# Troubleshooting Guide

## Installation Issues

### Skill doesn't appear in `/` menu

**Check 1: Verify file location**
```bash
# Should exist:
~/.claude/skills/delegate/SKILL.md

# Verify:
ls -la ~/.claude/skills/delegate/
```

**Fix:** If missing, re-copy from the repo:
```bash
mkdir -p ~/.claude/skills/delegate
cp skill/SKILL.md ~/.claude/skills/delegate/SKILL.md
```

**Check 2: Restart Claude Code**
- CLI: Start a fresh session
- Desktop: Close completely and reopen
- VS Code: Cmd+Shift+P → "Reload Window"
- JetBrains: Restart the IDE

**Check 3: YAML syntax is valid**
Open `SKILL.md` in a text editor and check frontmatter:
```yaml
---
name: delegate
description: ...
disable-model-invocation: false
user-invocable: true
allowed-tools: Agent, AskUserQuestion
---
```

All fields required. No tabs (spaces only). Colons followed by spaces.

### "Skill not found" when calling `/delegate`

**Verify installation:** Did you restart Claude Code after installing? Try:

```bash
ls ~/.claude/skills/delegate/SKILL.md
```

If file exists but skill still doesn't load:
- Check frontmatter YAML for syntax errors (← most common)
- Try project-level installation: `./.claude/skills/delegate/SKILL.md`
- Restart again

### Skill appears but throws errors

**Error: "Agent tool not available"**
- Skill needs the `Agent` tool to work
- Verify you're in Claude Code (not another LLM interface)
- Check allowed-tools in frontmatter includes `Agent` and `AskUserQuestion`

---

## Usage Issues

### "This task is too simple for `/delegate`"

**This is expected!** The skill qualifies tasks first.

**What happened:** Your task doesn't meet the complexity threshold (typically needs 3+ independent steps).

**What to do:**
- Use Claude directly for simple tasks
- Save `/delegate` for multi-step, architectural, high-risk tasks
- See [How It Works](./how-it-works.md) for examples

### Fable's plan is vague or incomplete

**Cause:** Your task description was ambiguous. Fable needs specifics.

**Fix:**
1. Use "Revise plan" option
2. Tell Fable what's missing:
   - "Be specific about file paths"
   - "Include branching logic for cases where X happens"
   - "Spell out each config change needed"
3. Fable will regenerate with more detail

**Example input (bad):**
> "Refactor the payment module"

**Better:**
> "Refactor the payment module to support multiple payment gateways. We have Stripe, PayPal, and Square. Files: src/payment/\*. Maintain compatibility with v1.2+ of our API."

### Model recommendation seems wrong

**Example:** Task seems mechanical but recommends Opus 4.8

**Why:** Fable detected ambiguity in requirements or edge cases needing strategy.

**What to do:**
1. Accept Fable's recommendation if possible (quality is worth the cost)
2. Or use "Swap model" to try Sonnet 5
3. If Sonnet 5 fails, learn for next time (Fable was right)

**To tune this:** Edit step 6 in `skill/SKILL.md` to adjust Fable's decision logic.

---

## Execution Issues

### Execution seems to go off-plan

**Cause:** Plan had assumptions that didn't match reality (e.g., "file is at `src/auth.js`" but it's actually at `src/auth/handler.js`).

**What happens:**
- Model detects mismatch and reports it
- Doesn't blindly execute if assumptions broken
- Asks for clarification before proceeding

**What to do:**
1. Provide the missing context (actual file location, actual structure, etc.)
2. Model continues with corrected assumptions
3. Or: Cancel, fix the plan, re-run `/delegate`

**To prevent:** Make sure your task description includes correct file paths, current structure, and constraints.

### Execution takes too long

**Normal range:** 5-30 minutes depending on task complexity.

**If > 60 minutes:**
- Task might be too large for one run
- Consider breaking into 2-3 smaller `/delegate` tasks
- Monitor token usage in the status bar

**If much faster than expected:**
- Might indicate something went wrong
- Check execution output for errors
- Verify success criteria were met

### "Context window exceeded" or token errors

**Cause:** Very large task generated large plan + execution.

**Fix:**
1. Break into smaller tasks: `/delegate` part 1, then part 2
2. Or reduce scope: focus on core functionality first, then extensions
3. Clean up verbose output: ask model to be concise

---

## Cost Issues

### Execution more expensive than expected

**Verify:**
1. Was Sonnet 5 or Opus 4.8 actually used? Check the model name in output.
2. Task might have been larger than estimated.
3. Model may have regenerated sections if encountering issues.

**To reduce:**
- Use Sonnet 5 more often (tell Fable to recommend Sonnet unless truly ambiguous)
- Break large tasks into smaller `/delegate` runs
- Use Claude directly for simple tasks instead

### Planning phase was expensive

**Planning should be:** 2-5 min (relatively cheap even with Fable)

**If much longer:**
- Fable was deeply analyzing a complex task (expected)
- Or context already large before starting
- Good investment if execution will run well

---

## Model-Specific Issues

### Sonnet 5 execution fails mid-task

**Cause:** Sonnet doesn't have enough flexibility for ambiguous parts of the plan.

**Fix:**
1. Cancel and revise plan to be even more specific
2. Or re-run with Opus 4.8 (more capable with ambiguity)
3. Provide more context about edge cases in revised plan

### Opus 4.8 over-engineers the solution

**Cause:** Opus is powerful and sometimes adds features beyond the plan.

**Fix:**
1. Include "stay scoped to the plan" in execution instructions
2. Or for future tasks: Sonnet might be fine if your plan is detailed enough

---

## No Issues, But Results Unexpected

### Results are correct but look different than expected

**Cause:** Model followed plan correctly but implementation differs from what you mentally pictured.

**What to do:**
- Verify success criteria were met
- If output doesn't match success criteria → report as issue
- If output is different but still correct → this is fine; you can revise for next time

---

## Getting Help

### Still stuck?

1. **Check installation:** `ls ~/.claude/skills/delegate/SKILL.md`
2. **Review:** [How It Works](./how-it-works.md) — often the issue is in task description clarity
3. **Check examples:** [Examples](../examples/) for real working patterns
4. **Open an issue** on GitHub with:
   - Exact error message
   - Task description you used
   - Your OS and Claude Code version
   - What you expected vs what happened

### Before opening an issue:

- ✅ Restarted Claude Code
- ✅ Verified file location and YAML syntax
- ✅ Checked if task complexity threshold met
- ✅ Read relevant docs above

---

## Common Patterns

### Pattern: Vague plan → Revise → Concrete plan → Success

**This is normal.** First iteration teaches the skill about your task.

### Pattern: Sonnet tries but fails → Opus succeeds

**Indicates:** Task had more ambiguity than plan showed. For future: either make plan more detailed or recommend Opus from the start.

### Pattern: Quick qualification → No execution needed

**Means:** Skill correctly identified task as too simple. Use Claude directly next time.

---

## Platform-Specific Issues

### macOS: "Permission denied" copying skill

```bash
chmod 755 ~/.claude/skills/delegate
chmod 644 ~/.claude/skills/delegate/SKILL.md
```

### Linux: Symlink issues

If using symlinks to `.claude`, verify they're readable:
```bash
ls -la ~/.claude/skills/delegate/
```

### Windows: Path not found

Use PowerShell (not cmd.exe) and verify path exists:
```powershell
Test-Path "$env:USERPROFILE\.claude\skills\delegate"
```

---

## Advanced

### Customizing model routing rules

Edit `skill/SKILL.md`, step 2:
```
6. **Rekomendacja modelu**:
   - Sonnet 5: [your criteria]
   - Opus 4.8: [your criteria]
```

### Adding support for other models

Edit the prompt templates in steps 2 and 5 to reference different models:
```
model: claude-opus-4-1  # or your preferred model
```

Note: Tested with Fable 5 / Sonnet 5 / Opus 4.8. Other models may need tuning.

### Disable auto-invocation

In `skill/SKILL.md` frontmatter:
```yaml
disable-model-invocation: true  # Only allow manual /delegate
```

---

**Still need help?** Open an issue on [GitHub](https://github.com/zdzisiek/delegate-skill/issues) or check the main [README](../README.md).
