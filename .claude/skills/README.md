# Claude Skills

This directory contains skills that provide specialized workflows and capabilities for agents.

## Available Skills

### Backlog Management

**Location**: [backlog-management/](backlog-management/)

**Purpose**: Provides workflows for managing product tickets in the `.claude/backlog/` directory.

**Workflows**:

1. **Initialize Backlog** - Creates the folder structure for organizing tickets
2. **Prepare Ticket** - Converts raw notes/requests into structured tickets
3. **Update Ticket** - Modifies existing ticket fields
4. **Close Ticket** - Marks tickets as complete and moves them to Done folder

**Folder Structure**:
```
.claude/backlog/
├── 0_Done/       # Completed tickets
├── 1_WIP/        # Work in progress
├── 2_To_Do/      # Ready to work on
├── 3_To_Plan/    # Need planning/refinement
├── 4_Wait/       # On hold/blocked
└── 5_Archive/    # Archived tickets
```

**Ticket Format**:

Tickets use a structured markdown format with frontmatter containing:
- Epic, ID, Title, Type, Status, Dates, Priority, Sprint
- Summary, User Story, Acceptance Criteria, Initial Request

**Template**: [backlog-management/templates/ticket-template.md](backlog-management/templates/ticket-template.md)

**Ticket Naming Convention**: `{TICKET_ID}_{TYPE}_{Title_Snake_Case}.md`

Example: `0001_Feature_User_Authentication.md`

## Skill Directory Structure

```
.claude/skills/
├── README.md                                    # This file
└── backlog-management/
    ├── skill.md                                 # Skill definition
    └── templates/
        └── ticket-template.md                   # Ticket template
```

## Creating New Skills

To create a new skill:

1. Create a new directory under `.claude/skills/`
2. Add a `skill.md` file with the skill definition
3. Include any templates or supporting files in subdirectories
4. Update this README with the new skill information
5. Reference the skill in relevant agent configurations

## Best Practices

- Keep skills focused on specific domains or workflows
- Use templates for consistent output formatting
- Document all workflows clearly with step-by-step instructions
- Include examples where helpful
- Make skills reusable across multiple agents
