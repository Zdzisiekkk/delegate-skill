# Installation Guide

## Quick Setup (2 minutes)

### 1. Download the Skill

Clone or download this repository:

```bash
git clone https://github.com/zdzisiek/delegate-skill.git
```

Or download the ZIP file from GitHub and extract it.

### 2. Copy to Claude Code

**Option A: User-level (recommended — all projects)**

Copy the `skill` folder to your Claude Code skills directory:

```bash
# macOS / Linux
mkdir -p ~/.claude/skills/delegate
cp skill/SKILL.md ~/.claude/skills/delegate/

# Windows (PowerShell)
mkdir -Path "$env:USERPROFILE\.claude\skills\delegate" -Force
Copy-Item "skill/SKILL.md" -Destination "$env:USERPROFILE\.claude\skills\delegate\"
```

**Option B: Project-level (specific project only)**

If you want the skill available in just one project:

```bash
# Inside your project directory
mkdir -p .claude/skills/delegate
cp skill/SKILL.md .claude/skills/delegate/
```

### 3. Restart Claude Code

- **CLI:** Restart your session
- **Desktop App:** Restart the application
- **VS Code Extension:** Reload the extension (Cmd+Shift+P → "Reload Window")

### 4. Verify Installation

In any Claude Code chat, type:

```
/delegate
```

If the skill loads, you'll see it in the skill list. If not, check the troubleshooting section below.

---

## Detailed Setup by Platform

### macOS

```bash
# Create directories
mkdir -p ~/.claude/skills/delegate

# Copy skill file
cp skill/SKILL.md ~/.claude/skills/delegate/SKILL.md

# Verify
ls ~/.claude/skills/delegate/
# Should output: SKILL.md
```

### Linux

Same as macOS:

```bash
mkdir -p ~/.claude/skills/delegate
cp skill/SKILL.md ~/.claude/skills/delegate/SKILL.md
```

### Windows (PowerShell)

```powershell
# Create directories
New-Item -ItemType Directory -Path "$env:USERPROFILE\.claude\skills\delegate" -Force

# Copy skill file
Copy-Item "skill\SKILL.md" -Destination "$env:USERPROFILE\.claude\skills\delegate\"

# Verify
Get-ChildItem "$env:USERPROFILE\.claude\skills\delegate\"
# Should output: SKILL.md
```

---

## IDE-Specific Setup

### Claude Code CLI

1. Copy the skill to `~/.claude/skills/delegate/SKILL.md`
2. Use `/delegate <task>` in any project

### Claude Code Desktop App

1. Copy the skill to `~/.claude/skills/delegate/SKILL.md`
2. Skills are auto-loaded from `~/.claude/skills/`
3. Use `/delegate <task>` in chat

### VS Code Extension

1. Copy the skill to `~/.claude/skills/delegate/SKILL.md`
2. The extension inherits from `~/.claude/skills/`
3. Reload the extension (Cmd+Shift+P → "Reload Window")
4. Use `/delegate <task>` in the extension chat

### Other JetBrains IDEs (IntelliJ, PyCharm, etc.)

1. Copy the skill to `~/.claude/skills/delegate/SKILL.md`
2. Restart the IDE plugin
3. Use `/delegate <task>` in the IDE chat

---

## Updating

To update to a newer version:

```bash
# Navigate to your delegate-skill directory
cd delegate-skill

# Pull latest changes
git pull origin main

# Copy updated SKILL.md
cp skill/SKILL.md ~/.claude/skills/delegate/
```

---

## Uninstalling

Simply remove the skill directory:

```bash
# macOS / Linux
rm -rf ~/.claude/skills/delegate

# Windows (PowerShell)
Remove-Item "$env:USERPROFILE\.claude\skills\delegate" -Recurse
```

---

## Troubleshooting Installation

### Skill doesn't appear after installation

**Check 1: File location**
```bash
ls ~/.claude/skills/delegate/SKILL.md
# Should exist
```

**Check 2: Restart Claude Code**
- CLI: Start a new session
- Desktop: Full restart (not just close)
- VS Code: Cmd+Shift+P → "Reload Window"

**Check 3: YAML syntax**
Open `SKILL.md` and verify the frontmatter is valid:
```yaml
---
name: delegate
description: ...
disable-model-invocation: false
user-invocable: true
allowed-tools: Agent, AskUserQuestion
---
```

### "Skill not found" error

1. Verify the file path: `~/.claude/skills/delegate/SKILL.md`
2. Check file permissions: `ls -l ~/.claude/skills/delegate/SKILL.md`
3. Try user-level installation instead of project-level

### Permission denied when copying

```bash
# macOS / Linux: Add write permissions
chmod 644 ~/.claude/skills/delegate/SKILL.md
```

### Still not working?

Check Claude Code's system requirements:
- Latest version of Claude Code / extension
- `.claude/` directory exists and is readable
- No conflicting skills with the same name

For more help, see [Troubleshooting Guide](./troubleshooting.md) or open an issue on GitHub.

---

## Next Steps

Once installed:

1. Read [How It Works](./how-it-works.md) to understand the workflow
2. See [Examples](../examples/) for real-world usage
3. Try `/delegate` on a complex task in your project

Questions? See [Troubleshooting](./troubleshooting.md) or check the main [README](../README.md).
