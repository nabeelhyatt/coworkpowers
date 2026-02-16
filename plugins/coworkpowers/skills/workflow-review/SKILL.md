---
name: workflow-review
description: "Run parallel multi-agent review on completed knowledge work. Use after the work phase to evaluate output quality from multiple specialized perspectives before finalizing. Triggers on requests like 'review this', 'check this before I send it', 'stress-test this recommendation', or when quality assurance is needed on a deliverable."
---

# Review: Multi-Agent Knowledge Work Review

You are orchestrating the **Review phase** of the Compound Knowledge Work loop. Your job is to evaluate completed work from multiple specialized perspectives and synthesize findings into actionable improvements.

**Different perspectives catch different issues.** A single reviewer misses things that parallel review catches.

## Process

### Phase 1: Determine Review Scope

1. **Read the completed work** thoroughly.
2. **Identify the work type** to select appropriate reviewers:

| Work Type | Standard Reviewers | Conditional Reviewers |
|-----------|-------------------|----------------------|
| Communication | clarity-reviewer, tone-calibrator, completeness-auditor | sensitivity-scanner (if sensitive topic), strategic-alignment-checker (if strategic) |
| Decision | completeness-auditor, risk-assessor, devil's-advocate, actionability-validator | strategic-alignment-checker (if organizational), sensitivity-scanner (if political) |
| Analysis | completeness-auditor, clarity-reviewer, actionability-validator | risk-assessor (if recommendations included), devil's-advocate (if controversial) |
| Meeting prep | completeness-auditor, actionability-validator, clarity-reviewer | stakeholder-mapper (if complex dynamics), sensitivity-scanner (if contentious topics) |
| Coaching notes | clarity-reviewer, actionability-validator | tone-calibrator (if shared with coachee) |

3. **Check if the plan specified reviewers.** If so, use those as the baseline.

### Phase 2: Parallel Agent Review

Launch all selected review agents in parallel using the Task tool.

Each agent reviews independently and returns findings in their specialized format.

**Agent Instructions:**
- Each agent receives the complete work output
- Each agent applies its specialized lens
- Each agent returns findings with severity levels

### Phase 3: Synthesize Findings

After all agents return, synthesize their findings:

**Output Format:**

```markdown
## Review Summary

### Overall Assessment
**Quality Score**: [1-10]
[2-3 sentence assessment of overall quality and readiness]

### Critical Issues (Must Fix)
Issues that would cause real problems if not addressed.

#### Issue 1: [Title]
- **Found by**: [Agent name]
- **Location**: [Where in the document]
- **Problem**: [What's wrong]
- **Impact**: [What happens if not fixed]
- **Fix**: [Specific recommendation]

### Important Issues (Should Fix)
Issues that meaningfully improve quality.

#### Issue 1: [Title]
- **Found by**: [Agent name]
- **Location**: [Where in the document]
- **Problem**: [What's wrong]
- **Fix**: [Specific recommendation]

### Minor Issues (Nice to Fix)
Polish and refinement opportunities.

- [Issue]: [Quick fix] _(found by [agent])_
- [Issue]: [Quick fix] _(found by [agent])_

### What's Working Well
- [Strength 1] _(noted by [agent])_
- [Strength 2] _(noted by [agent])_

### Conflicting Feedback
[If agents disagree, note the conflict and recommend resolution]

### Recommended Action
- [ ] Fix critical issues (estimated: [time])
- [ ] Fix important issues (estimated: [time])
- [ ] Fix minor issues (estimated: [time])
- [ ] Ready to finalize after fixes
```

### Phase 4: Apply Fixes

If the user approves:

1. **Fix critical issues first.**
2. **Fix important issues.**
3. **Fix minor issues if time permits.**
4. **Present the revised version** with a summary of changes made.

If issues conflict, present the tradeoff to the user and let them decide.

## Review Principles

### Severity Calibration

- **Critical**: Would cause real damage - wrong tone in sensitive email, missing key stakeholder concern, factual error in analysis, flawed logic in decision
- **Important**: Meaningful quality improvement - unclear structure, missing context, weak evidence, incomplete consideration
- **Minor**: Polish - word choice, formatting, small redundancies

### Independence Matters
- Each agent reviews independently
- Don't let one agent's findings influence another
- Conflicts between agents are valuable signal

### Review Should Be Proportional
- Quick internal note: clarity-reviewer only
- Important email: clarity + tone + completeness
- Board presentation: all standard + conditional reviewers
- Strategic decision: all reviewers including devil's-advocate

### The Devil's Advocate is Special
- Always include for decisions and recommendations
- Its job is to find the strongest counterargument
- Don't dismiss its findings just because you disagree
- If the devil's advocate can't find a good counterargument, that's strong validation

## Next Step

When the work is finalized, capture what you learned: **`/coworkpowers:workflow-compound`**

## Anti-Patterns to Avoid

- Running review on low-stakes work (wastes time)
- Ignoring conflicting feedback instead of resolving it
- Treating all findings as equal severity
- Over-revising based on minor feedback
- Not running devil's advocate on important decisions
- Applying fixes without user awareness of what changed
