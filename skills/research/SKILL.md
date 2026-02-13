---
name: research
description: "Research and plan a knowledge work task thoroughly before execution. Use when starting any significant piece of work - drafting important communications, making strategic decisions, preparing for meetings, or tackling analysis projects. Triggers on requests like 'help me prepare for', 'I need to draft', 'plan out', or any high-stakes knowledge work."
---

# Research: Knowledge Work Research Workflow

You are orchestrating the **Research phase** of the Compound Knowledge Work loop. Your job is to thoroughly research a task and transform it into an actionable plan that makes execution straightforward.

**80% of compound knowledge work is in research and review.** Do not rush this phase.

## Process

### Phase 1: Understand the Task

1. **Read the task description carefully.** If the user provided a document, file, or URL, read it thoroughly.
2. **Classify the work type:**
   - Communication (email, memo, announcement, presentation)
   - Decision (strategic choice, vendor selection, resource allocation)
   - Analysis (market research, financial analysis, competitive review)
   - Meeting (preparation, facilitation, follow-up)
   - Coaching (leadership challenge, personal effectiveness)
   - Operations (process design, project planning, documentation)

3. **Determine stakes and complexity:**
   - **Low stakes**: Internal notes, routine updates -> lighter planning
   - **Medium stakes**: Team communications, standard decisions -> moderate planning
   - **High stakes**: Board communications, strategic decisions, sensitive topics -> full planning

### Phase 1.5: Ask Clarifying Questions

Before launching research, identify gaps and ask the user clarifying questions. This prevents wasted research on the wrong problem.

**When to ask questions:**
- Task description is vague or has multiple interpretations
- Success criteria are unclear
- Stakeholders or constraints aren't specified
- High-stakes work where misunderstanding would be costly
- User's stated request might differ from their actual need

**Question patterns (from superpowers):**
- **Ask one at a time**, wait for answer before next question
- **Include your hypothesis**: "What does success look like? My hypothesis: [X]"
- **Focus on research-direction questions**: What would change your approach?
- **Catch red flags early**: Political sensitivity, irreversibility, high stakes

**Hard Gate for high-stakes work** - You MUST get answers to:
1. Who is the audience/stakeholder?
2. What does success look like?
3. What constraints exist (political, budget, timing)?
4. What have you tried before that didn't work?

**Example questions:**
- "What does success look like for this communication? My hypothesis: Board approval vs. team buy-in require different approaches"
- "Who is the decision-maker here? This affects stakeholder mapping"
- "What's the timeline? This determines research depth"
- "Are there political sensitivities I should know about?"
- "What have you already tried? What didn't work?"

**When to skip this phase:**
- Low-stakes routine work (internal notes, simple updates)
- User provided comprehensive brief with explicit success criteria
- Task is crystal clear and unambiguous

### Phase 2: Search Past Learnings

Before any new research, check what we already know. This is where compounding pays off.

**In Claude Code** (file-based retrieval):
1. **Check the learnings index** at `.context/learnings/INDEX.md` - scan for matching category, type, and tags.
2. **Search by category**: Grep `.context/learnings/[category]/` for the relevant work type (e.g., `communication/`, `decision/`, `meeting/`).
3. **Search by type**: Look specifically for `pattern` and `template` insights that match the current task.
4. **Search by keywords**: Grep across all learnings for topic-specific terms (stakeholder names, project names, framework names).
5. **Search for preferences**: Grep for `type: preference` insights in the relevant category - these capture style, tone, and detail preferences from previous work.

If past learnings exist, incorporate them into the plan:
- **Reuse patterns** (type: `pattern`) that worked before
- **Avoid failures** (type: `failure`) that were documented
- **Apply templates** (type: `template`) if a relevant one exists
- **Honor preferences** (type: `preference`) from previous work in this category

Surface what you found: "Based on previous [category] work, we learned [X] and have a template for [Y]."

### Phase 3: Parallel Research

Launch research agents in parallel based on the work type. Use the Task tool with appropriate subagents.

**Always run:**
- **context-gatherer**: Research all relevant background - previous communications, related documents, organizational context, domain knowledge

**Run based on work type:**

| Work Type | Additional Agents |
|-----------|-------------------|
| Communication | stakeholder-mapper, precedent-researcher |
| Decision | stakeholder-mapper, constraint-analyzer, precedent-researcher |
| Analysis | constraint-analyzer, precedent-researcher |
| Meeting | stakeholder-mapper, precedent-researcher |
| Coaching | stakeholder-mapper |
| Operations | constraint-analyzer, precedent-researcher |

**For high-stakes work, always add:**
- External research via web search for best practices, frameworks, and examples

### Phase 4: Research Decision

After parallel research returns, assess whether you need additional external research.

**Always research externally when:**
- The topic involves legal, compliance, or regulatory considerations
- The decision is irreversible or very high stakes
- The domain is unfamiliar
- Best practices or industry standards exist that should be consulted

### Phase 5: Synthesize the Plan

Use the **plan-synthesizer** agent mindset to create the final plan.

**Plan Output Format:**

```markdown
# Plan: [Task Name]

## Task Summary
[2-3 sentences: What we're doing, why it matters, what success looks like]

## Context Brief
[Key context gathered - what we know, what matters, what's sensitive]

## Prior Learnings Applied
[What we found from past compound phases, organized by type:
- **Patterns**: [approaches that worked before]
- **Failures**: [mistakes to avoid]
- **Templates**: [reusable structures available]
- **Preferences**: [style/tone/detail preferences for this category]
If none found, state "No prior learnings found for this work type."]

## Stakeholder Considerations
[Who's affected, their interests, anticipated reactions]

## Constraints
[Time, political, resource, or other constraints identified]

## Relevant Precedents
[What's been done before in similar situations, what worked/didn't]

## Approach
[Step-by-step plan for execution]

### Step 1: [Action]
- **What**: [Specific action]
- **Why**: [Rationale]
- **Agent**: [Which work-phase agent to use]
- **Inputs needed**: [What information is required]

### Step 2: [Action]
[Same structure]

## Review Plan
[Which review agents should evaluate the output, and why]

| Reviewer | Why Needed |
|----------|------------|
| [Agent] | [What they'll catch] |

## Success Criteria
- [ ] [Measurable outcome 1]
- [ ] [Measurable outcome 2]
- [ ] [Measurable outcome 3]

## Risks & Mitigations
| Risk | Likelihood | Mitigation |
|------|------------|------------|
| [Risk] | [H/M/L] | [How to address] |

## Timeline
[Suggested sequencing and any time constraints]
```

### Phase 6: User Approval

Present the plan to the user. Ask if they want to:
1. **Approve and proceed** to the Work phase
2. **Modify** specific sections
3. **Add context** you may have missed
4. **Adjust scope** (more or less thorough)

## Important Principles

- **Plans are living documents.** They will be updated during execution.
- **Front-load the thinking.** Every minute spent planning saves ten in execution.
- **Be explicit about assumptions.** If you're guessing, say so.
- **Match rigor to stakes.** A routine email doesn't need a 20-step plan.
- **Include review in the plan.** Every plan should specify which reviewers will check the output.

## Anti-Patterns to Avoid

- Planning so long that urgency passes
- Over-planning low-stakes work
- Skipping stakeholder analysis on communications
- Assuming context instead of gathering it
- Creating plans that are too abstract to execute
