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

---

### Solution Design

**Location**: [solution-design/](solution-design/)

**Purpose**: Provides workflows for creating comprehensive execution plans that break down complex features into manageable tasks.

**Workflows**:

1. **Create Execution Plan** - Analyzes tickets and generates detailed implementation plans
2. **Update Plan** - Modifies existing plans while preserving progress
3. **Create Development Log** - Documents completed work and implementation details

**Plan Structure**:
- YAML frontmatter with metadata
- Overview and analysis sections
- Solution approach and architecture
- Phased task breakdown with checkboxes
- Dependencies and testing strategy

**Templates**:
- [solution-design/templates/plan-template.md](solution-design/templates/plan-template.md)
- [solution-design/templates/log-template.md](solution-design/templates/log-template.md)

**Plan Naming Convention**: `{TICKET_ID}_{TYPE}_{Title_Snake_Case}_Plan.md`

**Log Naming Convention**: `{TICKET_ID}_{TYPE}_{Title_Snake_Case}_Log.md`

---

### Stakeholder Management

**Location**: [stakeholder-management/](stakeholder-management/)

**Purpose**: Provides workflows for managing stakeholder information and interaction logs through structured markdown files.

**Workflows**:

1. **Create Stakeholder** - Add new stakeholders with contact information
2. **Update Stakeholder Information** - Modify contact details
3. **Log Interaction** - Record dated interactions with stakeholders
4. **List Stakeholders** - Display all stakeholders in organized format
5. **Search Stakeholders** - Find stakeholders by name, company, or role
6. **Retrieve Interaction Log** - View complete interaction history
7. **Delete Stakeholder** - Remove stakeholders with confirmation

**Stakeholder File Structure**:
- Contact information (name, company, role, email, phone)
- Interaction log with date-based entries (YYYY-MM-DD format)
- Reverse chronological order (newest first)

**Template**: [stakeholder-management/templates/stakeholder-template.md](stakeholder-management/templates/stakeholder-template.md)

**Stakeholder Naming Convention**: `familyname_firstname.md` (lowercase with underscores)

**Storage Location**: `.claude/stakeholders/`

Example: `mueller_anna.md`

## Skill Directory Structure

```
.claude/skills/
├── README.md                                    # This file
├── backlog-management/
│   ├── skill.md                                 # Skill definition
│   └── templates/
│       └── ticket-template.md                   # Ticket template
├── solution-design/
│   ├── skill.md                                 # Skill definition
│   └── templates/
│       ├── plan-template.md                     # Plan template
│       └── log-template.md                      # Development log template
└── stakeholder-management/
    ├── skill.md                                 # Skill definition
    └── templates/
        └── stakeholder-template.md              # Stakeholder template
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
