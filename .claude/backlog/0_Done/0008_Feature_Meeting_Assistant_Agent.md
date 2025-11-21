# Ticket 0008: Meeting Assistant Agent

**Epic**: Project Management
**Type**: Feature
**Priority**: High
**Status**: 0_Done
**Sprint**: N/A
**Created**: 2025-11-21
**Updated**: 2025-11-21

---

## User Story

As a project manager, I want a meeting assistant agent that can extract important information from meeting transcripts and prepare for next meetings, so that I can efficiently process meeting outcomes and maintain continuity across meetings.

---

## Description

Create a meeting assistant agent to help extract important information from meeting transcripts and prepare for upcoming meetings (detailed agendas, questions to ask, action items, etc.).

### Key Requirements:

1. **Input Format**: Raw meeting transcripts provided as markdown files in `/.claude/meetings/transcripts/` with filename format `YYYYMMDD-HHMMSS MeetingName-transcript.md`

2. **Integration with Solution Designer**: When a new ticket is created in `/.claude/backlog/2_To_Do` with type "meeting", the Solution Designer should allocate tasks mainly to this meeting assistant agent

3. **Ticket Processing**: In the ticket, the user will provide synthetic instructions on what to extract from the transcript and what to do with it

4. **Agent Orchestration**: The meeting assistant extracts information in separate pieces and triggers other agents to perform specific tasks:
   - **Stakeholder extraction** → Trigger HR agent to fill in stakeholder info (with link to transcript)
   - **Knowledge extraction** → Trigger Knowledge Manager to create knowledge entry (with link to transcript) - *Note: Knowledge Manager agent doesn't exist yet, prepare placeholder for future integration*
   - **Meeting preparation** → Trigger Meeting Assistant (itself) to prepare agenda for next meeting with date YYYYMMDD-HHMMSS or meeting name (e.g., "steerco" or stakeholder name) with link to transcript

---

## Acceptance Criteria

- [x] Meeting assistant agent is created with proper role definition
- [x] Agent can read and process transcript files from `/.claude/meetings/transcripts/` directory
- [x] Agent can extract information from transcripts based on synthetic user instructions
- [x] Agent can trigger HR agent for stakeholder information extraction
- [x] Agent has placeholder integration for future Knowledge Manager agent
- [x] Agent can prepare meeting agendas based on extracted information
- [x] Solution Designer recognizes "meeting" type tickets and assigns tasks to meeting assistant agent
- [x] Agent includes transcript links when triggering other agents or creating outputs

---

## Technical Notes

- Transcript filename format: `YYYYMMDD-HHMMSS MeetingName-transcript.md`
- Meeting type tickets location: `/.claude/backlog/2_To_Do/`
- Knowledge Manager integration is planned but not yet implemented - prepare for future integration

---

## Dependencies

- HR Agent (existing)
- Solution Designer (existing)
- Knowledge Manager Agent (future dependency - placeholder needed)

---

## Links

- Original note: `.claude/backlog/2_To_Do/meeting_assistant.md`
