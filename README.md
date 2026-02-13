# CoworkPowers

**Knowledge work superpowers that compound over time.**

CoworkPowers gives Claude systematic capabilities for tackling knowledge work—drafting communications, making decisions, preparing for meetings, and more. Each completed task feeds insights back into the system, making the next similar task faster and better.

## The Compound Loop

1. **Research** (`/coworkflows:research`) - Thoroughly research the task, search past learnings, gather context
2. **Work** (`/coworkflows:work`) - Execute the plan with specialized agents
3. **Review** (`/coworkflows:review`) - Multi-agent quality review from multiple perspectives
4. **Compound** (`/coworkflows:compound`) - Extract patterns, templates, and preferences for next time

## Key Features

### 🔄 Compounding Knowledge
- Automatically captures patterns, templates, and preferences from completed work
- Searches past learnings before starting new tasks
- Gets smarter with each use—first board update takes 4 hours, next takes 1 hour

### 🎯 Specialized Agents
- **decision-architect**: Structure decisions with 40+ frameworks (SPADE, SWOT, Cynefin, Pre-Mortem)
- **context-gatherer**: Research comprehensive background before acting
- **executive-writer**: Draft clear, concise business communications
- **coach**: CEO-level coaching for leadership challenges
- Plus 10+ more specialized agents

### ✅ Hard Gates & Red Flags
- Asks clarifying questions before launching expensive research
- Catches high-stakes work early (board communications, sensitive topics)
- Verification-before-claims patterns from superpowers

### 📚 Dual-Environment Design
- Works in Claude Code (file-based retrieval with grep/glob)
- Designed for Camp channels (automatic compaction + relevance filtering)
- Insights stored as discrete markdown files with YAML frontmatter

## Quick Start

### 1. Research Phase
```
/coworkflows:research

"I need to draft an email to the board about Q2 results"
```

Claude will:
- Ask clarifying questions (stakes? audience? constraints?)
- Search past board communications for patterns
- Gather context on Q2 results and board concerns
- Produce a thorough plan

### 2. Work Phase
```
/coworkflows:work

Follow the plan from research phase
```

### 3. Review Phase
```
/coworkflows:review

Review the draft email
```

Multiple specialized reviewers check in parallel:
- Clarity, tone, completeness
- Political sensitivities, risks
- Actionability, strategic alignment

### 4. Compound Phase
```
/coworkflows:compound

The board loved it! Let's capture what worked
```

Extracts patterns, creates templates, documents preferences for next time.

## Installation

### Option 1: Claude Code Plugin (Recommended)
```bash
# Clone to Claude plugins directory
cd ~/.claude/plugins/repos/
git clone https://github.com/nabeelhyatt/coworkpowers.git

# Enable in Claude Code settings
```

### Option 2: Manual Installation
Copy the `workflows/` and `agents/` directories to your Claude skills folder.

## Workflows

| Command | Purpose | When to Use |
|---------|---------|-------------|
| `/coworkflows:research` | Research and plan thoroughly | Starting any significant work |
| `/coworkflows:work` | Execute the plan systematically | After research phase |
| `/coworkflows:review` | Multi-agent quality review | After drafting/execution |
| `/coworkflows:compound` | Extract learnings for next time | After completing work |

## Specialized Agents

### Research Phase Agents
- **context-gatherer** - Comprehensive background research
- **stakeholder-mapper** - Map interests and power dynamics
- **precedent-researcher** - Find similar past situations
- **constraint-analyzer** - Identify limits and requirements

### Work Phase Agents
- **executive-writer** - Business communications
- **analyst** - Rigorous analysis and synthesis
- **decision-architect** - Structured decision-making with frameworks
- **meeting-orchestrator** - Meeting prep and facilitation
- **coach** - Leadership coaching and thinking partner
- **diplomat** - Navigate sensitive conversations

### Review Phase Agents
- **clarity-reviewer** - Message clarity and conciseness
- **tone-calibrator** - Appropriate tone for audience
- **completeness-auditor** - Nothing important missing
- **sensitivity-scanner** - Political considerations and risks
- **actionability-validator** - Clear next steps

## Example: Board Communication

```bash
# 1. Research
/coworkflows:research "Draft Q2 board update"

# Claude asks clarifying questions:
# - What's the most important message? (hypothesis: growth trajectory)
# - Any sensitive topics? (political considerations)
# - Deadline? (affects research depth)

# Searches past board communications
# Gathers Q2 data and context
# Produces structured plan

# 2. Work
/coworkflows:work
# Follows plan, drafts update using executive-writer agent

# 3. Review
/coworkflows:review
# 5 specialized reviewers check in parallel
# Identifies: tone too casual for board, missing risk section

# 4. Compound
/coworkflows:compound "Board loved it"
# Captures: "Board prefers bullet points over prose"
# Creates: Board update template
# Documents: Success pattern for future use
```

Next board update will:
- Apply the template automatically
- Use captured preferences (bullet points)
- Avoid past failures
- Take 1 hour instead of 4

## Philosophy

### Compound Everything Worth Repeating
If you might do something similar again, compound it. Even partial successes have valuable patterns. Failures are the most valuable compounding opportunities.

### Front-Load the Thinking
80% of knowledge work is research and review. Every minute spent planning saves ten in execution.

### Match Rigor to Stakes
- **Low stakes** (internal notes): Light planning
- **Medium stakes** (team comms): Moderate planning
- **High stakes** (board, strategy): Full research + review

### Be Honest About Failures
Don't sugarcoat what went wrong. Root causes matter more than symptoms. Prevention > cure.

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

### File Structure
```
.context/learnings/
  INDEX.md                    # Searchable index of all insights
  communication/
    2026-02-13-pattern-board-format.md
    2026-02-13-template-board-update.md
  decision/
    2026-02-12-pattern-premortem-value.md
  ...
```

### Search & Retrieval
- **Claude Code**: Grep/glob search across category directories and INDEX.md
- **Camp**: Automatic compaction into channel knowledge base + relevance filtering

## Contributing

Contributions welcome! This plugin is designed to be extended:
- Add new specialized agents
- Create new workflow phases
- Enhance existing agents with new frameworks

## License

MIT License - See LICENSE file

## Credits

Inspired by:
- [Superpowers for Claude](https://github.com/obra/superpowers) - Hard Gates, Red Flags, verification patterns
- [Compound Engineering](https://github.com/EveryInc/compound-engineering-plugin) - Compounding knowledge philosophy
- Kieran Klaassen's work on compound systems

Built with ❤️ for knowledge workers who want their AI to get smarter over time.
