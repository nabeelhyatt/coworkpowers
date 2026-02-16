# Migration Guide: v1.x to v2.0.0

This guide helps you upgrade from coworkpowers v1.x to v2.0.0, which introduces a marketplace-compatible directory structure.

## What Changed

### Directory Structure

**v1.x (old):**
```
coworkpowers/
├── .claude-plugin/
├── skills/
├── agents/
├── CLAUDE.md
├── CONNECTORS.md
├── README.md
└── LICENSE
```

**v2.0.0 (new):**
```
coworkpowers/
├── plugins/
│   └── coworkpowers/
│       ├── .claude-plugin/
│       ├── skills/
│       ├── agents/
│       ├── CLAUDE.md
│       └── CONNECTORS.md
├── README.md
├── LICENSE
└── MIGRATION.md (this file)
```

### Why This Change?

The restructure enables proper Claude Code marketplace distribution. The nested `plugins/` structure matches Claude Code's marketplace expectations, allowing future installation via `/plugin install coworkpowers@coworkpowers`.

## Migration Instructions

### For Local Development Users

**Old command (v1.x):**
```bash
claude --plugin-dir ./coworkpowers
```

**New command (v2.0.0):**
```bash
claude --plugin-dir ./coworkpowers/plugins/coworkpowers
```

#### Option 1: Update Your Command

Simply update your shell alias or script to use the new path:

```bash
# ~/.zshrc or ~/.bashrc
alias cowork='claude --plugin-dir ~/code/coworkpowers/plugins/coworkpowers'
```

#### Option 2: Pull Latest Changes

If you have an existing clone:

```bash
cd coworkpowers
git pull origin main
# Update your launch command to use new path
claude --plugin-dir ./coworkpowers/plugins/coworkpowers
```

### For Fork Contributors

If you forked the repository before v2.0.0:

1. **Sync your fork with upstream:**
   ```bash
   git fetch upstream
   git checkout main
   git merge upstream/main
   ```

2. **Update local development path:**
   ```bash
   claude --plugin-dir ./coworkpowers/plugins/coworkpowers
   ```

3. **Rebase open PRs (if any):**
   - Pull requests created before v2.0.0 will have merge conflicts
   - We're happy to help! Comment on your PR and tag a maintainer
   - The restructure moved files with `git mv`, so history is preserved

### For Cowork (Claude Desktop) Users

> ⚠️ **Note:** Cowork installation with v2.0.0 structure is pending testing. The ZIP needs to be generated and validated with Cowork.

**If you have Cowork access and want to test:**
1. Generate ZIP: `cd plugins/coworkpowers && zip -r ../../coworkpowers.zip .claude-plugin skills agents CLAUDE.md CONNECTORS.md`
2. Upload to Cowork (Plugins → Upload Plugin)
3. Verify plugin loads and skills are accessible

For now, we recommend using the Claude Code local installation method instead.

## Troubleshooting

### "Plugin not found" error

Make sure you're using the new path:
```bash
claude --plugin-dir ./coworkpowers/plugins/coworkpowers
```

### Skills don't autocomplete

Verify the directory structure:
```bash
ls coworkpowers/plugins/coworkpowers/
# Should show: .claude-plugin, skills, agents, CLAUDE.md, CONNECTORS.md
```

### Git history looks wrong

The files were moved with `git mv`, which preserves history. Use `git log --follow` to see the full history of a moved file:
```bash
git log --follow plugins/coworkpowers/skills/workflow-research/SKILL.md
```

## Questions?

- **Marketplace installation:** Track progress in [Issue #8](https://github.com/nabeelhyatt/coworkpowers/issues/8)
- **Migration help:** Open an issue and tag @nabeelhyatt
- **General questions:** See [README.md](README.md) for documentation

## Rollback (if needed)

To temporarily use v1.x structure:

```bash
git checkout v1.0.0
claude --plugin-dir ./coworkpowers
```

Note that v1.x will not receive further updates. We recommend migrating to v2.0.0.
