# Changelog

All notable changes to the CoworkPowers plugin will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [2.0.0] - 2026-02-16

### Added
- **Marketplace compatibility**: Restructured repository for Claude Code marketplace distribution
- **Self-hosted marketplace**: Immediately installable via `/plugin add` + `/plugin install`
- **Marketplace manifest**: Added `.claude-plugin/marketplace.json` for marketplace configuration
- **Migration guide**: Comprehensive MIGRATION.md for v1.x → v2.0.0 upgrade path
- **Todo system**: Added structured todos/ directory for tracking improvements and issues
- **CHANGELOG.md**: This file to track version history

### Changed
- **Directory structure**: Moved plugin files into nested `plugins/coworkpowers/` directory
- **Installation path**: Changed from `./coworkpowers` to `./plugins/coworkpowers`
- **README.md**: Updated installation instructions with marketplace options
- **Agent naming**: Renamed `devils-advocate.md` → `devil's-advocate.md` for grammatical correctness
- **Tags**: Added "research" and "planning" tags to marketplace.json for better discoverability

### Fixed
- **Agent loading**: Fixed devils-advocate filename to match SKILL.md references
- **Documentation**: Clarified Cowork ZIP distribution plan
- **Installation guide**: Added self-hosted marketplace installation instructions

### Removed
- **Outdated ZIP**: Removed v1.x coworkpowers.zip (will be regenerated for v2.0.0)
- **Plan document**: Removed completed restructure plan from repository root

### Migration
See [MIGRATION.md](MIGRATION.md) for detailed upgrade instructions from v1.x.

**Breaking Change**: Installation command changed from:
```bash
# v1.x
claude --plugin-dir ./coworkpowers
```

To:
```bash
# v2.0.0
claude --plugin-dir ./plugins/coworkpowers
```

Or use marketplace installation (recommended):
```bash
/plugin add https://github.com/nabeelhyatt/coworkpowers
/plugin install coworkpowers@nabeelhyatt
```

## [1.0.0] - 2026-02-13

### Initial Release
- 4 workflow skills: research, work, review, compound
- 24 specialized agents across 4 categories
- File-based compound learning system
- MCP connector support
- Progressive loading based on stakes level
- Comprehensive agent documentation

---

## Version History Summary

| Version | Date | Type | Description |
|---------|------|------|-------------|
| 2.0.0 | 2026-02-16 | Major | Marketplace-compatible restructure |
| 1.0.0 | 2026-02-13 | Major | Initial public release |

---

[2.0.0]: https://github.com/nabeelhyatt/coworkpowers/compare/v1.0.0...v2.0.0
[1.0.0]: https://github.com/nabeelhyatt/coworkpowers/releases/tag/v1.0.0
