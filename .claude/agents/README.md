# Claude Agents

This directory contains agent configurations for specialized roles in the project.

## Available Agents

### Product Owner (PO)

**File**: [product-owner.md](product-owner.md)

**Purpose**: Manages the product backlog and ensures tickets are well-defined, prioritized, and actionable.

**Skills**:
- Backlog Management

**Use Cases**:
- Creating new tickets from requirements or raw notes
- Updating existing ticket information
- Closing completed tickets
- Organizing and prioritizing the backlog

**How to Use**:

The Product Owner agent will help you manage tickets in the `.claude/backlog/` directory. When you need to create or manage tickets, the PO will:

1. Ask clarifying questions to understand requirements fully
2. Gather necessary information (Epic, Priority, Type, etc.)
3. Create structured tickets using the standard template
4. Keep the backlog organized and up-to-date

**Example Interactions**:

```
"I need to create a ticket for adding user authentication"
"Update ticket 0042 to change priority to High"
"Close ticket 0015 as completed"
"Show me all tickets in the WIP folder"
```

### Solution Designer

**File**: [solution-designer.md](solution-designer.md)

**Purpose**: Analyzes ticket requirements and creates comprehensive execution plans that break down complex features into manageable, trackable tasks.

**Skills**:
- Solution Design

**Use Cases**:
- Creating execution plans for tickets in 3_To_Plan
- Breaking down complex features into actionable tasks
- Designing technical approaches and architectures
- Updating plans when requirements change
- Enabling work resumption after interruptions

**How to Use**:

The Solution Designer agent analyzes tickets and generates detailed plans in `.claude/plans/`. When you need a plan:

1. Ensure ticket is complete with user story and acceptance criteria
2. Invoke Solution Designer with ticket reference
3. Agent analyzes requirements and designs solution
4. Generates structured plan with phased, trackable tasks
5. Plan enables any developer to execute and track progress

**Example Interactions**:

```
"Create a plan for ticket 0003"
"Design a solution for the user authentication feature"
"Update the plan for ticket 0042 with new requirements"
"Generate an execution plan for the bug fix in ticket 0015"
```

**Output**:

Plans are saved to `.claude/plans/` with naming format: `{TICKET_ID}_{TYPE}_{Title_Snake_Case}_Plan.md`

Each plan includes:
- Problem analysis and solution approach
- Architecture and technical decisions
- Phased task breakdown with checkboxes
- Dependencies and testing strategy
- Implementation guidance

## Agent Directory Structure

```
.claude/agents/
├── README.md              # This file
├── product-owner.md       # Product Owner agent configuration
└── solution-designer.md   # Solution Designer agent configuration
```

## Workflow Integration

The agents work together in a coordinated workflow:

```
1. User Request
   ↓
2. Product Owner → Creates structured ticket → .claude/backlog/1_WIP/
   ↓
3. Ticket moved to → .claude/backlog/3_To_Plan/
   ↓
4. Solution Designer → Reads ticket → Generates plan → .claude/plans/
   ↓
5. Development Agent(s) → Read plan → Execute tasks → Check off progress
   ↓
6. Completed Implementation
```

## Creating New Agents

To create a new agent:

1. Create a new `.md` file in this directory
2. Define the agent's role, responsibilities, and skills
3. Document the agent's working style and principles
4. Update this README with the new agent information
