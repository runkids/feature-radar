---
name: feature-radar-validate
description: |
  Validate SKILL.md frontmatter and .feature-radar/ files against format rules. Runs validate.sh,
  reports errors/warnings, and offers to auto-fix what it can. Use this proactively after editing
  any SKILL.md or .feature-radar/ file — catching format issues early prevents runtime bugs
  (like the 1024-char description limit that broke skill registration).
  Use when:
  - User says "validate", "check format", "run validation", or "lint skills"
  - You just edited a SKILL.md file (description, name, or body)
  - You just created or modified files in .feature-radar/
  - Before committing changes that touch skills/ or .feature-radar/
  Trigger phrases: "validate", "check format", "lint", "run validation",
  "verify skills", "check skill format", "are my skills valid"
---

# Validate Feature Radar

Run `scripts/validate.sh` (bundled with this skill) to check SKILL.md frontmatter and `.feature-radar/` SPEC compliance, then fix any issues found.

## Why This Matters

The `description` field in SKILL.md has a hard 1024-character limit enforced by the skill registry. Exceeding it silently breaks skill registration. Similarly, `.feature-radar/` files must follow SPEC.md naming and metadata conventions or downstream tools can't parse them. This skill catches these issues before they cause problems.

## Workflow

### Step 1: Run Validation

```bash
bash skills/feature-radar-validate/scripts/validate.sh
```

Read the full output. Note the exit code:
- **Exit 0**: all checks passed (may still have warnings)
- **Exit 1**: errors found — must be fixed

### Step 2: Report Results

Present the results clearly:

```
── Feature Radar: Validate ──

Errors:   {n}
Warnings: {n}

{List each error/warning with file path and issue}
```

If everything passes, say so and stop. No further action needed.

### Step 3: Auto-Fix (if errors or warnings found)

For each issue, apply the appropriate fix:

| Issue | Fix Strategy |
|-------|-------------|
| `description` > 1024 chars | Trim to fit — cut the least essential trigger phrases or examples first, keep the core "what it does" and "Use when" intact. Show before/after char count. |
| `description` missing "Use when" | Add a "Use when:" section based on the skill's purpose |
| `name` not kebab-case | Rename to kebab-case |
| `name` missing | Derive from directory name |
| Body > 500 lines | Flag for user — this requires judgment about what to extract into reference files |
| Filename not `{nn}-{slug}.md` | Rename file to correct format |
| Missing `**Status**:` / `**Impact**:` / `**Effort**:` | Add field with a placeholder value, ask user to confirm |
| `base.md` count mismatch | Update the Tracking Summary table counts |

After fixing, re-run `bash skills/feature-radar-validate/scripts/validate.sh` to confirm all errors are resolved.

### Step 4: Completion Summary

```
── Feature Radar: Validate Complete ──

Files fixed:   ~ {path} ({what changed})
Errors fixed:  {n}
Warnings fixed: {n}
Remaining:     {n} (need user input)
```

## Proactive Triggering

When you notice yourself editing `skills/*/SKILL.md` or `.feature-radar/**/*.md`, run validation afterward without being asked. A quick `bash skills/feature-radar-validate/scripts/validate.sh` check takes seconds and prevents silent breakage.
