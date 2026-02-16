---
status: pending
priority: p3
issue_id: "007"
tags: [code-review, documentation, metadata, marketplace]
dependencies: []
---

# Tags Discrepancy Between plugin.json and marketplace.json

## Problem Statement

The `plugin.json` file defines 6 keywords, while `marketplace.json` only includes 4 tags. This inconsistency could affect plugin discoverability in the marketplace and may confuse users about the plugin's categorization.

**Why it matters:** Consistent metadata ensures better discoverability and professional presentation in the marketplace.

## Findings

**Current State:**
- **plugin.json keywords (6):**
  - `knowledge-work`
  - `productivity`
  - `compound-learning`
  - `decision-making`
  - `research`
  - `planning`

- **marketplace.json tags (4):**
  - `knowledge-work`
  - `productivity`
  - `compound-learning`
  - `decision-making`

**Missing from marketplace.json:**
- `research`
- `planning`

**Impact Assessment:**
- **Severity:** Low - Cosmetic/metadata issue
- **User Impact:** Reduced discoverability in marketplace search
- **Functionality Impact:** None (plugin works fine)

## Proposed Solutions

### Solution 1: Add Missing Tags to marketplace.json (Recommended)
**Action:** Add "research" and "planning" tags to marketplace.json

**Pros:**
- Complete feature set represented
- Better search discoverability
- Consistent with plugin.json
- More accurate categorization

**Cons:**
- None identified

**Effort:** Tiny (2 minutes)
**Risk:** None

**Implementation:**
```json
{
  "plugins": [{
    "tags": [
      "knowledge-work",
      "productivity",
      "compound-learning",
      "decision-making",
      "research",
      "planning"
    ]
  }]
}
```

### Solution 2: Remove Tags from plugin.json
**Action:** Reduce plugin.json keywords to match marketplace.json (4 tags)

**Pros:**
- Simpler, more focused tagging
- Matches current marketplace.json

**Cons:**
- Loses "research" and "planning" descriptors
- Less discoverable for those specific use cases
- Doesn't represent full feature set

**Effort:** Tiny (2 minutes)
**Risk:** Low (reduces discoverability)

### Solution 3: Document Intentional Difference
**Action:** Add comment to marketplace.json explaining why tags differ

**Pros:**
- Preserves current state
- Documents decision

**Cons:**
- Doesn't solve discoverability issue
- Comments not supported in JSON

**Effort:** N/A (not viable)
**Risk:** N/A

## Recommended Action

**Choose Solution 1** (add missing tags to marketplace.json) because:
1. Research and planning are core features of the plugin
2. Better marketplace discoverability
3. No downside to more accurate tagging
4. Takes 2 minutes to fix

## Technical Details

**Affected Files:**
- `.claude-plugin/marketplace.json` (line 21)

**Change Required:**
```diff
- "tags": ["knowledge-work", "productivity", "compound-learning", "decision-making"]
+ "tags": ["knowledge-work", "productivity", "compound-learning", "decision-making", "research", "planning"]
```

## Acceptance Criteria

- [ ] marketplace.json includes all 6 tags
- [ ] Tags match plugin.json keywords exactly
- [ ] JSON remains valid (test with `jq`)
- [ ] Marketplace structure unchanged

## Work Log

### 2026-02-16
- **Discovered:** Plugin validation review found tag count mismatch
- **Impact:** Reduced marketplace discoverability
- **Next:** Add missing tags to marketplace.json

## Resources

- **Review Report:** Plugin Structure Validation (agent af727f6)
- **Files:**
  - `plugins/coworkpowers/.claude-plugin/plugin.json`
  - `.claude-plugin/marketplace.json`
- **Context:** v2.0.0 marketplace restructure
