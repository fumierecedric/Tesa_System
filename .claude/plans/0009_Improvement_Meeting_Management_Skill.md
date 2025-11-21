---
Ticket: 0009
Title: Meeting Management Skill
Created: 2025-11-21
Updated: 2025-11-21
Status: Completed
---

## Overview

Refactor the Meeting Assistant agent's capabilities into a well-structured `meeting-management` skill following Claude Code best practices. This skill will organize three related workflows (information extraction/task allocation, meeting preparation, and transcript summarization) that handle the complete meeting lifecycle, with standardized templates and clear integration points for other agents.

## Analysis

### Problem Understanding

The Meeting Assistant agent (ticket 0008) currently has basic transcript processing capabilities embedded in the agent definition, but lacks:
- Structured skill organization following Claude Code conventions
- Standardized summarization workflow with reusable templates
- Clear separation of three distinct but related capabilities
- Formal integration patterns for task allocation to other agents (HR, Knowledge Manager)

Users need a systematic, repeatable approach to meeting workflow that can be easily invoked, extended, and maintained over time.

### Current State

- Meeting Assistant agent exists at `.claude/agents/meeting-assistant.md`
- Transcript processing capabilities are embedded in agent definition
- No formal skill structure for meeting workflows
- No standardized template for meeting summaries
- Meeting transcripts stored in `.claude/meetings/transcripts/` with format `YYYYMMDD-HHMMSS MeetingName-transcript.md`
- HR agent available for stakeholder extraction
- Knowledge Manager agent doesn't exist yet (planned future)
- Existing skills follow pattern: `skill.md` + `templates/` directory

### Gaps to Address

1. No `.claude/skills/meeting-management/` skill structure
2. No formal documentation of three meeting workflows
3. No standardized template for meeting summaries with required sections
4. No clear integration patterns for triggering other agents
5. Meeting Assistant agent doesn't reference a formal skill
6. Solution Designer doesn't know to invoke meeting-management skill

## Solution Approach

### Design Philosophy

- **Progressive capability organization**: Structure related workflows within one skill while keeping each workflow distinct
- **Template-driven consistency**: Use standardized templates to ensure meeting summaries follow consistent format
- **Agent orchestration patterns**: Document clear patterns for triggering HR and Knowledge Manager agents with context
- **Claude Code conventions**: Follow official guidelines for skill structure (YAML frontmatter, workflow documentation)
- **Extensibility**: Design for future addition of more meeting-related workflows

### Technical Approach

1. Create `.claude/skills/meeting-management/` directory structure
2. Create `skill.md` with YAML frontmatter and three documented workflows
3. Create `templates/meeting_summary_template.md` with all required sections
4. Document each workflow with clear steps, inputs, outputs, and agent integration
5. Update Meeting Assistant agent to reference the skill
6. Optionally create `examples.md` for usage guidance

### Key Design Decisions

- **Single skill, three workflows**: All meeting capabilities in one skill since they're tightly integrated in meeting lifecycle
- **Template location**: `templates/meeting_summary_template.md` within skill directory (following existing pattern)
- **Workflow organization**: Document workflows sequentially in `skill.md` (preparation → extraction → summarization)
- **YAML frontmatter**: Include `name`, `description`, and `allowed-tools` following Claude Code spec
- **Output directory**: Meeting summaries go to `.claude/meetings/summaries/` (parallel to transcripts)
- **Naming convention**: Replace `-transcript` with `-summary` to maintain correlation

## Architecture

### Component Structure

```
.claude/skills/meeting-management/
├── skill.md                          # Main skill documentation with YAML + 3 workflows
├── templates/
│   └── meeting_summary_template.md  # Standardized summary format
├── examples.md                       # (Optional) Usage examples
└── reference.md                      # (Optional) Quick reference guide
```

### Workflow Integration

```
User invokes meeting workflow
        ↓
Meeting Assistant references meeting-management skill
        ↓
    Workflow 1: Meeting Preparation
        - Read previous meeting summaries
        - Generate agenda with topics, questions, action item follow-ups
        - Output: Agenda document
        ↓
    Workflow 2: Information Extraction & Task Allocation
        - Read transcript from .claude/meetings/transcripts/
        - Identify stakeholder info → Trigger HR agent (with transcript link)
        - Identify knowledge entries → Trigger Knowledge Manager (with transcript link)
        - Identify meeting prep needs → Trigger Meeting Assistant (with transcript link)
        - Output: Task allocation to specialized agents
        ↓
    Workflow 3: Meeting Transcript Summarization
        - Read transcript
        - Apply meeting_summary_template.md
        - Extract: main topics, key takeaways, discussion points, action points
        - Add suggestions for information extraction
        - Save to .claude/meetings/summaries/
        - Output: Concise, synthetic summary
```

### Data Flow

1. **Input**: Meeting transcript at `.claude/meetings/transcripts/YYYYMMDD-HHMMSS MeetingName-transcript.md`
2. **Processing**:
   - Workflow reads transcript
   - Extracts structured information per template
   - Formats according to template sections
   - Identifies extraction opportunities and assigns to agents
3. **Output**:
   - Summary at `.claude/meetings/summaries/YYYYMMDD-HHMMSS MeetingName-summary.md`
   - Tasks allocated to HR agent, Knowledge Manager, Meeting Assistant
4. **Storage**: Summaries persist in `.claude/meetings/summaries/` for future reference

## Tasks

### Phase 1: Create Skill Structure
- [x] Create `.claude/skills/meeting-management/` directory
- [x] Create `.claude/skills/meeting-management/templates/` subdirectory
- [x] Verify directories created successfully

### Phase 2: Create Meeting Summary Template
- [x] Create `templates/meeting_summary_template.md` with YAML frontmatter
- [x] Add "Main Topics Discussed" section with placeholder guidance
- [x] Add "Key Takeaways" section with bullet point format
- [x] Add "Discussion Points" section for "who said what" crucial info
- [x] Add "Action Points" section for clear actionable items
- [x] Add "Suggestions for Information Extraction" section with agent allocation guidance
- [x] Add instructions to be concise and synthetic
- [x] Verify template completeness

### Phase 3: Create skill.md with YAML Frontmatter
- [x] Create `skill.md` in `.claude/skills/meeting-management/`
- [x] Add YAML frontmatter with `name: meeting-management`
- [x] Add `description` covering all three workflows
- [x] Add `allowed-tools: [Read, Write, Edit, Glob, Grep]`
- [x] Add introductory section explaining skill purpose

### Phase 4: Document Workflow 1 - Meeting Preparation
- [x] Add "Workflow 1: Meeting Preparation" section header
- [x] Document purpose: Create detailed agendas using insights from previous meetings
- [x] List workflow steps:
  - Search for previous meeting summaries
  - Extract action items and unresolved topics
  - Identify key questions to ask
  - Format agenda with topics, questions, follow-ups
- [x] Document inputs: Previous summaries, meeting name/date
- [x] Document outputs: Agenda document
- [x] Add example showing agenda creation

### Phase 5: Document Workflow 2 - Information Extraction & Task Allocation
- [x] Add "Workflow 2: Information Extraction and Task Allocation" section header
- [x] Document purpose: Extract information and allocate tasks to specialized agents
- [x] List workflow steps:
  - Read transcript from `.claude/meetings/transcripts/YYYYMMDD-HHMMSS MeetingName-transcript.md`
  - Identify stakeholder information (names, roles, contact, interactions)
  - Trigger HR agent with extracted stakeholder data and transcript link
  - Identify knowledge entries (decisions, processes, domain knowledge)
  - Trigger Knowledge Manager agent with knowledge data and transcript link (placeholder for future)
  - Identify meeting preparation needs for follow-up meetings
  - Trigger Meeting Assistant for agenda creation with date/name and transcript link
- [x] Document inputs: Transcript file path, extraction instructions from user
- [x] Document outputs: Task allocations to HR, Knowledge Manager, Meeting Assistant
- [x] Add integration examples with transcript links
- [x] Add placeholder notes for Knowledge Manager integration

### Phase 6: Document Workflow 3 - Meeting Transcript Summarization
- [x] Add "Workflow 3: Meeting Transcript Summarization" section header
- [x] Document purpose: Create concise, synthetic summaries using standardized template
- [x] List workflow steps:
  - Read transcript from `.claude/meetings/transcripts/`
  - Load template from `templates/meeting_summary_template.md`
  - Extract main topics discussed (few words each)
  - Extract key takeaways (synthetic bullet points)
  - Extract discussion points (who said what crucial info)
  - Extract action points (clear, actionable items)
  - Add suggestions for information extraction (what to extract, which agent)
  - Save to `.claude/meetings/summaries/YYYYMMDD-HHMMSS MeetingName-summary.md`
- [x] Document inputs: Transcript file path
- [x] Document outputs: Summary file in `.claude/meetings/summaries/`
- [x] Document naming convention: Replace `-transcript` with `-summary`
- [x] Add example showing template application
- [x] Emphasize being concise and synthetic (not verbose)

### Phase 7: Add Supporting Documentation
- [x] Add "Important Notes" section with:
  - File naming conventions
  - Template usage guidance
  - Agent integration patterns
  - Conciseness requirements
- [x] Add "Directory References" section listing all file locations
- [x] Add references to HR agent and Knowledge Manager (future)

### Phase 8: Update Meeting Assistant Agent
- [x] Read current meeting assistant agent at `.claude/agents/meeting-assistant.md`
- [x] Add reference to `meeting-management` skill in agent description
- [x] Update agent to invoke skill workflows when processing meeting tickets
- [x] Add example of invoking each workflow
- [x] Verify agent updates preserve existing functionality

### Phase 9: Validation and Testing
- [x] Verify skill.md has all required sections
- [x] Verify template has all required fields
- [x] Check YAML frontmatter syntax is valid
- [x] Verify file naming conventions are documented
- [x] Verify agent integration patterns are clear
- [x] Review against acceptance criteria from ticket 0009
- [x] Confirm all workflow steps are actionable
- [x] Verify template guidance is clear and complete

## Dependencies

### External Dependencies
- Existing Meeting Assistant agent (`.claude/agents/meeting-assistant.md`)
- HR agent for stakeholder extraction (`.claude/agents/hr.md`)
- Knowledge Manager agent - future dependency (placeholder integration)
- Meeting transcripts directory (`.claude/meetings/transcripts/`)

### Task Dependencies
- Phase 1 must complete before all other phases (directory structure needed)
- Phase 2 (template) must complete before Phase 6 (summarization workflow can reference it)
- Phase 3 (skill.md creation) must complete before Phases 4-7 (workflow documentation)
- Phases 4-7 can be done sequentially (workflow documentation)
- Phase 8 (agent update) requires Phases 3-7 complete (skill must be documented first)
- Phase 9 (validation) must be last (validates all previous work)

### Sequential Phases
1. Phase 1: Structure
2. Phase 2-3: Templates and skill foundation
3. Phases 4-7: Workflow documentation
4. Phase 8: Agent integration
5. Phase 9: Validation

## Testing Strategy

### Unit Testing
- Verify skill.md YAML frontmatter parses correctly
- Verify template has all required sections
- Check markdown formatting in all files
- Verify file paths and references are accurate

### Integration Testing
- Test Meeting Assistant can reference the skill
- Verify template can be loaded and used
- Test each workflow independently:
  - Workflow 1: Create a sample meeting agenda
  - Workflow 2: Process a transcript and allocate tasks to HR agent
  - Workflow 3: Generate a summary from a sample transcript using template
- Verify summaries follow template format
- Verify transcript links work correctly

### Validation Criteria
- [ ] skill.md exists with valid YAML frontmatter
- [ ] Template exists with all 5 required sections
- [ ] All three workflows documented with clear steps
- [ ] Meeting Assistant agent references the skill
- [ ] Integration examples included for HR and Knowledge Manager
- [ ] File naming conventions documented
- [ ] Output directories specified correctly

## Rollout Considerations

### Implementation Order
1. Start with directory structure and template (foundational)
2. Create skill.md with YAML and introduction
3. Document workflows sequentially (preparation → extraction → summarization)
4. Update Meeting Assistant agent integration
5. Validate against acceptance criteria

### Success Metrics
- Meeting summaries follow consistent format across all meetings
- Users can invoke workflows by referencing skill name
- Meeting Assistant successfully delegates to HR agent with context
- Summaries are concise and capture key information
- Future Knowledge Manager integration is clearly documented

### Future Enhancements (Out of Scope)
- Additional meeting workflows (attendance tracking, decision logging)
- Automated meeting scheduling and reminder generation
- Integration with calendar systems
- Meeting analytics and insights dashboard
- Voice-to-text transcript generation
- Real-time meeting assistance during live meetings

## Notes

### Design Considerations

**Why one skill vs. three separate skills?**
The three capabilities are tightly coupled in the meeting lifecycle. Information extraction informs summarization, summaries inform preparation for next meetings, and preparation may reference extraction patterns. Keeping them together reduces context switching and improves discoverability.

**Template design rationale:**
The template sections reflect the natural flow of meeting documentation: what was discussed (topics), what matters (takeaways), who contributed (discussion points), what needs to happen (actions), and what to extract for other systems (suggestions). This structure balances completeness with conciseness.

**Agent orchestration pattern:**
Always include transcript links when triggering other agents. This preserves context and allows agents to verify extracted information against source material, improving accuracy and traceability.

**Knowledge Manager placeholder:**
Document the integration pattern now even though Knowledge Manager doesn't exist. This prevents rework later and clarifies the intended architecture for future development.

### References

- Ticket: [0009_Improvement_Meeting_Management_Skill.md](.claude/backlog/1_WIP/0009_Improvement_Meeting_Management_Skill.md)
- Related ticket: [0008_Feature_Meeting_Assistant_Agent.md](.claude/backlog/0_Done/0008_Feature_Meeting_Assistant_Agent.md)
- Existing skills:
  - [stakeholder-management](.claude/skills/stakeholder-management/skill.md)
  - [solution-design](.claude/skills/solution-design/skill.md)
  - [backlog-management](.claude/skills/backlog-management/skill.md)
- Claude Code Skills Documentation: Progressive disclosure, YAML frontmatter requirements, workflow organization
