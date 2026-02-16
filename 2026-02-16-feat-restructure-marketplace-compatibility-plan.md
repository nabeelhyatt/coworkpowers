---
title: "feat: Restructure repository for Claude Code marketplace compatibility"
type: feat
status: active
date: 2026-02-16
---

# Restructure Repository for Claude Code Marketplace Compatibility

## Overview

Restructure the coworkpowers repository to match Claude Code's marketplace expectations by creating a `plugins/` subdirectory and moving plugin files into `plugins/coworkpowers/`. This enables future marketplace distribution via `/plugin install coworkpowers@coworkpowers` while maintaining compatibility with current installation methods.

## Problem Statement / Motivation

The current repository structure has all plugin files at the root level (`.claude-plugin/`, `skills/`, `agents/`, etc.), which doesn't match Claude Code's marketplace pattern.

**Current structure:**
```
coworkpowers/
├── .claude-plugin/
├── skills/
├── agents/
├── README.md
└── ...
```

**Expected marketplace structure (from cctop reference):**
```
coworkpowers/
├── plugins/
│   └── coworkpowers/
│       ├── .claude-plugin/
│       ├── skills/
│       └── agents/
├── README.md
└── LICENSE
```

Without this structure, the plugin cannot be properly distributed through Claude Code's marketplace system, limiting accessibility and requiring manual installation workarounds.

Related: [Issue #8 - Plugin not found in marketplace](https://github.com/nabeelhyatt/coworkpowers/issues/8)

## Proposed Solution

Restructure the repository to follow marketplace conventions:

1. **Create `plugins/coworkpowers/` subdirectory**
2. **Move plugin files** into the subdirectory:
   - `.claude-plugin/` (plugin metadata)
   - `skills/` (4 workflow skills)
   - `agents/` (24 specialized agents)
   - `CLAUDE.md` (plugin instructions)
   - `CONNECTORS.md` (MCP integration guide)

3. **Keep at root level**:
   - `README.md` (marketplace documentation)
   - `LICENSE` (MIT license)
   - `.gitignore` (update paths)
   - `.github/` (CI/CD workflows)

4. **Update documentation**:
   - README installation instructions
   - marketplace.json source paths
   - Migration guide for existing users

## Technical Considerations

### Architecture Impact

**Repository Structure**
- Changes from "plugin repository" to "marketplace repository with one plugin"
- Adds one level of directory nesting for all plugin files
- Maintains clean root with only marketplace metadata

**Installation Paths**
- **Before:** `claude --plugin-dir ./coworkpowers`
- **After:** `claude --plugin-dir ./coworkpowers/plugins/coworkpowers`
- Breaking change for local development workflows

### Performance Implications

- No runtime performance impact
- Slightly longer file paths (minimal impact on load time)
- Git operations unchanged (same number of files, just relocated)

### Security Considerations

**`.gitignore` Updates Required**
- User learnings stored in `.context/` directory
- Path changes from `.context/` to `plugins/coworkpowers/.context/`
- Must update .gitignore to prevent accidental commit of user data

**Recommendation:** Use layered .gitignore approach:
```gitignore
# Root .gitignore (repository-wide)
.DS_Store
*.log

# plugins/coworkpowers/.gitignore (plugin-specific)
.context/
```

### Critical Unknowns Requiring Testing

**1. Cowork ZIP Extraction Behavior** (CRITICAL)
- Current: `coworkpowers.zip` contains flat structure
- After: Will ZIP contain nested `plugins/coworkpowers/` structure?
- **Risk:** Cowork may expect `.claude-plugin/` at ZIP root
- **Test Required:** Upload restructured ZIP to Cowork before merge
- **Mitigation:** Keep separate flat ZIP for Cowork if nested structure fails

**2. Marketplace Source Path Resolution**
- `marketplace.json` currently has `"source": "./"`
- After move to `plugins/coworkpowers/.claude-plugin/marketplace.json`:
  - Does `"./"` resolve relative to manifest location or repo root?
- **Test Required:** Verify Claude Code marketplace path resolution rules
- **Likely Fix:** Update to `"source": "./plugins/coworkpowers"` or `"source": "../"`

**3. Relative Path References**
- Skills or agents may contain relative markdown links
- Example: `[CLAUDE.md](../../CLAUDE.md)` breaks if file moves
- **Audit Required:** `grep -r '\.\./\|\./[a-zA-Z]' --include="*.md" agents/ skills/`
- **Fix:** Update all relative paths to match new structure

## Acceptance Criteria

### Functional Requirements

- [x] `plugins/coworkpowers/` directory created with all plugin files
- [ ] Root level contains only: README.md, LICENSE, .gitignore, .github/
- [x] `.claude-plugin/marketplace.json` source field updated correctly
- [x] Local installation works: `claude --plugin-dir ./coworkpowers/plugins/coworkpowers` (structure verified, manual testing required)
- [ ] All 4 skills load correctly: `/coworkpowers:workflow-*`
- [ ] All 24 agents accessible to skills

### Documentation Requirements

- [x] README.md updated with new installation instructions
- [x] MIGRATION.md created with upgrade guide for existing users
- [ ] marketplace.json source field reflects new structure
- [ ] CONTRIBUTING.md updated with new paths for contributors
- [x] .gitignore updated to ignore `plugins/coworkpowers/.context/`

### Quality Gates

- [ ] Cowork ZIP extraction tested and working (or alternative provided)
- [x] All relative path references audited and fixed
- [ ] No broken links in documentation
- [x] Git history preserved using `git mv` commands
- [x] Version bumped to 2.0.0 (breaking change)

## Success Metrics

**Immediate Success:**
- Local installation works with new path
- All skills and agents load correctly
- Documentation is clear and complete

**Long-term Success:**
- Marketplace installation enabled (after publishing)
- No support issues from migration confusion
- Contributors can find and edit files easily

## Dependencies & Risks

### Prerequisites

1. **Cowork ZIP testing environment** - Need ability to test ZIP uploads
2. **Claude Code marketplace documentation** - Confirm source path resolution
3. **Active PR coordination** - Warn contributors of upcoming merge conflicts

### Blocking Dependencies

None - this is self-contained restructuring work

### Risks & Mitigations

| Risk | Impact | Probability | Mitigation |
|------|--------|-------------|------------|
| **Cowork ZIP fails with nested structure** | HIGH | MEDIUM | Test before merge; maintain flat ZIP separately if needed |
| **Breaking existing users' workflows** | HIGH | CERTAIN | Clear migration guide, version bump to 2.0.0, advance communication |
| **Open PRs get merge conflicts** | MEDIUM | HIGH | Coordinate timing, provide rebase assistance |
| **Relative paths break** | MEDIUM | LOW | Audit all markdown files, fix before merge |
| **Git history obscured** | LOW | MEDIUM | Use `git mv` to preserve file history |

## Implementation Plan

### Phase 1: Pre-Migration Testing (1-2 days)

1. **Test Cowork ZIP behavior**
   ```bash
   # Create test structure
   mkdir -p test-structure/plugins/coworkpowers
   cp -r .claude-plugin skills agents CLAUDE.md CONNECTORS.md test-structure/plugins/coworkpowers/
   cd test-structure && zip -r coworkpowers-test.zip plugins/
   # Upload to Cowork and verify loading
   ```

2. **Audit relative paths**
   ```bash
   grep -r '\.\./\|\./[a-zA-Z]' --include="*.md" agents/ skills/ CLAUDE.md CONNECTORS.md
   # Document all references needing updates
   ```

3. **Verify marketplace source resolution**
   - Review cctop marketplace.json as reference
   - Test with local marketplace if possible
   - Document correct source path format

### Phase 2: Communication (1 week)

1. **Create announcement issue**
   - Title: "BREAKING CHANGE: Repository restructure for marketplace support (v2.0.0)"
   - Explain motivation (marketplace compatibility)
   - Detail migration steps
   - Set target merge date

2. **Notify stakeholders**
   - Comment on all open PRs about upcoming changes
   - Tag contributors in announcement issue
   - Update README with migration warning

3. **Tag current version**
   ```bash
   git tag v1.0.0 -m "Last version before marketplace restructure"
   git push origin v1.0.0
   ```

### Phase 3: Implementation

1. **Create feature branch**
   ```bash
   git checkout -b restructure-for-marketplace
   ```

2. **Create directory structure**
   ```bash
   mkdir -p plugins/coworkpowers
   ```

3. **Move plugin files (preserves git history)**
   ```bash
   git mv .claude-plugin plugins/coworkpowers/
   git mv skills plugins/coworkpowers/
   git mv agents plugins/coworkpowers/
   git mv CLAUDE.md plugins/coworkpowers/
   git mv CONNECTORS.md plugins/coworkpowers/
   ```

4. **Update configuration files**

   **plugins/coworkpowers/.claude-plugin/marketplace.json:**
   ```json
   {
     "plugins": [
       {
         "name": "coworkpowers",
         "source": "./plugins/coworkpowers",  // Update this line
         ...
       }
     ]
   }
   ```

   **Root .gitignore:**
   ```gitignore
   # Add plugin-specific ignores
   plugins/coworkpowers/.context/
   ```

   **plugins/coworkpowers/.gitignore:** (new file)
   ```gitignore
   # User-specific learnings
   .context/
   ```

5. **Update documentation**

   **README.md installation section:**
   ```markdown
   ### Claude Code (Local Testing)

   ```bash
   git clone https://github.com/nabeelhyatt/coworkpowers.git
   claude --plugin-dir ./coworkpowers/plugins/coworkpowers
   ```
   ```

6. **Create MIGRATION.md:**
   ```markdown
   # Migration Guide: v1.x to v2.0.0

   ## Local Development Users

   **Before (v1.x):**
   ```bash
   claude --plugin-dir ./coworkpowers
   ```

   **After (v2.0.0):**
   ```bash
   claude --plugin-dir ./coworkpowers/plugins/coworkpowers
   ```

   ## Fork Contributors

   If you have an existing fork:
   1. Pull latest from upstream
   2. Update any local scripts/aliases with new path
   3. Rebase open PRs (we're happy to help!)
   ```

7. **Fix relative path references**
   - Update any `../../` references in markdown files
   - Test all documentation links

8. **Update version**

   **plugins/coworkpowers/.claude-plugin/plugin.json:**
   ```json
   {
     "version": "2.0.0",
     ...
   }
   ```

9. **Commit changes**
   ```bash
   git add .
   git commit -m "feat: Restructure for marketplace compatibility

   BREAKING CHANGE: Plugin files moved to plugins/coworkpowers/ subdirectory

   - Create plugins/coworkpowers/ directory structure
   - Move .claude-plugin/, skills/, agents/ to subdirectory
   - Update marketplace.json source path
   - Update README with new installation instructions
   - Create MIGRATION.md for existing users
   - Bump version to 2.0.0

   Migration required for local development:
   - Old: claude --plugin-dir ./coworkpowers
   - New: claude --plugin-dir ./coworkpowers/plugins/coworkpowers

   Closes #8"
   ```

### Phase 4: Testing & Release

1. **Test all installation methods**
   ```bash
   # Test local installation
   claude --plugin-dir ./coworkpowers/plugins/coworkpowers

   # Verify skills load
   # Type: /coworkpowers:workflow-
   # Should see all 4 skills in autocomplete
   ```

2. **Generate and test ZIP** (if needed for Cowork)
   ```bash
   cd plugins/coworkpowers
   zip -r ../../coworkpowers.zip .claude-plugin skills agents CLAUDE.md CONNECTORS.md
   # Upload to Cowork and verify loading
   ```

3. **Create PR to main**
   - Reference announcement issue
   - Link to MIGRATION.md
   - Request testing from contributors

4. **After merge: Create GitHub Release**
   ```bash
   git tag v2.0.0 -m "Marketplace-compatible structure"
   git push origin v2.0.0
   ```

   Release notes:
   - Highlight marketplace compatibility
   - Link to MIGRATION.md
   - Attach generated ZIP as release artifact
   - Note this is a breaking change for local development

## Alternative Approaches Considered

### Option A: Dual Structure with Symlinks

Keep files at root AND in `plugins/` via symlinks:
```bash
skills -> plugins/coworkpowers/skills
```

**Rejected because:**
- Symlinks don't work on all platforms (Windows)
- Confusing for contributors
- Maintenance burden

### Option B: Separate Plugin and Marketplace Repos

Create two repositories:
- `coworkpowers-plugin` (flat structure for development)
- `coworkpowers-marketplace` (nested structure for distribution)

**Rejected because:**
- Duplication of effort
- Complex release process
- Harder to keep in sync

### Option C: Build Step for Distribution

Keep development structure flat, build marketplace structure on release:
```bash
npm run build:marketplace
```

**Rejected because:**
- Requires build automation
- More complex CI/CD
- Testing distribution structure requires extra steps
- May revisit if symlink approach becomes necessary

## References & Research

### Internal References

- Current structure: Root level contains all plugin files
- Agents catalog: 24 specialized agents in `agents/` directory
  - Research phase: 5 agents
  - Work phase: 6 agents
  - Review phase: 8 agents
  - Compound phase: 5 agents
- Skills implementation: 4 workflow skills in `skills/` directory
- Plugin metadata: `.claude-plugin/plugin.json`, `.claude-plugin/marketplace.json`

### External References

- Claude Code marketplace reference: cctop structure at `~/.claude/plugins/marketplaces/cctop/plugins/`
- Issue #8: [Installation instructions don't work - marketplace not found](https://github.com/nabeelhyatt/coworkpowers/issues/8)
- PR #9: [docs: Fix installation instructions](https://github.com/nabeelhyatt/coworkpowers/pull/9)

### Related Work

- Issue #8: Documents failed marketplace installation attempts
- PR #9: Updated README to clarify marketplace not yet available
- This PR: Implements marketplace structure to enable future distribution

---

## Next Steps After Plan Approval

1. **Immediate:** Test Cowork ZIP behavior (blocks implementation)
2. **Before implementation:** Create announcement issue and communicate timeline
3. **Implementation:** Follow phase-by-phase plan above
4. **After merge:** Monitor for user issues, assist with migration
