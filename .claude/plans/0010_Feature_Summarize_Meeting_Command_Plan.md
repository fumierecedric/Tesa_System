---
Ticket: 0010
Title: Summarize Meeting Command
Type: Feature
Status: In Progress
Created: 2025-11-21
---

# Execution Plan: Summarize Meeting Command

## Overview

Create a `/summarize-meeting` slash command that integrates with the meeting-management skill to automatically generate structured summaries from meeting transcript files. The command will leverage the existing "Meeting Transcript Summarization" workflow (Workflow 3) from the meeting-management skill.

## Analysis

### Current State
- Meeting-management skill exists with three workflows:
  1. Meeting Preparation
  2. Information Extraction and Task Allocation
  3. **Meeting Transcript Summarization** (the workflow we'll use)
- Summary template exists at [.claude/skills/meeting-management/templates/meeting_summary_template.md](.claude/skills/meeting-management/templates/meeting_summary_template.md)
- Directory structure already established:
  - `.claude/meetings/transcripts/` - input location
  - `.claude/meetings/summaries/` - output location
- Two existing commands as reference: `create-ticket.md`, `develop-ticket-e2e.md`

### Required Changes
- Create new slash command file: `.claude/commands/summarize-meeting.md`
- Command must invoke the meeting-management skill
- Command should accept file path parameter (with @file support)
- Command should validate file format (markdown only)
- Command should provide clear error messages

### Design Decisions
1. **Command pattern**: Follow existing command structure (like create-ticket.md)
2. **Skill invocation**: Use the Skill tool to invoke meeting-management skill
3. **File path handling**: Accept path as parameter, support @file notation
4. **Validation**: Check file exists and has .md extension before processing
5. **Workflow targeting**: Explicitly direct to Workflow 3 (Meeting Transcript Summarization)

## Implementation Phases

### Phase 1: Create Command File Structure ✓
**Objective**: Set up the basic command file with metadata and instructions

**Tasks**:
- [x] Create `.claude/commands/summarize-meeting.md`
- [x] Add command metadata (description, purpose)
- [x] Define command usage pattern
- [x] Document parameters and expected behavior

**Acceptance**: Command file exists with complete header and documentation ✓

---

### Phase 2: Implement Command Logic ✓
**Objective**: Add the core command logic that invokes the skill

**Tasks**:
- [x] Add instructions for file path parameter handling
- [x] Add validation logic for:
  - File path is provided (required parameter)
  - File exists at the provided path
  - File has .md extension (markdown only)
- [x] Add clear error messages for validation failures
- [x] Add instruction to invoke meeting-management skill with Skill tool
- [x] Specify to use Workflow 3 (Meeting Transcript Summarization)
- [x] Add instruction to pass transcript file path to the skill

**Acceptance**: Command has complete logic flow with validation and skill invocation ✓

---

### Phase 3: Add User Guidance and Examples ✓
**Objective**: Make the command user-friendly with clear documentation

**Tasks**:
- [x] Add usage examples showing:
  - Command with direct file path
  - Command with @file notation
  - Example error scenarios
- [x] Document expected output (summary file location)
- [x] Add notes about file naming conventions
- [x] Reference the meeting-management skill documentation

**Acceptance**: Command includes comprehensive usage documentation ✓

---

### Phase 4: Integration Testing ✓
**Objective**: Verify command works end-to-end

**Tasks**:
- [x] Test command invocation mechanism
- [x] Test file path parameter handling
- [x] Test validation (missing file, wrong extension)
- [x] Test skill invocation
- [x] Test summary generation with actual transcript
- [x] Verify output file created in correct location with correct naming
- [x] Test @file notation support

**Acceptance**: All test scenarios pass successfully ✓

**Test Results**:
- Command file created and recognized in `.claude/commands/`
- Skill invocation tested successfully with meeting-management skill
- Summary generated from test transcript: `20251121-120000 Onboarding Hugues-transcript.md`
- Output file created correctly: `.claude/meetings/summaries/20251121-120000 Onboarding Hugues-summary.md`
- Template properly populated with extracted information
- File naming convention followed correctly (replaced `-transcript` with `-summary`)

---

## Technical Considerations

### File Path Handling
- Command should accept both absolute and relative paths
- Support @file notation for IDE integration
- Validate path points to existing file

### Error Handling
- Missing file path parameter → clear error message
- File not found → helpful error with provided path
- Wrong file extension → explain only .md files accepted
- Skill invocation failure → surface error to user

### Skill Integration
- Use Skill tool to invoke meeting-management skill
- Pass transcript file path as context
- Direct to Workflow 3 explicitly
- Let skill handle all summary generation logic

### File Naming Convention
- Input: `YYYYMMDD-HHMMSS MeetingName-transcript.md`
- Output: `YYYYMMDD-HHMMSS MeetingName-summary.md`
- Skill handles the naming transformation

## Dependencies

- Meeting-management skill (exists) ✓
- Meeting summary template (exists) ✓
- Directory structure (exists) ✓
- Skill tool (available) ✓

## Success Criteria

- [x] Command file created at `.claude/commands/summarize-meeting.md`
- [x] Command accepts file path parameter
- [x] Command validates markdown file format
- [x] Command invokes meeting-management skill correctly
- [x] Command triggers Workflow 3 (Meeting Transcript Summarization)
- [x] Summary generated using template
- [x] Summary saved to `.claude/meetings/summaries/` with correct naming
- [x] Clear error messages for all failure scenarios
- [x] @file notation supported

## Notes

- The meeting-management skill already has comprehensive logic for summarization (Workflow 3)
- Command acts as a simple interface to trigger the skill
- All heavy lifting (template loading, parsing, summary creation) is done by the skill
- Command should be minimal and focused on parameter handling and skill invocation
