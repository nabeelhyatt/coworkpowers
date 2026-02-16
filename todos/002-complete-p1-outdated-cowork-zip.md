---
status: complete
priority: p1
issue_id: "002"
tags: [code-review, documentation, cowork, user-experience]
dependencies: []
---

# Cowork ZIP File is Outdated and Untested

## Problem Statement

**What's broken:** The `coworkpowers.zip` file at the repository root contains the old (v1.x) flat structure, but the documentation (README.md and MIGRATION.md) instructs users to download this ZIP for Cowork installation, implying it works with the new v2.0.0 structure.

**Why it matters:** Users following the Cowork installation instructions will download a ZIP that doesn't match the new repository structure. This will likely cause the plugin to fail loading in Cowork, creating a poor user experience and eroding trust.

**Business impact:** This is a documented installation method that doesn't work. Users attempting Cowork installation will fail and may abandon the plugin.

## Findings

**From code-simplicity-reviewer agent:**

The plan explicitly marked "Test Cowork ZIP behavior" as **CRITICAL**, but:
- The ZIP was never updated to the new structure
- The ZIP was never tested with Cowork
- Documentation confidently instructs users to use it

**Current ZIP contents (examined earlier):**
- Contains old flat structure: `agents/`, `skills/`, `.claude-plugin/` at root
- Does NOT contain new structure: `plugins/coworkpowers/`

**Documentation claims:**
- README.md: "Download coworkpowers.zip from this repository"
- MIGRATION.md: "Download the updated ZIP file" and "The updated ZIP contains the new structure"

This is FALSE - the ZIP is not updated.

## Proposed Solutions

### Solution 1: Update and Test the ZIP (RECOMMENDED)

**Approach:**
```bash
# Generate new ZIP with correct structure
cd plugins/coworkpowers
zip -r ../../coworkpowers.zip .claude-plugin skills agents CLAUDE.md CONNECTORS.md

# Test in Cowork (if you have access):
# 1. Upload ZIP to Cowork
# 2. Verify it extracts correctly
# 3. Verify plugin loads
# 4. Verify skills appear in autocomplete
```

**Pros:**
- Maintains Cowork as supported installation method
- Documentation becomes accurate
- Users can actually use this method

**Cons:**
- Requires access to Cowork for testing
- Unknown if Cowork handles nested ZIP structure

**Effort:** Medium (need Cowork testing environment)
**Risk:** Medium - Cowork extraction behavior is untested

### Solution 2: Remove Cowork Installation Section

**Approach:**
- Delete `coworkpowers.zip` from repository
- Remove Cowork installation section from README.md
- Remove Cowork references from MIGRATION.md
- Add note: "Cowork installation pending testing"

**Pros:**
- Honest about what works
- Removes broken installation path
- No misleading documentation

**Cons:**
- Removes a documented feature
- May disappoint users wanting Cowork support

**Effort:** Small (15 minutes)
**Risk:** None - just documentation updates

### Solution 3: Add Warning Banner

**Approach:**
- Keep ZIP and documentation
- Add prominent warning:
  > ⚠️ **WARNING:** The Cowork ZIP has not been updated for v2.0.0 structure and may not work. Use local installation method instead.

**Pros:**
- Keeps Cowork section for future use
- Honest about status
- Quick fix

**Cons:**
- Documents a broken feature
- Creates confusion

**Effort:** Small (5 minutes)
**Risk:** Low - just adds clarity

## Recommended Action

**IMPLEMENT SOLUTION 2 or 3** depending on priority:

- **If Cowork testing is impossible/low-priority:** Solution 2 (remove section)
- **If Cowork testing will happen soon:** Solution 3 (add warning)
- **If Cowork access available now:** Solution 1 (fix and test)

DO NOT keep current state - documented features must work.

## Technical Details

**Affected files:**
- `coworkpowers.zip` (needs update or removal)
- `README.md` (Cowork section)
- `MIGRATION.md` (ZIP download instructions)

**ZIP generation command:**
```bash
cd plugins/coworkpowers
zip -r ../../coworkpowers.zip .claude-plugin skills agents CLAUDE.md CONNECTORS.md .gitignore
```

**Testing checklist (if updating ZIP):**
- [ ] ZIP contains `plugins/coworkpowers/` structure OR flat structure from within plugin dir
- [ ] Upload to Cowork succeeds
- [ ] Cowork finds `.claude-plugin/` after extraction
- [ ] Skills appear in Cowork autocomplete
- [ ] Workflows execute correctly

## Acceptance Criteria

**If Solution 1 (update ZIP):**
- [ ] New ZIP generated with correct structure
- [ ] Tested in Cowork successfully
- [ ] Documentation updated with test confirmation

**If Solution 2 (remove section):**
- [ ] `coworkpowers.zip` deleted or added to .gitignore
- [ ] Cowork section removed from README.md
- [ ] Cowork references removed from MIGRATION.md
- [ ] Note added about future Cowork support

**If Solution 3 (add warning):**
- [ ] Warning banner added to Cowork section
- [ ] MIGRATION.md updated with warning
- [ ] Clear alternative installation method provided

## Work Log

- **2026-02-16:** Issue identified during code review - ZIP is stale
- **Next:** Decide on solution based on Cowork testing availability

## Resources

- **Plan:** 2026-02-16-feat-restructure-marketplace-compatibility-plan.md (marks Cowork testing as CRITICAL)
- **Current ZIP:** `coworkpowers.zip` (92KB, outdated)
- **ZIP generation:** See "Technical Details" section above
