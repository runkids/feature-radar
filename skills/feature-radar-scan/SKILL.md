---
name: feature-radar-scan
description: |
  Discover new feature opportunities from creative brainstorming, user feedback, ecosystem
  trends, and cross-project research. Writes results to .feature-radar/opportunities/.
  MUST use this skill when the user wants to GENERATE new ideas — not evaluate existing ones.
  Trigger on any request to brainstorm, explore, discover, or find new feature ideas, even
  casual ones like "I wonder what else we could do" or "give me ideas".
  Use when the user:
  - Asks "what else could we build?", "give me feature ideas", "what are we missing?"
  - Wants to brainstorm, explore new directions, or refresh the opportunity backlog
  - Says "scan ecosystem", "scan opportunities", "find new features"
  - Asks to review GitHub issues, community feedback, or adjacent tools for inspiration
  - Mentions "explore", "discover", or "new directions" in a feature context
  - Has a vague idea: "I have an idea", "what if we...", "I was thinking about..."
  Do NOT use for evaluating/prioritizing existing features — that's feature-radar's job.
---

# Scan Opportunities

Discover new feature opportunities and add them to `.feature-radar/opportunities/`.

## Deep Read

<HARD-GATE>
Read and follow `../feature-radar/references/DEEP-READ.md` — complete all 6 steps before proceeding.
</HARD-GATE>

## Behavioral Directives

<HARD-GATE>
Read and follow `../feature-radar/references/DIRECTIVES.md`.

Additional directive for this skill:
- **Filter aggressively** — Do NOT create opportunity files for weak signals. If you can't cite concrete demand evidence, skip it.
</HARD-GATE>

## Brainstorm Intake

<HARD-GATE>
Evaluate whether the user arrived with a vague or exploratory idea.

Enter Brainstorm Intake if ANY of these are true:
- User says "I have an idea", "what if we...", "I was thinking about...", "brainstorm"
- User describes a problem without a clear feature shape
- User's input lacks specific demand signals, impact/effort estimates, or a concrete feature name

Skip Brainstorm Intake if ALL of these are true:
- User gave a specific directive like "scan opportunities", "scan ecosystem", "find new features"
- User's input does not contain a personal idea or vague exploration

If skipping, jump directly to ## Workflow.
</HARD-GATE>

### Phase 1: Core Questions

Ask these one at a time. Prefer multiple-choice when possible.

1. **Problem space** — "你想解決什麼問題，或改善什麼體驗？"
   - Cross-reference: search existing `opportunities/` and `archive/` for related themes.
   - If a match is found, surface it: "這跟 #{nn} {title} 有關嗎？還是完全不同的方向？"
2. **Target user** — "誰會從這個功能受益？"
   - Offer choices derived from `base.md` Project Context if available.
3. **Spark** — "是什麼觸發了這個想法？"
   - (A) 自己使用時遇到的痛點
   - (B) 看到別的工具/專案有類似功能
   - (C) 技術上新的可能性（新 API、新 library）
   - (D) 社群/使用者的回饋
   - (E) 純粹的 creative exploration

### Phase 2: Adaptive Depth

After Phase 1, assess idea maturity:

**Mature** (has clear problem + user + demand signal):
→ Ask 1 closing question to confirm scope, then proceed to Exit.

**Emerging** (has problem but fuzzy shape):
→ Ask up to 3 more questions to sharpen:
  - "你想像中的使用方式大概是什麼樣子？"
  - "有沒有你看過的實作方式特別喜歡的？" (if yes, consider creating a `references/` entry)
  - "這個功能做到什麼程度你會覺得夠用？" (MVP scoping)

**Raw** (pure exploration, no clear problem yet):
→ Switch to open-ended dialogue. Ask up to 5 more questions:
  - Explore adjacent possibilities
  - Challenge assumptions: "如果不做這個，最大的損失是什麼？"
  - Seek demand signals: "有沒有人（包括你自己）反覆遇到這個問題？"
  - Stop when: a clear feature shape emerges, OR user says "enough"

### Exit: Output Options

Summarize the refined idea:

"整理一下我們剛才的討論：
- **問題：** {problem}
- **對象：** {target user}
- **方向：** {feature shape}
- **需求信號：** {demand evidence or 'creative exploration'}
- **相關項目：** {related opportunities/archive/specs, or 'none found'}"

Then ask:

"接下來你想怎麼做？"
- **(A) 直接進入 scan** — 以這個方向作為 scan 的聚焦 context，搜尋 6 個來源尋找更多佐證和相關機會
- **(B) 先存成 opportunity 草稿** — 寫入 `opportunities/{nn}-{slug}.md`，標記 Status: Open，之後再決定是否 scan

If (A): Pass the summary as context into ## Workflow Step 1, with a narrowed focus on the identified direction.
If (B): Create the opportunity file following `../feature-radar/references/SPEC.md` § 3.3, populate fields from the intake summary, then run the Annotation Checkpoint per `../feature-radar/references/WORKFLOW-PATTERNS.md`. After approval, present Completion Summary and suggest "run a focused scan around this direction" as a next step.

## Workflow

1. **Identify sources** — where to look for ideas:
   - **User signals**: issues, discussions, forum posts, support requests
   - **Creative exploration**: "what if we..." brainstorming, combining existing features in new ways
   - **Ecosystem evolution**: adjacent tools, emerging standards, new capabilities in dependencies
   - **Technical possibilities**: new APIs, libraries, or techniques that enable things previously impossible
   - **Cross-project research**: interesting approaches from related projects (from base.md Inspiration Sources)
   - **Community conversations**: Reddit, HN, Discord, blog posts
   - **If Brainstorm Intake was completed**: use the intake summary as the primary focus direction. Prioritize sources most relevant to the identified problem space. Still scan all 6 source types, but weight results toward the intake direction.
2. **Scan and collect** — for each source, look for:
   - Unmet user needs and recurring pain points
   - Feature ideas with demand signals (upvotes, comments, multiple independent asks)
   - Creative approaches that could enhance existing functionality
   - Technical breakthroughs that unlock new possibilities
   - Patterns emerging across multiple tools
3. **Deduplicate** — check against existing `opportunities/` and `archive/` files
4. **Cross-reference codebase** — for each candidate, search the project to check:
   - Already partially implemented? → mark as "Partially Done"
   - Does existing architecture support this? → note in "Design Notes"
   - Related TODOs or FIXMEs in the code? → cite them
5. **Evaluate each candidate**:

<HARD-GATE>
Before creating any opportunity file, evaluate the candidate against ALL 6 criteria.
Each criterion must be explicitly addressed — do not skip any.
</HARD-GATE>

| Criterion | Question |
|-----------|----------|
| **Real user demand** | Are users actually asking for this, or does it solve a latent need? |
| **Value uplift** | Does this meaningfully improve the user experience or unlock new possibilities? |
| **Innovation potential** | Does this introduce a creative breakthrough or unique approach? |
| **Effort / impact ratio** | Is the cost justified by the benefit? |
| **Architectural fit** | Does it align with our core philosophy? |
| **Ecosystem timing** | Is the ecosystem ready? |

6. **Create opportunity files** — for each viable candidate, write `.feature-radar/opportunities/{nn}-{slug}.md`
7. **Checkpoint — Review & Annotate** per `../feature-radar/references/WORKFLOW-PATTERNS.md`

Present scan results using this format:

```
Scan complete: {n} new opportunities
| # | Opportunity | Demand Signal | Impact | Effort | Source |
|---|------------|---------------|--------|--------|--------|
| {nn} | {title} | {evidence} | H/M/L | H/M/L | {where found} |
```

8. **Update base.md** — increment opportunities count, update Value & Innovation Landscape if needed

## Opportunity File Format

Use the format defined in `../feature-radar/references/SPEC.md` § 3.3 (`opportunities/{nn}-{slug}.md`).

## Guidelines

- Don't create opportunities for every idea you find. Filter aggressively — weak signal wastes attention.
- 1 issue with no comments = weak signal. Multiple independent asks = strong signal.
- Creative ideas without existing demand can still be valid — evaluate innovation potential separately.
- Write an honest "Our Position" — it's OK to say "we don't want this" or "not yet."
- Number sequentially from the highest existing number in `opportunities/` and `archive/`.
- If scanning reveals problems others have that we've already solved, add to `references/` instead.

## Example Output

```
→ Created opportunities/07-streaming-output.md (Impact: High, Effort: Medium)
→ Skipped: "hook system" already exists as opportunities/03-hook-system.md
→ Updated base.md: opportunities 6 → 7
```

### Brainstorm Intake Example

```
User: "I was thinking... what if we could automatically detect when a feature is getting stale?"

Phase 1:
  Q1 (Problem): "你想解決什麼問題？" → Feature opportunities sitting unreviewed
  Cross-ref: Found #05 role-assignment — user confirms: different direction
  Q2 (Target): "誰受益？" → Project maintainers managing backlogs
  Q3 (Spark): (A) 自己的痛點

Phase 2 (Emerging → 2 follow-ups):
  Q4: "使用方式？" → Periodic check, flag items older than N days with no activity
  Q5: "夠用的程度？" → Just a reminder in completion summary, no automation needed

Exit summary:
  問題: Stale opportunities go unnoticed
  對象: Project maintainers
  方向: Staleness detection in completion summaries
  需求信號: Personal pain point (single user)
  相關: None found

User chose: (B) Save as opportunity draft
→ Created opportunities/06-staleness-detection.md (Impact: Low, Effort: Low)
→ Suggested next step: "run a focused scan around staleness detection"
```

## Completion Summary

Follow the template in `../feature-radar/references/DIRECTIVES.md`, with skill name "Scan Complete".
