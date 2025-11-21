---
name: meeting-management
description: Manages meeting lifecycle workflows including meeting preparation (agenda creation), information extraction and task allocation to other agents (HR, Knowledge Manager), and transcript summarization with standardized templates
allowed-tools: [Read, Write, Edit, Glob, Grep]
---

# Meeting Management Skill

You are assisting with meeting management operations. This skill provides three integrated workflows for handling the complete meeting lifecycle: preparing for meetings, extracting and allocating information from transcripts, and creating concise summaries.

## Directory Structure

Meeting-related files are organized as follows:
- `.claude/meetings/transcripts/` - Meeting transcript files (input)
- `.claude/meetings/summaries/` - Meeting summary files (output)
- `.claude/skills/meeting-management/templates/` - Templates for meeting summaries
- `.claude/stakeholders/` - Stakeholder files managed by HR agent
- `.claude/knowledge/` - Knowledge entries managed by Knowledge Manager agent (future)

## File Naming Conventions

- **Transcripts**: `YYYYMMDD-HHMMSS MeetingName-transcript.md`
- **Summaries**: `YYYYMMDD-HHMMSS MeetingName-summary.md` (replace `-transcript` with `-summary`)
- **Date format**: `YYYYMMDD` (e.g., 20251121)
- **Time format**: `HHMMSS` (e.g., 143000 for 2:30 PM)

## Available Workflows

---

### 1. Meeting Preparation

Create detailed meeting agendas using insights from previous meetings and context.

**Purpose**: Prepare comprehensive agendas for upcoming meetings that include relevant topics, questions to ask, and follow-ups on previous action items.

**When to use**:
- Before a scheduled meeting when you need to create an agenda
- When following up on previous meetings with the same stakeholder or meeting series
- When preparing for recurring meetings (e.g., steering committee, team sync)

**Steps**:

1. **Identify the meeting context**
   - Determine meeting name or stakeholder name (e.g., "steerco", "John_Doe")
   - Determine meeting date if known (YYYYMMDD-HHMMSS)
   - Understand the meeting purpose and participants

2. **Search for previous meeting summaries**
   - Use Glob to find previous summaries in `.claude/meetings/summaries/`
   - Pattern: `*{MeetingName}*-summary.md` or search by stakeholder name
   - Read the most recent 2-3 summaries if available

3. **Extract relevant information from previous meetings**
   - Review action points that may still be pending
   - Note unresolved topics or open questions
   - Identify recurring themes or concerns
   - Extract questions that need follow-up

4. **Create meeting agenda**
   - List main topics to cover
   - Include follow-up questions from previous meetings
   - List action items to review
   - Add new topics based on current context
   - Structure agenda in priority order

5. **Format and output agenda**
   - Create clear sections: Topics, Questions, Action Item Follow-ups
   - Make agenda actionable and time-conscious
   - Reference previous meeting summaries with links
   - Save or present agenda to user

**Inputs**:
- Meeting name or stakeholder name
- Meeting date (optional)
- Previous meeting summaries (if available)
- Current context or meeting purpose

**Outputs**:
- Structured meeting agenda document
- References to previous meeting summaries
- Prioritized topics and questions

**Example**:
```markdown
User: "Prepare agenda for next meeting with Hugues"
Agent:
1. Search .claude/meetings/summaries/ for "*hugues*-summary.md"
2. Read previous summaries
3. Extract: pending action items, open questions, recurring themes
4. Create agenda:
   - Topics: Follow-up on system architecture, discuss Q1 roadmap
   - Questions: Status of API integration? Timeline for deployment?
   - Action Items Review: Review completion of documentation updates
```

---

### 2. Information Extraction and Task Allocation

Extract important information from meeting transcripts and allocate tasks to specialized agents.

**Purpose**: Systematically process meeting transcripts to identify stakeholder information, knowledge entries, and meeting preparation needs, then delegate each to the appropriate specialized agent.

**When to use**:
- After receiving a new meeting transcript
- When processing meeting outcomes and follow-ups
- When user provides synthetic instructions about what to extract from a transcript

**Steps**:

1. **Read the meeting transcript**
   - Locate transcript file in `.claude/meetings/transcripts/`
   - Format: `YYYYMMDD-HHMMSS MeetingName-transcript.md`
   - Read full transcript content
   - Note transcript path for linking

2. **Review user instructions for extraction**
   - User will provide synthetic instructions in the ticket about what to extract
   - Understand what information is relevant for extraction
   - Identify which agents should be triggered

3. **Extract stakeholder information**
   - Identify mentions of new stakeholders (names, roles, organizations)
   - Extract stakeholder updates (contact info, responsibilities, interactions)
   - Note relevant stakeholder context from discussion
   - Collect discussion points involving specific stakeholders

4. **Trigger HR agent for stakeholder processing**
   - Invoke HR agent with extracted stakeholder information
   - **Include transcript link**: Provide path to transcript for context
   - Format: `[transcript](.claude/meetings/transcripts/YYYYMMDD-HHMMSS MeetingName-transcript.md)`
   - HR agent will create or update stakeholder files in `.claude/stakeholders/`

5. **Extract knowledge entries**
   - Identify important decisions made during the meeting
   - Extract process descriptions or workflow explanations
   - Note domain knowledge shared
   - Capture technical details or specifications
   - Document rationale behind decisions

6. **Trigger Knowledge Manager agent for knowledge processing** (FUTURE - Placeholder)
   - When Knowledge Manager agent exists, invoke it with extracted knowledge
   - **Include transcript link**: Provide path to transcript for context
   - Knowledge Manager will create entries in `.claude/knowledge/`
   - **Current state**: Document knowledge extraction but note agent doesn't exist yet

7. **Identify meeting preparation needs**
   - Determine if follow-up meetings are mentioned
   - Extract meeting names, dates, or stakeholder names for prep
   - Note topics that need agenda preparation

8. **Trigger Meeting Assistant for meeting preparation**
   - Invoke Meeting Assistant (Workflow 1: Meeting Preparation)
   - **Include transcript link**: Provide path to transcript for context
   - Provide meeting name/date and context for agenda creation

9. **Document extraction outcomes**
   - Summarize what information was extracted
   - Confirm which agents were triggered
   - Provide transcript links for traceability

**Inputs**:
- Transcript file path: `.claude/meetings/transcripts/YYYYMMDD-HHMMSS MeetingName-transcript.md`
- User instructions about what to extract and how to process it
- Context about which agents to trigger

**Outputs**:
- Stakeholder information sent to HR agent (with transcript link)
- Knowledge entries sent to Knowledge Manager agent (with transcript link) - FUTURE
- Meeting preparation requests sent to Meeting Assistant (with transcript link)
- Summary of extraction and task allocation

**Integration Patterns**:

**HR Agent Integration**:
```markdown
Trigger: "HR Agent - Process stakeholder information from meeting"
Context:
- Stakeholder: John Smith, CTO at TechCorp
- Interaction: Discussed API integration requirements
- Transcript: [20251121-143000 TechCorp Planning-transcript.md](.claude/meetings/transcripts/20251121-143000 TechCorp Planning-transcript.md)
```

**Knowledge Manager Integration** (FUTURE):
```markdown
Trigger: "Knowledge Manager - Document decision from meeting"
Context:
- Decision: Adopt microservices architecture for Phase 2
- Rationale: Scalability and team independence
- Transcript: [20251121-143000 TechCorp Planning-transcript.md](.claude/meetings/transcripts/20251121-143000 TechCorp Planning-transcript.md)
```

**Meeting Assistant Integration**:
```markdown
Trigger: "Meeting Assistant - Prepare agenda for follow-up meeting"
Context:
- Meeting: TechCorp Planning follow-up (scheduled for 20251128)
- Topics: Review API specs, discuss deployment timeline
- Transcript: [20251121-143000 TechCorp Planning-transcript.md](.claude/meetings/transcripts/20251121-143000 TechCorp Planning-transcript.md)
```

**Example**:
```markdown
User ticket instructions: "Extract stakeholder info and create summary for TechCorp planning meeting"
Agent:
1. Read .claude/meetings/transcripts/20251121-143000 TechCorp Planning-transcript.md
2. Extract: John Smith (CTO, TechCorp), discussed API requirements
3. Trigger HR agent: Create/update stakeholder file for John Smith with transcript link
4. Extract: Decision to use REST API, rationale: simplicity and compatibility
5. Note for Knowledge Manager: (agent doesn't exist yet, document for future)
6. Extract: Follow-up meeting needed on 20251128 to review API specs
7. Trigger Meeting Assistant Workflow 1 for agenda preparation
```

---

### 3. Meeting Transcript Summarization

Create concise, synthetic summaries of meeting transcripts using a standardized template.

**Purpose**: Generate consistent, high-quality meeting summaries that capture main topics, key takeaways, discussion points, action items, and suggestions for information extraction.

**When to use**:
- After receiving a new meeting transcript
- When user requests a meeting summary
- As part of meeting information processing workflow

**Steps**:

1. **Read the meeting transcript**
   - Locate transcript file in `.claude/meetings/transcripts/`
   - Format: `YYYYMMDD-HHMMSS MeetingName-transcript.md`
   - Read full transcript content
   - Note transcript path for template

2. **Load the summary template**
   - Read template from `.claude/skills/meeting-management/templates/meeting_summary_template.md`
   - Understand required sections and formatting

3. **Extract main topics discussed**
   - Identify 3-5 main topics from the transcript
   - Describe each topic in a few words (be concise!)
   - Focus on themes, not individual statements
   - Prioritize by importance or time spent

4. **Extract key takeaways**
   - Create synthetic bullet points (not verbatim transcription)
   - Highlight decisions made
   - Note important information shared
   - Capture conclusions and agreements
   - **Be concise**: Each takeaway should be one clear sentence

5. **Extract discussion points**
   - Identify crucial contributions from participants
   - Format: "**Name**: Statement or contribution"
   - **Only include crucial information**: Not every statement needs documentation
   - Focus on insights, decisions, concerns, or important context
   - Attribute information to speakers for context

6. **Extract action points**
   - Identify clear, actionable items
   - Format with checkboxes: `- [ ] Action description`
   - Include owner if identified: `- [ ] Action description (Owner: Name)`
   - Make action items specific and measurable
   - Prioritize by importance or urgency

7. **Create suggestions for information extraction**
   - **Stakeholder Information (HR Agent)**: List stakeholders mentioned or updates needed
   - **Knowledge Entries (Knowledge Manager Agent)**: List decisions, processes, or knowledge to document
   - **Meeting Preparation (Meeting Assistant)**: List follow-up meetings that need agendas

8. **Populate the template**
   - Fill in YAML frontmatter:
     - Meeting: Extract meeting name from filename
     - Date: Extract date/time from filename (YYYYMMDD-HHMMSS)
     - Transcript: Path to source transcript
     - Created: Current date
   - Fill in all content sections with extracted information
   - **Keep it concise and synthetic**: Quality over quantity

9. **Determine output filename**
   - Take original transcript filename
   - Replace `-transcript` with `-summary`
   - Example: `20251121-143000 TechCorp Planning-transcript.md` → `20251121-143000 TechCorp Planning-summary.md`

10. **Save summary file**
    - Save to `.claude/meetings/summaries/`
    - Use determined filename
    - Verify file created successfully

11. **Confirm completion**
    - Report summary location to user
    - Highlight key findings if appropriate
    - Suggest next steps based on action items or extraction suggestions

**Inputs**:
- Transcript file path: `.claude/meetings/transcripts/YYYYMMDD-HHMMSS MeetingName-transcript.md`

**Outputs**:
- Summary file: `.claude/meetings/summaries/YYYYMMDD-HHMMSS MeetingName-summary.md`
- Follows standardized template format
- Concise and synthetic content

**Quality Guidelines**:
- **Concise**: Capture essence, not every detail
- **Synthetic**: Summarize and synthesize, don't transcribe
- **Focused**: Include only crucial information
- **Structured**: Follow template sections consistently
- **Actionable**: Make action items clear and specific
- **Traceable**: Include transcript link for verification

**Example**:
```markdown
User: "Summarize the TechCorp planning meeting transcript"
Agent:
1. Read .claude/meetings/transcripts/20251121-143000 TechCorp Planning-transcript.md
2. Load templates/meeting_summary_template.md
3. Extract main topics: "API Architecture", "Deployment Timeline", "Team Resources"
4. Extract takeaways: "Decided on REST API approach for simplicity", "Deployment scheduled for Q1 2026"
5. Extract discussion: "**John (CTO)**: Prefers REST over GraphQL for team familiarity"
6. Extract actions: "- [ ] Jane to create API specification (Owner: Jane)", "- [ ] Team to review architecture doc by Friday"
7. Create extraction suggestions:
   - Stakeholder: John Smith (CTO, TechCorp)
   - Knowledge: Decision to use REST API with rationale
   - Meeting prep: Follow-up meeting on 20251128
8. Populate template with all extracted information
9. Save to .claude/meetings/summaries/20251121-143000 TechCorp Planning-summary.md
10. Confirm: "Summary created at .claude/meetings/summaries/20251121-143000 TechCorp Planning-summary.md"
```

---

## Important Notes

### General Guidelines
- **Always include transcript links** when triggering other agents for traceability
- **Be concise and synthetic** in all meeting summaries - quality over quantity
- **Use standardized templates** to ensure consistency across all meetings
- **Follow file naming conventions** strictly for easy discovery and organization

### Agent Integration
- **HR Agent**: Available now for stakeholder information extraction
- **Knowledge Manager Agent**: Placeholder for future - document patterns but note agent doesn't exist
- **Meeting Assistant**: Self-reference for meeting preparation workflow

### Template Usage
- Template location: `.claude/skills/meeting-management/templates/meeting_summary_template.md`
- All summaries must follow template structure
- Customize content but preserve section structure
- Instructions at bottom of template provide guidance

### File Organization
- **Transcripts**: Input files in `.claude/meetings/transcripts/`
- **Summaries**: Output files in `.claude/meetings/summaries/`
- **Maintain naming correlation**: Replace `-transcript` with `-summary` for easy matching

### Workflow Sequencing
Typical meeting lifecycle:
1. **Before meeting**: Use Workflow 1 (Meeting Preparation) to create agenda
2. **After meeting**: Receive transcript in `.claude/meetings/transcripts/`
3. **Process transcript**: Use Workflow 3 (Summarization) to create summary
4. **Extract information**: Use Workflow 2 (Information Extraction) to allocate tasks to agents
5. **Follow-up**: Use Workflow 1 again to prepare for next meeting

### Quality Standards
- **Summaries must be concise**: Capture essence, not everything
- **Action items must be clear**: Specific and actionable
- **Attribution matters**: Note who said what for crucial information
- **Context preservation**: Always link back to source transcript

## References

- Meeting Assistant Agent: `.claude/agents/meeting-assistant.md`
- HR Agent: `.claude/agents/hr.md`
- Stakeholder Management Skill: `.claude/skills/stakeholder-management/skill.md`
- Knowledge Manager Agent: (Future - not yet implemented)
