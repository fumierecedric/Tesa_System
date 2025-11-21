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

### Meeting Assistant

**File**: [meeting-assistant.md](meeting-assistant.md)

**Purpose**: Processes meeting transcripts to extract key information and coordinates with specialized agents for meeting-related workflows.

**Skills**:
- Transcript Processing
- Stakeholder Extraction
- Knowledge Capture (placeholder for future)
- Meeting Preparation

**Use Cases**:
- Extracting stakeholder information from meeting transcripts
- Coordinating with HR agent for stakeholder file creation
- Preparing agendas for upcoming meetings based on previous discussions
- Capturing knowledge items from technical or strategic meetings (placeholder)
- Multi-agent coordination for meeting follow-up workflows

**How to Use**:

The Meeting Assistant processes transcript files from `.claude/meetings/transcripts/` and coordinates with other agents. When you need to work with meeting transcripts:

1. Create a meeting-related ticket with clear instructions
2. Reference the transcript file (format: `YYYYMMDD-HHMMSS MeetingName-transcript.md`)
3. Specify what to extract (stakeholders, knowledge, action items)
4. Meeting Assistant reads transcript and delegates to appropriate agents
5. All outputs include links back to source transcript for traceability

**Example Interactions**:

```
"Extract stakeholder info from 20251120-120000 Call Hugues on Tesa-transcript.md"
"Prepare agenda for next meeting with Antoine based on previous call transcript"
"Process meeting transcript to identify key business insights and stakeholders"
"Create stakeholder files for all participants in today's standup meeting"
```

**Output**:

Meeting Assistant coordinates multiple outputs:
- Stakeholder files created via HR agent in `.claude/stakeholders/`
- Meeting agendas with context and transcript links
- Knowledge items documented (future: Knowledge Manager integration)
- All outputs maintain traceability to source transcripts

### HR Agent

**File**: [hr.md](hr.md)

**Purpose**: Manages stakeholder information and maintains comprehensive records of all interactions and key information.

**Skills**:
- Stakeholder Management

**Use Cases**:
- Creating new stakeholder files
- Updating stakeholder contact information
- Logging interactions with stakeholders
- Searching for stakeholders by name, company, or role
- Retrieving interaction history
- Managing stakeholder lifecycle

**How to Use**:

The HR agent manages stakeholder files in `.claude/stakeholders/`. When you need to work with stakeholders:

1. Provide stakeholder information (name, company, role, contact details)
2. Agent creates or updates stakeholder files using standardized template
3. Log interactions with date-based entries
4. Search and retrieve stakeholder information as needed

**Example Interactions**:

```
"Add a new stakeholder: Jane Smith, XYZ Inc, CTO, jane.smith@xyz.com"
"Log interaction with John Doe: Discussed Q4 budget allocation"
"Search for stakeholders at Tesa SE"
"Show me the interaction log for Anna Mueller"
"Update Jane Smith's phone number to +1-555-0199"
```

**Output**:

Stakeholder files are saved to `.claude/stakeholders/` with naming format: `familyname_firstname.md`

Each stakeholder file includes:
- Contact information (name, company, role, email, phone)
- Interaction log with date-based entries
- Professional interaction history tracking

## Agent Directory Structure

```
.claude/agents/
├── README.md              # This file
├── product-owner.md       # Product Owner agent configuration
├── solution-designer.md   # Solution Designer agent configuration
├── meeting-assistant.md   # Meeting Assistant agent configuration
└── hr.md                  # HR agent configuration
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

### Meeting-Specific Workflow

For meeting-related tickets, the workflow includes agent coordination:

```
1. Meeting Transcript → .claude/meetings/transcripts/
   ↓
2. Product Owner → Creates meeting ticket → .claude/backlog/1_WIP/
   ↓
3. Solution Designer → Recognizes meeting ticket → Assigns to Meeting Assistant
   ↓
4. Meeting Assistant → Reads transcript → Extracts information
   ↓
   ├─→ Stakeholders found → HR Agent → .claude/stakeholders/
   ├─→ Knowledge found → (Future: Knowledge Manager) → Knowledge base
   └─→ Meeting prep needed → Creates agenda → Specified location
   ↓
5. Completed Coordination (all outputs include transcript links)
```

## Creating New Agents

To create a new agent:

1. Create a new `.md` file in this directory
2. Define the agent's role, responsibilities, and skills
3. Document the agent's working style and principles
4. Update this README with the new agent information
