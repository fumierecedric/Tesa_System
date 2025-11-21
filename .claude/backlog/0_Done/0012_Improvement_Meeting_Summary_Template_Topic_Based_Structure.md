---
Epic: Product Management
Id: 0012
Title: Meeting Summary Template Topic-Based Structure
Type: Improvement
Status: 0_Done
Created: 2025-11-21
Updated: 2025-11-21
Completed: 2025-11-21
Priority: High
Sprint: none
---

## Summary

Improve the meeting summary template to organize content by main topics (in chronological order) rather than the current format. Each topic section should include a summary, details, action points, and suggestions for information extraction by various agents (HR Agent, Knowledge Manager Agent, etc.).

## User Story

As a meeting participant or stakeholder,
I want meeting summaries to be organized by main topics discussed (in chronological order),
So that I can quickly understand the key points, decisions, and action items for each topic, and relevant information can be efficiently extracted by specialized agents.

## Acceptance Criteria

- [x] The meeting summary template is updated with the new topic-based structure
- [x] Each main topic section includes:
  - Summary subsection with short, crisp bullet points
  - Details subsection with participant contributions
  - Action Points subsection with checkboxes and owner assignments
  - Suggestions for Information Extraction subsection for various agents (HR Agent, Knowledge Manager Agent, etc.)
- [x] Topics are organized in chronological order (topic 1 is the first discussed, etc.)
- [x] The new template completely replaces the existing one (no backward compatibility required)
- [x] Template emphasizes synthetic and structured content (short better than long)
- [x] Documentation is updated to reflect the new template structure
- [x] The `/summarize-meeting` command is tested with the new template and works correctly

## Initial Request

I still want to improve the meeting summary template.

I would like the followin structure:

```
# Meeting Summary: [Meeting Title]

## Main Topic 1

### Summary of Main Topic 1

- Summary of main topic 1 / short and crisp bullet points

### Details of main topic 1

- Participants 1: key detail
- Participant 2: key detail
- etc.

### Action Points for Main Topic 1

- [ ] Action point 1 (Owner: Name)
- [ ] Action point 2 (Owner: Name)

### Suggestions for Information Extraction

- Stakeholder Information (HR Agent)
    - some key details about stakeholders
- Knowledge Entries (Knowledge Manager Agent)
    - some key knowledge points

## Main Topic 2

### Summary of Main Topic 2

- Summary of main topic 2 / short and crisp bullet points

### Details of main topic 2

- Participants 1: key detail
- Participant 2: key detail

### Action Points for Main Topic 2

- [ ] Action point 1 (Owner: Name)
- [ ] Action point 2 (Owner: Name)

### Suggestions for Information Extraction

- Stakeholder Information (HR Agent)
    - some key details about stakeholders
- Knowledge Entries (Knowledge Manager Agent)
    - some key knowledge points

etc.
```

Keap it synthetic and structured around main topics. Short better than long.
