---
Epic: Project Management
Id: 0001
Title: Product Owner Agent System
Type: Feature
Status: 0_Done
Created: 2025-11-21
Updated: 2025-11-21
Priority: Critical
Sprint:
---

## Summary

Create a Product Owner Agent system with Backlog Management capabilities to manage product tickets in `.claude/backlog/` directory. The system includes agent configuration, skills, templates, and workflows for creating, updating, and closing tickets.

## User Story

As a project manager, I need a Product Owner agent that can help me manage the product backlog efficiently, so that I can create well-structured tickets, track work items, and maintain organized project documentation without manual overhead.

The PO should leverage reusable skills and interact with me to gather necessary information, asking clarifying questions to ensure tickets are properly defined before creation.

## Acceptance Criteria

- [x] Product Owner Agent configuration created in `.claude/agents/`
- [x] Agent setup is lightweight, leveraging Skills for workflows
- [x] Backlog Management skill created in `.claude/skills/`
- [x] Backlog folder structure initialized (0_Done, 1_WIP, 2_To_Do, 3_To_Plan, 4_Wait, 5_Archive)
- [x] Initialize Backlog workflow implemented
- [x] Prepare Ticket workflow implemented with:
  - [x] Auto-incrementing 4-digit ticket IDs (0001, 0002, etc.)
  - [x] Ticket template with all required fields (Epic, Id, Title, Type, Status, Dates, Priority, Sprint, Summary, User Story, Acceptance Criteria, Initial Request)
  - [x] Default behavior to look in `2_To_Do/` folder for raw notes
  - [x] Interactive prompts for Epic, Type, Priority, and Sprint
- [x] Update Ticket workflow implemented
- [x] Close Ticket workflow implemented (updates status and moves to 0_Done/)
- [x] PO agent asks clarifying questions before creating/updating tickets
- [x] Complete documentation for PO agent and Backlog Management skill
- [x] Template stored in `.claude/skills/backlog-management/templates/`
- [x] Ticket naming convention: `{TICKET_ID}_{TYPE}_{Title_Snake_Case}.md`

## Initial Request

- Create a Product Owner Agent (short name: PO)
- Store the agent configuration in `.claude/agents/`
- The PO will be responsible for managing the product backlog in `/.claude/backlog/`, that is the "tickets"
- The setup for the PO should be very light in itself, we will leverage Skills to implement the actual standard workflows of the PO
- You should create those Skills as needed, and store them in `.claude/skills/`
- A core skill "Backlog Management" should be created to start with
- The "Backlog Management" skill should implement at least the following workflows:
    - Initialize Backlog: in `.claude/backlog/`, create a folder structure: 0_Done, 1_WIP, 2_To_Do, 3_To_Plan, 4_Wait, 5_Archive if it does not exist yet
    - Prepare Ticket: for any given file in the backlog (raw note), per default look into 2_To_Do/ folder, prepare a ticket markdown file with all relevant fields (see below)
        - Assign a Ticket ID (incremental integer) based on all tickets in the backlog (4 digits, zero-padded, e.g. 0001, 0002, etc)
        - Create a markdown file in `/.claude/backlog/3_To_Plan/` using a template to be defined in the skill (in a dedicated sub-folder `templates/` inside the skill folder)
            - The template should include at least the following fields
                - Epic: Ask user for confirmation
                - Id: the numbering of the ticket (4 digits, zero-padded, e.g. 0001, 0002, etc)
                - Title: name of the ticket
                - Summary: a short description of the ticket
                - Type: (Feature, Bug, Improvement), ask user for confirmation
                - Status 0_Done, 1_WIP, 2_To_Do, 3_To_Plan, 4_Wait, 5_Archive
                - Created Date
                - Update Date
                - User Story: detailed description of the ticket
                - Acceptance Criteria: list of criteria to be met for the ticket to be considered done
                - Inital Request: a copy of the initial request that led to the creation of the ticket
                - Prioritization: (Low, Medium, High, Critical), ask user for confirmation - per default Medium
                - Sprint: assign to a sprint if applicable, otherwise leave blank
    - Update Ticket: update fields of an existing ticket as needed
    - Close Ticket: update status and move ticket file to 0_Done/ folder
- The PO agent should be able to leverage the "Backlog Management" skill to perform backlog operations as needed
- The PO agent should interact with the user to gather necessary information for ticket creation and updates
- Ensure proper documentation of the PO agent and the "Backlog Management" skill for future reference
- It's important for the product owner to ask clarifying questions to fully understand the requirements before creating or updating tickets
