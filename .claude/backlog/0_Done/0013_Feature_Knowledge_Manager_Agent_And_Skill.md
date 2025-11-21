---
Epic: Project Management
Id: 0013
Title: Knowledge Manager Agent And Skill
Type: Feature
Status: 0_Done
Created: 2025-11-21
Updated: 2025-11-21
Priority: Medium
Sprint: Unassigned
---

## Summary

Create a Knowledge Manager agent with a knowledge-management skill to organize, categorize, retrieve, update, and maintain a local knowledge base stored as markdown files in `.claude/knowledge/`. The system should handle standalone pieces of information (methodologies, client systems, tools, etc.) that may be synthesized from multiple sources, with zero hallucinations allowed.

## User Story

**As a** project owner and other agents in the system
**I want** a Knowledge Manager that can store, retrieve, and maintain structured knowledge entries locally
**So that** I can access accurate, well-organized information about methodologies, client systems, tools, and other topics without relying on online searches or risking hallucinations

**As a** developer working with multiple agents
**I want** the Knowledge Manager to be accessible both as a skill and as an agent
**So that** agents can share knowledge seamlessly and I can interact with it directly when needed

## Acceptance Criteria

### Knowledge Manager Agent
- [x] Create a Knowledge Manager agent that can be invoked via the Task tool
- [x] Agent can interface with other agents to share knowledge as needed
- [x] Agent strictly uses only local knowledge base entries - NO online searches, NO hallucinations

### Knowledge-Management Skill
- [x] Create a knowledge-management skill with the following methods:
  - [x] Add new information to the knowledge base
  - [x] Search for information in the knowledge base
  - [x] Update existing information
  - [x] Delete outdated information
- [x] Skill can be invoked by other agents
- [x] Skill operates exclusively on local knowledge entries

### Knowledge Entry Template
- [x] Template includes the following fields:
  - [x] Title
  - [x] Epic (can be a list of epics - epics will be created in `.claude/epics/` folder later on)
  - [x] Date Added
  - [x] Date Updated
  - [x] Quick Summary
  - [x] Source (links to markdown files in `.claude/` setup, external docs, or URLs - can be multiple sources)
  - [x] Details section (below metadata)
- [x] Template stored in `.claude/skills/knowledge-management/templates/`

### Knowledge Base Structure
- [x] Knowledge base stored in `.claude/knowledge/` folder as markdown files
- [x] File naming convention: title of the knowledge entry with dashes instead of spaces (e.g., `SOSTAC-Framework.md`)
- [x] Knowledge entries are synthetic and precise

### Quality Requirements
- [x] All knowledge entries use only information present in the knowledge base
- [x] NO hallucinations whatsoever - only factual information from stored sources
- [x] Each entry clearly indicates its source(s)
- [x] Knowledge entries are concise and well-structured

## Initial Request

- Create a Knowledge Manager agent
- The Knowledge Manager should be able to:
  - Organize and categorize information
  - Retrieve relevant knowledge based on queries
  - Update and maintain the knowledge base
- The agent use a skill to manage knowledge effectively
- The knowledge-management skill should include:
  - A method to add new information
  - A method to search for information
  - A method to update existing information
  - A method to delete outdated information
  - A method to search online
- In the skill, there is a template for knowledge entries that includes:
  - Title
  - Epic (can be a list of epics - epics will be created in .claude/epics/ folder later on)
  - Date Added
  - Date Updated
  - Quick Summary
  - Source: link to the md in the .claude set-up (if applicable: meeting, etc), link to a external doc, or url, there can be multiple sources
  and then the details below
- The Knowledge Manager should be able to interface with other agents to share knowledge as needed
- No hallucinations whatsoever are allowed: only use the knowledge present in the knowledge base or search online
- the knowledge base should be stored in .claude/knowledge/ folder as markdown files
- Title of the markdown files should be the title of the knowledge entry with dashes instead of spaces
- Be synthetic and precise in your knowledge entries

**Note**: During clarification, online search functionality was split into a separate skill (online-search) to be created as a separate ticket. This ticket focuses on local knowledge management only.
