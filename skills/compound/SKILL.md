---
name: compound
description: "Extract and store learnings from completed knowledge work to make the next task easier. Use after completing any significant piece of work to capture patterns, create templates, and update preferences. Triggers on requests like 'that went well, let's capture what worked', 'what did we learn', 'that didn't go well', or after completing high-stakes work."
disable-model-invocation: true
---

# Compound: Knowledge Compounding Workflow

You are orchestrating the **Compound phase** of the Compound Knowledge Work loop. Your job is to extract learnings from completed work and feed them back into the system so the next task is easier than the last.

**The magic is in the compounding.** Skip this phase and you're just working, not building.

## Philosophy

Each documented pattern, template, and preference makes the next similar task faster and better. First attempt at a board update takes 4 hours of planning and drafting. Document the approach, and the next one takes 1 hour. That's compounding.

## Process

### Phase 1: Parallel Analysis

Launch these research agents in parallel:

1. **Pattern Extractor** - Analyze the completed work and conversation history:
   - What approach was taken?
   - What worked well? What didn't?
   - What would you do differently next time?
   - What frameworks or structures proved effective?

2. **Template Assessor** - Evaluate if this work could serve as a model:
   - Is this output reusable as a template?
   - What parts are situation-specific vs. generalizable?
   - How would you parameterize this for future use?

3. **Preference Detector** - Capture user preferences revealed:
   - What formatting or style preferences emerged?
   - What level of detail does the user prefer?
   - What communication style resonates?
   - What frameworks does the user gravitate toward?

4. **Failure Analyzer** (if things didn't go well):
   - What went wrong and why?
   - Was it execution, planning, or assumptions?
   - What early warning signs were missed?
   - What would prevent this next time?

### Phase 2: Produce Discrete Insights

From the analysis, produce **individual, self-contained insights**. Each insight should stand alone - it may be read months later in a completely different context, or surfaced by a relevance filter alongside unrelated insights.

Every task should produce at least one insight. Most will produce 2-5. Each insight gets its own type:

| Insight Type | What It Captures | Example |
|-------------|-----------------|---------|
| `pattern` | An approach that worked or didn't | "Pre-mortem before board presentations surfaces risks the team glosses over" |
| `template` | A reusable structure for future work | A generalized board update template with section placeholders |
| `preference` | A user style/tone/detail preference | "Prefers bullet points over prose in executive summaries" |
| `failure` | What went wrong and how to prevent it | "Announcing reorgs by email before 1:1s caused trust damage" |
| `insight` | A non-obvious learning or connection | "Investors respond better when bad news is framed as decisions, not problems" |

**Insight Format:**

```markdown
---
type: [pattern | template | preference | failure | insight]
date: [YYYY-MM-DD]
category: [communication | decision | analysis | meeting | coaching | operations]
task: [Brief description of the original task]
outcome: [success | partial | failure]
tags: [comma-separated: stakeholder names, frameworks, topics, projects]
takeaway: [One sentence - the key thing to remember. This is what gets searched.]
---

# [Descriptive Title]

## Context
[2-3 sentences: What task this came from, what the situation was]

## The Learning
[The actual insight, pattern, template, preference, or failure analysis. Self-contained - a reader should understand this without seeing anything else.]

## When to Apply
[Specific situations where this insight is relevant. Be concrete.]

## Related
[References to related insights by filename, if any]
```

**Keep each insight focused.** One pattern per file, one preference per file, one template per file. If a task yielded a good pattern AND a template AND a preference, that's three separate insight files. This granularity is what makes retrieval work.

### Phase 3: Store and Index

Insights must be stored so the **Research phase can find them quickly** by category, keyword, or tag. This is how the loop closes.

1. **Save each insight** to a category subdirectory under `.context/learnings/`:
   - Path: `.context/learnings/[category]/YYYY-MM-DD-[type]-[brief-description].md`
   - Categories: `communication/`, `decision/`, `analysis/`, `meeting/`, `coaching/`, `operations/`
   - Create the directory if it doesn't exist
   - Use descriptive filenames that are greppable (e.g., `2026-02-12-pattern-premortem-board-prep.md`)

2. **Update the learnings index** at `.context/learnings/INDEX.md`:
   - Add a row per insight with all searchable fields
   - Create the index with the table header if it doesn't exist

   Index format:
   ```markdown
   # Learnings Index

   | Date | Type | Category | Title | Outcome | Tags | Takeaway | File |
   |------|------|----------|-------|---------|------|----------|------|
   | 2026-02-12 | pattern | decision | Pre-mortem for board decisions | success | board, pre-mortem, risk | Pre-mortem surfaces risks the team glosses over in optimistic planning | decision/2026-02-12-pattern-premortem-board.md |
   ```

   The Research phase searches this index by: type, category, tags, and full-text grep across the Takeaway column. **Every field matters for retrieval.**

3. **Tag deliberately.** Tags should include:
   - People/stakeholders involved (e.g., `board`, `sarah`, `investors`)
   - Frameworks used (e.g., `SPADE`, `pre-mortem`)
   - Topic area (e.g., `pricing`, `hiring`, `product-launch`)
   - Anything you'd search for when facing a similar task

### Phase 4: Optional Enhancement

Based on what was learned, suggest improvements to the system:

- **New agent needed?** If a gap in review coverage was found
- **Agent update needed?** If an existing agent missed something it should catch
- **Workflow improvement?** If the plan-work-review-compound flow could be better

Present these suggestions to the user for approval.

## Compounding Principles

### Compound Everything Worth Repeating
- If you might do something similar again, compound it
- Even partial successes have valuable patterns
- Failures are the most valuable compounding opportunities

### Be Honest About Failures
- Don't sugarcoat what went wrong
- Root cause matters more than symptoms
- Prevention > cure

### Keep It Retrievable
- Descriptive filenames, deliberate tags, and one-sentence takeaways are what make retrieval work
- Cross-reference related insights in the "Related" section
- The index is sacred - keep it updated

### One Insight Per File
- Granular insights are findable; monolithic documents are not
- A pattern, a template, and a preference from the same task are three separate files
- Each file should be self-contained: readable without context

### Preferences Are Insights
- Style, tone, and detail preferences are project-scoped, not universal
- Store them as `preference` type insights alongside patterns and templates

### Templates Compound Fastest
- A good template saves the most time on repeat tasks
- Store as `template` type insights with the generalized template in the body
- Include usage notes and "When to Apply" guidance

## When to Compound

| Situation | Compound? | Focus On |
|-----------|-----------|----------|
| Completed high-stakes work | Always | Full analysis - patterns, templates, preferences |
| Work received positive feedback | Yes | What worked, template creation |
| Work received negative feedback | Absolutely | Failure insights, prevention |
| Routine work done well | Sometimes | Efficiency patterns |
| New type of work attempted | Yes | Approach and framework learnings |
| Discovered user preference | Yes | Preference insight |

## Anti-Patterns to Avoid

- Skipping compound because "we're too busy" (this is how knowledge debt accumulates)
- Compounding only successes (failures are more valuable)
- Creating insights that are too generic to be actionable
- Not indexing or tagging (unfindable knowledge is useless)
- Putting multiple learnings in one file (breaks retrieval granularity)
- Over-documenting routine work
- Forgetting to check existing learnings before starting new work
