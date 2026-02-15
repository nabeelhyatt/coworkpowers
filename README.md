# CoworkPowers

**Knowledge work superpowers that compound over time.**

CoworkPowers is a Claude Code plugin that gives Claude systematic capabilities for tackling knowledge work -- drafting communications, making decisions, preparing for meetings, and more. Each completed task feeds insights back into the system, making the next similar task faster and better.

## The Compound Loop

1. **Research** (`/coworkpowers:workflow-research`) - Thoroughly research the task, search past learnings, gather context
2. **Work** (`/coworkpowers:workflow-work`) - Execute the plan with specialized agents
3. **Review** (`/coworkpowers:workflow-review`) - Multi-agent quality review from multiple perspectives
4. **Compound** (`/coworkpowers:workflow-compound`) - Extract patterns, templates, and preferences for next time

## How Each Phase Works

### Research

Research runs parallel agents to gather context before any work begins. The **context-gatherer** pulls relevant background. The **stakeholder-mapper** identifies who cares and why. The **constraint-analyzer** finds the boundaries. The **precedent-researcher** checks what's worked before. These run in parallel -- not sequentially -- so research is fast even when it's thorough.

Stakes classification happens here too. A routine email gets a lightweight context scan. A board presentation gets the full agent roster. This prevents the overwork problem where every task gets treated like a crisis.

### Work

Work is where execution happens. The system picks the right agent mindset for the task type: **executive-writer** for communications, **analyst** for data work, **decision-architect** for strategic choices (this one has 40+ decision frameworks it selects from), **meeting-orchestrator** for meeting prep, **coach** for leadership challenges. The work uses everything Research gathered, so there's no redundant context-fetching.

### Review

Review is where progressive loading gets interesting. Low-stakes work might only get a clarity pass. High-stakes work activates up to 8 specialized reviewers running in parallel:

- **clarity-reviewer** -- is this understandable?
- **tone-calibrator** -- does this sound right for the audience?
- **completeness-auditor** -- is anything missing?
- **sensitivity-scanner** -- any political landmines?
- **devil's-advocate** -- what's the strongest counter-argument?
- **risk-assessor** -- what could go wrong?
- **strategic-alignment-checker** -- does this fit the bigger picture?
- **actionability-validator** -- are next steps clear?

Each reviewer returns findings tagged by severity: **Critical**, **Important**, or **Minor**. Criticals get fixed before delivery. Important items get flagged. Minor items are noted but not blocking.

### Compound

After Work and Review complete, the Compound phase runs analysis agents that extract reusable knowledge:

- **Patterns**: "When writing partner updates, leading with portfolio metrics before narrative gets better engagement"
- **Templates**: The actual structure that worked, saved for reuse
- **Preferences**: "This user prefers concise bullets over flowing prose for internal comms"
- **Failures**: "Tone was too formal for this audience -- calibrate down next time"

Each insight gets stored as a discrete, tagged file in `.context/learnings/`. One insight per file, because granular knowledge is findable. A monolithic "things we learned" doc isn't.

Next time you do similar work, the Research phase searches these learnings before doing any new research. It loads matching patterns, applies saved templates, honors your preferences, and avoids documented failures.

**The practical effect**: your first partner update might take the full Research > Work > Review cycle. Your fourth one loads the template, applies your preferred tone, and skips the research it already has. Faster, cheaper, and more consistent.

## Installation - There are a few ways you can get this up and running in Claude

### 1. Claude Code

```bash
# Option A: (Easiest) Open Claude Code, then install from Marketplace just copy and paste this line into Claude Code and hit yes, then restart Claude Code after install and start with the first command - /workflow-research and the first task
/plugin install coworkpowers@coworkpowers

# Option B: Test locally
git clone https://github.com/nabeelhyatt/coworkpowers.git
claude --plugin-dir ./coworkpowers
```

### Cowork (Claude Desktop) - This is beta. Using the new Claude Cowork you can try this as a plug-in

1. Download [coworkpowers.zip](coworkpowers.zip) from this repository
2. In Cowork, clikc Plugins in the left sidebar > + to add plug-in > Upload Plugin
3. Drag and drop the zip file and hit upload
4. Go back to cowork and type /workflow-research [task you want done] to get started

### Connectors (Optional)

Connect MCP tools for richer context -- email, calendar, meeting notes, CRM, etc. See [CONNECTORS.md](CONNECTORS.md) for supported categories and example MCPs. No connectors are required; the plugin works with web search and local files alone. But it will gather from most of the connectors/mcp/apis to gather more context for your task without any additional setup.

## Skills

| Command | Purpose | When to Use |
|---------|---------|-------------|
| `/coworkpowers:workflow-research` | Research and plan thoroughly | Starting any significant work |
| `/coworkpowers:workflow-work` | Execute the plan systematically | After research phase |
| `/coworkpowers:workflow-review` | Multi-agent quality review | After drafting/execution |
| `/coworkpowers:workflow-compound` | Extract learnings for next time | After completing work |

## Quick Start

```bash
# 1. Research
/coworkpowers:workflow-research "Draft competitive analysis"

# Claude asks clarifying questions:
# - What's the most important competitor? (hypothesis: growth trajectory)
# - Any strategic advanteges to consider? (strategic considerations)
# - Deadline? (affects research depth)

# Searches past board communications
# Gathers data from web, past emails, and context from X MCP
# Produces structured plan

# 2. Work
/coworkpowers:workflow-work
# Follows plan, drafts update using executive-writer agent

# 3. Review
/coworkpowers:workflow-review
# 5 specialized reviewers check in parallel
# Identifies: tone too casual for board, missing risk section

# 4. Compound
/coworkpowers:workflow-compound "Board loved it"
# Captures: "Board prefers bullet points over prose"
# Creates: Board update template
# Documents: Success pattern for future use
```

Next board update will:
- Apply the template automatically
- Use captured preferences (bullet points)
- Avoid past failures
- Take 1 hour instead of 4

## Design Learnings

**Progressive loading beats uniform rigor.** This started by treating all review agents equally -- every task got the full review battery. It was thorough but painfully slow for simple tasks. The classification step in Research that determines stakes level was an afterthought that turned into making this generally usable daily.

**Granular beats monolithic for compound learning.** Early versions stored learnings in big category documents. But as most others have found (see Cursor context gathering, Anthropic, etc) just trusting in grep to scour across lots of little files and directories is the better model. Switching to one-insight-per-file with YAML frontmatter (type, category, tags, takeaway) made retrieval actually work.

## Philosophy

### Compound Everything Worth Repeating
If you might do something similar again, compound it. Even partial successes have valuable patterns. Failures are the most valuable compounding opportunities. Feel free to add WHAT you want to compoound, your learnings, and it will make sure to incorporate that along with anything else it finds.

### Front-Load the Thinking
80% of knowledge work is research and review. Every minute spent planning saves ten in execution. We sometimes jump to the doing, when the context gathering is the key.

### Match Rigor to Stakes
- **Low stakes** (internal notes): Light planning
- **Medium stakes** (team comms): Moderate planning
- **High stakes** (board, strategy): Full research + review

## Plugin Structure

```
coworkpowers/
  .claude-plugin/
    plugin.json           # Plugin manifest
  skills/
    workflow-research/SKILL.md   # Research & planning skill
    workflow-work/SKILL.md       # Execution skill
    workflow-review/SKILL.md     # Multi-agent review skill
    workflow-compound/SKILL.md   # Knowledge compounding skill
  agents/                 # 20+ specialized agent definitions
  CLAUDE.md               # Project instructions
  README.md
```

## Technical Details

### Insight Storage
Learnings are stored as discrete markdown files:
```markdown
---
type: pattern | template | preference | failure | insight
date: 2026-02-13
category: communication | decision | analysis | meeting | coaching | operations
task: Brief description
outcome: success | partial | failure
tags: stakeholders, frameworks, topics, projects
takeaway: One-sentence key learning
---

# Descriptive Title

## Context
[What task this came from]

## The Learning
[The actual insight]

## When to Apply
[Specific situations where relevant]
```


## Contributing

Contributions welcome! This plugin is designed to be extended:
- Add new specialized agents
- Create new skill phases
- Enhance existing agents with new frameworks

## License

MIT License - See LICENSE file

## Credits

Inspired by:
- [Superpowers for Claude](https://github.com/obra/superpowers) - Hard Gates, Red Flags, verification patterns
- [Compound Engineering](https://github.com/EveryInc/compound-engineering-plugin) - Compounding knowledge philosophy
- Kieran Klaassen's work on compound systems

Built for knowledge workers who want their AI to get smarter over time.
