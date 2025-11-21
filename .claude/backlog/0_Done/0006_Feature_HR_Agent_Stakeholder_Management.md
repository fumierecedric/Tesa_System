# Ticket 0006: HR Agent Stakeholder Management

> **Historical Note**: This ticket used the original agent name "HR Agent". The agent was later renamed to "Stakeholder Manager Agent" (see ticket 0015) to better reflect its broader role in managing stakeholder relationships.

**Epic:** Project Management
**Type:** Feature
**Priority:** Medium
**Sprint:** None
**Status:** 0_Done
**Created:** 2025-11-21
**Updated:** 2025-11-21

---

## User Story

As a project manager, I want an HR agent so that I can manage my stakeholders effectively and maintain a comprehensive record of all interactions and key information.

---

## Description

Create a new HR agent with stakeholder management capabilities. The agent should manage stakeholder information and interaction logs in structured markdown files stored in `.claude/stakeholders/`, with one file per stakeholder.

---

## Initial Request

Original requirements from note file `.claude/backlog/2_To_Do/stakeholder_management.md`:

- Create a new agent called HR
- HR is managing people
- In a folder `.claude/stakeholders` there should be one file per person, named with `familyname_firstname.md`
- There should be a new skill called `stakeholder-management`
- Template in that skill with key information per stakeholder:
  - Family Name
  - First Name
  - Company
  - Role
  - Email
  - Phone
- Below those fields in the template, a log with H2 heading `## YYYY-MM-DD` (date of interaction)
- Below that heading, a free text area to log interactions with that stakeholder
- The HR agent should be able to:
  - Create new stakeholder files based on that template
  - Update the stakeholder information fields
  - Update the log section with new interactions
  - List all stakeholders
  - Search stakeholders by name, company, or role
  - Retrieve the interaction log for a specific stakeholder
  - Delete a stakeholder file if needed
  - Ensure that all stakeholder files are stored in the `.claude/stakeholders` directory
- The Solution Designer should be briefed: when the ticket goes about stakeholder management, the HR agent should be used

---

## Acceptance Criteria

### 1. Stakeholder Management Skill
- [x] Create a new skill called `stakeholder-management`
- [x] Include a template with key stakeholder information fields
- [x] Template should support logging interactions with date-based entries

### 2. Stakeholder File Template
The template must include the following fields:
- [x] Family Name
- [x] First Name
- [x] Company
- [x] Role
- [x] Email
- [x] Phone
- [x] Interaction Log section with H2 headings using format `## YYYY-MM-DD`
- [x] Free text area below each date heading for logging interactions

### 3. File Storage
- [x] All stakeholder files stored in `.claude/stakeholders/` directory
- [x] Files named using format: `familyname_firstname.md`

### 4. HR Agent Capabilities
The HR agent must be able to:
- [x] Create new stakeholder files based on the template
- [x] Update stakeholder information fields
- [x] Update the log section with new interactions (append new date entries)
- [x] List all stakeholders
- [x] Search stakeholders by name, company, or role
- [x] Retrieve the interaction log for a specific stakeholder
- [x] Delete a stakeholder file if needed
- [x] Ensure all stakeholder files are stored in the correct directory

### 5. Solution Designer Integration
- [x] Brief Solution Designer: when tickets involve stakeholder management, the HR agent should be used

---

## Technical Notes

- Stakeholder files are markdown-based for easy version control and readability
- Date-based logging allows chronological tracking of all interactions
- Search functionality should support partial matches across multiple fields

---

## Dependencies

None

---

## Related Tickets

None
