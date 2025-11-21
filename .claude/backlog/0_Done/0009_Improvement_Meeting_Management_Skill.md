---
Epic: Project Management
Id: 0009
Title: Meeting Management Skill
Type: Improvement
Status: 0_Done
Created: 2025-11-21
Updated: 2025-11-21
Priority: High
Sprint: N/A
---

## Summary

Refactor the meeting assistant agent's capabilities into a well-structured `meeting-management` skill following Claude Code best practices with three distinct workflows: information extraction and task allocation, meeting preparation, and transcript summarization.

## User Story

As a project manager, I want the meeting assistant's capabilities organized as a structured skill with three distinct workflows (information extraction, meeting preparation, and transcript summarization), so that meeting-related processes are standardized, efficient, and properly integrated with other agents.

## Acceptance Criteria

### Skill Structure
- [ ] Create `.claude/skills/meeting-management/` directory
- [ ] Create `SKILL.md` with proper YAML frontmatter (name: `meeting-management`, description, allowed-tools)
- [ ] Create `templates/` subdirectory
- [ ] Create `templates/meeting_summary_template.md` with required sections

### Workflow 1: Information Extraction and Task Allocation
- [ ] Document workflow for extracting information from meeting transcripts
- [ ] Define process for identifying stakeholder information → trigger HR agent (with transcript link)
- [ ] Define process for identifying knowledge entries → trigger Knowledge Manager agent (with transcript link) - *placeholder for future*
- [ ] Define process for identifying meeting preparation needs → trigger Meeting Assistant (with transcript link)
- [ ] Specify input format: `/.claude/meetings/transcripts/YYYYMMDD-HHMMSS MeetingName-transcript.md`

### Workflow 2: Meeting Preparation
- [ ] Document workflow for creating detailed meeting agendas
- [ ] Include process for using insights from previous meeting summaries
- [ ] Define agenda components: questions to ask, action item follow-ups, topics to cover
- [ ] Specify how to reference date (YYYYMMDD-HHMMSS) or meeting name (e.g., "steerco", stakeholder name)

### Workflow 3: Meeting Transcript Summarization
- [ ] Document workflow for creating concise, synthetic meeting summaries
- [ ] Template must include sections:
  - **Main Topics Discussed**: A few words each
  - **Key Takeaways**: Synthetic bullet points
  - **Discussion Points**: Who said what (crucial info only)
  - **Action Points**: Clear, actionable items
  - **Suggestions for Information Extraction**: What info to extract and which agent to allocate to
- [ ] Output location: `.claude/meetings/summaries/`
- [ ] Naming convention: Keep original transcript name, replace `-transcript` with `-summary`
- [ ] Ensure summaries are concise and synthetic (not verbose)

### Integration Requirements
- [ ] Meeting assistant agent updated to reference the new skill
- [ ] Solution Designer recognizes meeting-related tickets and invokes this skill
- [ ] Workflow documentation includes examples of agent orchestration

---

## Technical Notes

### Directory Structure
```
.claude/skills/meeting-management/
├── SKILL.md (main documentation with YAML frontmatter + 3 workflows)
├── templates/
│   └── meeting_summary_template.md
├── examples.md (optional)
└── reference.md (optional)
```

### YAML Frontmatter Requirements
```yaml
name: meeting-management
description: Manages meeting lifecycle workflows including transcript summarization, information extraction and task allocation to other agents, and meeting preparation
allowed-tools: [Read, Write, Edit, Glob, Grep]
```

### File Naming Conventions
- Input: `YYYYMMDD-HHMMSS MeetingName-transcript.md`
- Output: `YYYYMMDD-HHMMSS MeetingName-summary.md`

### Agent Integration Points
- **HR Agent**: Stakeholder information extraction
- **Knowledge Manager Agent**: Knowledge entry creation (future)
- **Meeting Assistant Agent**: Meeting preparation and agenda creation

---

## Dependencies

- Meeting Assistant Agent (ticket 0008) - existing
- HR Agent (ticket 0006) - existing
- Knowledge Manager Agent - future dependency (placeholder needed)

---

## References

- Original note: [.claude/backlog/2_To_Do/skills_meeting_assistant.md](.claude/backlog/2_To_Do/skills_meeting_assistant.md)
- Related ticket: [0008_Feature_Meeting_Assistant_Agent.md](.claude/backlog/0_Done/0008_Feature_Meeting_Assistant_Agent.md)
- Claude Code Skills Documentation: Follow pattern from existing skills (stakeholder-management, solution-design, backlog-management)

---

## Definition of Done

- [ ] Skill structure created with all required files
- [ ] Three workflows fully documented with clear steps and examples
- [ ] Meeting summary template created with all required sections
- [ ] Meeting assistant agent updated to use the new skill
- [ ] Existing meeting assistant functionality preserved and enhanced
- [ ] Documentation includes integration examples with HR and Knowledge Manager agents
- [ ] Solution Designer can successfully invoke meeting-management skill for meeting-type tickets

## Initial Request

From [.claude/backlog/2_To_Do/skills_meeting_assistant.md](.claude/backlog/2_To_Do/skills_meeting_assistant.md):

```
- the process of extracting information from meeting transcripts allocating tasks to other agents (HR for stakeholder, knowledge manager for knowledge entry, self for meeting prep) should be transferred to a skill: .claude/skills/meeting-management
- you can split different capabilities:
  - information extraction from transcript and allocation of tasks to other agents
  - meeting preparation (agenda creation)
  - summary of meeting transcript
- Summary of meeting transcript is new and meeting assistant should also be made aware of it
- summary should have following requirements
    - use a template in the skills/meeting-management/meeting_summary_template.md
        - format should be sequential with headings "main topics discussed" (a few words), "key take-away" (synthetic bullet points), "discussion points" (who said what crucial info), "action points", suggestion for the information extraction (cf. capability above: what info should be extracted and allocated to which agent)
        - be concise and synthetic
        - generate output in .claude/meetings/summaries/ and keep the initial naming of the meeting and replace -transcript with -summary
    - meeting assistant should be able to use the summary capability when asked to summarize a meeting transcript
```

---

## Technical Notes

### Current State
The meeting assistant agent (from ticket 0008) has basic transcript processing capabilities but lacks:
- Structured skill organization
- Standardized summarization workflow with templates
- Clear separation of the three core capabilities
- Integration points for task allocation to other agents

### Target State
Create `.claude/skills/meeting-management/` with:
1. `SKILL.md` documenting three workflows
2. `templates/meeting_summary_template.md` for consistent summaries
3. Optional `examples.md` and `reference.md` for guidance
