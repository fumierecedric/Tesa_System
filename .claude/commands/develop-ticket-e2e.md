# Develop Ticket End-to-End Command

Execute the complete development workflow from ticket creation through closure.

## Overview

This command orchestrates the full ticket lifecycle:
1. **Create Ticket** (Product Owner)
2. **Create Plan** (Solution Designer)
3. **Execute Implementation**
4. **Create Log** (Solution Designer)
5. **Close Ticket** (Product Owner)

## Instructions

You will guide the user through each step of the development workflow. Execute each step in sequence, providing clear progress updates.

---

### Step 1: Create Ticket (Product Owner)

Execute the "Prepare Ticket" workflow from the Backlog Management skill.

**Actions:**
- Ask clarifying questions to understand requirements
- Gather all necessary information (Epic, Title, Type, Priority, Sprint, User Story, Acceptance Criteria)
- Create ticket in `.claude/backlog/1_WIP/`
- Assign next available ticket ID
- Delete original note file if applicable

**Output:** Ticket created at `.claude/backlog/1_WIP/{TICKET_ID}_{TYPE}_{Title}.md`

---

### Step 2: Create Execution Plan (Solution Designer)

Execute the "Create Execution Plan" workflow from the Solution Design skill.

**Actions:**
- Read and analyze the ticket
- Understand requirements from user story and acceptance criteria
- Design comprehensive solution
- Break down into phased, actionable tasks
- Create plan file in `.claude/plans/`

**Output:** Plan created at `.claude/plans/{TICKET_ID}_{TYPE}_{Title}_Plan.md`

---

### Step 3: Execute Implementation

Follow the execution plan and implement the feature.

**Actions:**
- Read the execution plan
- Execute tasks in order, checking them off as completed
- Update plan status as work progresses
- Handle issues and document deviations
- Verify implementation meets acceptance criteria

**Output:** Implementation complete, all plan tasks checked off

---

### Step 4: Create Development Log (Solution Designer)

Execute the "Create Development Log" workflow from the Solution Design skill.

**Actions:**
- Review completed work
- Gather implementation details
- Document deviations from plan
- Capture technical decisions and issues
- List all files created/modified
- Create log file in `.claude/logs/`

**Output:** Log created at `.claude/logs/{TICKET_ID}_{TYPE}_{Title}_Log.md`

---

### Step 5: Close Ticket (Product Owner)

Execute the "Close Ticket" workflow from the Backlog Management skill.

**Actions:**
- Verify ticket is ready to close
- Update ticket status to `0_Done`
- Update `Updated` date
- Move ticket to `.claude/backlog/0_Done/`
- Confirm successful closure

**Output:** Ticket closed at `.claude/backlog/0_Done/{TICKET_ID}_{TYPE}_{Title}.md`

---

## Usage

Run this command with a requirement description:

```
/develop-ticket-e2e
<Describe the feature or provide note file reference>
```

Or simply:

```
/develop-ticket-e2e
```

Then provide the requirement when prompted.

## Important Notes

- **Sequential execution**: Each step must complete before proceeding to the next
- **User confirmation**: Between major steps, confirm completion before continuing
- **Error handling**: If a step fails, address the issue before proceeding
- **Flexibility**: Steps can be adjusted based on context (e.g., skip Step 1 if ticket already exists)
- **Documentation**: Ensure log captures actual implementation details

## State Management

This command completes in a single session. If interrupted:
- Note which step was last completed
- Resume from the next step
- All artifacts (ticket, plan, log) are preserved

## Success Criteria

The workflow is complete when:
- ✓ Ticket exists in `.claude/backlog/0_Done/`
- ✓ Plan exists in `.claude/plans/` with all tasks checked
- ✓ Log exists in `.claude/logs/` documenting implementation
- ✓ Ticket status is `0_Done`
- ✓ All acceptance criteria are met

---

**Now begin Step 1: Create Ticket**

If the user has provided a requirement, use that to start the ticket creation process. Otherwise, ask what they would like to build.
