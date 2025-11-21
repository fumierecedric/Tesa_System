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

## Agent Directory Structure

```
.claude/agents/
├── README.md              # This file
└── product-owner.md       # Product Owner agent configuration
```

## Creating New Agents

To create a new agent:

1. Create a new `.md` file in this directory
2. Define the agent's role, responsibilities, and skills
3. Document the agent's working style and principles
4. Update this README with the new agent information
