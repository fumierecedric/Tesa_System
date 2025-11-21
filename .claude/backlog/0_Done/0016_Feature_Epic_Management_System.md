---
Epic: Project Management
Id: 0016
Title: Epic Management System
Type: Feature
Status: 0_Done
Created: 2025-11-22
Updated: 2025-11-22
Priority: Medium
Sprint: N/A
---

## Summary

Enhance the backlog management skill with comprehensive epic management functionality, including CRUD operations, template-based epic creation, automatic ticket-epic linking, and a dedicated folder structure for epic files.

## User Story

As a Product Owner, I want to manage epics within the backlog management system so that I can organize and track related tickets under high-level business objectives, automatically maintain epic-ticket relationships, and navigate between epics and their associated tickets through clickable links.

## Acceptance Criteria

- [ ] Epic CRUD operations implemented in backlog management skill:
  - [ ] Create a new epic using the template
  - [ ] Update an existing epic
  - [ ] Delete an epic
  - [ ] List all epics
- [ ] Epic template created at `.claude/skills/backlog-management/templates/epic-template.md` with fields:
  - [ ] Epic Name
  - [ ] Description
- [ ] Epic storage folder created at `.claude/epics/`
- [ ] First epic file created: `.claude/epics/project_management.md` for Epic Name: "Project Management"
- [ ] Epic functionality includes listing all tickets from backlog that relate to the specific epic
- [ ] When a new ticket is created, the underlying epic is automatically updated with the new ticket reference
- [ ] Epic files contain clickable links (from root directory) to open tickets listed in the epic
- [ ] Product Owner agent documentation updated to reflect epic management capabilities
- [ ] All epic management functions are accessible through the backlog management skill

## Initial Request

```
- Enhance backlog management skill
- Product Owner agent will be the one to use this new aspect of the skill, so update the doc
- in the skill, create functions to:
  - create a new epic
  - update an existing epic
  - delete an epic
  - list all epics
- Use a skill/templates/epic-template.md
    -  Epic Name
    -  Description
- Create a first folder .claude/epics/ to store epic files
- Create a first project_mangement.md file for the Epic Name: Project Management
- Add a functionnality: list all tickets from backlog that relate to the specific Epic
- When a new ticket is created, underlying epic should be updated (list of tickets improved)
- from root director, we want to be able to click on a link to open the tickets listed in the epic file
```
