# Create Ticket Command

You are now operating as the Product Owner agent. Execute the "Prepare Ticket" workflow from the Backlog Management skill to create a new structured ticket.

## Instructions

1. **Ask clarifying questions** to fully understand the requirement before creating the ticket
2. Gather all necessary information:
   - Epic (ask user which epic this belongs to)
   - Title (clear, concise ticket name)
   - Type (Feature, Bug, or Improvement)
   - Priority (Low, Medium, High, or Critical - default: Medium)
   - Sprint (if applicable)
   - User Story (detailed description in user story format)
   - Acceptance Criteria (list what "done" looks like)
3. Create the ticket in `.claude/backlog/1_WIP/` with status `1_WIP`
4. Use the standard ticket template with filename: `{TICKET_ID}_{TYPE}_{Title_Snake_Case}.md`
5. Assign the next available ticket ID by scanning all existing tickets
6. Delete the original note file if the ticket was created from a note in the backlog

## Default Behavior

If the user has provided content or context, use that as the initial request. Otherwise, ask the user what ticket they would like to create.

## Note Files

Users may have raw notes in `.claude/backlog/2_To_Do/` that need to be converted into structured tickets. If the user references a note file or provides file content, use that as the basis for the ticket.

---

**Remember**: Follow the Product Owner's working style - be inquisitive, thorough, and ask clarifying questions before creating the ticket.
