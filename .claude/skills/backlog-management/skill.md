# Backlog Management Skill

You are assisting with backlog management operations. This skill provides workflows for managing product tickets in the `.claude/backlog/` directory.

## Folder Structure

The backlog uses the following folder structure:
- `0_Done/` - Completed tickets
- `1_WIP/` - Work in progress tickets
- `2_To_Do/` - Tickets ready to be worked on
- `3_To_Plan/` - Tickets that need planning
- `4_Wait/` - Tickets on hold
- `5_Archive/` - Archived tickets

## Available Workflows

### 1. Initialize Backlog

Create the backlog folder structure if it doesn't exist yet.

**Steps:**
1. Check if `.claude/backlog/` exists
2. Create the following folders if they don't exist:
   - `0_Done/`
   - `1_WIP/`
   - `2_To_Do/`
   - `3_To_Plan/`
   - `4_Wait/`
   - `5_Archive/`

### 2. Prepare Ticket

Convert a raw note or request into a structured ticket.

**Steps:**
1. **Ask clarifying questions** to fully understand the requirements before creating the ticket
2. Scan all existing tickets in `.claude/backlog/` to determine the next ticket ID
3. Assign a 4-digit zero-padded ticket ID (e.g., 0001, 0002, 0010, 0100)
4. Gather required information from the user:
   - **Epic**: Ask user which epic this belongs to
   - **Title**: Clear, concise ticket name
   - **Summary**: Brief description
   - **Type**: Ask user to confirm (Feature, Bug, Improvement)
   - **Priority**: Ask user to confirm (Low, Medium, High, Critical) - default: Medium
   - **Sprint**: Ask if this should be assigned to a sprint
   - **User Story**: Detailed description in user story format
   - **Acceptance Criteria**: List what "done" looks like
   - **Initial Request**: Capture the original request verbatim
5. Load the template from `.claude/skills/backlog-management/templates/ticket-template.md`
6. Replace all placeholders:
   - `{{TICKET_ID}}`: The assigned ticket ID
   - `{{EPIC}}`: Epic name
   - `{{TITLE}}`: Ticket title
   - `{{TYPE}}`: Feature/Bug/Improvement
   - `{{STATUS}}`: Initial status (usually "1_WIP")
   - `{{CREATED_DATE}}`: Current date in ISO format (YYYY-MM-DD)
   - `{{UPDATED_DATE}}`: Current date in ISO format (YYYY-MM-DD)
   - `{{PRIORITY}}`: Low/Medium/High/Critical
   - `{{SPRINT}}`: Sprint name or empty
   - `{{SUMMARY}}`: Brief summary
   - `{{USER_STORY}}`: User story description
   - `{{ACCEPTANCE_CRITERIA}}`: Bullet list of acceptance criteria
   - `{{INITIAL_REQUEST}}`: Original request text
7. Create the ticket file in `.claude/backlog/1_WIP/` with filename: `{TICKET_ID}_{TYPE}_{Title_Snake_Case}.md`

### 3. Update Ticket

Update fields in an existing ticket.

**Steps:**
1. **Ask clarifying questions** to understand what needs to be updated and why
2. Locate the ticket file
3. Read the current ticket content
4. Ask user what fields to update
5. Update the frontmatter and/or content sections as needed
6. Update the `Updated` date to current date
7. If status changed, consider if the file needs to be moved to a different folder

### 4. Close Ticket

Mark a ticket as complete and move it to the Done folder.

**Steps:**
1. Locate the ticket file
2. Update the `Status` field to `0_Done`
3. Update the `Updated` date to current date
4. Move the ticket file from its current location to `.claude/backlog/0_Done/`

## Important Notes

- Always **ask clarifying questions** before creating or updating tickets to ensure full understanding
- Ticket IDs are unique and incremental across the entire backlog
- Use consistent naming: `{TICKET_ID}_{TYPE}_{Title_Snake_Case}.md`
- When updating tickets, preserve all existing information unless explicitly asked to change it
- Status field should always match the folder location
- All dates should be in ISO format (YYYY-MM-DD)
