---
Epic: Project Management
Id: 0010
Title: Summarize Meeting Command
Type: Feature
Status: 0_Done
Created: 2025-11-21
Updated: 2025-11-21
Priority: Medium
Sprint:
---

## Summary

Create a `/summarize-meeting` slash command that leverages the meeting-management skill to generate structured summaries from meeting transcript files. The command will process markdown transcript files and produce formatted summaries using the existing meeting summary template.

## User Story

As a Project Manager, I want to quickly summarize meeting transcripts using a simple slash command, so that I can efficiently document meetings and extract actionable insights without manually processing the transcript.

## Acceptance Criteria

- [x] Command `/summarize-meeting` is created and functional
- [x] Command requires a file path parameter (supports @file notation)
- [x] Command only accepts markdown (.md) transcript files
- [x] Command triggers the meeting-management skill's "Summarize" workflow
- [x] Output is generated in markdown format using the meeting summary template from [.claude/skills/meeting-management/templates/meeting_summary_template.md](.claude/skills/meeting-management/templates/meeting_summary_template.md)
- [x] Summary is saved to `.claude/meetings/summaries/` with proper naming convention (YYYYMMDD-HHMMSS MeetingName-summary.md)
- [x] Command provides clear error messages if file path is missing or file format is invalid
- [x] Integration with the meeting-management skill's existing workflow is seamless

## Initial Request

- create a command `summarize_meeting` that uses the meeting-management skill (trigger the meeting assistant to use the skill !) to summarize meetings based on transcripts
- variable is the meeting transcript file path (with @file if needed)
