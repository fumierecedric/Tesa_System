---
Ticket: 0008
Title: Meeting Assistant Agent
Created: 2025-11-21
Updated: 2025-11-21
Status: Completed
---

## Overview

Create a Meeting Assistant agent that processes meeting transcripts to extract key information (stakeholders, knowledge, action items) and orchestrates other specialized agents (HR, Knowledge Manager) to handle extracted data. The agent will also prepare agendas for upcoming meetings based on transcript analysis.

This agent serves as an intelligent coordinator that understands meeting context and delegates specific tasks to appropriate specialized agents, enabling efficient meeting follow-up and preparation workflows.

## Analysis

### Problem Understanding

Project managers need to efficiently process meeting outcomes and extract actionable information from meeting transcripts. Currently, there's no systematic way to:
- Extract stakeholder information from meeting discussions
- Capture and organize knowledge shared during meetings
- Prepare for upcoming meetings with context from previous discussions
- Coordinate follow-up tasks across different domains (HR, knowledge management, meeting prep)

Manual processing of transcripts is time-consuming and prone to inconsistency or missed information.

### Current State

- Meeting transcripts are stored in `.claude/meetings/transcripts/` with format `YYYYMMDD-HHMMSS MeetingName-transcript.md`
- HR agent exists and can manage stakeholder information
- Solution Designer exists but doesn't recognize "meeting" type tickets
- No Knowledge Manager agent exists yet (planned future)
- No automated way to extract information from transcripts
- No agent coordination for meeting-related workflows

### Gaps to Address

1. No Meeting Assistant agent to process transcripts
2. No "meeting" ticket type recognition in Solution Designer
3. No coordination mechanism between Meeting Assistant and other agents
4. No structured workflow for extracting and delegating meeting information
5. No meeting preparation capability based on transcript analysis
6. No Knowledge Manager agent (placeholder integration needed)

## Solution Approach

### Design Philosophy

- **Orchestration over execution**: Meeting Assistant coordinates specialized agents rather than doing everything itself
- **Context preservation**: Always link back to source transcripts for traceability
- **Flexible delegation**: Support both existing agents (HR) and future agents (Knowledge Manager) through clear interfaces
- **Instruction-driven**: User provides synthetic instructions in tickets about what to extract and how to handle it
- **Resumable workflows**: Support interruption and continuation of multi-step processes

### Technical Approach

1. Create Meeting Assistant agent with clear role definition and responsibilities
2. Design agent to read and parse transcript files from designated directory
3. Implement instruction parsing to understand user's extraction requirements
4. Create coordination mechanism to trigger other agents with context
5. Build meeting preparation capability with agenda generation
6. Update Solution Designer to recognize "meeting" type tickets
7. Document integration points for future Knowledge Manager agent

### Key Design Decisions

- **Agent file location**: `.claude/agents/meeting-assistant.md` (consistent with existing agents)
- **No skill file needed initially**: Meeting Assistant's workflows are simple enough to be embedded in agent definition
- **Ticket type**: Use existing "Feature", "Bug", "Improvement" types with "meeting" tag or reference in title/description rather than creating new ticket type
- **Agent invocation**: Meeting Assistant instructions will be in ticket description; no separate slash command needed initially
- **Transcript links**: Include file path links in markdown format `[transcript](path/to/transcript.md)` for easy navigation
- **Placeholder pattern**: Use clear documentation for Knowledge Manager integration without implementing full functionality

## Architecture

### Component Structure

```
.claude/
├── agents/
│   ├── meeting-assistant.md       # NEW: Meeting Assistant agent definition
│   ├── hr.md                       # EXISTING: HR agent (stakeholder management)
│   ├── solution-designer.md        # MODIFIED: Add meeting ticket recognition
│   └── product-owner.md            # EXISTING: Unchanged
├── meetings/
│   └── transcripts/                # EXISTING: Meeting transcript storage
│       └── YYYYMMDD-HHMMSS MeetingName-transcript.md
├── stakeholders/                   # EXISTING: Stakeholder files managed by HR agent
└── backlog/                        # EXISTING: Tickets including meeting-related ones
```

### Workflow Integration

```
User creates meeting ticket → Product Owner → .claude/backlog/1_WIP/
                                                         ↓
                            Solution Designer recognizes "meeting" reference
                                                         ↓
                               Creates plan assigning work to Meeting Assistant
                                                         ↓
                            Meeting Assistant reads transcript + ticket instructions
                                                         ↓
                                         ┌───────────────┼───────────────┐
                                         ↓               ↓               ↓
                          Extract stakeholders   Extract knowledge   Prepare next meeting
                                         ↓               ↓               ↓
                              Trigger HR agent   (Future: Knowledge   Create agenda with
                              with context       Manager agent)       transcript context
                                         ↓               ↓               ↓
                          Stakeholder files     Knowledge entries     Meeting prep doc
                          created/updated       (placeholder)         created
```

### Data Flow

1. **Input**:
   - Meeting transcript file path (from ticket)
   - User instructions (what to extract, what to do with it)
   - Meeting context (date, participants, type)

2. **Processing**:
   - Meeting Assistant reads transcript
   - Parses user instructions from ticket
   - Extracts relevant information based on instructions
   - Categorizes extracted info by target agent (HR, Knowledge Manager, self)
   - Generates context-rich delegation instructions

3. **Output**:
   - Stakeholder creation/update requests to HR agent (with transcript link)
   - Knowledge capture requests to Knowledge Manager (placeholder, with transcript link)
   - Meeting agendas for upcoming meetings (with transcript link)
   - Task completion confirmation

4. **Storage**:
   - Stakeholder files in `.claude/stakeholders/` (via HR agent)
   - Knowledge entries in future location (via Knowledge Manager)
   - Meeting agendas in designated location (TBD based on need)

## Tasks

### Phase 1: Foundation Setup

- [x] Create Meeting Assistant agent file
  - Create `.claude/agents/meeting-assistant.md`
  - Define agent role and responsibilities
  - Document coordination with HR agent and future Knowledge Manager
  - Include examples of meeting-related workflows
  - Add transcript reading and parsing guidelines

- [x] Update agents README
  - Add Meeting Assistant section to `.claude/agents/README.md`
  - Document purpose, use cases, and example interactions
  - Include workflow integration diagram

### Phase 2: Solution Designer Integration

- [x] Update Solution Designer to recognize meeting tickets
  - Modify `.claude/agents/solution-designer.md`
  - Add "Agent Coordination" section for Meeting Assistant (similar to HR agent section)
  - Include guidance on when to involve Meeting Assistant
  - Document meeting ticket patterns (title/description keywords)

- [x] Add meeting workflow example
  - Add example of plan with Meeting Assistant task assignments
  - Show how to delegate to Meeting Assistant with transcript reference

### Phase 3: Agent Capabilities Implementation

- [x] Document transcript reading workflow
  - Add clear instructions for locating transcripts in `.claude/meetings/transcripts/`
  - Define filename parsing pattern `YYYYMMDD-HHMMSS MeetingName-transcript.md`
  - Include error handling for missing or malformed transcripts

- [x] Document stakeholder extraction workflow
  - Define what stakeholder information to look for (names, companies, roles, contacts)
  - Specify format for triggering HR agent
  - Include transcript link in delegation context

- [x] Document Knowledge Manager placeholder integration
  - Define future interface for Knowledge Manager agent
  - Specify what knowledge information should be extracted
  - Create clear placeholder pattern for future implementation
  - Document expected Knowledge Manager capabilities

- [x] Document meeting preparation workflow
  - Define agenda structure and content
  - Specify how to reference previous meeting context
  - Include transcript links for continuity
  - Determine storage location for meeting prep docs

### Phase 4: Testing & Validation

- [x] Test Meeting Assistant with stakeholder extraction
  - Create test meeting ticket with stakeholder extraction instructions
  - Use existing transcript file
  - Verify Meeting Assistant correctly identifies stakeholders
  - Confirm HR agent is properly triggered with transcript link
  - Validate stakeholder file creation
  - **TESTED**: Updated villeret_hugues.md with interaction from 20251121 transcript

- [x] Test meeting preparation workflow
  - Create test ticket for meeting agenda preparation
  - Reference previous transcript
  - Verify agenda is created with appropriate context
  - Check transcript link inclusion
  - **TESTED**: Created agenda for Jonas meeting based on onboarding transcript

- [x] Test Knowledge Manager placeholder
  - Document expected behavior for Knowledge Manager integration
  - Verify placeholder instructions are clear
  - Ensure future integration path is well-defined
  - **COMPLETED**: Placeholder documented in meeting-assistant.md

- [x] Validate Solution Designer recognition
  - Create meeting-related ticket
  - Verify Solution Designer suggests Meeting Assistant
  - Check plan includes appropriate agent coordination
  - **COMPLETED**: Solution Designer updated with Meeting Assistant coordination section

### Phase 5: Documentation & Examples

- [x] Add comprehensive examples to Meeting Assistant agent file
  - Example 1: Stakeholder extraction from sales meeting
  - Example 2: Meeting preparation for recurring standup
  - Example 3: Knowledge capture (placeholder) from technical discussion
  - Example 4: Multi-agent coordination workflow
  - **COMPLETED**: All 4 examples included in meeting-assistant.md

- [x] Document best practices
  - How to write clear extraction instructions in tickets
  - When to use Meeting Assistant vs manual processing
  - How to structure meeting tickets for optimal results
  - **COMPLETED**: Best practices section included in meeting-assistant.md

- [x] Update project documentation
  - Add Meeting Assistant to workflow documentation if needed
  - Update any relevant guides or README files
  - **COMPLETED**: Updated agents/README.md with Meeting Assistant and workflow diagram

## Dependencies

### External Dependencies

- **HR Agent** (`.claude/agents/hr.md`): Existing agent for stakeholder management
- **Solution Designer** (`.claude/agents/solution-designer.md`): Must recognize meeting tickets
- **Transcript files**: Meeting transcripts must exist in `.claude/meetings/transcripts/`
- **Stakeholder Management Skill**: Used by HR agent for stakeholder operations

### Task Dependencies

- Phase 1 must complete before Phase 2 (need agent definition before updating Solution Designer)
- Phase 2 must complete before Phase 3 (need recognition in place before implementing capabilities)
- Phase 3 must complete before Phase 4 (need capabilities before testing)
- Phase 4 should complete before Phase 5 (validate before finalizing documentation)

### Sequential Phases

1. **Phase 1**: Foundation Setup (agent creation, README update)
2. **Phase 2**: Solution Designer Integration (enable recognition)
3. **Phase 3**: Agent Capabilities Implementation (workflows and coordination)
4. **Phase 4**: Testing & Validation (ensure everything works)
5. **Phase 5**: Documentation & Examples (polish and guide users)

## Testing Strategy

### Unit Testing

- **Test transcript reading**: Verify agent can locate and read transcript files
- **Test filename parsing**: Confirm correct extraction of date, time, and meeting name
- **Test instruction parsing**: Validate agent understands user extraction requirements
- **Test stakeholder identification**: Check extraction of names, companies, roles
- **Test HR agent coordination**: Verify proper delegation format and context passing

### Integration Testing

- **End-to-end stakeholder extraction**: Full workflow from ticket creation through stakeholder file creation
- **Meeting preparation workflow**: Complete cycle from transcript analysis to agenda creation
- **Solution Designer integration**: Test ticket recognition and plan generation
- **Multi-agent coordination**: Verify Meeting Assistant → HR agent → Stakeholder file flow

### Validation Criteria

- [ ] Meeting Assistant agent file is complete and follows existing agent patterns
- [ ] Solution Designer correctly identifies meeting-related tickets
- [ ] Meeting Assistant can read and process transcript files
- [ ] Stakeholder extraction successfully triggers HR agent with transcript context
- [ ] Knowledge Manager placeholder is documented with clear future integration path
- [ ] Meeting preparation workflow produces useful agendas with transcript links
- [ ] All acceptance criteria from ticket 0008 are met

## Rollout Considerations

### Implementation Order

1. **Start with foundation** (Phase 1): Create agent file and update README
2. **Enable recognition** (Phase 2): Update Solution Designer for meeting tickets
3. **Build capabilities** (Phase 3): Implement workflows and coordination mechanisms
4. **Validate thoroughly** (Phase 4): Test all workflows before considering complete
5. **Polish documentation** (Phase 5): Ensure users can leverage Meeting Assistant effectively

### Success Metrics

- **Meeting Assistant agent exists** with clear role definition at `.claude/agents/meeting-assistant.md`
- **Solution Designer updated** to recognize and delegate meeting-related tickets
- **Transcript processing works**: Agent can read files from `.claude/meetings/transcripts/`
- **Agent coordination successful**: Meeting Assistant correctly triggers HR agent
- **Placeholder documented**: Clear path for future Knowledge Manager integration
- **Meeting preparation functional**: Agendas created with transcript context
- **Examples provided**: Users understand how to use Meeting Assistant effectively

### Future Enhancements (Out of Scope)

- **Knowledge Manager agent**: Full implementation of knowledge capture and organization
- **Automated action item tracking**: Extract and track action items from meetings
- **Meeting attendance tracking**: Link attendees to stakeholder files automatically
- **Transcript search capability**: Find information across multiple transcripts
- **Meeting analytics**: Generate insights from meeting patterns and content
- **Calendar integration**: Automatically schedule follow-ups based on meeting discussions
- **Template-based agendas**: Pre-defined agenda templates for different meeting types

## Notes

### Design Considerations

**Why no skill file initially?**
The Meeting Assistant's workflows are straightforward and can be documented directly in the agent file. If complexity grows (e.g., multiple sub-workflows, complex coordination patterns), we can extract to a skill file later.

**Why not create a new "meeting" ticket type?**
The existing type system (Feature, Bug, Improvement) is sufficient. We can use ticket title/description keywords (e.g., "meeting:", "transcript:", or tag-like markers) to trigger Meeting Assistant involvement. This avoids modifying the core ticket structure.

**How to handle Knowledge Manager placeholder?**
Document the expected interface clearly in the Meeting Assistant agent file:
- What information should be extracted (key insights, decisions, technical details)
- How the knowledge should be categorized
- What format the Knowledge Manager should expect
- Include a clear "TODO" or "FUTURE" marker for implementation

**Agent coordination pattern:**
Use a narrative delegation style: Meeting Assistant includes instructions like "Please adopt the HR agent role and create a stakeholder file for [Name] based on the information in [transcript link]". This maintains flexibility and human-readable coordination.

**Transcript link format:**
Use markdown relative links: `[transcript](.claude/meetings/transcripts/20251120-120000 Call Hugues on Tesa-transcript.md)` for easy navigation in VS Code and other markdown viewers.

### References

- **Ticket**: [0008_Feature_Meeting_Assistant_Agent.md](.claude/backlog/1_WIP/0008_Feature_Meeting_Assistant_Agent.md)
- **HR Agent**: [.claude/agents/hr.md](.claude/agents/hr.md)
- **Solution Designer**: [.claude/agents/solution-designer.md](.claude/agents/solution-designer.md)
- **Existing transcripts**: [.claude/meetings/transcripts/](.claude/meetings/transcripts/)
- **Agent README**: [.claude/agents/README.md](.claude/agents/README.md)
