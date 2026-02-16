---
status: pending
priority: p3
issue_id: "005"
tags: [code-review, documentation, quality]
dependencies: ["001", "002", "003"]
---

# Address Uncompleted Acceptance Criteria

## Problem Statement

**What's broken:** The plan document has status `completed` but several acceptance criteria remain unchecked or are demonstrably false:

1. "Root level contains only: README.md, LICENSE, .gitignore, .github/" - FALSE (plan doc exists at root)
2. "All 4 skills load correctly" - NOT TESTED (can't test within nested session)
3. "CONTRIBUTING.md updated with new paths" - DOESN'T EXIST (file never existed)
4. "Cowork ZIP extraction tested and working" - NOT DONE (ZIP is stale)

**Why it matters:** This creates disconnect between stated completion and actual completion. It's a quality/honesty issue in project management.

**Business impact:** Minor - mostly an internal process issue. But matters for credibility if sharing the plan.

## Findings

**From code-simplicity-reviewer agent:**

The plan shows `status: completed` but acceptance criteria tell a different story:
- Some criteria are demonstrably false
- Some criteria were never validated
- Some criteria reference files that don't exist

This suggests either:
1. Criteria were overly ambitious, OR
2. Work was marked complete prematurely, OR
3. Criteria should have been removed when found to be N/A

## Proposed Solutions

### Solution 1: Delete the Plan (RECOMMENDED)

**Approach:**
Since the plan is being deleted anyway (see todo #003), this issue becomes moot.

**Pros:**
- Simplest resolution
- No need to fix a document being deleted

**Cons:**
- None

**Effort:** None (handled by todo #003)
**Risk:** None

### Solution 2: Update Plan Before Deletion

**Approach:**
Before deleting the plan (todo #003):
1. Remove CONTRIBUTING.md criterion (doesn't exist)
2. Mark "Root level" criterion as incomplete
3. Add note that manual testing required for skills/ZIP
4. Then delete

**Pros:**
- Git history shows accurate final state
- Honest about what was/wasn't done

**Cons:**
- Extra work for a document being deleted
- Low value

**Effort:** Small (10 minutes)
**Risk:** None

### Solution 3: Keep Plan and Fix Criteria

**Approach:**
- Don't delete plan (contradicts todo #003)
- Update all criteria to match reality
- Document what's actually done

**Pros:**
- Preserves planning artifact

**Cons:**
- Plan still clutters root
- Contradicts todo #003 recommendation
- More maintenance

**Effort:** Medium (30 minutes)
**Risk:** None

## Recommended Action

**IMPLEMENT SOLUTION 1** - This issue is automatically resolved by deleting the plan (todo #003).

If the plan is NOT deleted, implement Solution 2 to maintain integrity.

## Technical Details

**Affected files:**
- `2026-02-16-feat-restructure-marketplace-compatibility-plan.md`

**Uncompleted criteria:**
```markdown
### Functional Requirements
- [ ] Root level contains only: README.md, LICENSE, .gitignore, .github/
  # FALSE: Plan doc at root, coworkpowers.zip at root

- [ ] All 4 skills load correctly: `/coworkpowers:workflow-*`
  # NOT TESTED: Can't test in nested session

### Documentation Requirements
- [ ] CONTRIBUTING.md updated with new paths for contributors
  # N/A: File doesn't exist

### Quality Gates
- [ ] Cowork ZIP extraction tested and working
  # NOT DONE: ZIP is stale (see todo #002)
```

**Dependencies:**
- Blocks on todo #001 (marketplace.json move)
- Blocks on todo #002 (ZIP update/removal)
- Blocks on todo #003 (plan deletion)

## Acceptance Criteria

**If plan is deleted (Solution 1):**
- [ ] This issue is closed when todo #003 completes

**If plan is kept (Solution 2/3):**
- [ ] All false criteria corrected
- [ ] Non-existent criteria (CONTRIBUTING.md) removed
- [ ] Untested criteria marked with "manual testing required"
- [ ] Plan status reflects reality (active, not completed)

## Work Log

- **2026-02-16:** Issue identified during code review - uncompleted criteria
- **Next:** Resolve by implementing todo #003 (delete plan)

## Resources

- **Plan location:** `2026-02-16-feat-restructure-marketplace-compatibility-plan.md`
- **Related todos:** #003 (remove plan), #002 (ZIP issue), #001 (marketplace.json)
