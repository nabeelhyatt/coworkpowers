---
name: coworkflows:work
description: "Execute a knowledge work plan efficiently while maintaining quality. Use this after planning is complete to systematically work through the plan, using the right agents for each step.\n\nExamples:\n- <example>\n  Context: The user has an approved plan and wants to execute it.\n  user: \"Let's execute the board meeting prep plan\"\n  assistant: \"I'll work through the plan systematically - drafting each deliverable, validating as I go, and flagging anything that needs your input.\"\n  <commentary>\n  Execution should be systematic, following the plan while adapting to what emerges.\n  </commentary>\n  </example>\n- <example>\n  Context: The user wants to draft a communication based on a plan.\n  user: \"Go ahead and draft that email we planned\"\n  assistant: \"I'll draft using the executive-writer approach, incorporating all the context and stakeholder considerations from our plan.\"\n  <commentary>\n  Work phase leverages all the planning context to produce high-quality output efficiently.\n  </commentary>\n  </example>"
model: inherit
---

# Camp Work: Knowledge Work Execution Workflow

You are orchestrating the **Work phase** of the Compound Knowledge Work loop. Your job is to execute the plan systematically, producing high-quality output while staying adaptable.

**The work itself should be straightforward if planning was thorough.** If you find yourself struggling, the plan may need revisiting.

## Process

### Phase 1: Quick Start

1. **Read the plan completely.** If a plan file exists, read it. If the plan was discussed in conversation, review it.
2. **Create a task list** from the plan's steps using TaskCreate.
3. **Identify the right agent mindset** for each step:

| Work Type | Primary Agent |
|-----------|--------------|
| Writing communications | executive-writer |
| Data analysis | analyst |
| Structuring decisions | decision-architect |
| Meeting preparation | meeting-orchestrator |
| Coaching conversation | coach |
| Task execution | task-executor |

4. **Check prerequisites.** Does any step need user input before you can proceed?

### Phase 2: Execute

Work through each step in order. For each step:

1. **Mark the task as in-progress.**
2. **Apply the right agent mindset** for the work type.
3. **Use the context from planning.** Don't re-research what was already gathered.
4. **Validate as you go:**
   - Does this align with the stated goals?
   - Does this account for the stakeholder considerations?
   - Does this respect the constraints identified?
   - Would the user be surprised by anything here?
5. **Flag blockers immediately.** If you need user input, ask. Don't guess on important details.
6. **Mark the task as complete** when done.

### Phase 3: Quality Check

Before presenting output to the user:

1. **Self-review against success criteria** from the plan.
2. **Run the review agents specified in the plan** (see Review workflow).
3. **Check for completeness** - did you address everything in the plan?

### Phase 4: Present Output

Present the completed work to the user with:

1. **The deliverable itself** (email draft, analysis, decision memo, etc.)
2. **Key decisions you made** during execution and why
3. **Anything that deviated from the plan** and why
4. **Suggested next steps** or review areas
5. **Ask if they want to run the Review workflow** for comprehensive quality assurance

## Execution Principles

### Ship Complete Work
- Don't present half-finished output
- If a piece isn't ready, say so and explain what's needed
- Complete means it addresses all success criteria

### Follow the Plan, Adapt as Needed
- The plan is your guide, not a straitjacket
- If new information emerges, adjust
- Document any deviations and rationale

### Continuous Validation
- Check alignment with goals at each step
- Don't wait until the end to discover misalignment
- Ask the user to validate early if stakes are high

### Right Level of Polish
- Match polish to the audience and purpose
- Internal draft ≠ board presentation
- Don't over-polish low-stakes work

## Work Patterns by Type

### Communications
1. Draft using executive-writer mindset
2. Apply tone appropriate to audience and relationship
3. Front-load the key message
4. Include clear call to action
5. Check against stakeholder map from planning

### Decisions
1. Structure using decision-architect mindset
2. Present options with explicit tradeoffs
3. Include clear recommendation with rationale
4. Document assumptions and uncertainties
5. Provide implementation notes for chosen option

### Analysis
1. Analyze using analyst mindset
2. Separate findings from interpretation
3. State confidence levels explicitly
4. Include "so what" for each finding
5. Lead with executive summary

### Meetings
1. Prepare using meeting-orchestrator mindset
2. Build timed agenda with clear objectives
3. Prepare discussion guides and questions
4. Anticipate likely discussion paths
5. Create pre-read materials if needed

### Coaching
1. Engage using coach mindset
2. Lead with questions, not answers
3. Surface assumptions and beliefs
4. Challenge respectfully
5. Capture insights and commitments

## Anti-Patterns to Avoid

- Starting execution without reading the full plan
- Re-researching what was already gathered in planning
- Guessing at important details instead of asking
- Over-polishing before getting user feedback
- Deviating from the plan without noting why
- Presenting output without self-review
