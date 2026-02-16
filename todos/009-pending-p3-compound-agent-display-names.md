---
status: pending
priority: p3
issue_id: "009"
tags: [code-review, documentation, clarity, cosmetic]
dependencies: []
---

# Compound Agent Display Names Differ from Filenames

## Problem Statement

The `workflow-compound/SKILL.md` uses display names like "Template Assessor" and "Preference Detector" while the actual filenames are `template-creator.md` and `preference-learner.md`. This inconsistency could confuse developers and make the codebase harder to navigate.

**Why it matters:** Consistent naming between documentation and code improves maintainability and reduces cognitive load when working with the codebase.

## Findings

**Naming Mismatches:**

| Display Name (SKILL.md) | Actual Filename | Match? |
|-------------------------|-----------------|--------|
| Pattern Extractor | `pattern-extractor.md` | ✅ |
| Template Assessor | `template-creator.md` | ❌ |
| Preference Detector | `preference-learner.md` | ❌ |
| Failure Analyzer | `failure-analyzer.md` | ✅ |
| Knowledge Curator | `knowledge-curator.md` | ✅ |

**Locations:**
- `workflow-compound/SKILL.md` lines 23, 29, 34

**Impact Assessment:**
- **Severity:** Very Low - Cosmetic/clarity issue
- **Functionality Impact:** None (agents load correctly)
- **User Impact:** Minor confusion for contributors/maintainers
- **Developer Impact:** Slightly harder to trace references

## Proposed Solutions

### Solution 1: Update SKILL.md Display Names to Match Filenames (Recommended)
**Action:** Change display names in SKILL.md to match actual filenames

**Changes:**
- "Template Assessor" → "Template Creator"
- "Preference Detector" → "Preference Learner"

**Pros:**
- Single file change
- Maintains accurate filenames
- More descriptive names (creator/learner vs assessor/detector)
- No code changes required

**Cons:**
- None identified

**Effort:** Tiny (2 minutes)
**Risk:** None

### Solution 2: Rename Files to Match Display Names
**Action:** Rename files to match SKILL.md display names

**Changes:**
- `template-creator.md` → `template-assessor.md`
- `preference-learner.md` → `preference-detector.md`

**Pros:**
- SKILL.md stays unchanged

**Cons:**
- Less descriptive names ("assessor" and "detector" are more passive)
- Git history requires careful preservation (git mv)
- Multiple file changes
- May affect other references

**Effort:** Small (10 minutes with testing)
**Risk:** Low (could miss references)

### Solution 3: Document the Mapping
**Action:** Add comment to SKILL.md explaining the intentional difference

**Pros:**
- Preserves both names
- Documents decision

**Cons:**
- Doesn't solve confusion
- Perpetuates inconsistency

**Effort:** Tiny
**Risk:** None but unhelpful

## Recommended Action

**Choose Solution 1** (update display names in SKILL.md) because:
1. "Creator" and "Learner" are more accurate than "Assessor" and "Detector"
2. Single file change with no code impact
3. Maintains consistency across codebase
4. Simpler than renaming files

## Technical Details

**Affected Files:**
- `plugins/coworkpowers/skills/workflow-compound/SKILL.md` (lines 23, 29, 34)

**Changes Required:**

```diff
Line 23:
- The **Pattern Extractor** looks for successful approaches that could apply elsewhere. The **Template Assessor** identifies reusable
+ The **Pattern Extractor** looks for successful approaches that could apply elsewhere. The **Template Creator** identifies reusable

Line 29:
- - **Template Assessor** (templates): Saves successful structures for reuse
+ - **Template Creator** (templates): Saves successful structures for reuse

Line 34:
- - **Preference Detector** (preferences): Captures style and tone preferences
+ - **Preference Learner** (preferences): Captures style and tone preferences
```

**Verification:**
After changes, grep for old names to ensure no other references:
```bash
grep -r "Template Assessor" plugins/coworkpowers/
grep -r "Preference Detector" plugins/coworkpowers/
```

## Acceptance Criteria

- [ ] All display names in workflow-compound/SKILL.md match filenames
- [ ] No references to "Template Assessor" remain
- [ ] No references to "Preference Detector" remain
- [ ] Agent functionality unchanged
- [ ] Documentation reads naturally with new names

## Work Log

### 2026-02-16
- **Discovered:** Plugin validation review found display name mismatches
- **Impact:** Minor confusion for maintainers/contributors
- **Next:** Update SKILL.md to use "Template Creator" and "Preference Learner"

## Resources

- **Review Report:** Plugin Load Simulation (agent a2552c6)
- **Files:**
  - `plugins/coworkpowers/skills/workflow-compound/SKILL.md`
  - `plugins/coworkpowers/agents/compound/template-creator.md`
  - `plugins/coworkpowers/agents/compound/preference-learner.md`
- **Type:** Documentation consistency improvement
