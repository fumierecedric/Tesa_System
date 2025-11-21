---
Epic: Project Management
Id: 0014
Title: Online Search Skill
Type: Feature
Status: 0_Done
Created: 2025-11-21
Updated: 2025-11-21
Priority: Medium
Sprint: Unassigned
---

## Summary

Create an online-search skill that enables agents and the user to search the web for information. This skill complements the knowledge-management skill by providing access to external information sources when local knowledge is insufficient.

## User Story

**As a** project owner and other agents in the system
**I want** an online-search skill that can query web sources for information
**So that** I can find current information, documentation, and resources that aren't yet in the local knowledge base

**As a** developer working with multiple agents
**I want** the online-search skill to be accessible by any agent
**So that** agents can autonomously gather external information when needed to complete their tasks

## Acceptance Criteria

### Online-Search Skill
- [x] Create an online-search skill in `.claude/skills/online-search/`
- [x] Skill can be invoked by any agent via the Skill tool
- [x] Skill can be invoked directly by the user

### Search Functionality
- [x] Implement web search capability using available search APIs/tools (e.g., WebSearch tool)
- [x] Return search results in a structured, consistent format
- [x] Include source URLs and brief descriptions for each result
- [x] Handle search errors gracefully (no results, API failures, etc.)

### Search Methods
- [x] Method to perform basic web search with query string
- [x] Method to search within specific domains (if needed)
- [x] Optional: Method to filter results by date/relevance

### Integration
- [x] Skill can be called independently from knowledge-management skill
- [x] Clear separation: online-search handles web queries, knowledge-management handles local storage
- [x] Document how agents should decide between using local knowledge vs. online search

### Quality Requirements
- [x] Search results clearly indicate they are from external sources
- [x] Include metadata (source URL, date if available, relevance)
- [x] Results are factual and directly related to the search query
- [x] No mixing of online search results with local knowledge base entries

## Initial Request

This ticket was created as a split from the Knowledge Manager requirements. The original request included "a method to search online" as part of the knowledge-management skill. During clarification, this was separated into its own skill to maintain clear separation of concerns:
- **knowledge-management skill**: Local knowledge base only, no online access
- **online-search skill**: Web search only, no local knowledge storage

The online-search skill should enable agents to find external information when local knowledge is insufficient, while maintaining clear boundaries between local and online information sources.
