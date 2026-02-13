# CoworkPowers: Knowledge Work Superpowers

You have access to CoworkPowers, a system that makes knowledge work compound over time. Use the four core workflows to research, execute, review, and capture learnings.

## Core Workflows

Use these workflows for any significant knowledge work:

### `/cowork:research`
Research and plan thoroughly before execution. Use when starting:
- Important communications (board updates, difficult conversations)
- Strategic decisions (build vs. buy, pricing, hiring)
- Meeting preparation (board meetings, negotiations)
- Analysis projects (market research, competitive review)

**What it does:**
1. Asks clarifying questions to understand the task
2. Searches past learnings for relevant patterns/templates
3. Gathers comprehensive context
4. Runs parallel research agents
5. Synthesizes into actionable plan

**Example:**
```
/cowork:research

"I need to prepare for next week's board meeting"
```

### `/cowork:work`
Execute a plan systematically with specialized agents. Use after research phase.

**Available agents:**
- `executive-writer` - Business communications
- `decision-architect` - Structured decisions with 40+ frameworks
- `analyst` - Rigorous analysis
- `coach` - Leadership coaching
- `meeting-orchestrator` - Meeting prep
- `diplomat` - Sensitive conversations

**Example:**
```
/cowork:work

Follow the board prep plan using meeting-orchestrator
```

### `/cowork:review`
Multi-agent quality review from specialized perspectives. Use after drafting/execution.

**Review agents run in parallel:**
- Clarity, tone, completeness
- Sensitivity, risks, alignment
- Actionability, strategic fit

**Example:**
```
/cowork:review

Review the board presentation draft
```

### `/cowork:compound`
Extract patterns, templates, and preferences to make next time easier. Use after completing work.

**What it captures:**
- Patterns that worked (or didn't)
- Reusable templates
- User preferences (style, tone, detail level)
- Failure lessons

**Example:**
```
/cowork:compound

That board meeting went really well, let's capture what worked
```

## Key Principles

### Ask First, Research Second
The research workflow asks clarifying questions BEFORE launching expensive parallel research. This prevents wasted work on the wrong problem.

### Compound Everything Worth Repeating
Every completed task should feed insights back into the system. The first board update takes 4 hours. The second takes 1 hour. That's compounding.

### Match Rigor to Stakes
- **Low stakes** (internal notes): Skip research, go straight to work
- **Medium stakes** (team comms): Light research + review
- **High stakes** (board, strategy, sensitive): Full research + multi-agent review + compound

### Be Honest About Failures
When something doesn't go well, run `/cowork:compound` immediately. Failure insights are the most valuable compounding opportunities.

## Hard Gates & Red Flags

For high-stakes work, the research workflow will ask these questions BEFORE proceeding:
1. Who is the audience/stakeholder?
2. What does success look like?
3. What constraints exist (political, budget, timing)?
4. What have you tried before that didn't work?

This catches dangerous patterns early: irreversible decisions, political sensitivities, missing context.

## Insight Storage

Past learnings are stored in `.context/learnings/` and automatically searched during the research phase:

```
.context/learnings/
  INDEX.md                          # Searchable index
  communication/
    2026-02-13-pattern-board-format.md
    2026-02-13-template-board-update.md
  decision/
    2026-02-12-pattern-premortem-value.md
  ...
```

Each insight is a discrete, self-contained markdown file with YAML frontmatter for fast retrieval.

## Example Session

```bash
# User asks for help with difficult communication
User: "I need to tell the team about layoffs"

# Research phase
/cowork:research
# Asks: Stakes? Audience? Timeline? Past attempts?
# Searches: Past sensitive communications
# Gathers: Company context, team morale
# Produces: Structured communication plan

# Work phase
/cowork:work
# Uses diplomat + executive-writer agents
# Drafts sensitive communication

# Review phase
/cowork:review
# 5 agents review in parallel
# Flags: Tone issue, missing support resources section

# Revise and finalize
# ...

# Compound phase
/cowork:compound
# Captures: Pattern for sensitive communications
# Documents: "Always include support resources"
# Creates: Template for layoff communications
```

Next time there's a difficult communication, Claude will:
- Apply the layoff communication template
- Remember to include support resources
- Use the proven pattern for sensitive topics
- Avoid past failures

The second difficult communication takes half the time and has twice the quality.

---

**That's it.** Four workflows. Each task makes the next one easier. Knowledge compounds.
