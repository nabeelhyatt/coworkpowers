---
status: pending
priority: p1
issue_id: "001"
tags: [code-review, architecture, marketplace, critical]
dependencies: []
---

# marketplace.json Must Be at Repository Root

## Problem Statement

**What's broken:** The `marketplace.json` file is currently located at `plugins/coworkpowers/.claude-plugin/marketplace.json`, but according to the cctop reference pattern, it should be at the repository root (`.claude-plugin/marketplace.json`).

**Why it matters:** Claude Code marketplace distribution looks for marketplace metadata at the repository root. If marketplace.json is nested inside the plugin subdirectory, the marketplace system won't be able to discover or distribute the plugin.

**Business impact:** This blocks the entire purpose of the restructure - enabling marketplace distribution. Without fixing this, `/plugin install coworkpowers@coworkpowers` will fail.

## Findings

**From architecture-strategist agent:**

The cctop reference structure shows:
```
cctop/                          # Marketplace root
├── .claude-plugin/
│   └── marketplace.json        # At root!
├── plugins/
│   └── cctop/
│       ├── .claude-plugin/
│       │   └── plugin.json     # Plugin manifest only
│       └── skills/
```

**Current (incorrect) structure:**
```
coworkpowers/
├── plugins/
│   └── coworkpowers/
│       └── .claude-plugin/
│           ├── marketplace.json  # WRONG LOCATION
│           └── plugin.json
```

**Expected structure:**
```
coworkpowers/
├── .claude-plugin/
│   └── marketplace.json          # Correct!
├── plugins/
│   └── coworkpowers/
│       ├── .claude-plugin/
│       │   └── plugin.json       # Plugin metadata only
│       └── skills/
```

**Source path implication:** The marketplace.json currently has `"source": "./plugins/coworkpowers"`, which is correct IF marketplace.json is at the repository root. If it stays in the plugin subdirectory, this path would be wrong.

## Proposed Solutions

### Solution 1: Move marketplace.json to Repository Root (RECOMMENDED)

**Approach:**
```bash
# Create root .claude-plugin directory
mkdir -p .claude-plugin

# Move marketplace.json to root
git mv plugins/coworkpowers/.claude-plugin/marketplace.json .claude-plugin/

# Keep plugin.json in plugin subdirectory
# No changes needed to marketplace.json content - source path is already correct
```

**Pros:**
- Matches cctop reference pattern exactly
- Claude Code marketplace will find it
- Source path `"./plugins/coworkpowers"` is correct from root

**Cons:**
- None - this is the correct pattern

**Effort:** Small (5 minutes)
**Risk:** None - this is a straightforward file move

### Solution 2: Test Current Structure First

**Approach:**
- Test if Claude Code marketplace actually requires marketplace.json at root
- If current structure works, keep it

**Pros:**
- Avoids unnecessary change if current structure works

**Cons:**
- HIGH RISK: If it doesn't work, marketplace distribution fails
- Deviates from proven reference pattern
- No documentation suggests nested marketplace.json works

**Effort:** Medium (requires marketplace testing environment)
**Risk:** High - likely to fail

## Recommended Action

**IMPLEMENT SOLUTION 1** - Move marketplace.json to repository root.

This is non-negotiable for marketplace compatibility. The cctop pattern is proven and documented.

## Technical Details

**Affected files:**
- `plugins/coworkpowers/.claude-plugin/marketplace.json` → `.claude-plugin/marketplace.json`
- `plugins/coworkpowers/.claude-plugin/plugin.json` (stays in place)

**Configuration changes:**
- No changes to marketplace.json content needed
- Source path `"./plugins/coworkpowers"` is already correct

**Dependencies:**
- Must be done before any marketplace publication attempts
- Should be tested with local marketplace installation

## Acceptance Criteria

- [ ] `.claude-plugin/marketplace.json` exists at repository root
- [ ] `plugins/coworkpowers/.claude-plugin/` contains only `plugin.json`
- [ ] marketplace.json `source` field remains `"./plugins/coworkpowers"`
- [ ] Git history preserved using `git mv`
- [ ] Local installation still works: `claude --plugin-dir ./coworkpowers/plugins/coworkpowers`

## Work Log

- **2026-02-16:** Issue identified during code review by architecture-strategist agent
- **Next:** Move marketplace.json to root and test

## Resources

- **Reference:** cctop marketplace structure at `~/.claude/plugins/marketplaces/cctop/`
- **Related:** Issue #8 - Plugin not found in marketplace
- **Documentation:** Claude Code marketplace requirements (need to verify)
