# Solution Design Skill

You are assisting with solution design operations. This skill provides workflows for creating and managing execution plans for tickets.

## Directory Structure

Plans are stored in:
- `.claude/plans/` - Execution plans for tickets
- `.claude/skills/solution-design/templates/` - Plan templates

## Plan Template

The standard plan template is located at:
`.claude/skills/solution-design/templates/plan-template.md`

This template includes all required sections with placeholders.

## Available Workflows

### 1. Create Execution Plan

Generate a comprehensive execution plan for a ticket.

**Steps:**
1. **Locate and read the ticket**
   - Find ticket in `.claude/backlog/` by ID or filename
   - Read all sections: summary, user story, acceptance criteria, technical considerations
   - Note the "Initial Request" for original context

2. **Analyze requirements**
   - Identify core functionality needed
   - Understand business goals and constraints
   - Extract technical requirements
   - Assess complexity and risks
   - Consider integration points

3. **Design solution**
   - Determine technical approach
   - Make architectural decisions
   - Identify components and dependencies
   - Map out workflow integration
   - Document data flow

4. **Break down into tasks**
   - Divide into logical phases
   - Create specific, actionable tasks
   - Order by dependencies
   - Add checkboxes for tracking
   - Include setup, implementation, testing, documentation

5. **Generate plan file**
   - Determine filename: `{TICKET_ID}_{TYPE}_{Title_Snake_Case}_Plan.md`
   - Populate all template sections
   - Save to `.claude/plans/`

6. **Validate plan**
   - Verify comprehensiveness
   - Check task actionability
   - Confirm proper formatting
   - Ensure resumability support

### 2. Update Execution Plan

Modify an existing plan when requirements change.

**Steps:**
1. **Read current plan and ticket**
   - Load plan from `.claude/plans/`
   - Note completed tasks (checked boxes)
   - Read updated ticket requirements

2. **Identify changes**
   - Compare ticket with plan
   - Determine impact on tasks
   - Assess what needs updating

3. **Update plan**
   - Modify affected sections
   - Add/remove/modify tasks
   - **Preserve completed checkboxes**
   - Update "Updated" date in frontmatter
   - Add notes about changes

4. **Save updated plan**
   - Overwrite existing file
   - Maintain same filename

## Plan Structure Requirements

Every plan must include these sections:

1. **YAML Frontmatter** - Ticket metadata
2. **Overview** - Brief summary
3. **Analysis** - Problem understanding, current state, gaps
4. **Solution Approach** - Design philosophy, technical approach, key decisions
5. **Architecture** - Component structure, workflow integration, data flow
6. **Tasks** - Phased, ordered, checkboxed tasks
7. **Dependencies** - External, task, and phase dependencies
8. **Testing Strategy** - Unit, integration, validation criteria
9. **Rollout Considerations** - Implementation order, success metrics, future enhancements
10. **Notes** - Design considerations and references

## File Naming Convention

Plans must match their ticket filename with `_Plan` suffix:
- Format: `{TICKET_ID}_{TYPE}_{Title_Snake_Case}_Plan.md`
- Location: `.claude/plans/`
- Example: `0003_Feature_Solution_Designer_Agent_Plan.md`

## Task Writing Guidelines

### Good Tasks
- Specific and clear
- Actionable immediately
- Include checkbox `- [ ]`
- Properly sequenced
- Small enough to complete in one session

### Task Format
```markdown
- [ ] Task description: Clear action to take
  - Sub-detail or context
  - Dependencies if any
```

## Important Notes

- Plans enable work resumption after interruptions
- Any developer should be able to execute tasks
- Preserve completed checkboxes when updating
- Group related tasks into phases
- Document design decisions with rationale
- Include testing in task breakdown
- Consider future enhancements but keep them out of scope
