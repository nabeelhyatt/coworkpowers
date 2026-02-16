---
status: pending
priority: p2
issue_id: "006"
tags: [code-review, plugin-structure, agent-loading]
dependencies: []
---

# Devil's Advocate Apostrophe Inconsistency

## Problem Statement

The `devils-advocate.md` agent filename is missing an apostrophe, while SKILL.md references it as `devil's-advocate` (with apostrophe). This naming mismatch could prevent the agent from loading correctly when the workflow-review skill tries to invoke it.

**Why it matters:** Agent loading failures would break the review workflow, preventing users from getting comprehensive code reviews.

## Findings

**Agent Discovery:**
- **Actual filename:** `plugins/coworkpowers/agents/review/devils-advocate.md` (no apostrophe)
- **SKILL.md reference:** `devil's-advocate` (with apostrophe)
- **Locations:** `workflow-review/SKILL.md` lines 22, 23, 120

**Impact Assessment:**
- **Severity:** Medium - Could cause agent loading failures
- **Likelihood:** High - Reference doesn't match filename
- **User Impact:** Review workflow would fail or skip this agent

**Related Findings:**
- All other 23 agents have correctly matching names
- This is the only filename/reference mismatch in the plugin

## Proposed Solutions

### Solution 1: Rename File to Include Apostrophe (Recommended)
**Action:** Rename `devils-advocate.md` → `devil's-advocate.md`

**Pros:**
- Grammatically correct (possessive form of "devil")
- Matches SKILL.md expectations
- More discoverable naming

**Cons:**
- Apostrophes in filenames can cause issues on some filesystems
- Git mv required to preserve history

**Effort:** Small (5 minutes)
**Risk:** Low (single file rename)

**Implementation:**
```bash
cd plugins/coworkpowers/agents/review
git mv devils-advocate.md devil\'s-advocate.md
git commit -m "fix: rename devils-advocate to include apostrophe"
```

### Solution 2: Update SKILL.md References to Remove Apostrophe
**Action:** Update `workflow-review/SKILL.md` to reference `devils-advocate`

**Pros:**
- Safer for cross-platform compatibility
- No special characters in filename
- Simpler filesystem handling

**Cons:**
- Grammatically incorrect
- Requires updating multiple references in SKILL.md

**Effort:** Small (5 minutes)
**Risk:** Low (text replacement)

**Implementation:**
- Update all references in `workflow-review/SKILL.md`
- Search for `devil's-advocate` and replace with `devils-advocate`

### Solution 3: Test Current Behavior First
**Action:** Load plugin and test if Claude Code resolves the mismatch automatically

**Pros:**
- May not be an actual issue if loader is flexible
- Avoids unnecessary changes

**Cons:**
- Delays resolution
- Risk of discovering issue in production

**Effort:** Medium (requires testing environment)
**Risk:** Medium (might waste time if it's actually broken)

## Recommended Action

**Choose Solution 1** (rename file to include apostrophe) because:
1. It's grammatically correct
2. Claude Code should handle apostrophes in filenames fine on modern systems
3. Matches the SKILL.md expectation
4. Git mv preserves history

## Technical Details

**Affected Files:**
- `plugins/coworkpowers/agents/review/devils-advocate.md` (to be renamed)
- `plugins/coworkpowers/skills/workflow-review/SKILL.md` (references this agent)

**Testing Criteria:**
After fix, verify:
```bash
# 1. Check file exists with apostrophe
ls -la plugins/coworkpowers/agents/review/devil\'s-advocate.md

# 2. Load plugin and test review workflow
claude --plugin-dir ./plugins/coworkpowers
/coworkpowers:workflow-review "test code review"

# 3. Verify agent is invoked (check logs)
```

## Acceptance Criteria

- [ ] File renamed to `devil's-advocate.md` with apostrophe
- [ ] Git history preserved using `git mv`
- [ ] SKILL.md references continue to work
- [ ] Plugin loads without errors
- [ ] Review workflow successfully invokes the devil's advocate agent
- [ ] All other agent references remain functional

## Work Log

### 2026-02-16
- **Discovered:** Plugin validation review identified filename/reference mismatch
- **Impact:** Could prevent agent loading in review workflow
- **Next:** Decide on solution and implement fix

## Resources

- **Review Report:** Plugin Load Simulation (agent a2552c6)
- **Agent File:** `plugins/coworkpowers/agents/review/devils-advocate.md`
- **SKILL File:** `plugins/coworkpowers/skills/workflow-review/SKILL.md`
- **Issue Type:** Plugin structure validation
