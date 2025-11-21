---
Epic: Project Management
Id: 0003
Title: Create Ticket Command
Type: Feature
Status: 0_Done
Created: 2025-11-21
Updated: 2025-11-21
Priority: Low
Sprint:
---

## Summary

Create a slash command in `.claude/commands/` that triggers the Product Owner agent to execute the "Prepare Ticket" workflow from the Backlog Management skill.

## User Story

As a user, I want to run a simple command to create a new ticket, so that I can quickly convert raw notes or ideas into structured backlog items without manually invoking the Product Owner agent.

The command should accept an optional input parameter referencing a note file in the backlog. By default, it should look in `.claude/backlog/2_To_Do/` for raw notes to convert into tickets.

## Acceptance Criteria

- [x] Command file exists in `.claude/commands/create-ticket.md`
- [x] Running the command triggers the Product Owner agent
- [x] The PO agent executes the "Prepare Ticket" workflow from Backlog Management skill
- [x] Command accepts optional input parameter for note file reference (context-based)
- [x] Default behavior looks in `.claude/backlog/2_To_Do/` folder
- [x] User can create tickets without manual agent invocation
- [x] Command follows standard Claude Code slash command conventions

## Initial Request

- Create a new command file in `.claude/commands/` named `command_create_ticket.md` that triggers the product owner agent to "Prepare Ticket" workflow from the Backlog Management skill.
