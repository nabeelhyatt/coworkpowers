---
status: pending
priority: p2
issue_id: "010"
tags: [marketplace, publication, distribution, release]
dependencies: ["006"]
---

# Claude Code Marketplace Submission Checklist

## Problem Statement

The coworkpowers plugin is structured for marketplace compatibility (v2.0.0) but has not been submitted to the official Claude Code marketplace. Users cannot install via `/plugin install coworkpowers` until the plugin is published.

**Why it matters:** Marketplace publication makes the plugin easily discoverable and installable for all Claude Code users without manual setup.

## Submission Options

### Option 1: Official Anthropic Marketplace (Recommended)

**Benefits:**
- Centralized discovery for all Claude Code users
- Potential for "Anthropic Verified" badge
- Automatic updates
- Quality and security review
- Professional credibility

**Requirements:**
- Meet quality and security standards
- Pass automated review
- Optional: Additional review for "Anthropic Verified" badge

**Submission URL:** https://claude.com/plugins

### Option 2: Community Marketplaces

**Available Platforms:**
- **claudemarketplaces.com** - Community plugin directory
- **claudecodecommands.directory** - Submit commands and agents
- **GitHub marketplaces** - Self-hosted or community-managed

**Benefits:**
- Faster approval process
- Community-driven curation
- Lower barrier to entry

### Option 3: Self-Hosted Marketplace

**How it works:**
- Host `marketplace.json` in a git repository
- Users add your marketplace URL to their Claude Code settings
- Full control over distribution

**Best for:**
- Private/internal plugins
- Beta testing before official submission
- Custom plugin collections

## Pre-Submission Checklist

### ✅ Code Quality (Complete)

- [x] Plugin structure follows v2.0.0 marketplace format
- [x] All 4 skills have valid SKILL.md files
- [x] All 24 agent files present and documented
- [x] plugin.json and marketplace.json are valid
- [x] No critical blocking issues (P1 findings resolved)
- [ ] Fix P2 finding: devils-advocate apostrophe (**DEPENDENCY**)
- [ ] Address P3 findings (optional but recommended)

### 📝 Documentation (Nearly Complete)

- [x] README.md with clear installation instructions
- [x] MIGRATION.md for v1.x → v2.0.0 upgrade path
- [x] CLAUDE.md with plugin overview and skills
- [x] CONNECTORS.md with MCP integration guide
- [x] LICENSE file (MIT)
- [ ] Add CHANGELOG.md documenting v2.0.0 changes
- [ ] Add CONTRIBUTING.md for contributors
- [ ] Verify all documentation links work

### 🔒 Security & Privacy

- [ ] Review all agent prompts for security best practices
- [ ] Ensure no hardcoded credentials or API keys
- [ ] Validate input sanitization in skills
- [ ] Check for potential command injection vulnerabilities
- [ ] Review permissions required by plugin
- [ ] Document data handling and privacy practices

### 🧪 Testing

- [ ] Test plugin loading with `--plugin-dir` flag
- [ ] Verify all 4 skills are invocable:
  - [ ] `/coworkpowers:workflow-research`
  - [ ] `/coworkpowers:workflow-work`
  - [ ] `/coworkpowers:workflow-review`
  - [ ] `/coworkpowers:workflow-compound`
- [ ] Test each workflow end-to-end
- [ ] Verify agents invoke correctly via Task tool
- [ ] Test with different Claude Code versions (if possible)
- [ ] Validate on different operating systems (macOS, Linux, Windows)

### 📦 Release Preparation

- [ ] Create GitHub release for v2.0.0
- [ ] Tag release: `git tag -a v2.0.0 -m "Marketplace-ready release"`
- [ ] Generate Cowork ZIP (optional): `cd plugins/coworkpowers && zip -r ../../coworkpowers-v2.0.0.zip .`
- [ ] Upload ZIP as GitHub release asset
- [ ] Update README with release download links
- [ ] Write release notes highlighting v2.0.0 changes

### 🎨 Marketing Materials

- [ ] Create plugin icon/logo (if required)
- [ ] Write compelling description (already in marketplace.json)
- [ ] Prepare screenshots or demo video (optional but recommended)
- [ ] Create example use cases for README
- [ ] Highlight unique features (compound learning, 24 agents, etc.)

## Official Submission Process

### Step 1: Prepare Submission

1. **Verify Prerequisites:**
   - [ ] Plugin loads without errors
   - [ ] All P2 findings resolved (devils-advocate fix)
   - [ ] Documentation is complete
   - [ ] GitHub repository is public

2. **Gather Required Information:**
   - Plugin name: `coworkpowers`
   - Version: `2.0.0`
   - GitHub URL: `https://github.com/nabeelhyatt/coworkpowers`
   - Category: `productivity`
   - Description: (from marketplace.json)
   - Author: Nabeel Hyatt
   - License: MIT

### Step 2: Submit to Anthropic

1. **Visit Submission Form:**
   - URL: https://claude.com/plugins
   - Follow submission instructions
   - Provide GitHub repository URL

2. **Submission Details:**
   - **Repository:** `https://github.com/nabeelhyatt/coworkpowers`
   - **Plugin Path:** `plugins/coworkpowers` (per marketplace.json)
   - **Version:** `2.0.0`
   - **Marketplace JSON:** `.claude-plugin/marketplace.json`

3. **Wait for Review:**
   - Automated review checks basic requirements
   - Manual review for quality and security (if seeking verified badge)
   - Response time: Unknown (check with Anthropic)

### Step 3: Post-Approval

1. **Test Marketplace Installation:**
   ```bash
   /plugin install coworkpowers
   ```

2. **Update Documentation:**
   - Update README.md installation section
   - Mark marketplace installation as "Available"
   - Remove "pending publication" notes

3. **Announce Launch:**
   - GitHub release announcement
   - Social media (if applicable)
   - Community forums

## Alternative: Self-Hosted Marketplace (Quick Option)

If official submission takes time, you can immediately create a self-hosted marketplace:

### Quick Setup

1. **Your marketplace.json is already ready** at `.claude-plugin/marketplace.json`

2. **Users can add your marketplace:**
   ```bash
   /plugin add https://github.com/nabeelhyatt/coworkpowers
   ```

3. **Then install your plugin:**
   ```bash
   /plugin install coworkpowers@nabeelhyatt
   ```

This works immediately without waiting for Anthropic approval.

## Acceptance Criteria

### Minimum (Self-Hosted Marketplace):
- [ ] marketplace.json hosted in public GitHub repo
- [ ] Plugin installable via `/plugin add` + `/plugin install`
- [ ] All 4 skills work after marketplace installation

### Complete (Official Marketplace):
- [ ] Plugin submitted to https://claude.com/plugins
- [ ] Automated review passed
- [ ] Plugin appears in official marketplace directory
- [ ] Installable via `/plugin install coworkpowers` (no URL needed)
- [ ] Optional: "Anthropic Verified" badge obtained

## Resources

**Official Documentation:**
- [Discover and Install Plugins](https://code.claude.com/docs/en/discover-plugins)
- [Create Plugin Marketplaces](https://code.claude.com/docs/en/plugin-marketplaces)
- [Official Plugins Repository](https://github.com/anthropics/claude-plugins-official)
- [Anthropic Plugin Submission](https://claude.com/plugins)

**Community Resources:**
- [Claude Marketplaces](https://claudemarketplaces.com/)
- [Claude Code Commands Directory](https://claudecodecommands.directory/submit)
- [Community Marketplace Example](https://github.com/ananddtyagi/cc-marketplace)

**Your Repository:**
- [CoworkPowers GitHub](https://github.com/nabeelhyatt/coworkpowers)
- Issue #8: Track marketplace publication progress

## Work Log

### 2026-02-16
- **Created:** Marketplace submission checklist based on research
- **Findings:** Multiple submission options available (official, community, self-hosted)
- **Recommendation:** Start with self-hosted for immediate availability, then pursue official marketplace for broader reach
- **Next:** Fix P2 finding (devils-advocate), then choose submission path

## Recommended Timeline

### Week 1 (Immediate):
1. Fix devils-advocate apostrophe issue (todo #006)
2. Test plugin loading thoroughly
3. Create GitHub v2.0.0 release
4. Set up self-hosted marketplace (5 minutes)

### Week 2 (Short-term):
1. Address P3 findings for polish
2. Write CHANGELOG.md
3. Create demo screenshots/video
4. Submit to official Anthropic marketplace

### Week 3+ (Long-term):
1. Wait for Anthropic review
2. Address any review feedback
3. Announce official marketplace availability
4. Consider "Anthropic Verified" badge application

## Notes

- Self-hosted marketplace can run in parallel with official submission
- Users can switch from self-hosted to official marketplace once approved
- Consider submitting to community marketplaces for additional exposure
- "Anthropic Verified" badge requires additional quality/security review but adds credibility
