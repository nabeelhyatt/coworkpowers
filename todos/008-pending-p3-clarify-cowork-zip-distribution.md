---
status: pending
priority: p3
issue_id: "008"
tags: [code-review, documentation, installation, cowork]
dependencies: []
---

# Clarify Cowork ZIP Distribution Plan

## Problem Statement

The README.md states "The previous `coworkpowers.zip` has been removed" but doesn't specify where users should look for the updated v2.0.0 ZIP when it becomes available. MIGRATION.md provides a ZIP generation command but doesn't clarify whether users should generate it themselves or wait for an official release.

**Why it matters:** Users familiar with v1.x Cowork installation may be confused about how to install v2.0.0 in Claude Desktop (Cowork).

## Findings

**Current Documentation:**
- **README.md:** "⚠️ **Note:** Cowork installation is pending testing with the v2.0.0 structure. The previous `coworkpowers.zip` has been removed..."
- **MIGRATION.md:** Provides ZIP generation command but labels it "If you have Cowork access and want to test"
- **Status:** No clear guidance on where to find official ZIP when ready

**User Confusion Points:**
1. Should users generate their own ZIP?
2. Where will the official ZIP be published?
3. When will it be available?
4. How will users know when it's ready?

**Impact Assessment:**
- **Severity:** Low - Alternative installation method exists (Claude Code)
- **User Impact:** Confusion for Cowork users, may generate incorrect ZIPs
- **Functionality Impact:** None (plugin works in Claude Code)

## Proposed Solutions

### Solution 1: Add GitHub Releases Reference (Recommended)
**Action:** Update README.md to specify GitHub Releases as distribution point

**Pros:**
- Standard distribution mechanism
- Versioned releases
- Downloadable assets
- Clear update path

**Cons:**
- Requires creating actual release when ready

**Effort:** Small (5 minutes to update docs)
**Risk:** Low

**Implementation:**
Add to README.md Cowork section:
```markdown
> ⚠️ **Note:** Cowork installation is pending testing with the v2.0.0 structure.
> A tested v2.0.0 ZIP will be provided in [GitHub Releases](https://github.com/nabeelhyatt/coworkpowers/releases)
> once validation is complete. Subscribe to releases to be notified when it's ready.
```

### Solution 2: Provide Self-Service Instructions
**Action:** Update docs to clearly state users can generate their own ZIP

**Pros:**
- Empowers advanced users
- No waiting for official release
- Good for testing

**Cons:**
- Risk of incorrect ZIPs
- No quality control
- Support burden for user-generated ZIPs

**Effort:** Small (5 minutes)
**Risk:** Medium (support issues)

### Solution 3: Remove Cowork Installation Until Ready
**Action:** Remove Cowork section entirely until ZIP is validated

**Pros:**
- No confusion
- No partial information

**Cons:**
- Users lose important context
- Doesn't help v1.x users migrate

**Effort:** Tiny (2 minutes)
**Risk:** Low but unhelpful

## Recommended Action

**Choose Solution 1** (add GitHub Releases reference) because:
1. Standard practice for open source projects
2. Clear user expectation
3. Notification mechanism (watch releases)
4. Professional distribution

**Additional Enhancement:**
Also update MIGRATION.md to reference the same GitHub Releases URL and clarify:
- Self-generation is for testing only
- Official release will be in GitHub Releases
- Issue #8 tracking link (verify it exists first)

## Technical Details

**Affected Files:**
- `README.md` (lines 75-76)
- `MIGRATION.md` (lines 97-104)

**Changes Required:**

**README.md:**
```markdown
### 2. Cowork (Claude Desktop) - Beta

> ⚠️ **Note:** Cowork installation is pending testing with the v2.0.0 structure.
> A tested v2.0.0 ZIP will be provided in [GitHub Releases](https://github.com/nabeelhyatt/coworkpowers/releases)
> once validation is complete. Subscribe to releases to be notified when it's ready.

**When ZIP is available:**
1. Download `coworkpowers-v2.0.0.zip` from GitHub Releases
2. In Cowork, click Plugins → + → Upload Plugin
3. Drag and drop the zip file and hit upload
4. Type `/coworkpowers:workflow-research [task]` to get started
```

**MIGRATION.md:**
```markdown
### For Cowork (Claude Desktop) Users

> ⚠️ **Note:** An official v2.0.0 ZIP will be published to
> [GitHub Releases](https://github.com/nabeelhyatt/coworkpowers/releases)
> after validation is complete. Track progress in
> [Issue #8](https://github.com/nabeelhyatt/coworkpowers/issues/8).

**If you want to test before official release:**
1. Generate ZIP: `cd plugins/coworkpowers && zip -r ../../coworkpowers.zip ...`
2. Upload to Cowork (Plugins → Upload Plugin)
3. Verify plugin loads and skills are accessible

For production use, we recommend waiting for the official release.
```

## Acceptance Criteria

- [ ] README.md references GitHub Releases for ZIP distribution
- [ ] MIGRATION.md includes release timeline expectations
- [ ] Issue #8 exists and is referenced correctly (or reference removed)
- [ ] Self-generation instructions labeled as "testing only"
- [ ] Clear notification mechanism for users (watch releases)

## Work Log

### 2026-02-16
- **Discovered:** Documentation review found unclear ZIP distribution plan
- **Impact:** User confusion about Cowork installation path
- **Next:** Add GitHub Releases reference and clarify testing vs production

## Resources

- **Review Report:** Documentation Validation (agent aab2000)
- **Files:**
  - `README.md`
  - `MIGRATION.md`
- **Related:** Issue #8 (verify existence)
- **Context:** v2.0.0 marketplace restructure removed old ZIP
